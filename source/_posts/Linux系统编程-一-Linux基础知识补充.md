---
title: 'Linux系统编程(一):Linux基础知识补充'
author: bucaike
top: false
cover: false
toc: true
mathjax: false
date: 2021-05-09 21:12:17
img: https://i.loli.net/2021/05/09/DBSVMmLG1WInqvo.png
coverImg: https://i.loli.net/2021/05/09/DBSVMmLG1WInqvo.png
summary: Linux系统编程第一章：Linux的基础知识补充
tags:
  - Linux
  - 编程
categories:
  - 技术
---


# 第 1章：Linux操作系统编程基础知识补充

> 课程视频：[黑马程序员 - Linux系统编程](https://www.bilibili.com/video/BV1KE411q7ee?p=35)

## 1.1 基础命令

* `cd` 命令

  `cd -` 在当前目录和上一个目录之间切换

  ```bash
  ❯ cd /etc/nginx
  ❯ cd ~/my_code
  ❯ cd -
  /etc/nginx
  ❯ pwd
  /etc/nginx
  ❯ cd -
  ~/my_code
  ❯ pwd
  /home/black/my_code
  ```

* `ls`命令

  `ls -R` 递归显示当前目录下文件和文件夹

  ```bash
  ❯ cd Downloads
  ❯ ls -R
  .:
  Compressed  Documents  Music  Programs  Video
  
  ./Compressed:
  Hack.zip
  
  ./Documents:
  cryptous.pdf  PDF_611399243.html
  
  ./Music:
  
  ./Programs:
  code-server_3.8.0_amd64.deb
  
  ./Video:
  
  ```

## 1.2 文件和用户

|     名称     | ls -l 中的表示 |
| :----------: | :------------: |
|   普通文件   |       -        |
|   目录文件   |       d        |
| 字符设备文件 |       c        |
|  块设备文件  |       b        |
|    软链接    |       l        |
|   管道文件   |       p        |
|    套接字    |       s        |

* `chmod`命令

  ```bash
  chmod [who] [+|-|=] [mode] filename
  ```

  `who`可以是下面字母中的任意一个或者他们的组合：

  * u : 表示用户，即文件或目录的所有者
  * g : 表示同组用户，即与文件属主有相同ID的所有用户
  * o : 表示其他用户
  * a : 表示所有用户，是系统默认值

  操作符号可以是：

  * +: 添加某个权限
  * -: 取消某个权限
  * =: 赋予给定权限并取消其他所有权限

  `mod` 即可读可写可执行的任意组合

* `tar`命令

  * `-c`：创建新的档案文件
  * `-r`：把要存档的文件追加到档案文件的末尾
  * `-t`：列出档案文件内容，查看档案包中的文件
  * `-u`：更新文件。用新增的文件取代原档案文件，如果在档案文件中找不到要更新的文件，则把他追加到档案文件的最后
  * `-x`：从档案文件中释放文件
  * `-z`：使用`gzip`进行压缩
  * `-j`：使用`bzip2`方式压缩

  常用创建压缩文件的命令

  ```bash
  tar -zcvf compress.tar.gz file1 file2 dir1
  ```

  常用解压缩文件命令

  ```bash
  tar -jcvf compress.tar.gz
  ```

* `rar`和`unrar`

  压缩文件

  ```bash
  rar a -r compress.rar file1 dir2 file2
  ```

  解压文件

  ```bash
  unrar x compress.rar
  ```

* `zip`和`unzip`

  压缩文件

  ```bash
  zip -r compress.zip file1 dir1 file3
  ```

  解压缩文件

  ```bash
  unzip compress.zip
  ```

## 1.3 搜索

* `chown`命令

  ```bash
  chown [OPTION] ... [OWNER:GROUP] FILE ...
  ```

  `OPTION` 的主要参数：

  * -R：递归地改变指定目录及其下的所有子目录和文件的拥有者。
  * -v：显示`chown`命令所做的工作。

* `find`命令

  ```bash
  find [PATHNAME] [-OPTIONS: -print -exec -ok -name -type ...]
  ```

  * `-name` ：按文件名搜索
  * `-maxdepth`：指定搜索深度
  * `-size`：按文件大小搜索：k、M、G
  * `-atime、-mtime、-ctime`：accsess time访问时间、mod change属性更改时间、change time文件内容更改时间
  * `-type`：按文件类型搜索。d/p/s/c/b/l/f(文件)
  
  扩展
  
  ```bash
  find /usr/ -name '*tmp*' -exec rm -r {} \;
  find /usr/ -name '*tmp*' -ok rm -r [] \;
  ```
  
  如果查找的文件名中有空格，同时又想利用`xargs`管道的话：
  
  ```bash
  find ./ type f print0 | xargs -0 ls -l
  ```
  
* `grep` 命令

  ```bash
  grep [OPTIONS] PATTERN [FILE...]
  ```

  `-r`：递归搜索

  `-n`：显示行号

  ```bash
  ❯ cat abc
  kkfdasjfklasfj
  hello! world
  dfasjfklasnflk
  2131312
  ❯ grep "hello\!" ./ -rn
  ./abc:2:hello! world
  ```

* `xargs`

  有时后面的命令不接受管道，此时可以添加`xargs`实现。

  ```bash
  ❯ ls -l
  总用量 108
  -rw-r--r-- 1 black black    51  1月 20 15:58 abc
  -rw-r--r-- 1 black black 98571  1月 14 12:05 blog.WordPress.2021-01-14.xml
  drwxr-xr-x 2 black black  4096  1月 20 16:01 temp
  ❯ find ./ -type f | ls -l
  总用量 108
  -rw-r--r-- 1 black black    51  1月 20 15:58 abc
  -rw-r--r-- 1 black black 98571  1月 14 12:05 blog.WordPress.2021-01-14.xml
  drwxr-xr-x 2 black black  4096  1月 20 16:01 temp
  ❯ find ./ -type f | xargs ls -l
  -rw-r--r-- 1 black black    51  1月 20 15:58 ./abc
  -rw-r--r-- 1 black black 98571  1月 14 12:05 ./blog.WordPress.2021-01-14.xml
  ❯ find ./ -type f | grep ab
  ./abc
  ```

## 1.4 `GCC`补充知识

* `gcc`编译可执行程序的步骤：

  ![1.4_1](https://i.loli.net/2021/05/09/bhCnOsjJ7qdGy5V.png)

* `gcc`常用参数：

  * `-I [directory]`：指定头文件目录。

    ```bash
    ❯ cat hello.c
    #include<hello.h>
    int main(){
                    printf("nihao\n");
                    return 0;
    }
    ❯ cat inc/hello.h
    #include<stdio.h>
    ❯ gcc hello.c -o hello
    hello.c:1:9: 致命错误：hello.h：没有那个文件或目录
        1 | #include<hello.h>
          |         ^~~~~~~~~
    编译中断。
    ❯ gcc hello.c -o hello -I ./inc/
    ❯ ./hello
    nihao
    ❯
    ```

  * `-c`：只做预处理、编译、汇编操作，生成`.o`二进制文件，不进行链接

  * `-g`：包含调试信息
  
  * `-O[n]`：`n`可取0～3，`n`越大，优化越多
  
  * `-Wall`：提示更多警告信息
  
  * `-E`：生成预处理文件
  
  * `-D[DEF]`：编译时定义宏
  
  * `-l`：指定动态库名
  
  * `-L`：指定动态库路径

## 1.5 其他命令

* `jobs`、`fg`、`bg`

  * `jobs`用来显示当前shell下正在运行那些作业。
  * `fg`切换到前台

  示例如下：

  ```bash
  ❯ kolourpaint &
  [1] 481488
  ❯ jobs
  [1]  + running    kolourpaint
  ❯ fg kolourpaint
  [1]  + 483544 running    kolourpaint
  
  ```

* `man`

  使用中需要注意的一点是，有很多重名的函数，比如`shell`编程中和`c`语言中都有`prinrf`这个函数，直接使用`man printf`可能不是我们想要的信息，因此需要注意章节信息。

  * `man man` ：查看章节以及帮助信息
  
  * `man read`：查看`read`命令的 man page
  * `man 3 printf`：查看程序库函数函数中`printf`的信息。（即在第三个 section 中，表示为 `printf(3)`）。
  * `man -k printf`：以`printf`为关键字查找相关的 man page.
  
  附章节信息如下（可通过`man man`查看）：
  
  ```tex
  1  可执行程序或 shell 命令 
  2  系统调用(内核提供的函数) 
  3  库调用(程序库中的函数) 
  4  特殊文件(通常位于 /dev) 
  5  文件格式和规范，如  /etc/passwd 
  6  游戏 
  7  杂项(包括宏包和规范，如 **man**(7)，**groff**(7)) 
  8  系统管理命令(通常只针对 root 用户) 
  9  内核例程 [非标准
  ```


## 1.6 `vim`的实用补充：

* 命令模式：

  * `I`：光标跳转到行首并跳转到编辑插入模式。
  * `A`：光标跳转到行尾并跳转到编辑插入模式。
  * `ci"`：删除双引号中间的所有内容并进入编辑模式，i有`in`的意思，可以配合其他使用。
  * `fw`：光标跳转到w。
  * `s`：删除光标所在字符并跳转到编辑插入模式。
  * `S`：删除光标所在行并跳转到编辑插入模式。
  * `gg=G`：格式化代码。
  * `%`：光标如果在成对的符号上（如大括号、小括号、注释的斜线）则会跳转到下一个与其对应的下一个符号上，如果光标字在函数名上，则会跳转到括号上。
  * `dw`：删除光标所在的单词
  * `D`：从光标处删除至行尾
  * `0`：光标跳转到行首
  * `d0`：从光标删除至行首
  * `$`：光标跳转到行尾
  * `3dd`：从光标处行开始往下删除3行
  * `3yy`：从光标行开始向下复制3行
  * `*`：光标至于字符（单词）上，查找下一个与此匹配的字符（单词）。
  * `#`：与`*`作用相同，但是是向前搜索。
  * `>>`和`<<`：光标所在行向右或者向左缩进一次
  * `[Ctrl+]ww`：在不同分屏窗口之间切换
  * `3K`：跳转到光标所在单词的`man page`，其中3表示字在`man page`的第三章查找
  * `[d`：查看光标所在单词的宏定义
* 末行模式：

  * `s /name1/name2/g`：将光标所在行的所有`name1`替换成`name2`。
  * `s /name1/name2`：将光标所在行的出现的第一个`name1`替换成`name2`。
  * `%s /name1/name2/g`：将文件中所有出现的`name1`替换成`name2`。
  * `%s /name1/name2`：将文件中每一行第一个出现的`name1`替换成`name2`。
  * `5, 9s /name1/name2/g`：自第5行起至第9行所有出现的`name1`替换成`name2`
  * `sp`和`vsp`：上下分屏和左右分屏
  * `qall`：退出所有分屏
* 可视模式
  * `[shift]+v`：进入行可视模式，一次选中一行。
  * `ctrl+v`：可视块模式。
  * 

