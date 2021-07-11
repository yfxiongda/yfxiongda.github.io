---
title: 一次MySQL线上死锁分析
author: bucaike
top: false
cover: false
toc: true
mathjax: false
date: 2021-07-11 11:58:48
img: https://i.loli.net/2021/07/11/aMQvIwYlWPbocmf.png
coverImg: https://i.loli.net/2021/07/11/aMQvIwYlWPbocmf.png
summary: 单行SQL语句出现死锁情况分析
tags: MySQL 死锁
categories: 技术
---
# 一次MySQL线上死锁分析

> 本文原作者：[是小桔啦](https://blog.csdn.net/shixiaojula/article/details/114004360)，此处略作整理和补充

## 前言

MySQL 的锁机制相信大家在学习 MySQL 的时候都有简单的了解过，那既然有锁就必定绕不开死锁这个问题。其实 MySQL 在大部分场景下是不会存在死锁问题的(比如并发量不高，SQL 写得不至于太拉胯的情况)，但是在高并发的业务场景下，一不注意就会产生死锁，而这个死锁分析起来也比较麻烦。

下面介绍一个遇到的一个比较**奇怪的死锁**。

## 业务场景

简单说一下业务背景，公司做的是电商直播，这个死锁就出现在主播后台对商品信息进行更新的时候。

一个商品会有两个关联的 ID，通过其中任何一个 ID 都无法确定唯一一件商品（也就是说这个 ID 和商品是**一对多**的关系），只能同时查询两个 ID，才能确定一件商品。所以在更新商品信息的时候，需要在 where 条件中同时指定两个 ID，下面是死锁 SQL 的结构（已脱敏）：

```sql
UPDATE test_table SET `name`="zhangsan" WHERE class_id = 10 AND teacher_id = 8;
```

**这个 SQL 非常简单，根据两个等值条件，对一个字段进行更新。**

不知道你看到这个 SQL 会不会懵逼，按常理来说，应该是一个事务里有多条 SQL 才会有可能出现死锁，这一条 SQL 怎么可能出现死锁呢？

最后查出来是由于 MySQL 的索引合并优化导致的，即 Index Merge，下面会进行详细讲解并复现一下死锁场景。

## 索引合并

Index Merge 是 MySQL 在 5.0 的时候引入的一项优化功能，主要是用于优化一条 SQL 使用多个索引的情况。

我们来看刚刚的 SQL，假设 `class_id` 和 `teacher_id` 分别是两个普通索引：

```sql
UPDATE test_table SET `name`="zhangsan" WHERE class_id = 10 AND teacher_id = 8;
```

**如果没有 Index Merge 优化的时候**，MySQL 查询数据的步骤如下：

* 根据 class_id 或 teacher_id （具体使用哪个索引由优化器根据实际数据情况自行判断，这里假设使用 `class_id` 的索引）在二级索引上查询到对应数据的主键 ID
* 根据查询到的主键 ID 进行回标查询（即查询聚簇索引），得到相应的数据行
* 从数据行中获取 `teacher_id` ，判断其是否等于 8，满足条件则返回

从这个过程中，不难看出，**MySQL 只使用到了一个索引**，至于为什么不使用多个索引，简单来说就是因为多个索引在多棵树上，强行使用反而降低性能。

再来看看**引入了 Index Merge 优化后**，MySQL 查询数据的步骤如下：

* 根据 `class_id` 查询到相应的主键，再根据主键回表查询到对应的数据行（记为结果集 A）
* 根据 `teacher_id` 查询到相应的主键，再根据主键回表查询到对应的数据行（记为结果集 B）

* 将结果集 A 和结果集 B 执行交集操作，获得最终满足条件的结果集

这里可以看出，有了 Index Merge 之后，MySQL 将一条 SQL 语句拆分成了两个查询步骤，**分别使用两个索引，再用交集操作优化性能**。

## 死锁分析

分析完了 Index Merge 的步骤，我们再回过头想一下为什么会出现死锁呢？

还记得上面说的 Index Merge 将一条 SQL 查询拆分成了两个步骤吗，问题就出现在这里。我们知道 `UPDATE` 语句是会加上一个**行级排他锁**的，在分析加锁步骤之前，我们假设有如下一个数据表：

![](https://img-blog.csdnimg.cn/img_convert/3844e0d10f8cb651115b686f51a330df.png)

上表数据满足我们文章开头说的特点，根据 `class_id` 和 `teacher_id` 单个字段均无法唯一确定一条数据，只能联合两个字段，才能确定一条数据，并且设定 `class_id` 和 `teacher_id` 分别为两个普通索引。

假设有如下两条 SQL 语句并发执行，它们的参数完全不同，直觉告诉我们应该不会出现死锁，但直觉往往是错误的：

```sql
// 线程 A 执行
UPDATE test_table SET `name`="zhangsan" WHERE class_id = 2 AND teacher_id = 1;

// 线程 B 执行
UPDATE test_table SET `name`="zhangsan" WHERE class_id = 1 AND teacher_id = 2;
```

那么**在 Index Merge 的优化下**，并发执行如上 SQL 的时候，MySQL 的加锁步骤如下：

![](https://img-blog.csdnimg.cn/img_convert/dd4390c91f1c83e58dc756177c737490.png)

**最终，两个事务互相等待，形成死锁**

## 解决方案

因为这个死锁本质上还是由于 Index Merge 这个优化导致的，所以要解决这个场景的死锁问题，本质上只要让 MySQL 不走 Index Merge 优化即可。

### 方案一

手动将一条 SQL 拆分成多条 SQL，在逻辑层做交集操作，阻止 MySQL 的憨憨优化行为，比如这里我们可以先根据 `class_id` 查询到相应主键，再根据 `teacher_id` 查询相应主键，最后根据交集后的主键查询数据。

### 方案二

建立联合索引，比如这里可以将 `class_id` 和 `teacher_id` 建立一个联合索引，MySQL 就不会走 Index Merge 了

### 方案三

强制走单个索引，在表名后添加 `for index(class_id)` 可以指定该语句仅走 class_id 索引

### 方案四

关闭 Index Merge 优化：

* 永久关闭：

  ```sql
  SET [GLOBAL|SESSION] optimizer_switch='index_merge=off'
  ```

* 临时关闭：

  ```sql
  UPDATE /*+ NO_INDEX_MERGE(test_table) */ test_table SETname="zhangsan" WHERE class_id = 10 AND teacher_id = 8
  ```

## 场景复现

### 数据准备

为了方便测试，这里提供一个 SQL 脚本，将其用 Navicat 导入后即可得到需要的测试数据：

下载地址：https://cdn.juzibiji.top/file/index_merge_student.sql

导入之后，我们会得到如下格式的 10000 条测试数据：

![](https://img-blog.csdnimg.cn/img_convert/b2dc406b2a656cf7edd8503eaec9dbbb.png)

### 测试代码

由于篇幅限制，这里仅给出代码 Gist 链接：https://gist.github.com/juzi214032/17c0f7a51bd8d1c0ab39fa203f930c60

![](https://img-blog.csdnimg.cn/img_convert/926d2a5947f3b5528cfd3adbf7a7fc0f.png)

上述代码主要是开启 100 个线程执行我们的数据修改 SQL 语句，来模拟线上并发情况，在运行几秒钟后，我们会得到下面这样一个报错：

```log
com.mysql.cj.jdbc.exceptions.MySQLTransactionRollbackException: Deadlock found when trying to get lock; try restarting transaction
```

这代表已经产生了死锁异常。

### 死锁分析

上面我们用代码已经构造出了一个死锁，接下来我们进入 MySQL 看看死锁日志，在 MySQL 中执行如下命令即可查看死锁日志：

```sql
SHOW ENGINE INNODB STATUS;
```

![](https://img-blog.csdnimg.cn/img_convert/84c61d74c6a05925daaa2baad6700767.png)

在日志中，我们找到 `LATEST DETECTED DEADLOCK` 这一行，这里开始便是我们上次产生的死锁，接下来我们开始分析。

通过第 29 行可以看到，事务 1 执行的 SQL 的条件是 `class_id = 6` 和 `teacher_id = 16`，它目前持有了一个行锁，第 34~39 行是该行数据，34 行是主键的十六进制表示，我们转换为 10 进制即为 **1616**。同样的，看 45 行，其等待拿锁的是主键 id 1517 的数据。

![](https://img-blog.csdnimg.cn/img_convert/623f79359f3da63e5a29959e23d558af.png)

接下来用同样的方法分析事务 2，可知事务 2 持有了 3 把锁，分别是主键 id 为**1317、1417、1517** 的数据行，等待的是 **1616** 。

看到这里我们就已经发现了，事务 1 持有 1616 等待 1517，事务 2 持有1517 等待 1616，所以形成了一个死锁。此时 MySQL 的处理方法是回滚持有锁最少的事务，并且 JDBC 会抛出我们前面的 MySQLTransactionRollbackException 回滚异常。

## 总结

这个死锁在排查的时候其实非常不好排查，如果你不知道 MySQL 的 Index Merge，那么在排查的时候其实是毫无头绪的，因为呈现在你面前的就只有一条非常简单的 SQL，就算看死锁日志，也是一样的不明所以。

所以处理这类问题，更多的还是考验你的知识储备量和经验，只要遇到过一次，后面在写 SQL 的时候多加注意就好了！