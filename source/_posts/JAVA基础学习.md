---
title: JAVA基础学习
author: bucaike
top: false
cover: false
toc: true
mathjax: false
date: 2021-05-19 09:32:54
img: https://i.loli.net/2021/05/19/HNmrLQ12lsD5yMx.png
coverImg: https://i.loli.net/2021/05/19/PUyIjvXQa9Yk6pR.png
summary: 介绍了入门Java的基础知识，包含面向对象编程支持——封装、继承、多态
tags: 
  - JAVA
  - 面向对象
categories:
  - 技术
---

# IDEA

## IDEA项目结构

![IDEA项目结构](https://i.loli.net/2021/05/19/p8szrflw9eyaB7g.png)

## IDEA常用的快捷键

|        快捷键        |                  功能                   |
| :------------------: | :-------------------------------------: |
|     `Alt+Enter`      |          导入包，自动修正代码           |
|       `Ctrl+Y`       |             删除光标所在行              |
|       `Ctrl+D`       |     复制光标所在行，并粘贴在下一行      |
|     `Ctrl+Alt+L`     |               格式化代码                |
|       `Ctrl+/`       |         单行注释 / 取消单行注释         |
|    `Ctrl+Shift+/`    |         多行注释 / 取消多行注释         |
|      `Alt+Ins`       | 自动生成代码，toString，get，set 等方法 |
| `Alt+Shift+上下箭头` |             移动当前代码行              |
|      `HOME/END`      |         快速移动光标到行首/行尾         |



## IDEA代码自动生成

* **`psvm`**

  ```java
  public static void main(String[] args) {
          
      }
  ```

* **`5.fori`**

  ```java
  for (int i = 0; i < 5; i++) {
              
          }
  ```

* **`数组名称.fori`**

  ```java
  for (int i = 0; i < 数组名称.length; i++) {
              
          }
  ```

* **`sout`**

  ```java
  System.out.println();
  ```

* `Alt + Insert`

  在定义一个标准类时，按 `Alt + Insert` 可以快速生成 `Getter/Setter` 方法，选择 `Constructor` 可以快速生成无参数和全参数的构造方法

# Java中的关键字

## 关键字的特点

* **完全小写**的字母
* 在增强版的记事本（如Notepad++）有特殊颜色



# 标识符

* **标识符**是指在程序中，我们自定义内容。比如类的名字、方法的名字、和变量的名字等
  * HelloWorld案例中，出现的标识符有类名字`HelloWorld`


* **命名规则**：`硬性要求`
  * 标识符可以包含`英文字母26个（区分大小写）`、`0~9数字`、`$（美元符号）`和`_（下划线）`
  * 标识符不能以数字开头
  * 标识符不能是关键字

* **命名规范**：`软性建议`
  * 类名规范：首字母大写，后面每个单侧首字母大写（大驼峰式）
  * 变量名规范：首字母小写，后面每个单词首字母大写（小驼峰式）
  * 方法名规范：同变量名



# 数据类型

## 数据类型的分类

Java的数据类型基本分为两大类：

* **基本数据类型**：包括`整数`、`浮点数`、`字符`、`布尔`
* **引用数据类型**：包括`字符串`、`类`、`数组`、`接口`

### 基本数据类型

四类八种基本数据类型：

| **数据类型** | 关键字           | 内存占用 | 取值范围              |
| ------------ | ---------------- | -------- | --------------------- |
| 字节型       | byte             | 1个字节  | -127~127              |
| 短整型       | short            | 2个字节  | -32768~32767          |
| 整型         | int（`默认`）    | 4个字节  | -2^31~2^31-1          |
| 长整型       | long             | 8个字节  | -2^63~2^63-1          |
| 单精度浮点数 | float            | 4个字节  | 1.4031E-45~3.4028E+38 |
| 双精度浮点   | double（`默认`） | 8个字节  | 4.9E-324~1.7977E+308  |
| 字符型       | char             | 2个字节  | 0~65535               |
| 布尔类型     | Boolean          | 1个字节  | true，false           |



## 数据类型转换

### 自动转换

一个`int`类型的变量和一个`byte`类型的变量进行加法运算，结果将会是`int`类型

* **自动转换**：将`取值范围小的类型`自动提升为`取值范围大的类型`。

  同样道理，当一个`int`类型的变量和一个`double`变量运算时，`int`类型将会自动提升为`double`类型进行运算

### **强制转换**

将`1.5`赋值到`int`类型变量会发生错误，编译失败。

`double`类型内存8个字节，`int`类型内存4个字节，`1.5`是`double`类型，取值范围大于`int`。要想赋值成功，只能通过强制类型转换。

* **强制类型转换**：将`取值范围大的类型`强制转换成`取值范围小的类型`

**转换格式**：

`数据类型 变量名 = (数据类型)被转换数据值`

 **强烈注意**：

* 浮点转成整数，直接取消小数点，可能造成数据损失精度。
* `int`强制转换成`short`砍掉连个字节，可能造成数据丢失。
* `byte`、`short`、`char`这三种类型在运算的时候，都会被首先提升为int类型，然后再计算



# 运算符

## 算数运算符

|   运算符   |           作用           |
| :--------: | :----------------------: |
|    `+`     | 加法运算，字符串连接运算 |
|    `-`     |         减法运算         |
|    `*`     |         乘法运算         |
|    `/`     |         除法运算         |
|    `%`     |         取模运算         |
| `++`、`--` |      自增、自减运算      |

**注意**：

* Java中，整数使用以上运算符，无论怎么计算，都不会得到小数。

```java
public static void main(String[] args){
    System.out.println(10 / 3);//计算结果是3
}
```

* `+`中字符串连接和字符串加减优先级

  ```java
  public static void main(String[] args){
      String str1 = "Hello,";
      System.out.println(str1 + 20 + 30);//结果是Hello,2030
  }
  ```



## 赋值运算符

| 运算符 |   作用   |
| :----: | :------: |
|  `=`   |   等于   |
|  `+-`  |  加等于  |
|  `-=`  |  减等于  |
|  `*=`  |  乘等于  |
|  `/=`  |  除等于  |
|  `%=`  | 取模等于 |

* 赋值运算符就是将符号右边的值赋给左边的变量

  ```java
  public static void mian(String[] args){
      int i = 5;
      i += 5;//	i = i + 5
      System.out.println(i)//10
  }
  ```



## 比较运算符

运算结果是布尔型



## 逻辑运算符

| 运算符 | 作用 |
| :----: | :--: |
|  `&&`  |  与  |
|  `\|\|`  |  或  |
|  `!`   |  非  |



## 三元运算符

* 格式：

  数据类型 变量 = 条件判断 ? 表达式A : 表达式B；

* 流程：

  首先判断条件是否成立：

  ​	如果成立，那么将表达式 A 的值赋值给左侧的变量；

  ​	如果不成立，那么将 B 赋值给左侧的变量；

  二者选其一。



# 方法入门

## 概述

**方法**：就是将一个功能抽取出来，把代码单独定义在一个大括号内，形成一个单独的功能。

当我们需要这个功能的时候，就可以去调用。这样即实现了代码的复用性，也解决了代码冗余的现象。



## 方法的定义

* 定义格式：

  ```java
  修饰符 返回值类型 方法名	(参数列表){
      代码...
       return ;
  }
  ```

* 定义格式解释;
  * 修饰符：目前固定写法 `public static`.
  * 返回值类型：目前固定写法 `void`，其他返回值类型在后面的课程讲解。
  * 方法名：为我们定义的方法起名，满足标识符的规范，来调用方法。

## 方法的定义

格式：方法名();



# 流程控制

## 判断语句

```java
if (关系表达式){
    语句体1;
}
else if (关系表达式){
    语句体2;
}
else {
    语句体3;
}
```



## 选择语句

* **`switch`语句格式：**

  ```java
  switch (表达式){
      case 常量值1:
          语句体1;
          break;
      case 常量值2:
          语句体2;
          break;
          ...
      default:
          语句体n+1;
          break;
  }
  ```

* **流程**
  1. 计算出表达式的值；
  2. 和 `case` 值比较，一旦有对应的值，就会**从该条语句开始执行**，在执行的过程中，遇到 `break` 就会结束；d
  3. 如果所有的 `case` 都和表达式不匹配，就会执行 `default` 语句体部分，然后程序结束；

* **注意**：
  * `switch` 后面小括号中只能是以下数据类型：
    * 基本数据类型：byte/short/char/int
    * 引用数据类型：String字符串/enum枚举
  * `switch` 语句格式可以很灵活：前后顺序可以颠倒，`break` 可以省略。`break` 省略的时候，由于是从匹配的 `case` 值**开始执行**，因此，会发生 **`case` 穿透**



## 循环语句

### for 循环

```java
for (初始化表达式；布尔表达式；步进表达式){
    循环体;
}
```

**注意**：`for` 循环里的 `i` 只能在 `for` 循环里使用



### while 循环

```java
初始化表达式;
while (布尔表达式){
	循环体;
	步进表达式;
}
```



### do ... while 循环

```java
初始化表达式;
do{
    循环体;
    步进表达式;
}
while (布尔表达式);
```

会先无条件执行一次 `do` 里面的内容，然后再执行 `while` 判断



# 方法详解

## 回顾

```java
修饰符 返回值类型 方法名(参数类型 参数名称,...){
    代码...
     return 返回值;
}
```

* 修饰符：`public static` 固定写法 
* 返回值类型： 表示方法运行的结果的数据类型，方法执行后将结果返回到调用者 
* 参数列表：方法在运算过程中的未知数据，调用者调用方法时传递
* return：将方法执行后的结果带给调用者，方法执行到 return ，整体方法运行结束



## 方法的三种调用格式

* 单独调用

  方法名称(参数);

* 打印调用

  把单独调用放在赋值语句里面

  ```java
  System.out.println(方法名称(参数));
  ```

* 赋值调用

  数据类型 变量名称 = 方法名称(参数);

  

## 注意事项

* 方法不能嵌套
* 一个方法中可以有个多个 `return` 语句，但是必须保证同时只有一个会被执行。



## 方法重载

多个方法的名称一样，但是参数列表不一样

好处：只需要记住唯一一个方法名称，就可以实现类似的多个功能

下面的例子中，完成了对对两个、三个、四个数字求和的方法

```java
public class MethodOverload {
    public static void main(String[] args) {
        System.out.println(sum(10, 20));
    }
    public static int sum(int a, int b){
        return a + b;
    }

    public static int sum(int a, int b, int c){
        return a + b + c;
    }

    public static int sum(int a, int b, int c, int d){
        return a + b + c + d;
    }
}

```



# 数组

* 数组是一种引用数据类型

* 数组当中的多个数据，类型必须统一

* 数组的长度在程序运行期间不可改变

* 数组的初始化：

  * 动态初始化（指定长度）

    数据类型[] 数组名称 = new 数据类型[数组长度];

    ```java
    // 动态初始化一个300的 int 类型数组
    int [] ArrayInt = new int [300];
    // 动态初始化一个5的 String 类型数组，里面可以存放 5 个字符串
    String[] ArrayStr = new String[5];
    
    ```

  * 静态初始化（指定内容）

    * 标准格式：数据类型[] 数组名臣 = new 数据类型[] {元素1, 元素2, ...};

    ```java
    //静态初始化一个放食物的 food 数组
    String[] food = new String[]{"rice", "noodle"};
    ```

    * 省略格式：数据类型[] 数组名称 = {元素1, 元素2, ...}

    ```java
    int[] array = {10, 20, 30};
    ```

* 注意：

  * 直接打印输出数组名的话会得到数组的内存信息
  * 对于动态初始化的数组，元素会自动拥有一个默认值：
    * 数组为整数类型，默认为 0；
    * 数组为浮点类型，默认为 0.0；
    * 数组为字符类型，默认为‘\u0000’；
    * 如果是布尔类型，默认为 false；
    * 如果是引用类型，默认为 null

* 数组的基本操作
  * 获取数组长度：数组名称.length
  * 数组的遍历：`数组名称.fori` `Tab` 键补全



# Java中的内存划分

1. **栈（Stack）：**存放的都是方法中的局部变量。方法的运行一定要在栈当中运行
2. **堆（Heap）：**凡是 `new` 出来的东西，都在堆当中。堆内存里的东西都有地址值，堆内存里的数据都有默认值
3. **方法区（Method Area）：**存储 `.class` 相关信息，包含方法的信息
4. **本地方法栈（Native Method Stack）：**与操作系统相关
5. **寄存器（PC Register）：**与 CPU 相关



# 面向对象思想

## 概述

**对象**泛指一切事物，每种事物都具备自己的**属性**和**行为**。面向对象思想就是在计算机程序设计过程中，参照现实中的事物，将事物的属性特征、行为特征抽象出来，描述成计算机时间的设计思想。它区别于面向过程思想，强调的是通过调用对象的行为来实现功能，而不是自己一步一步地去操作实现。

## 类和对象

### 什么是类

* **类**：是一组相关**属性**和行为的集合，可以看成是一类事物的模板，使用事物的属性特征和行为特征来描述该类事物。
* **属性**：开水奇偶该事物的状态信息。
* **行为**：就是该事物能够做什么。

### 什么是对象

* **对象**：是一类事物的具体体现，对象是类的一个**实例**，必须具备该类事物的属性和行为。

### 类和对象的关系

* 类是对一类事物的描述，是**抽象的**
* 对象是一类事物的实例，是**具体的**
* **类是对象的模板，对象是类的实体**



## 类的定义

* **定义格式**

  ```java
  public class ClassName(){
      // 成员变量
      // 成员方法
  }
  ```

  * **定义类**：就是定义类的成员，包括**成员变量**和**成员方法**。
  * **成员变量**：和以前的定义几乎一样，只不过是位置发生了改变。成员变量的定义**在类中，方法外**
  * **成员方法**：和以前的定义几乎一样，只不过**把 `static` 去掉**，`static` 的作用见后。

  举例：

  ```java
  public class Student {
  
      // 成员变量
      String name;    // 姓名
      int age;    //年龄
  
      // 成员方法
      public void eat(){
          System.out.println("吃饭！！！！！！");
  
      }
  
      public void sleep(){
          System.out.println("睡觉！！！！！！！");
  
      }
  
      public void study(){
          System.out.println("学习！！！！！！");
      }
  
  }
  ```

* **使用**

  1. 导包

     指出所需要使用的类在什么位置

     ```java
     import 包名称.类名称;
     ```

  2. 创建格式：

     ```java
     类名 对象名 = new 类名();
     ```

  3. 使用分为两种

     * 使用成员变量：对象名.成员变量;
     * 使用成员方法：对象名.成员方法名(参数);

## 对象的使用

* 创建对象

  ```java
  类名 对象名 = new 类名();
  ```

* 使用对象访问类中的成员：

  ```java
  对象名.成员变量;
  对象名.成员方法名(参数);
  ```

* 一个对象的内存图

  ![Java类的内存图](https://i.loli.net/2021/05/19/QhZzT3XcNn4FDtu.png)

* 两个对象的内存图

  ![两个对象的内存](https://i.loli.net/2021/05/19/HIJmjO9CBr78xZM.png)

* 两个引用指向同一个对象内存

  ![两个引用指向同一个对象内存](https://i.loli.net/2021/05/19/eATGRybgHkm1pUM.png)

* 使用对象类型作为方法的参数

  ![使用对象类型作为方法的参数](https://i.loli.net/2021/05/19/S4WdGagJNYvyR3H.png)

* 使用对象类型作为方法的返回值

  ![使用对象类型作为方法的返回值](https://i.loli.net/2021/05/19/USxvTBQRtjE6k5G.png)

## 成员变量与局部变量

1. **定义的位置不同**
   * 局部变量：在方法的内部
   * 成员变量：在方法的外部，在类之中
2. **作用范围不一样**
   * 局部变量：只有在方法中才可以使用，方法之外不能用
   * 成员变量：整个类都可以用
3. **默认值不一样**
   * 局部变量：没有默认值，如果想使用，必须手动赋值
   * 成员变量：如果没有赋值，会有默认值，规则见前
4. **内存位置不一样**
   * 局部变量：位于栈内存
   * 成员变量：位于堆内存
5. **生命周期不一样**
   * 局部变量：随着方法进栈而诞生，随着方法出栈而消失
   * 成员变量：随着对象创建而诞生，随着垃圾回收（ JVM 控制）而消失



# 封装

## 概述

面向对象编程语言是对客观世界的模拟，客观世界里成员变量都是隐藏在对象内部的，外界无法直接操作和修改。 封装可以被认为是一个保护屏障，防止该类的代码和数据被其他类随意访问。要访问该类的数据，必须通过指定的 方式。适当的封装可以让代码更容易理解与维护，也加强了代码的安全性。 

## 原则

将**属性隐藏**起来，若需要访问某个属性，**提供公共方法**对其访问。

## 步骤

1. 使用 `private` 关键字来修饰成员变量。
2. 对需要访问的成员变量，提供对应的一对 `getter` 方法 、 `setter` 方法。 

## 封装的操作—— `private` 关键字

### `privte` 的含义

1.  `private` 是一个权限修饰符，代表最小权限

2. 可以修饰成员变量和成员方法。 

3.  被private修饰后的成员变量和成员方法，只在本类中才能访问。

   正因为用 `private` 修饰之后超出本类范围之外就不能直接访问了，所以需要间接的方法——定义一对 `getter` 方法 、 `setter` 方法。

   这样做的好处是，可以在 `getter` 方法 、 `setter` 方法中**添加其他代码来对传入的内容审核**，保证了代码的安全性

### `private` 的使用格式

```java
private 数据类型 变量名
```

1.  使用 `private` 修饰成员变量，代码如下：

   ```java
   public class Person {
       String name;
       private int age;
   
       public void show() {
           System.out.println("我叫" + name + "，我今年" + age + "了！");
   
       }
       // 这个成员方法，专门用于向 age 设置数据
       public void setAge(int age) {
           if (age < 100 && age >= 0) {
               this.age = age;
           }
           else {
               System.out.println("参数错误！！！");
           }
       }
   
       // 这个成员方法，专门用于获取 age 的数据
   
       public int getAge() {
           return age;
       }
   }
   ```

   这里的 `age` 被 `private` 修饰了，所以在其他类中不能直接访问。

   在其他类中要想访问，必须通过 `setAge` 和 `getAge()` 来间接赋值和访问。

   这里在 `setAge` 方法中还添加了判断 `age` 设置是否合理的代码，保证了代码的有效性。

2. 使用 `setXxx` 和 `getXxx` 来赋值和访问 `private` 修饰的变量

   ```java	
   import Person;
       
   public class DemoPerson {
       public static void main(String[] args) {
           Person person = new Person();
           person.name = "王祖贤";
   //        person.age = 18; // 直接访问 private 内容是错误写法
           person.setAge(60);
   
           person.show();
       }
   }
   
   ```

3. **注意：**

   * 对于 `boolean` 值，`Getter` 方法一定要写成 `isXxx` 的形式，而 `setXxx` 不变

   * 当方法的局部变量和成员变量重名的时候，根据就近原则，优先使用局部变量。

     如果需要访问本类中的成员变量，需要使用格式：this.成员变量名

     通过谁调用的方法，谁就是 this

### 构造方法

* 构造方法不能通过普通方法以 ” . “ 的形式来使用，只能以 `new` 的方法使用

* 当一个对象被创建时候，构造方法用来初始化该对象，给对象的成员变量赋初始值。

* 无论你与否自定义构造方法，所有的类都有构造方法，因为Java自动提供了一个无参数构造方法， 一旦自己定义了构造方法，Java**自动提供的默认无参数构造方法**就会失效。 

* 前面使用 `new` 来创建一个新的对象的时候，就使用了自动提供的默认的无参数构造方法

  ```java
  Student xiaohong = new Student();
  ```

#### 构造方法的定义格式

```java
修饰符 构造方法名 (参数列表){
    方法体
}
```

构造方法的写法上，方法名与它所在的类名相同。它没有返回值，所以不需要返回值类型，不需要 void。使用构造方法后，代码如下：

```java
public class Student {   
    private String name;   
    private int age;   
    // 无参数构造方法   
    public Student() {}    
    // 有参数构造方法   
    public Student(String name,int age) {     
        this.name = name;     
        this.age = age;    
    } 
}
```

### 定义一个标准的类（Java Bean）

一个标准的类通常拥有下面四个组成部分：

1. 所有的成员变量都要使用 private 关键字修饰

2. 为每一个成员变量编写一对 Getter/Setter 方法
3. 编写一个无参数的构造方法
4. 编写一个全参数的构造方法



# API

* 使用 `API` 帮助文档
  1. 打开帮助文档
  2. 点击显示，找到索引，看到输入框。
  3. 在输入框里输入需要寻找的关键字，然后回车。 
  4. . 看包。java.lang下的类不需要导包，其他需要。
  5. 看类的解释和说明。
  6. 学习构造方法

# Scanner类

* 示例代码

  ```java
  import java.util.Scanner;
  /*
  键盘输入两个数，并进行求和。
   */
  public class ScannerSum {
      public static void main(String[] args) {
          Scanner sc = new Scanner(System.in);
  
          int num1 = sc.nextInt();
          int num2 = sc.nextInt();
  
          System.out.println("输入的两个数分别是：" + num1 + ", " + num2);
          System.out.println("他们的和是：" + sum(num1, num2));
      }
  
      public static int sum(int a, int b) {
          return a + b;
      }
  }
  ```

## 匿名对象

### 概念

没有变量名的对象							

创建对象时，只有创建对象的语句，却没有把对象地址值赋值给某个变量。虽然是创建对象的简化写法，但是应用 场景非常有限

匿名对象只能使用一次

### 格式

```java
new 类名(参数列表);
```

### 举例

```java
new Scanner(System.in);
```



### 引用场景

1. 创建匿名对象直接调用方法，没有变量名。

2.  匿名对象可以作为方法的参数和返回值

   * 例子：

     ```java
     package Anonymous;
     
     import java.util.Scanner;
     
     public class Demo01Anonymous {
         public static void main(String[] args) {
             // 普通方式
     //        Scanner sc = new Scanner(System.in);
     //        int num = sc.nextInt();
     
             // 匿名对象的方式
     //        int num = new Scanner(System.in).nextInt();
     //        System.out.println("输入的数字是：" + num);
     
             // 使用一般方法传入参数
     //        Scanner sc = new Scanner(System.in);
     //        methodParam(sc);
     
             // 使用匿名对象来进行传参
     //        methodParam(new Scanner(System.in));
     
             // 使用匿名对象作为返回值
             Scanner sc = methodReturn();
             int num = sc.nextInt();
             System.out.println("输入的参数是：" + num);
         }
     
         public static void methodParam(Scanner sc) {
             int num = sc.nextInt();
             System.out.println("输入的数字是：" + num);
         }
     
         public static Scanner methodReturn() {
             return new Scanner(System.in);
         }
     }
     
     ```

     

# Random 类

* 举例：

  ```java
  package Random;
  
  import java.util.Random;
  import java.util.Scanner;
  
  public class GuessNum {
      public static void main(String[] args) {
  
          int num1 = new Random().nextInt(101);
  //        System.out.println("电脑给出的数字是：" + num1);
  
          int i = 0;
          boolean flag = true;
          while (flag) {
              System.out.print("选一个0 ~ 100 之间的数字：");
              int num2 = new Scanner(System.in).nextInt();
              System.out.println("你猜的数字是：" + num2);
  
              i++;
              flag = isclose(num1, num2, i);
              System.out.println("====================");
          }
      }
  
      public static boolean isclose(int a, int b, int i) {
          boolean flag = true;
          if (a > b) {
              System.out.println("你猜的数字小了");
          } else if (a == b) {
              System.out.println("恭喜你，你才猜了" + i + "就次猜对了");
              flag = false;
          } else {
              System.out.println("你猜的数字大了");
          }
          return flag;
  
      }
  }
  
  ```



# ArrayList 类

## 简介

数组的长度是不可以发生改变的，但`java.util.ArrayList` 是大小可变的数组的实现，存储在内的数据称为元素。此类提供一些方法来操作内部存储 的元素。 `ArrayList` 中可不断添加元素，其大小也自动增长。

## 使用方法

* 创建一个 `String` 类型的 `ArrayList` :

  ```java
  ArrayList<String> list = new ArrayList<String>();
  ```

  `<E>` ，表示一种指定的数据类型，叫做泛型。 `E` ，取自 `Element`（元素）的首字母。在出现 `E` 的地方，我们使用一种**引用数据类型**将其替换即可，表示我们将存储哪种引用类型的元素。

  从 JDK 1.7 + 开始，**右侧的尖括号内部可以不写内容，但是 <> 本身需要写**

  ```java
  ArrayList<String> list = new ArrayList<>();
  ```

* 常用方法
  1. `public boolean add(E e)` ：将指定的元素添加到此集合的尾部。 
  2. `public E remove(int index)` ：移除此集合中指定位置上的元素。返回被删除的元素。 
  3. `public E get(int index)` ：返回此集合中指定位置上的元素。返回获取的元素。
  4. `public int size()` ：返回此集合中的元素数。遍历集合时，可以控制索引范围，防止越界。

## 如何存储基本数据类型

`ArrayList` 对象不能存储基本类型，只能存储引用类型的数据。类似 ` <int>`  不能写，但是存储基本数据类型对应的包装类型是可以的。所以，想要存储基本类型数据， `<>` 中的数据类型，必须**转换后才能编写**，转换写法如下：

| 基本类型 | 基本包装类型 |
| :------: | :----------: |
|   byte   |     Byte     |
|  short   |    Short     |
|   int    |   Integer    |
|   long   |     Long     |
|  float   |    Float     |
|  double  |    Double    |
|   char   |  Character   |
| boolean  |   Boolean    |

从 `JDK 1.5+` 开始，支持自动装箱、自动拆箱

* 自动装箱： 基本类型 ————> 包装类型
* 自动拆箱： 包装类型 ————> 基本类型

例子：

```java
public class Demo05ArrayListBasic {
    public static void main(String[] args) {
        ArrayList<String> listA = new ArrayList<>();

        // 错误写法，因为集合里面保存的都是地址值，而基本数据类型没有地址值
//        ArrayList<int> listB = new ArrayList<int>();

        ArrayList<Integer> listB = new ArrayList<>();
        listB.add(20);
        listB.add(65);
        listB.add(5);
        listB.add(95);
        int num = listB.get(0);
        System.out.println("第零号元素是：" + num);
        System.out.println(listB);


    }
}
```

* `ArrayList` 既可以作为参数传入，也可以作为参数传出：

  ```java
  import java.util.ArrayList;
  import java.util.Random;
  
  public class Demo07ArrayListReturn {
      public static void main(String[] args) {
          ArrayList<Integer> listA = new ArrayList<>();
          Random rd = new Random();
          for (int i = 0; i < 20; i++) {
              int num = rd.nextInt(101);
              listA.add(num);
          }
          System.out.println("原集合是：" + listA);
          ArrayList listB = iseven(listA);
          System.out.println("由其中的偶数组成的集合是：" + listB);
  
      }
  
      public static ArrayList iseven(ArrayList<Integer> list) {
          ArrayList<Integer> listB = new ArrayList<>();
          for (int i = 0; i < list.size(); i++) {
              if (list.get(i) % 2 == 0) {
                  listB.add(list.get(i));
              }
          }
          return listB;
      }
  }
  ```

  

# String 类

## 概述

`java.lang.String` 类代表字符串。Java 程序中所有的字符串文字（例如 `"abc"` ）都可以被看作是**实现此类的实例。**
类 `String` 中包括用于检查各个字符串的方法，比如用于**比较**字符串，**搜索**字符串，**提取**子字符串以及创建具有翻译为**大写**或**小写**的所有字符的字符串的副本

## 特点

1. 字符串不变：字符串的值在创建后不能被更改。

   ```java
   String s1 = "abc"; 
   s1 += "d"; System.out.println(s1); // "abcd"  
   // 内存中有"abc"，"abcd"两个对象，s1从指向"abc"，改变指向，指向了"abcd"。
   ```

2. 因为 `String` 对象是不可变的，所以它们可以被共享以节约内存

   ```java
   String s1 = "abc"; 
   String s2 = "abc"; // 内存中只有一个"abc"对象被创建，同时被s1和s2共享。
   ```

3. 字符串效果上相当于是 `char[]` 字符数组，最底层原理是 `byte[]` 字节数组。

   ```java
   // 例如：  
   String str = "abc";   
   // 相当于：  char data[] = {'a', 'b', 'c'};      
   String str = new String(data); 
   // String底层是靠字符数组实现的。
   ```

## 使用

* `public String()` ：初始化新创建的 `String` 对象，以使其表示空字符序列。
* `public String(char[] value)` ：通过当前参数中的字符数组来构造新的 `String`。 
* `public String(byte[] bytes)` ：通过使用平台的默认字符集解码当前参数中的字节数组来构造新的 `String` 。
* String str = "abc"  ：直接写上双引号，就是字符串对象（Jvm 帮你 new）。

## 字符串常量池

* 字符串常量池：程序当中直接写上的双引号字符串，就在字符串常量池中。
  * 对于基本类型来说，== 是进行数值的比较
  * 对于引用类型来说，== 是进行地址值的比较

```java
public class Demo02StringPool {
    public static void main(String[] args) {
        String str1 = "abc";
        String str2 = "abc";

        char[] charArray = {'a', 'b', 'c'};
        String str3 = new String(charArray);

        System.out.println(str1 == str2);   //true str1 的地址值和 str2 的地址值一样
        System.out.println(str2 == str3);   //false str3 的地址值和 str2 的地址值不一样
        System.out.println(str1 == str3);   //false str1 的地址值和 str3 的地址值不一样
    }
}
```

![StringPool内存](https://i.loli.net/2021/05/19/Hcf3SRjbdgAZqoF.png)

## 常用方法

1. **字符串比较**

   `==`  是进行对象的地址值比较，如果确实需要字符串的内容比较，可以使用两个方法

   * public boolean equals(Object obj)：

     参数可以是任何对象，只有参数是一个字符串并且内容相同才会返回 true

   * public boolean equalsIgnoreCase(String str)：

     忽略大小写，进行内容比较

   **注意**：

   1. 任何对象都能使用 Object 进行接收。
   2. 如果比较双方一个是常量一个是变量，推荐把字符常量字符串写在前面。

2. **字符串获取**
   * `public int length ()` ：返回此字符串的长度。 
   * `public String concat (String str)` ：将指定的字符串连接到该字符串的末尾。 
   * `public char charAt (int index) `：返回指定索引处的 char值。 
   * `public int indexOf (String str)` ：返回指定子字符串第一次出现在该字符串内的索引，如果没有返回 -1。 
   * `public String substring (int beginIndex)` ：返回一个子字符串，从beginIndex开始截取字符串到字符 串结尾。 
   * `public String substring (int beginIndex, int endIndex)`：返回一个子字符串，从beginIndex到 endIndex截取字符串。含beginIndex，不含endIndex

3. **字符串转换**

   * `public char[] toCharArray()`：将当前字符串拆分成为字符数组作为返回值

   * `public byte[] getBytes()`：获取当前字符串底层的字节数组

   * `public String replace(CharSequence oldString, CharSequence newString)`：

     将所有出现的老字符串替换成新的字符串，返回替换后的结果新字符串

   **备注**：CharSequence 意思就是可以接受字符串类型

4. **字符串的分割**

   * public String[] split(String regex)：按照参数的规则，将字符串切分成为若干部分

   **注意事项**：

   1. split 方法的参数其实是一个"正则表达式"。要注意：如果按照英文句点 “.” 进行切分，必须写 "\\\\." （两个反斜杠）



# Static 关键字

## 引入

* `static` 是属于类的，这样所有的成员都可以共享使用，这样不仅节省内存，而且便于后期修改：

  ![Static引入](https://i.loli.net/2021/05/19/4F8YlBHwAdEbrP5.png)

## 概述

关于 `static` 关键字的使用，它可以用来修饰的成员变量和成员方法，被修饰的成员是属于类的，而不是单单是属 于某个对象的。也就是说，既然属于类，就可以不靠创建对象来调用了。

## 定义和使用格式

### 类变量

当 `static` 修饰成员变量时，该变量称为**类变量**。该类的每个对象都共享同一个类变量的值。任何对象都可以更改 该类变量的值，但也可以在不创建该类的对象的情况下对类变量进行操作。

定义格式：

```java
static 数据类型 变量名;
```

举例;

```java
static int numberID;
```

使用举例;

比如，对于一个班级来说，每个学生对象都有自己的名字，年龄，学号等，但他们所属的教室却是相同的、静态的，因此，可以在类里定义一个静态变量 `room` 来存放这类学生的教室。

另外，从第一名同学开始，`id` 为 1，以此类推。学号必须是唯一的，连续的，并且与班级的人数相符，这样以便知道，要分配给下一名新同学的学号是多少。这样我们就需要一个变量，与单独的每一个学生对象无关，而是与整个班级同学数量有关。所以，我们可以定义一个静态变量 `idCounter` ，代码如下：

```java
package Static;

public class Student {
    private int id;   // 学号
    private String name;    // 姓名
    private int age;    // 年龄
    private static int idCounter = 0;   // 学号计数器，每当 new 了一个新对象，计数器加一

    static String room; // 所在教室

    public Student() {
        this.id = ++idCounter;
    }

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
        this.id = ++idCounter;
    }

    // Gerter & Seter 方法....
}

```

### 类方法

当 `static` 修饰成员方法时，该方法称为**类方法** 。静态方法在声明中有 `static` ，建议使用类名来调用，而不需要 创建类的对象。

定义格式:

```java
修饰符 static 返回值类型 方法名(参数列表){
    // 执行语句
}
```

举例：在 `Student` 类中定义静态方法

```java
public static void methodStatic(){
    System.out.println("这是一个静态方法");
}
```

**注意事项：**

1. 静态方法只能访问静态成员。
2. 静态方法可以直接访问类变量和静态方法。
3. 静态方法不能直接访问普通成员变量或成员方法。反之，成员方法可以直接访问类变量或静态方法。 
4. 静态方法中，不能使用 `this` 关键字。

### 调用格式

被 `static` 修饰的成员可以并且建议直接通过**类名直接访问**。

```java
// 访问类变量 
类名.类变量名；   
// 调用静态方法 
类名.静态方法名(参数)
```

代码演示：

```java
package Static;
/*
注意事项:
1. 静态不能直接访问非静态
原因：在内存当中是【先有】的静态内容，【后有】的非静态内容。
2. 静态方法中不能使用 this。
原因：this 代表当前对象，通过谁调用的方法，谁就是当前对象。
 */

public class Demo02StaticMethod {
    public static void main(String[] args) {
        MyClass one = new MyClass();    // 首先创建对象
        // 然后才能使用没有 static 关键字的内容
        one.method();

        // 对于静态方法来说，可以通过对象名进行调用（可以，但没必要）
        // 也可以直接通过类名称来调用
        one.methodStatic(); // 正确，但不推荐。
        // 这种写法在编译之后也会被 javac 翻译成为类名称.静态方法名

        MyClass.methodStatic(); // 正确且推荐

        // 对于本类当中的静态方法，可以省略类名称
        myMethod();
        Demo02StaticMethod.myMethod();  // 完全等效

    }

    public static void myMethod(){
        System.out.println("这是自己的方法。");
    }
}

```

## 静态原理图解

![static内存](https://i.loli.net/2021/05/19/2RPAKTGDceWsaCH.png)

## 静态代码块

```java
package Static;

/*
静态代码块的格式是:
public class 类名称{
    static{
        // 静态代码块的内容
    }
}
 */
// 特点：当第一次使用到本类时，静态代码块执行唯一的一次。
public class Person {
    static {
        System.out.println("静态代码块执行！！");
    }

    public Person(){
        System.out.println("构造方法执行！！！");
    }
}

```

```java
package Static;

/*
// 静态内容总是优先于非静态，所以静态代码块比构造方法先执行

// 静态代码块的典型用途：
// 用来一次性地对静态成员变量进行赋值

public class Demo03Static {
    public static void main(String[] args) {
        Person one = new Person();
        Person two = new Person();

    }
}

```



# Arrays 类

## 概述

`java.util.Arrays` 此类包含用来操作数组的各种方法，比如排序和搜索等。其所有方法均为静态方法，调用起来 非常简单

## 常用方法

* `public static String toString(数组)`：将参数数组变成字符串（按照[元素1，元素2，...]）
*  `public static void sort(数组)`：按照默认升序对数组的元素进行排序

备注：
1. 如果是数值，sort 默认按照升序从小到大
2. 如果是字符串，sort 默认按照字母升序
3. 如果是自定义的类型，那么这个自定义的类型需要有 Comparable 或者 Comparator 接口。



# Math 类

## 概述

`java.lang.Math` 类包含用于执行基本数学运算的方法，如初等指数、对数、平方根和三角函数。类似这样的工具 类，其所有方法均为静态方法，并且不会创建对象，调用起来非常简单。 

## 常用方法

* `public static double abs(double num)`：获取绝对值
* `public static double ceil(double num)`：向上取整
* `public static double floor(double num)`：向下取整
* `public static long round(double num)`：四舍五入



# 继承

## 引入

多个类中存在相同属性和行为时，将这些内容抽取到单独一个类中，那么多个类无需再定义这些属性和行为，只要 继承那一个类即可。继承主要解决的问题就是：**共性抽取**

![继承引入](https://i.loli.net/2021/05/19/bZOTEmFv78XR5lw.png)

继承描述的是事物之间的所属关系，这种关系是： `is-a` 的关系。例如，父类是员工，子类是讲师，那么“讲师就是一个员工”。关系：`is-a`。可见，父类更通用，子类更具体。通过继承，可以使多种事物之间形成一种关系体系。 

* **继承：**就是子类继承父类的**属性**和**行为**，使得子类对象具有与父类相同的属性、相同的行为。子类可以直接 访问父类中的**非私有**的属性和行为。 

## 格式

通过 `extends` 关键字，可以声明一个子类继承另外一个父类，定义格式如下：

```java
class 父类 { 
    ...      
}   
class 子类 extends 父类 { 
    ...      
} 
```

## 继承后的特点——成员变量

* 父类与子类定义的成员变量**不重名**时，访问是**没有任何影响的**，即子类可以轻松地访问定义在父类中的成员变量，因为此时每一个变量都是唯一可识别的。

* 父类与子类定义的成员变量**重名**时，访问是有影响的。

  这是因为在子类中访问成员变量时，总是**先从本类中找是否有此变量，没有在向上（父类）找**。

  子父类中出现了同名的成员变量时，在子类中需要访问父类中非私有成员变量时，需要使用 super 关键字，修饰 父类成员变量，类似于之前学过的 `this` 。

  ```java
  public class Zi extends Fu{
      int num = 50;
  
      public void methodZi(){
          // 因为本类当中有 num，所以这里用的是本类的 num。
          System.out.println(num);
  
  
          int num = 30;
          System.out.println(num);    // 30 局部变量
          System.out.println(this.num);   // 50 本类的成员变量
          System.out.println(super.num);  // 100 父类的成员变量
      }
  }
  
  ```


## 继承后的特点——成员方法

* 父类与子类定义的成员方法**不重名**时。这是的调用是**没有任何影响的**。对象调用方法时，会在子类中查找有没有对应的方法，若子类中存在就会执行子类中的方法，若子类中不存在就会执行父类中相应的方法。

  ```java
  class Fu{ 
      public void show(){
          System.out.println("Fu类中的show方法执行");
      }
  }
  class Zi extends Fu{
      public void show2(){
          System.out.println("Zi类中的show2方法执行");
      }
  } 
  public  class ExtendsDemo04{
      public static void main(String[] args) {
          Zi z = new Zi();
          //子类中没有show方法，但是可以找到父类方法去执行
          z.show();	// Fu类中的show方法执行
          z.show2();	// Zi类中的show2方法执行
      }
  }
  ```

* 父类与子类定义成员方法**重名**时。叫做**方法重写（Override）**。

  * **方法重写**：在继承关系中，方法的名称一样，参数列表也一样。也叫覆盖、覆写。**声明不变，重新实现**。

  * **注意事项**：

    1. 保证父子间方法名称相同，参数列表也相同。可用 `@Override`写在方法前面，用来检测是不是有效的正确覆盖重写。
    2. 类方法的返回值必须**小于等于**父类方法的返回值范围。
       如：`java.lang.Object` 类是所有类的公共最高父类
               `java.lang.String` 就是 Object 的子类
    3. 类方法的权限必须**大于等于**父类方法的权限修饰符
           `public` > `protected` > `(default)` > `private`
           备注：(`default`) 不是关键字 `default` ， 而是留空，什么都不写

  * 应用场景：子类可以根据需要，定义特定于自己的行为。既沿袭了父类的功能名称，又根据子类的需要重新实现父类方法，从 而进行扩展增强。比如新的手机增加来电显示头像的功能，代码如下：

    ```java
    class Phone {
        public void sendMessage(){
            System.out.println("发短信");
        }
        public void call(){
            System.out.println("打电话");
        }
        public void showNum(){
            System.out.println("来电显示号码");
        }
    }
    //智能手机类
    class NewPhone extends Phone {
        //重写父类的来电显示号码功能，并增加自己的显示姓名和图片功能
        public void showNum(){
            //调用父类已经存在的功能使用super
            super.showNum();
            //增加自己特有显示姓名和图片功能
            System.out.println("显示来电姓名");
            System.out.println("显示头像");
        }
    } 
    public class ExtendsDemo06 {
        public static void main(String[] args) {
            // 创建子类对象
            NewPhone np = new NewPhone()；
                // 调用父类继承而来的方法
                np.call();
            // 调用子类重写的方法
            np.showNum();
        }      
    
    ```

## 继承后的特点——构造方法

继承关系中，父子类构造方法的访问特点：

1. 子类构造方法中有一个隐含的 super() 调用，所以一定是先调用的父类构造，后执行的子类构造
2. 子类构造可以通过 super 关键字来父类重载构造
3. `super` 的父类构造调用，必须是子类构造方法的第一个语句，不能一个子类构造调用多次 `super` 构造

总结

* 子类必须调用父类构造方法，不写则赠送 super()；写了则用指定的 super(参数) 调用
* `super` 只能有一个，还必须在第一句

示例代码：

```java
public class Fu {
    public Fu(){
        System.out.println("父类无参构造方法！！");
    }

    public Fu(int num){
        System.out.println("父类有参构造方法！！");
    }
}
package Override;

/*
在子类继承父类时，执行子类构造方法时，默认是会执行父类无参构造方法的
如果父类中写了有参构造方法，而没有写无参构造方法，在子类中写无参构造方法时会报错
    此时的解决方法是要么在父类中写一个无参构造方法，要么在写子类构造方法时手动执行 super(参数)
 */

public class Zi extends Fu{
    public Zi(){
//        super();    // 在调用父类无参构造方法
        super(20);  // 在调用父类重载的构造方法
        System.out.println("子类构造方法！！");
    }

    public void method(){
//        super();  // 错误写法！只有子类构造方法才能调用父类构造方法
    }
}

```



## super 和 this 关键字

* **`super`**：用来访问父类内容。代表**父类的存储空间标识**(可以理解为父亲的引用)。 

  用法有三种：

  1. 在子类的成员方法中，访问父类的成员变量。
  2. 在子类的方法成员中，访问父类的成员方法。
  3.  在子类的构造方法中，访问父类的构造方法。

* **`this`**：用来访问本类内容。代表当**前对象的引用**(谁调用就代表谁)。 

  用法有三种：

  1. 在本类的成员方法中，访问本类的成员变量。
  2. 在本类的成员方法中，访问本类的另一个成员方法（强调不是继承自父类的方法）。
  3. 在本类的构造方法中，访问本类的另一个构造方法。(必须是构造方法的第一个语句，且是唯一一个)

`this` 示例代码：

```java
public class Fu {
    int num = 30;
}

public class Zi extends Fu {

    int num = 20;

    public Zi() {

        this(12);   // 本类的无参构造，调用本类的有参构造
    }

    public Zi(int n) {

    }

    public void showNum() {
        int num = 10;
        System.out.println(num);    // 局部变量
        System.out.println(this.num);   // 本类中的成员变量
        System.out.println(super.num);  // 父类中的成员变量
    }

    public void methodA() {
        System.out.println("AAAA");
    }

    public void methodB() {
        this.methodA();
        System.out.println("BBBB");
    }
}
```

内存关系：![SuperThis内存](https://i.loli.net/2021/05/19/D89aVUjFxZ2PgCc.png)



## Java 中继承的特点

* `Java` 只支持单继承，不支持多继承（最多只能有一个直接父类）。
* `Java` 支持多层继承。（顶层父类是 `Object` 类。所有的类默认继承 `Object` 作为父类）。
* `Java` 中一个子类的直接父类是唯一的，但是一个父类可以拥有很多个子类。



# 抽象类

## 引入

如果父类当中的方法不确定如何进行方法体**具体**实现，那么这就是一个**抽象方法**。

如父类是图形，其中有一个求面积的方法，子类包含正方形、圆形、三角形等众多形状，对于父类，没有办法写出统一的求面积的方法，对于每一个子类，重写自父类的求面积方法不尽相同，因此父类图形就是一个抽象类

## 定义

* **抽象方法**：没有方法体的方法。
* **抽象类**：包含抽象方法的类。

## abstract 使用格式

### 抽象方法

使用 `abstract` 关键字修饰方法，该方法就成了抽象方法，抽象方法只包含一个方法名，而没有方法体。

定义格式;

```java
修饰符 abstract 返回值类型 方法名 (参数列表)；
```

代码举例：

```java
public abstract void eat();
```

### 抽象类

如果一个类包含抽象方法，那么该类必须是抽象类。

代码举例：

```java
public abstract class Animal {
    public abstract void eat();
}
```

### 抽象的使用

继承抽象类的子类**必须重写父类所有的抽象方法**。除非，该子类也为抽象类。最终，必须有子类实现该父类的抽象方法，否则，从最初的父类到最终的子类都不能创建对象，失去意义。

## 注意事项

关于抽象类的使用，以下为语法上需要注意的细节，着重注意理解抽象的本质：

1. 抽象类**创建对象**，如果创建，编译无法通过而报错，只能创建其非抽象子类的对象。

   > 理解：假设创建了抽象类的对象，调用抽象的方法，而抽象方法没有具体的方法体，没有意义。

2. 抽象类中，可以有构造的方法，是供子类创建对象时，初始化父类成员使用的。

   > 理解：子类构造方法中，有默认的 `super()` ，需要访问父类构造方法。

3. 抽象类中，不一定包含抽象方法，但是有抽象方法的类必定是抽象类。

   > 理解：未包含抽象方法的抽象类，目的就是不想让调用者创建该类对象，通常用于某些特殊的类结构设计。

4. 抽象类的子类，必须重写抽象父类中**所有的**抽象方法，否则，编译无法通过而报错。除非该子类也是抽象类。

   > 理解：假设不重写所有抽象方法，则子类中可能包含抽象方法。那么创建对象后，调用抽象的方法，没有意义。

下面这个例子中，最高类是 Animal ，其子类 Dog 继承了该抽象类，只重写了一个抽象方法，然后再有 DogGolden 和 Dog2Ha 继承 Dog ，重写了 Dog 类里面继承自 Animal 的抽象方法：

```java
public abstract class Animal {
    public abstract void eat();
    public abstract void sleep();
}

// 子类也是一个抽象类
public abstract class Dog extends Animal {
    @Override
    public void eat() {
        System.out.println("我爱吃骨头！");
    }
}

public class DogGolden extends Dog {
    @Override
    public void sleep() {
        System.out.println("睡觉呼呼呼~~~");
    }
}

public class Dog2Ha extends Dog{
    @Override
    public void sleep() {
        System.out.println("睡觉嘿嘿嘿~~~");
    }
}

public class Demo03AnimalDog {
    public static void main(String[] args) {
        Dog2Ha ha = new Dog2Ha();
        ha.eat();	// 我爱吃骨头！
        ha.sleep();	// 睡觉嘿嘿嘿~~~

        System.out.println("==========");

        DogGolden golden = new DogGolden();
        golden.eat();	// 我爱吃骨头！
        golden.sleep();		// 睡觉呼呼呼~~~

    }
}


```



# 继承的综合案例

## 描述：

群主发普通红包。某群有多名成员，群主给成员发普通红包。普通红包的规则：

1. 群主的一笔金额，从群主余额中扣除，平均分成 n 等分，让成员领取。
2. 成员领红包后，保存到成员余额中。

## 分析：

![红包案例分析](https://i.loli.net/2021/05/19/CcIQktiaebAM8GY.png)

## 实现

```java
public class User {
    private String name;    // 姓名
    private int money;      // 余额，当前用户拥有的钱数

    public void show() {
        System.out.println("我叫" + name + "我的余额是：" + money);
    }

    public User() {
    }

    public User(String name, int money) {
        this.name = name;
        this.money = money;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getMoney() {
        return money;
    }

    public void setMoney(int money) {
        this.money = money;
    }
}

```

```java
import java.util.ArrayList;

public class Manager extends User{
    public Manager(){
        // super();
    }

    public Manager(String name, int money) {
        super(name, money);
    }

    public ArrayList<Integer> send(int totalMoney, int count){
        // 首先需要一个集合，用来存储若干金额的红包
        ArrayList redlist = new ArrayList<>();

        // 首先看一下群主有多少钱
        int leftMoney = super.getMoney();   // 群主当前余额
        if (totalMoney > leftMoney){
            System.out.println("余额不足");
            return redlist; // 返回空集合
        }

        // 扣钱，重新设置余额
        super.setMoney(leftMoney - totalMoney);

        // 发红包需要平均拆分成 count 份
        int avg = totalMoney / count;
        int left = totalMoney % count;  // 零头

        // 除不开的零头放在最后一个红包中
        // 下面把红包一个一个放在集合中
        for (int i = 0; i < count - 1; i++) {
            redlist.add(avg);
        }

        // 最后 一个红包
        left += avg;
        redlist.add(left);

        return redlist;
    }
}

```

```java
import java.util.ArrayList;
import java.util.Random;

public class Member extends User {

    public Member() {
    }

    public Member(String name, int money) {
        super(name, money);
    }

    public void receive(ArrayList<Integer> list){
        // 从众多红包中抽取一个给自己
        // 随机获取一个集合当中的索引编号
        int index = new Random().nextInt(list.size());
        // 根据索引，从集合中删除，并且得到被删除的红包给自己
        int rmoney =  list.remove(index);
        // 当前成员自己有多少钱
        int money = super.getMoney();
        // 重新设置回去
        super.setMoney(rmoney + money);
    }
}

```

```java
import java.util.ArrayList;

public class MainRedPacket {
    public static void main(String[] args) {
        Manager manager = new Manager("群主", 100);

        Member one = new Member("成员A", 0);
        Member two = new Member("成员B", 10);
        Member three = new Member("成员C", 0);

        manager.show();
        one.show();
        two.show();
        three.show();

        System.out.println("=========================");

        // 群主总共发 20 块钱，分成三个红包
        ArrayList<Integer> redList = manager.send(20, 3);

        // 三个普通成员收红包
        one.receive(redList);
        two.receive(redList);
        three.receive(redList);

        manager.show();
        one.show();
        two.show();
        three.show();

    }
}

```



# 接口

## 概述

接口，是 Java 语言中一种引用类型，是方法的集合，如果说类的内部封装了成员变量、构造方法和成员方法，那么 接口的内部主要就是**封装了方法**，包含常量和抽象方法（JDK 7及以前），默认方法和静态方法（JDK 8），私有方法 （JDK 9）。

接口的定义，它与定义类方式相似，但是使用 interface 关键字。它也会被编译成.class文件，但一定要明确它并 不是类，**而是另外一种引用数据类型**。

> 引用数据类型：数组、类、接口。

接口不能创建对象，但是可以被实现（ `implements` ，类似于被继承）。一个实现接口的类（可以看做是接口的子类），需要实现接口中所有的抽象方法，创建该类对象，就可以调用方法了，否则它必须是一个抽象类。 

## 定义格式

```java
public interface 接口名称 {
    // 抽象方法
    // 默认方法
    // 静态方法
    // 私有方法
}
```

### 含有抽象方法

抽象方法：使用 `abstract` 关键字修饰，可以省略，没有方法体。该方法供子类实现使用。

```java
public interface InterFaceName {
    public abstract void method();
}
```

### 含有默认方法和静态方法

默认方法：使用 `default` 修饰，不可省略，供子类调用或者子类重写。 

静态方法：使用 static 修饰，不可省略，供接口直接调用。

```java
public interface InterFaceName {
    public default void method() {
        // 执行语句
    }
    public static void method2() {
        // 执行语句
    }
}
```



## 实现概述

类与接口的关系为实现关系，即**类实现接口**，该类可以称为接口的实现类，也可以称为接口的子类。实现的动作类 似继承，格式相仿，只是关键字不同，实现使用 `implements` 关键字。
非抽象子类实现接口：

1. 必须重写接口中所有抽象方法。
2. 继承了接口的默认方法，即可以直接用，也可以重写。

实现格式：

```java
public class 类名 implements 接口名{
    // 重写接口中抽象方法【必须】
    // 重写接口中默认方法【可选】
}
```

### 抽象方法

定义接口：

```java
public interface LiveAble {
    // 这是一个抽象方法
    public abstract void eat();
    public abstract void sleep();
}
```

> 定义接口时，`public abstract` 可以选择性地全部或部分省略。最简化即可写成`返回值类型 方法名称();`

定义实现类：

```java
public class Animal implements LiveAble {
    @Override
    public void eat() {
        System.out.println("吃东西");
    }
    @Override
    public void sleep() {
        System.out.println("晚上睡");
    }
}
```

定义测试类：

```java
public class InterfaceDemo {
    public static void main(String[] args) {
        // 创建子类对象
        Animal a = new Animal();
        // 调用实现后的方法
        a.eat();
        a.sleep();
    }
}
输出结果：
吃东西
晚上睡
```

### 默认方法

可以继承，可以重写，二选一（实现类中没有重写则默认继承），但是只能通过实现类的对象来调用。

1. **继承默认方法**，代码：

   定义接口：

   ```java
   public interface LiveAble {
       public default void fly(){
           System.out.println("天上飞");
       }
   }
   ```

   定义实现类：

   ```java
   public class Animal implements LiveAble {
       // 没有对默认方法重写，则自动继承
   }
   ```

   定义测试类：

   ```java
   public class InterfaceDemo {
       public static void main(String[] args) {
           // 创建子类对象
           Animal a = new Animal();
           // 调用默认方法
           a.fly();
       }
   }
   输出结果：
   天上飞
   ```

2. **重写默认方法**，代码：

   定义接口：

   ```java
   public interface LiveAble {
       public default void fly(){
           System.out.println("天上飞");
       }
   }
   ```

   定义实现类：

   ```java
   public class Animal implements LiveAble {
       @Override
       public void fly() {
           System.out.println("地上跑");
       }
   }
   ```

   定义测试类：

   ```java
   public class InterfaceDemo {
       public static void main(String[] args) {
           // 创建子类对象
           Animal a = new Animal();
           // 调用重写方法
           a.fly();     }
   }
   输出结果：
   地上跑
   ```

### 静态方法

静态与 `.class` 文件相关，只能使用接口名调用，不可以通过实现类的类名或者实现类的对象调用，也就是常说的**静态与对象无关**，代码：

定义接口：

```java
public interface LiveAble {
    public static void run(){
        System.out.println("跑起来~~~");
    }
}
```

定义实现类：

```java
public class Animal implements LiveAble {
    // 无法重写静态方法
}
```

定义测试类：

```java
public class InterfaceDemo {
    public static void main(String[] args) {
        // Animal.run();	// 【错误】无法继承方法,也无法调用
        LiveAble.run(); 	// 【正确】直接通过接口名称调用静态方法
    }
}
输出结果：
跑起来~~~
```

### 私有方法

* 私有方法：只有默认方法可以调用
* 私有静态方法：默认方法和静态方法都可以调用。

如果一个接口中有多个默认方法，并且方法中有重复的内容，那么可以抽取出来，封装到私有方法中，供默认方法 去调用。从设计的角度讲，**私有的方法是对默认方法和静态方法的辅助**。代码：

定义有私有方法的接口：

```java
public interface MyInterfacePrivateA {

    public default void methodDefault1(){
        System.out.println("默认方法1");
        methodCommon();	//	抽取代码，重复利用
    }

    public default void methodDefault2(){
        System.out.println("默认方法2");
        methodCommon();	//	抽取代码，重复利用
    }

    private void methodCommon(){
        System.out.println("AAA");
        System.out.println("BBB");
        System.out.println("CCC");
    }
}
```

定义有私有静态方法的接口：

```java
public interface MyInterfacePrivateB {

    public static void methodDefault1(){
        System.out.println("静态方法1");
        methodCommon();	//	抽取代码，重复利用
    }

    public default void methodDefault2(){
        System.out.println("静态方法2");
        methodCommon();	//	抽取代码，重复利用
    }

    private static void  methodCommon(){
        System.out.println("AAA");
        System.out.println("BBB");
        System.out.println("CCC");
    }
}
```

### 常量

接口当中也可以定义“成员变量”，但是必须使用 `public static final` 三个关键字进行修饰。从效果上看，这其实就是接口的【常量】（一旦有 `final` 关键字就不可更改）。

接口当中的常量，**必须进行赋值**，接口中常量的名称使用完全的大写字母，用下划线进行分割（推荐）。

代码：

定义接口：

```java
public interface MyInterfaceConst {

    // 这其实就是一个常量，一旦赋值，就不可以修改
    public static final int NUM_OF_MY_CLASS = 10;
    // 可以省略 public static final
}
```

定义测试类：

```java
public class Demo04Interface {

    public static void main(String[] args) {
        // 访问接口中的常量
        System.out.println(MyInterfaceConst.NUM_OF_MY_CLASS);
    }
}
```

## 接口的多实现

之前学过，在继承体系中，一个类只能继承一个父类。而对于接口而言，**一个类是可以实现多个接口的**，这叫做接 口的**多实现**。并且，**一个类能继承一个父类，同时实现多个接口**。

实现格式：

```java
class 类名 [extends 父类名] implements 接口名1,接口名2,接口名3... {
    // 重写接口中抽象方法【必须】
    // 重写接口中默认方法【不重名时可选】
} 
```

> [ ]：表示可选操作。

### 抽象方法

接口中，有多个抽象方法时，实现类必须重写所有抽象方法。**如果抽象方法有重名的，只需要重写一次**。这很好理解，反正重名抽象方法在接口中都没有实现，因此在实现类中不存在冲突。代码如 下：

定义多个接口：

```java
interface A {
    public abstract void showA();
    public abstract void show();
}

interface B {
    public abstract void showB();
    public abstract void show();
}
```

定义实现类：

```java
public class C implements A,B{
	@Override
    public void showA() {
        System.out.println("showA");
    }
    @Override
    public void showB() {
        System.out.println("showB");
    }
    @Override
    public void show() {
        System.out.println("show");
    }
}
```

### 默认方法

接口中，有多个默认方法时，实现类都可继承使用。如果**默认方法有重名的，必须重写一次**，因为产生了冲突。代码如下：

定义多个接口：

```java
interface A {
    public default void methodA(){}
    public default void method(){}
}
interface B {
    public default void methodB(){}
    public default void method(){}
}
```

定义实现类：

```java
public class C implements A,B{
    @Override
    public void method() {
        System.out.println("method");
    }
}
```

### 静态方法

接口中，存在同名的静态方法并不会产生冲突，原因是只能通过各自接口名访问静态方法。

### 优先级问题

当一个类，既继承一个父类，又实现若干个接口时，父类中的成员方法与接口中的默认方法重名，子类就近选择**执 行父类的成员方法**。代码如下

定义接口：

```java
interface A {
    public default void methodA(){
        System.out.println("AAAAAAAAAAAA");
    }
}
```

定义父类：

```java
class D {
    public void methodA(){
        System.out.println("DDDDDDDDDDDD");
    }
}
```

定义子类：

```java
class C extends D implements A {
    // 未重写methodA方法
}
```

定义测试类：

```java
public class Test {
    public static void main(String[] args) {
        C c = new C();
        c.methodA();
    }
}
输出结果:
DDDDDDDDDDDD
```

## 接口的多继承

一个接口能继承另一个或者多个接口，这和类之间的继承比较相似。接口的继承使用 `extends` 关键字，子接口继 承父接口的方法。**如果父接口中的默认方法有重名的，那么子接口需要重写一次**。代码如下：

定义父接口：

```java
public interface MyInterfaceA {

    public abstract void methodA();

    public abstract void methodCommon();

    public default void methodDefault(){
        System.out.println("AAA");
    }
}

public interface MyInterfaceB {

    public abstract void methodB();

    public abstract void methodCommon();

    public default void methodDefault(){
        System.out.println("BBB");
    }
}
```

定义子接口：

```java
/*
这个子接口当中有【4】个方法。
    methodA ———> 接口A
    methodB ———> 接口B
    methodCommon ————> 同时来源于接口 A 和 B
    method ————> 来源于我自己

注意事项：
1. 多个父接口当中的抽象方法如果重复，没关系
2. 多个父接口当中的默认方法如果重复，那么子接口必须进行默认方法的覆盖重写，【而且要带着 default 关键字】
 */
public interface MyInterface extends MyInterfaceA, MyInterfaceB{

    public abstract void method();

    @Override
    public default void methodDefault() {
        System.out.println("父接口默认方法冲突，重写");
    }
}
```

> 子接口重写默认方法时，`default` 关键字可以保留
>
> 子接口重写默认方法时，`default` 关键字不保留

## 小总结及补充

在 Java 9+ 版本中，接口内容可以有：

1. 成员变量其实是常量，格式：

   ```java
   [public] [static] [final] 数据类型 常量名称 = 数据值；
   ```

   注意：

   * 常量必须进行赋值，而且一旦赋值不能改变。
   * 常量名称完全大写，用下划线分割。

2. 接口中最重要的就是抽象方法，格式：

   ```java
   [public] [abstract] 返回值类型 方法名称(参数列表);
   ```

   注意：

   * 实现类必须覆盖重写所有的抽象方法，除非实现类是抽象类。

3. 从 Java 8开始，接口里允许定义默认方法（方便方法升级），格式：

   ```java
   [public] default 返回值类型 方法名称(参数列表){
      	// 方法体
   }
   ```

   注意：

   * 默认方法也可以被覆盖重写

4. 从 Java 8开始，接口里允许定义静态方法，格式：

   ```java
   [public] static 返回值类型 方法名称(参数列表){
       // 方法体
   }
   ```

   注意：

   * 应该通过接口名称进行调用，不能通过实现类对象调用接口静态方法

5. 从 Java 9开始，接口里允许定义私有方法，格式：

   * 普通私有方法：

     ```java
     private 返回值类型 方法名称(参数列表){
         // 方法体
     }
     ```

   * 静态私有方法：

     ```java
     private static 返回值类型 方法名称(参数列表){
         // 方法体
     }
     ```

     注意：

     * `private` 的方法只有接口自己才能调用，不能被实现类或别人使用。

   6. 接口中不允许有代码块。
   7. 接口中不允许有构造方法。



# 多态

## 概述

* 引入

  多态是继封装、继承之后，面向对象的第三大特性。
  生活中，比如跑的动作，小猫、小狗和大象，跑起来是不一样的。再比如飞的动作，昆虫、鸟类和飞机，飞起来也是不一样的。可见，同一行为，通过不同的事物，可以体现出来的不同的形态。多态，描述的就是这样的状态。 

* 定义

  **多态**：是指同一行为，具有多个不同的表现形式。

## 前提

1. 继承或者实现（拥有父类或者父接口）【二选一】

2. 方法的重写【意义体现：不重写，无多态，无意义】
3. 父类引用指向子类对象

## 多态的体现

多态体现的格式：

```java
父类名称 对象名 = new 子类名称();
```

> 这里的父类名称专指子类对象继承的父类类型，或者实现类的父接口类型

示例：

```java
Fu one = new Zi();
one.method();
```

**当使用多态方式调用方法时，首先检查父类中是否有该方法，如果没有，则编译错误；如果有，执行的是子类重写后方法。**也就是说，使用多态调用方法时：编译看左，执行看右

**当使用多态方式访问成员变量时**，有两种方式：

1. 直接通过对象名称访问成员变量：**看等号左边是谁，优先用谁，没有则向上找**。
2. 间接通过成员方法访问成员变量：**看该方法属于谁优先用谁，没有则向上找**

对比：

成员变量：编译看左边，运行还看左边
成员方法：编译看左边，运行看右边

## 多态的好处

实际开发的过程中，父类类型作为方法形式参数，传递子类对象给方法，进行方法的调用，更能体现出多态的扩展性与便利。例如，我只关心一个父类下的子类运行某个方法，而不具体关心是哪个子类运行，而且父类下面的子类方法实现各不相同，这时使用多态就十分方便快捷。举例：

定义父类：

```java
public abstract class Animal {
    public abstract void eat();
} 
```

定义子类：

```java
class Cat extends Animal {
    public void eat() {
        System.out.println("吃鱼");
    }
}
class Dog extends Animal {
    public void eat() {
        System.out.println("吃骨头");
    }
}
```

定义测试类：

```java
public class Test {
    public static void main(String[] args) {
        // 多态形式，创建对象
        Cat c = new Cat();
        Dog d = new Dog();
        // 调用showCatEat
        showCatEat(c);
        // 调用showDogEat
         showDogEat(d);
        /*         
        以上两个方法, 均可以被showAnimalEat(Animal a)方法所替代
        而执行效果一致
        */
        showAnimalEat(c);
        showAnimalEat(d);
    }
    public static void showCatEat (Cat c){
        c.eat();
    }
    public static void showDogEat (Dog d){
        d.eat();
    }
    public static void showAnimalEat (Animal a){
        a.eat();
    }
}
```

由于多态特性的支持，`showAnimalEat` 方法的 `Animal` 类型，是 `Cat` 和 `Dog` 的父类类型，父类类型接收子类对象，当 然可以把 `Cat` 对象和 `Dog` 对象，传递给方法。
当 `eat` 方法执行时，多态规定，执行的是子类重写的方法，那么效果自然与 `showCatEat` 、 `showDogEat` 方法一致， 所以 `showAnimalEat` 完全可以替代以上两方法。 不仅仅是替代，在扩展性方面，无论之后再多的子类出现，我们都不需要编写 `showXxxEat` 方法了，直接使用 `showAnimalEat` 都可以完成。
所以，多态的好处，体现在，可以使程序编写的更简单，并有良好的扩展。

## 引用类型转换

多态的转型分为向上转型与向下转型两种：

### 向上转型

* **向上转型**：多态本身就是子类类型向父类类型向上转换的过程，这个过程是默认的。

  使用格式：

  ```java
  父类类型  变量名 = new 子类类型();
  如：Animal a = new Cat();
  ```

向上转型一定是安全的，没有问题的，但是也有一个弊端：**对象一旦向上转型为父类，那么就无法调用子类原本特有的内容**。当使用多态方式调用方法时，首先检查父类中是否有该方法，如果没有，则编译错误。也就是说，不能调用子类拥有，而父类没有的方法。编译都错误，更别说运行了。这也是多态给我们带来的一点"小麻烦"。所以，想要调用子 类特有的方法，必须做向下转型

解决方法：用对象的向下转型【还原】

### 向下转型

* **向下转型**：父类类型向子类类型向下转换的过程，这个过程是强制的。

  一个已经向上转型的子类对象，将父类引用转为子类引用，可以使用强制类型转换的格式，便是向下转型。

  使用格式：

  ```java
  子类类型 变量名 = (子类类型) 父类变量名;
  如:Cat c =(Cat) a; 
  ```

代码演示：

定义类：

```java
public abstract class Animal {
    abstract void eat();
}
public class Cat extends Animal {
    public void eat() {
        System.out.println("吃鱼");
    }
    public void catchMouse() {
        System.out.println("抓老鼠");
    }
}
public class Dog extends Animal {
    public void eat() {
        System.out.println("吃骨头");
    }
    public void watchHouse() {
        System.out.println("看家");
    }
}
```

定义测试类：

```java
public class Test {
    public static void main(String[] args) {
        // 向上转型
        Animal a = new Cat();
        a.eat();  // 调用的是 Cat 的 eat
        
        // 向下转型
        Cat c = (Cat)a;
        c.catchMouse();
        // 调用的是 Cat 的 catchMouse
    }  
}
```

### 转型的异常

转型的过程中，一不小心就会遇到这样的问题，请看如下代码：

```java
public class Test {
    public static void main(String[] args) {
        // 向上转型
        Animal a = new Cat();
        a.eat();
        // 调用的是 Cat 的 eat
        
        // 向下转型
        Dog d = (Dog)a;
        d.watchHouse();        // 调用的是 Dog 的 watchHouse 【运行报错】
    }
}
```

这段代码可以通过编译，但是运行时，却报出了 `ClassCastException` ，类型转换异常！这是因为，明明创建了 Cat 类型对象，运行时，当然不能转换成 Dog 对象的。这两个类型并没有任何继承关系，不符合类型转换的定义。 

![向上向下类型转换](https://i.loli.net/2021/05/19/bEfkhQo9Wzi6xRg.png)

为了避免 `ClassCastException` 的发生，Java 提供了 `instanceof` 关键字，给引用变量做类型的校验，格式如下：

```java
变量名 instanceof 数据类型
如果变量属于该数据类型，返回true。
如果变量不属于该数据类型，返回false。
```

所以，转换前，我们最好先做一个判断，代码：

```java
public class Test {
    public static void main(String[] args) {
        // 向上转型
        Animal a = new Cat();
        a.eat();	// 调用的是 Cat 的 eat
        
        // 向下转型
        if (a instanceof Cat){
            Cat c = (Cat)a;
            c.catchMouse();        // 调用的是 Cat 的 catchMouse
        } else if (a instanceof Dog){
            Dog d = (Dog)a;
            d.watchHouse();       // 调用的是 Dog 的 watchHouse
        }
    }
}
```



# 接口多态的综合案例

## 要求

笔记本电脑（laptop）通常具备使用 USB 设备的功能。在生产时，笔记本都预留了可以插入 USB 设备的 USB 接口， 但具体是什么 USB 设备，笔记本厂商并不关心，只要符合 USB 规格的设备都可以。 

定义 USB 接口，具备基本的开启功能和关闭功能。鼠标和键盘要想能在电脑上使用，那么鼠标和键盘也必须遵守 USB 规范，实现 USB 接口，否则鼠标和键盘的生产出来也无法使用。

## 分析

进行描述笔记本类，实现笔记本使用USB鼠标、USB键盘

* USB接口，包含开启功能、关闭功能
*  笔记本类，包含运行功能、关机功能、使用USB设备功能 
* 鼠标类，要实现USB接口，并具备点击的方法 
* 键盘类，要实现USB接口，具备敲击的方法

## 实现

定义接口：

```java
public interface USB {

    public abstract void open();    // 打开设备

    public abstract void close();   // 关闭设备
}
```

定义鼠标类：

```java
// 鼠标就是一个 USB 设备
public class Mouse implements USB {
    @Override
    public void open() {
        System.out.println("鼠标打开！");
    }

    @Override
    public void close() {
        System.out.println("鼠标关闭！");
    }

    public void click(){
        System.out.println("鼠标点击。。。");
    }
}
```

定义键盘类：

```java
// 键盘就是一个 USB 设备
public class Keyboard implements USB {
    @Override
    public void open() {
        System.out.println("键盘打开！");
    }

    @Override
    public void close() {
        System.out.println("键盘关闭！");
    }

    public void type(){
        System.out.println("键盘输入。。。");
    }
}
```

定义电脑类：

```java
public class Computer {
    public void powerOn() {
        System.out.println("电脑开机！欢迎使用");
    }

    public void powerOff() {
        System.out.println("电脑关机！再见");
    }

    // 使用 USB 设备的方法, 使用接口作为方法的参数
    public void useDevice(USB usb) {
        usb.open();     // 打开设备

        if (usb instanceof Mouse) {
            Mouse usbMouse = (Mouse) usb;   // 向下转型
            usbMouse.click();
        } else if (usb instanceof Keyboard) {
            Keyboard usbKeyboard = (Keyboard) usb;  // 向下转型
            usbKeyboard.type();
        }

        usb.close();    // 关闭设备
    }
}
```

定义测试类：

```java
public class DemoMain {
    public static void main(String[] args) {
        // 首先创建一个笔记本电脑
        Computer computer = new Computer();
        computer.powerOn();

        // 准备一个鼠标，供电脑使用
        Mouse mouse = new Mouse();
        // 首先进行向上转型
        USB usbMouse = mouse;   // 多态写法
        // 参数是 USB 类型，正好传递进去的就是 USB 鼠标
        computer.useDevice(usbMouse);

        // 创建一个 USB 键盘
        Keyboard USBKeyboard = new Keyboard(); // 没有使用多态写法
        // 方法参数是 USB 类型，传递进去的是实现类对象
        computer.useDevice(USBKeyboard);   // 也是正确写法！自动发生了向上转型。

        computer.powerOff();

        System.out.println("-------------------------");

        method(10.0);   // 正确写法：double --> double
        method(20); // 正确写法：int --> double
        int a = 30;
        method(a);  // 正确写法：int --> double

    }

    public static void method(double num){
        System.out.println(num);
    }

}
```



# final 关键字

## 概述

学习了继承后，我们知道，子类可以在父类的基础上改写父类内容，比如，方法重写。那么我们能不能随意的继承 API 中提供的类，改写其内容呢？显然这是不合适的。为了避免这种随意改写的情况，Java 提供了 `final` 关键字， 用于修饰不可改变内容。

* **final**：不可改变，可以用于修饰类、方法和变量
  * 类：被修饰的类，不能被继承
  * 方法：被修饰的方法，不能被重写
  * 变量：被修饰的变量，不能被重新赋值

## 使用方式

### 修饰类：

格式：

```java
public final class 类名{
    // ...
}
```

* 当 `final` 关键字修饰一个类的时候，表示这个类【不能有任何的子类】
* 一个类如果是 `final` 的，那么其中所有的成员方法都无法进行覆盖重写

### 修饰方法：

格式：

```java
修饰符 final 返回值类型 方法名(参数列表){
    // 方法体
}
```

* 当 `final` 关键字用来修饰一个方法的时候，这个方法就是最终方法，也就是不能被覆盖重写
* 正因为方法不能被重写，所以对于类、方法来说，`abstract` 和 `final` 不能连用

### 修饰局部变量

基本类型的局部变量，被ﬁnal修饰后，只能赋值一次，不能再更改

```java
public class FinalDemo1 {
    public static void main(String[] args) {
        // 声明变量，使用final修饰
        final int a;
        // 第一次赋值
        a = 10;
        // 第二次赋值
        a = 20; // 报错,不可重新赋值
        
        // 声明变量，直接赋值，使用final修饰
        final int b = 10;
        // 第二次赋值
        b = 20; // 报错,不可重新赋值
    }
}
```

引用类型的局部变量，被 `ﬁnal` 修饰后，只能指向一个对象，地址不能再更改。但是不影响对象内部的成员变量值的 修改，代码如下：

```java
public class FinalDemo2 {
    public static void main(String[] args) {
        // 创建 User 对象
        final   User u = new User();
        // 创建 另一个 User对象
        u = new User();
        // 报错，指向了新的对象，地址值改变。
        
        // 调用setName方法
        u.setName("张三"); // 可以修改
    }
} 
```

### 修饰成员变量

成员变量涉及到初始化的问题，初始化方式有两种，只能二选一：

* 显示初始化：

  ```java
  public class User {
      final String USERNAME = "张三";
      private int age;
  }
  ```

* 构造方法初始化：

  ```java
  public class User {
      final String USERNAME ;
      private int age;
      public User(String username, int age) {
          this.USERNAME = username;
          this.age = age;
      }
  }
  ```

  > 被ﬁnal修饰的常量名称，一般都有书写规范，所有字母都**大写**。



# 权限修饰符

## 概述

在 Java 中提供了四种访问权限，使用不同的访问权限修饰符修饰时，被修饰的内容会有不同的访问权限

* public：公共的。
*  protected：受保护的
*  default：默认的
*  private：私有的

## 不同权限的访问能力

|          情形          | public | protected | default | private |
| :--------------------: | :----: | :-------: | :-----: | :-----: |
|        同一类中        |   √    |     √     |    √    |    √    |
| 同一包中(子类与无关类) |   √    |     √     |    √    |         |
|      不同包的子类      |   √    |     √     |         |         |
|    不同包中的无关类    |   √    |           |         |         |

可见，`public` 具有最大权限。`private` 则是最小权限。
编写代码时，如果没有特殊的考虑，建议这样使用权限：

* 成员变量使用 `private` ，隐藏细节。

*  构造方法使用 `public` ，方便创建对象。

*  成员方法使用 `public` ，方便调用方法。

  >  不加权限修饰符，其访问能力与default修饰符相同 
