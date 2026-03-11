java

## java入门

### Java是什么

#### 人机交互

打开CMD

1. WIN+R
2. CMD
3. 按下回车键

##### 常见CMD命令

1. 盘符名称+冒号：
    说明：E:回车，表示切换到E盘
2. dir
    说明：查看当前路径下的内容
3. cd 目录
    说明：进入单词目录
    举例：cd home
4. cd ..
    说明：回到上一级目录
5. cd 目录1\目录2\
    说明：进入多级目录
6. cd \
    说明：回退到盘符目录
7. cls
    说明：清屏
8. exit
    说明：退出命令提示符窗口

##### 例：用cmd打开QQ

添加环境变量

系统变量的路径增加QQ路径

配置系统环境变量的页面

### java程序初体验

#### JDK的下载和安装

https://wwwOrcale.com

bin:该路径下存放了各种工具命令

conf:该路径下存放了相应的配置文件

include：该路径下存放了一些平台特定的头文件

jmods：该路径下存放了各种模块

legal：该路径下存放了个模块的授权文档

lib：该路径下存放了工具的一些补充JAR包

#### HelloWorld案例

1. 用记事本编写程序

    ```java
    public class HelloWorld{
        public static void main(String[],args){
            System.out.println("HelloWorld");
        }
    }
    ```

2. 编译文件

    javac是JDK提供的编译工具，把当前路径下的HelloWorld.java文件编译成class文件

3. 运行程序

    java也是JDK提供的一个工具，作用是用来用来运行代码的，运行当前后缀下的helloWorld.class这个文件。在运行的时候不加后缀名

#### 常见问题

中英文符号问题

- 英文状态下的分号

单词拼写问题

- System——system

#### 环境变量

配置环境变量可以任意的目录下都可以打开指定文件

将软件的路径配置到环境变量中

配置Path环境变量

步骤

1. 先配置JAVA_HOME(路径不带bin)
2. 在配Path(%JAVA_HOME%\bin)

#### Notepad++

高级记事本，而且Java中的一些特殊单词会高亮显示

##### 配置

修改默认语言和编码

### java语言的发展

![image-20250521214315477](images/image-20250521214315477.png)


#### java能做什么

##### java SE

java语言的标准版，用于桌面应用的开发，是其他两个版本的基础

###### 桌面应用

用户只要打开程序，程序的界面会让用户在最短事件内找到他们所需的功能，同时主动带领用户完成他们的工作斌不过得到最好的体验

为将来java EE开发打基础

##### java ME

java语言的小型版，用于嵌入式电子设备，用于嵌入式或者小型移动设备

##### java EE

java语言的企业版，用于web方向的网站开发。在这个领域的第一

###### 开发

桌面应用开发

税务管理软件，IDEA，Clion，Pycharm

企业级应用开发

微服务，springcloud

移动应用开发

鸿蒙，Android，医疗设备

科学计算

matlab

大数据开发

hadoop

游戏开发

我的世界 Minecraft

网站开发

浏览器+服务器

### java为什么这么火

用户量

适用面

与时俱进

自身特点

1. 面向对象

2. 安全性

3. 多线程

    同时做多项事情

4. 简单易用

5. 开源

6. 跨平台

    java程序可以在任意操作系统上运行

#### 高级语言运行方式

编程：java程序员写.java代码，c程序员写.c代码，python程序员写.py代码

编译：机器只认识0011的机器语言，把.java,.c.py的代码转化成机器仍是的过程

运行：让机器执行编译后的指令

#### 高级语言的编译运行方式

编译型

​		![image-20250521221225837](images/image-20250521221225837.png)	

解释型

![image-20250521221322658](images/image-20250521221322658.png)

混合型，半编译，半解释

![image-20250521221444950](images/image-20250521221444950.png)

不是直接运行在系统中的，而是直接运行在虚拟机中的

#### 跨平台原理

![image-20250521221820139](images/image-20250521221820139-17478371019101.png)


- java语言的跨平台通过虚拟机实现的
- java语言不是直接运行在操作系统里面的，而是运行虚拟机中的
- 针对于不同的系统，安装不同的虚拟机

### JRE和JDK

JDK是java的开服工具包

JVM(kava Virtual Machine):java虚拟机，真正运行java程序的地方

核心类库：Java已经写好的东西，我们可以直接用

开发工具：

1. javac编译工具
2. java运行工具
3. jdb调试工具
4. jhat内存分析工具

![image-20250521222327325](images/image-20250521222327325.png)


JDK(java Development kit):java开发工具包

![image-20250521222612073](images/image-20250521222612073.png)


JRE(java Runtime Enviorment):java的运行环境

JDK>JRE>JVM

## java基础概念

### 注释

- 注释是在程序指定位置添加的说明性信息
- 简单理解，就是对代码的一种解释

#### 注释种类

1. 单行注释

    ```java
    //注释信息
    ```

2. 多行注释

    ```java
    /*注释信息*/
    ```

3. 文档注释

    ```Java
    /**注释信息*/
    ```

    文档注释暂时用不到

#### 注释的使用细节

注释内容不会参与编译和运行，仅仅是对代码的解释说明

不管是单行注释还是多行注释，在书写的时候不要嵌套

### 关键字

关键字：被Java赋予了特定涵义的英文单词

#### 	关键字的特点

关键字的字母全部小写

常用的代码编辑器，针对关键词有特殊颜色标记，非常直观

#### class

class:用于（创建/定义）一个类，后面跟随类名

类是Java最基本的组成单元

### 字面量

告诉程序在程序的书写格式

#### 字面量的分类

| 字面量类型 | 说明                             | 举例                      |
| ---------- | -------------------------------- | ------------------------- |
| 整数类型   | 不带小数点的数字                 | 666，-88                  |
| 小数类型   | 带小数点的数字                   | 13.14，-5.21              |
| 字符串类型 | 用双括号括起来的内容             | "helloworld","黑马程序员" |
| 字符类型   | 用单引号括起来的，内容只能有一个 | 'A','0','我'              |
| 布尔类型   | 布尔值，表示真假                 | 只要两个值：true，false   |
| 空类型     | 一个特殊的只，空值               | 值是：null                |

#### 特殊字符

- \t 制表符

    在打印的时候，把前面的字符串的长度补齐到8，或者8的整数倍。最少补一个空格，最多不8个空格

### 变量

在程序执行的过程中部，其值可能发生改变的量（数据）

#### 变量定义的格式

数据类型 变量名 = 数据值;

数据值：存在空间里面的数值

变量名：为空间（小箱子）起的名字

数据类型：为空间中存储的数据，加入类型（限制）

#### 变量的使用方式

1. 输出打印
2. 参与计算
3. 修改记录的值

#### 变量的注意事项

1. 只能存在一个值
2. 变量名不允许重复定义
3. 一条语句可以定义多个变量
4. 变量在使用之前一定要进行赋值

#### 使用场景

1. 重复使用某个值
2. 某个数据经常改变

### 计算机存储规则

文本，图片，声音

在计算机，任意的数据都是以二进制的形式来存储的

#### 文本

##### 常见进制在代码中的表现形式

二进制：由0和1组成，代码中以0b开头

十进制：由0~9组成，前面不加任何前缀

八进制：由0~7组成，代码中以0开头

十六进制：由0~9还要a~f组成，代码中以0x开头

| 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   | 13   | 14   | 15   |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | a    | b    | c    | d    | e    | f    |

JDK7的特性

##### 任意进制转十进制

公式：系数*基数的权次幂相加

系数：就是每一位上的数

基数：当前进制数

权：从右往左，依次为0 1 2 3 4 5 ...

###### 二进制转十进制

8421快速转换法

![image-20250523215340875](images/image-20250523215340875.png)

##### 十进制转其他进制

除基取余法

不断的除以基数（几进制，基数就是几）得到余数，直到商为0，再将余数倒着拼起来即可

![image-20250523215709226](images/image-20250523215709226.png)

##### 编码

ASCII码表

![image-20250523220158638](images/image-20250523220158638.png)

汉语

1. GB2312编码：1981年5月1日发布的简体中文汉字编码国家标准。收录7445个图形字符，其中包括6763个汉字
2. BIG5编码：台湾地区繁体中文标准字符集，共收录13053个中文字，1984年逝世
3. GBK编码：2000年3月17日发布，共收录21003个汉字，包含国家标准GB13000-1中的全部中日韩字，和BIG5编码中的所有汉字
4. Unicode编码：国际标准字符集，它将世界各种语言的每个字符定义为唯一的编码，以满足跨语言、跨平台的文本信息转换

#### 图片

黑白图，灰度图，彩色图

黑白图：用0-1表示图片

灰白图：用0~255表示灰度数据

三原色 计算机颜色采用光学三原色，分别为红，绿，蓝，也称为RGB取值范围0~255或0~FF

#### 声音

对声音的波形图进行采样再存储

## java基础语法

### 数据类型

基本数据类型

| 数据类型 | 关键字         | 取值范围                                 | 内存占用 |
| -------- | -------------- | ---------------------------------------- | -------- |
| 整数     | byte           | (-128,127)                               | 1        |
| 整数     | short          | (-32768,32767)                           | 2        |
| 整数     | int（默认）    | (-8388608,8388607)                       | 4        |
| 整数     | long           | (-2147483648,21747483647)                | 8        |
| 浮点数   | float          | (-3.402823466 E-38,-3.402823466351 E+38) | 4        |
| 浮点数   | double（默认） | (-1.797E-308，1.797E308)                 | 8        |
| 字符     | char           | 0-65535                                  | 2        |
| 布尔     | boolean        | true，false                              | 1        |

整数和小数取值范围大小关系：

double>float>long>int>short>byte

定义long类型的变量

再数据值的后面加一个L作为后缀

L可以大写可以小写

定义float类型的变量

再数据值的后面加一个F作为后缀

F可以大写可以小写

引用数据类型



### 标识符

标识符：就是给类，方法，变量起的名字

#### 标识符命名规则

##### 硬性要求

- 由数字、字母、下划线（_）和美元符（$）组成
- 不能以数字开头
- 不能是关键字
- 区分大小写

##### 软性建议

###### 小驼峰命名法：方法、变量

规范1：标识符是由一个单词组成的时候，全部小写

规范2：标识符是由多个单词组成的时候，第一个单词首字母小写，其他单词首字母大写

###### 大驼峰命名法：类名

规范1：标识符是一个单词的时候，首字母大写

规范2：标识符由多个单词组成的时候，每个单词的首字母大写

### 键盘录入

Java帮我们写好一个类叫Scanner，这个类可以接收键盘输入的数字

1. 导包——Scanner这个类在哪

    ```java
    import java.util.Scanner;
    ```

2. 创建对象——表示我要开始用Scanner这个类了

    ```java
    Scanner sc = new Scanner(System.in)
    ```

    上面这个格式里面，只有sc是变量名，可以变，其他的都不允许变

3. 接收数据

    ```java
    int i = sc.nextInt();
    ```

    上面这个格式里面，只有变量名，可以变，其他的都不允许变

## IDEA

### IDEA概述

IDEA全程Intellij IDEA，是用于Java语言开发的集成环境

集成环境

将代码编写、编译、执行、调试等多种功能综合到一起的开发工具

### IDEA下载和安装

[IDEA网址][https://www.jetbrains.com/idea/]

### IDEA中的第一个代码

IDEA项目结构介绍

![image-20250524180445805](images/image-20250524180445805.png)

psvm快速生成主入口

### IDEA的项目和模块操作

#### 类的操作

新建类，修改类删除类

#### 模块的操作 

新建模块，修改模块，删除模块，删除模块

#### 项目的操作

关闭项目、新建项目、打开项目、修改项目

## 运算符

运算符

对字面量或者变量进行操作的符号

表达式

用运算符把字面量或者变量连接起来，符号java语法的式子就可以称为表达式

不同运算符连接的表达是体现的是不同类型的表达式

### 算数运算符

| 符号 | 作用       |
| ---- | ---------- |
| +    | 加         |
| -    | 减         |
| *    | 乘         |
| /    | 除         |
| %    | 取余、取模 |

整数操作只能得到整数，要想得到小数，必须有浮点数参与运算

"+"操作的三种情况

数字相加

- 数字进行运算时，数据类型不一样是不能运算的，需要转成一样的，才能运算

- 类型转化分类

    - 隐式转化（自动类型提升）

        把一个取值范围小的数值，转成取值范围大的数据

        double<-float<-long<-int<-short<-byte

        提升规则

        - 取值范围小的，和取值范围大的进行计算，小的会先提升为大的，再进行计算
        - byte short char 三种类型的数据在运算的时候，都会先提升为int，然后再进行计算
        
    - 强制转化
	  
        - 如果把一个取值范围大的数值，赋值给一个取值范围小的变量，是不允许直接赋值的。如果一定要这么做就要加入强制类型转挂
        - 格式：目标数据类型 变量名 = （目标数据类型）被强转的数据

字符串相加

- 当"+"操作出现字符串时，这个"+"是字符串连接符，而不是算数运算符了。会将前后的数据进行拼接，并产生一个新的字符串
- 连续"+"的操作，从左到右逐个执行

字符相加

byte short char 三种数据类型在运算的时候，都会优先提升为int，然后再进行计算

当字符+字符或字符+数字时，会把字符通过ASCII码表查询到对应的数字进行计算

"A"=65,"a"=97

### 自增自减运算符

| 符号 | 作用 | 说明         |
| ---- | ---- | ------------ |
| ++   | 加   | 变量的值加一 |
| --   | 建   | 变量的值减一 |

注意实现：

++和--即可以放在变量的前面，也可以放在变量的后面

两种用法

- 单独使用 ++和--无论是放在变量的前边还是后边，单独写一行结果时一样的
- 参与计算
    - ++在后 先用后加
    - ++在前 先加后用

### 赋值运算符

| 符号 | 作用       | 说明                        |
| ---- | ---------- | --------------------------- |
| =    | 赋值       | int a=10，将10赋值给变量a   |
| +=   | 加后赋值   | a+=b，将a+b的值给a          |
| -=   | 减后赋值   | a-=b，将a-b的值给a          |
| *=   | 乘后赋值   | a*=b，将a$\times$b的值赋给a |
| /=   | 除后赋值   | a/=b，将a$\div$b的值赋给a   |
| %=   | 取余后赋值 | a%=b，将a$\div$b的余数给a   |

### 关系运算符

| 符号 | 说明                                                    |
| ---- | ------------------------------------------------------- |
| ==   | a==b，判断a和b的值是否相等，成立为true，不成立为false   |
| !=   | a!=b，判断a和b的值是否不相等，成立为true，不成立为false |
| >    | a>b，判断a是否大于b，成立为true，不成立为false          |
| >=   | a>=b，判断a是否大于等于b，成立为true，不成立为false     |
| <    | a<b，判断a是否小于b，成立为true，不成立为false          |
| <=   | a<=b，判断a是否小于等于b，成立为true，不成立为false     |

注意事项：关系运算符的结果都是boolean类型，要么是true，要么是false。千万不要把"=="误写成"="。

### 逻辑运算符

| 符号 | 作用         | 说明                         |              |
| ---- | ------------ | ---------------------------- | ------------ |
| &    | 逻辑与（且） | 并且，两边都为真，结果才是真 | 两边都要满足 |
| \|   | 逻辑或       | 或者，两边都为假，结果才是假 | 两边满足一个 |
| ^    | 逻辑异或     | 相同为false，不同为true      |              |
| !    | 逻辑非       | 取反                         |              |

短路逻辑运算符

| 符号 | 作用   | 说明                         |
| ---- | ------ | ---------------------------- |
| &&   | 短路与 | 结果和&相同，但是有短路效果  |
| \|\| | 短路或 | 结果和\|相同，但是有短路效果 |

注意事项

&，|，无论左边 true false，右边都要执行

&&，||，如果左边能确定整个表达式的结果，右边不执行

&&：左边为false，右边不管是真是假，整个表达式的结果一定是false

||：左边为true，右边不管是真是假，整个表达式的结果一定是true

这两种情况下，右边不执行，提高了效率

最常用的逻辑运算符：&&，||，!

### 三元运算符

可以进行判断，根据判断的结果得到不同的内容

（三元运算符/三元表达式）格式

格式：关系表达式?表达式1:表达式2;

把三元运算符的结果赋值为一个变量

把三元运算符的结果直接打印

### 运算符优先级

| 优先级 | 运算符                      |
| ------ | --------------------------- |
| 1      | .、()、{}                   |
| 2      | !、~、++、--                |
| 3      | *、/、%                     |
| 4      | +、-                        |
| 5      | <<、>>、>>>                 |
| 6      | <<、=>、>=、instance of     |
| 7      | ==、!=                      |
| 8      | &                           |
| 9      | ^                           |
| 10     | \|                          |
| 11     | &&                          |
| 12     | \|\|                        |
| 13     | ?:                          |
| 14     | =、+=、-=、*=、/=、%=、&=、 |



### 原码反码补码

原码：十进制数据的二进制表现形式，最左边是符号位，0为正，1为负

- 利用源码对正数计算是不会有问题的
- 必读：但如果是负数计算，结果就会出错，实际运算的结果，跟我们的预期的结果是相反的

反码：正数的补码反码是其本身，负数的反码是符号位保存不变，其余位取反

- 目的：是为了解决原码不能计算负数的问题而出现的
- 计算规则：正数的反码不变，负数的反码在原码符号位不变，数值取反，0变1，1变0。
-  弊端：负数运算的时候，如果结果不跨0，是没有任何问题的，但是如果结果跨0，跟实际结果会有1的偏差

补码：正数的补码是其本身，负数的补码在其反码的基础上加1

- 目的：解决负数计算跨0的问题而出现的
- 计算规则：正数的反码不变，负数的补码在反码的基础上+1.另外补码还能多记录一个特殊值-128，该数据在1个字节下，没有原码和反码
- 注意点:计算机中的存储和计算都是以补码的形式进行的

| 运算符 | 含义       | 运算规则             |
| ------ | ---------- | -------------------- |
| &      | 逻辑与     | 0为false1为true      |
| \|     | 逻辑或     | 0为false1为true      |
| <<     | 左移       | 向左移动，低位补0    |
| >>     | 右移       | 向右移动，高位补0或1 |
| >>>    | 无符号右移 | 向右移动，高位补0    |

## 流程控制语句

通过一些语句，控制程序的执行进程

### 顺序

顺序结构语句是Java程序默认的执行流程，按照代码的先后顺序，从上到下依次执行

### 分支

#### if语句

if语句在程序中用于执行判断

##### 第一种格式：单条件判断

```java
if(关系表达式){
    语句体;
}
```

执行流程：

1. 首先计算关系表达式的值
2. 如果关系表达式的值为true就执行语句体
3. 如果关系表达式的值为false就不执行语句体
4. 继续执行后面的其他语句

注意点：

1. 大括号的开头可以另起以行书写，但是建议写在第一行末尾
2. 在语句体中，如果只有一行代码，大括号可以省略不写
3. 如果对一个布尔类型的变量进行判断，不要使用==号

##### 第二种格式：二条件判断

```java
if(关系表达式){
    语句体1;
}else{
    语句体2;
}
```

执行流程：

1. 首先计算关系表达式的值
2. 如果关系表达式的值为true就执行语句体1
3. 如果关系表达式的值为false就执行语句体2
4. 继续执行后面的其他语句

![image-20250526165559369](images/image-20250526165559369.png)

##### 第三种格式：多条件判断

```java
if(关系表达式1){
    语句体1;
}else if(关系表达式2){
    语句体2;
}
	...
 else {
     语句体 n+1;
 }        
```

执行流程：

1. 首先计算关系表达式1的值
2. 如果为true就执行语句体1；如果为false就计算关系表达式2的值
3. 如果为true就执行语句体2；如果为false就计算关系表达式3的值
4. ...
5. 如果所有关系表达式结果都为false，就执行语句体n+1。

从上往下依次进行判断

只要要有一个判断为真，就执行对应的语句体

如果所有的判断都为假，就执行else的语句体

#### switch语句

##### switch格式

```java
switch(表达式){
    case 值1:
        语句体1;
        break;
    case 值2:
        语句体2;
        break;
    ...
    default:
        语句体n+1;
        break;       
}
```

执行流程：

1. 首先计算表达式的值
2. 依次和case后面的值进行比较，如果有对应的值，就会执行相应的语句，在执行的过程中，遇到break就会结束。
3. 如果所有case后面的值和表达式的值不匹配，就会执行default里面的语句体，然后结束整个switch语句。

##### 其他知识点

###### default的位置和省略

1. 位置：default不一定是写最下面的，我们可以写在任意位置，只不过习惯写在最下面
2. 省略：default可以省略，语法不会有问题，但是不建议省略

###### case穿透

就是语句体中没有break导致的
执行流程：

首先还是会拿着小括号中表达式的值跟下面每一个case进行匹配

如果匹配上了，就会执行对应的语句体，如果发现了break，那么结束整个switch语句

如果没有发现break，那么程序会继续执行下一个case的语句体，已知遇到break或者有大括号为止
使用场景：

如果多个case语句重复了，那么我们考虑利用case穿透去简化代码

###### switch新特性

JDK12

将冒号`:`改为箭头`->`省略break

```java
case 数值 ->{
    语句体;
}
```

```java
case 数值 -> 单行语句;
```

###### switch与if第三种格式各自的使用场景

if 第三种格式：一般用于对范围的判断

switch：把有限个数据一一列举处理，让我们任选其一

### 循环

#### for循环

```java
for(初始化语句;条件判断语句;条件控制语句){
    循环体语句;
}
```

执行流程：

1. 执行初始化语句

2. 执行条件判断语句，看起结果是true还是false

    ​		如果是false，循环结束

    ​		如果是true，执行循环体语句

3. 执行条件控制语句

4. 回到2继续执行条件判断语句

![image-20250526195517118](images/image-20250526195517118.png)

#### while循环

```java
初始化语句;
while(条件判断语句){
    循环体语句;
    条件控制语句;
}
循环下面的其他语句
```

初始化语句只执行一次

判断语句为true，循环继续

判断语句为false，循环结束

![image-20250526204515417](images/image-20250526204515417.png)

#### for和while的对比

相同点：运行规则都是一样的

for和while的区别：

- for循环中：知道循环次数或者循环的范围
- while循环：不知道循环的次数和范围，只知道循环结束的条件 

#### do-while循环

```java
初始化语句;
do{
    循环体语句;
    条件控制语句;
}while(条件控制语句);
```

先执行后判断

![image-20250526215645268](images/image-20250526215645268.png)

## 循环高级

### 无限循环

循环一直停不下

```java
for(;;){
    语句体;
}
```

```java
while(true){
    语句体;
}
```

```java
do{
    语句体;
}while(true);
```

### 跳转控制语句

再循环的过程中，跳到其他语句执行

`continue`结束本次循环，继续下次循环

`break`结束整个循环

### 练习

#### 逢七过

```java
public class test1 {
    static public void main(String[] args){
        for(int i=1;i<=100;i++){
            if(i%7==0||i%10==7){
                System.out.println(i);
            }
        }
    }
}
```

#### 求平方根

```java
import java.util.Scanner;
public class test2 {
    static public void main(String [] args){
        Scanner sc=new Scanner(System.in);
        int i = sc.nextInt();
        for(int j=0;j<i;j++)
        {
            if(Math.pow(j,2)>i){
                System.out.println(i+"平方根是"+(j-1));
                break;
            }
        }
    }
}
```

#### 是否是质数

定义一个变量，表示标记

标记着number是否是一个质数

true：是一个质数

false：不是一个质数

```java
package com.yuanshenligong;
import java.util.Scanner;
public class test3 {
    static public void main(String[] args){
        Scanner sc =new Scanner(System.in);
        int i = sc.nextInt();
        boolean flag = true;
        for(int j=2;j<Math.sqrt(i);j++){
            if(i%j==0) {
                flag = false;
                break;
            }
        }
        if(flag){
            System.out.println(i+"是质数");
        }
        else{
            System.out.println(i+"不是质数");
        }

    }
}
```

#### 猜数

获取随机数

java帮我们写好一个类Random，这个类就可以生成一个随机数

使用步骤：

1. 导包——Random这个类在哪

    ```java
    import java.util.Random;
    ```

    导包的动作必须出现在类的定义的上边

2. 创建对象——表示我要开始用Random这个类了

    ```java
     Random r = new Random();
    ```

    上面这个格式里面，只要r是变量名，可以变，其他的都不允许变

3. 生成随机数——真正开始干活了

    ```java
    int number = r.nextInt(随机数的范围);
    ```

    在上面这个格式里面，只要number是变量名，可以变，其他的都不允许变

秘诀：

1. 让这个范围头尾都减去一个只，让这个范围从0开始
2. 尾巴加1
3. 最中结果，再加上第一步减去的值

注意点：

1. 不能写在循环里面，否则每一次都会生成一个新随机数
2. 添加计数器，作为保底机制

## 数组

### 数组介绍

数组指的是一种容器，可以用来存储同种数据类型的多个值

数组容器在存储数据的时候，需要结合隐式转换考虑

容器的类型，和存储的数据类型保持一致

### 数组的定义与静态初始化

#### 数组的定义

1. ```java
    数据类型 [] 数组名
    ```

2. ```java
    数据类型 数组名[]
    ```

#### 数组的静态初始化

初始化：就是在内存中，为数组容器开辟空间，并将数据存入容器的过程

完整格式：[] 数组名 = new 数据类型[]{元素1,元素2,元素3...};

简化格式：数据类型[] 数组名 = {元素1,元素2,元素3...};

### 数组元素的访问

#### 地址值

![image-20250527201336535](images/image-20250527201336535.png)

地址值的含义

- [，表示当前是一个数组
- D，表示当前数组里面的元素是double类型的
- @，表示一个间隔符号（固定格式）
- 十六进制字串：才是数组真正的地址值

#### 数组元素访问

格式：数组名[索引];

##### 索引

也叫下标，角标

索引的特点：从0开始，逐个+1增长，连续不间断

##### 数组元素访问

1. 获取数组中的元素

    格式：数组名[索引]

2. 把数据存储到数组中

    格式：数组名[索引] = 具体数据/变量

    细节：一旦覆盖之后，原来的数据就不存在了

### 数组遍历

数组变量：将数组中所有内容取出来

- 注意：遍历值得是取出数据的过程，不要局限的理解为，遍历就是打印

- 利用循环改进代码

    开始条件：0

    结束条件：数组的长度-1（最大索引）

- 在Java当中，关于数组的一个长度属性：length

    调用方式：数组名.length

- 拓展：

    快速自动生成数组的遍历方式

    idea提供的

    数组名.for+变量名

### 数组动态初始化

动态初始化：初始化时只指指定数组长度，由系统为数组分配初始值

格式：数值类型[] 数组名 = new 数据类型[数组长度];

在创建的时候，由我们指定数组的长度，由虚拟机给出默认初始化值

数组默认初始化规律:

- 整数类型：默认初始值0
- 小数类型：默认初始值0.0
- 字符类型：默认初始化值'/u0000' 空格
- 布尔类型：默认初始化值 false
- 引用数据类型：默认初始化值 null

#### 动态初始化和静态初始化的区别

动态初始化：收费指定数组长度，由系统给出默认值

只明确元素个数，不明确具体数值，推荐使用动态初始化

静态初始化：手动指定数组元素，系统会根据元素个数，计算除数组的长度

需求中已经明确了要操作的具体数据，直接静态初始化即可

### 数组内存图

#### java内存分配

栈、堆、方法区、本地方法栈、寄存器

JDK7之前

![image-20250527215758113](images/image-20250527215758113.png)

注意从JDK8器，取消方法区，心中原空间。把原来方法区的多种功能进行了拆分，有的功能放到了堆中，有的功能放到了元空间中。

![image-20250527220205783](images/image-20250527220205783.png)

- 栈
    方法运行时使用的内存
- 堆
    存储对象或者数组，new来创建的，都存储在堆内存
- 方法区
    存储可运行的class文件
- 本地方法栈
    JVM在使用操作系统功能时使用
- 寄存器
    给CPU用

![image-20250527221356452](images/image-20250527221356452.png)

1. 只要是new出来的一定是堆里面开辟了一个小空间
2. 如果new了多次，那么堆里面有多个小空间，每个小空间都有各自的数据
3. 当两个数组指向同一个小空间时，其中一个数组堆小空间中的值发生了改变，那么其他数组再次访问的时候都是修改之后的结果了

### 数组常见问题

当访问了数组不存在的索引，就会引发索引越界异常

避免：索引的范围

### 数组常见操作

#### 求最值

1. 求最值是初始化值在数组内部
2. 当开始条件为0时，相当于自己和自己比较，没有任何影响，但影响效率
    为了提高效率，减少一次循环的次数，循环条件可以写1

```java
public class tset5 {
    public static void main(String[] args) {
        int[] array={1,2,3,4,5};
        int max=array[0];
        for (int i = 1; i <5 ; i++) {
            max=max>array[i]?max:array[i];
        }
        System.out.println(max);
    }
}
```

#### 求和

```java
public class test6 {
    public static void main(String[] args) {
        Random r =new Random();
        int[] array=new int [10];
        for (int i = 0; i < 10; i++) {
            array[i]=r.nextInt(1,101);
        }
        int sum=0;
        for (int i = 0; i < 10; i++) {
            sum+=array[i];
        }
        int average=sum/10;

        int count=0;
        for (int i = 0; i < 10; i++) {
            if(array[i]<average)
            {
                count++;
            }
        }
        System.out.println(sum);
        System.out.println(average);
        System.out.println(count);
    }
}
```

#### 交换数据

```java
public class test7 {
    public static void main(String[] args) {
        int [] array={1,2,3,4,5};
        for (int i = 0,j=array.length-1; i < j; i++,j--) {
            int tmp=array[i];
            array[i]=array[j];
            array[j]=tmp;
        }
        for (int i = 0; i < array.length; i++) {
            System.out.print(array[i]);
        }
    }
}
```

#### 打乱数据

```java
import java.util.Random;
public class test8 {
    public static void main(String[] args) {
        int[] array={1,2,3,4,5};
        Random r= new Random();
        for (int i = 0; i < 5; i++) {
            int j = r.nextInt(5);
            int tmp=array[i];
            array[i]=array[j];
            array[j]=tmp;
        }
        for (int i = 0; i < 5; i++) {
            System.out.print(array[i]);
        }
    }
}
```

## 方法

### 什么是方法

方法是程序中的最小执行单元

重复的代码、具有独立功能的代码可以抽取到方法中

- 可以提高代码的复用性
- 可以提高代码的可维护性

### 方法的格式

把一些代码打包在一起，用到的时候就调用

方法定义

把一些代码打包在一起，该过程称为方法定义

方法调用

方法定义后并不是直接运行的，需要手动调用才能执行，该过程称为方法调用

#### 简单方法定义和调用

定义

```java
public static void 方法名(){
    方法体(就是打包起来的代码);
}
```

调用

```java
方法名();
```

注意：方法必须先定义后调用，否则程序将报错

#### 带参数的方法定义

定义

单个参数

```java
public static void 方法名(参数){
    方法体;
}
```

多个参数

```java
public static void 方法名(参数1,参数2,...){
    方法体;
}
```

调用

单个参数

```java
方法名(参数);
```

多个参数

```java
方法名(参数1,参数2,...);
```

注意：方法调用时，参数的数量与类型必须与方法定义中小括号里面的变量一一对应，否则程序将报错

形参与实参

形参：全程形式参数，是指方法定义中的参数

实参：全称实际参数，方法调用中的参数

注意方法调用时，形参和实参必须一一对应，否则程序将报错。

我要干嘛？方法体

我干这件事情需要什么？ 形参

方法调用除是否需要使用方法的结果

如果要用方法必须要有返回值

如果不要用，方法可以写返回值，也可以不写返回值

#### 带返回值的方法定义

![image-20250528200953187](images/image-20250528200953187.png)

调用处拿到结果之后，才能根据结果进行下一步操作

方法的返回值起始就是方法运行的最终结果

- 如果在调用处要根据方法的结果，去编写另外一段代码逻辑
- 为了在调用处拿到方法产生的结果，就需要定义待遇返回值的方法

定义

```java
public static 返回值的类型 方法名(参数){
    方法体;
    return 返回值;
}
```

1. 直接调用

    ```java
    方法名(实参);
    ```

2. 赋值调用

    ```java
    整数类型 变量名 = 方法名 (实参);
    ```

3. 输出调用

    ```java
    System.out.println(方法名(实参));
    ```

方法的完整定义

```java
public static 返回值类型 方法名 (参数){
    方法名;
    return 返回值;
}
```

注意事项

- 方法不调用就不执行
- 方法与方法之间时评级关系，不能互相嵌套定义
- 方法的编写顺序和执行顺序无关
- 方法返回值类型为void，表示该方法没有返回值
    没有返回值的方法可以省略return语句不写
    如果要编写return，后面不能跟具体数据
- return语句下面，不能编写代码，因为永远执行不到，属于无效的代码

##### return关键字

方法没有返回值：可以省略不写。如果要书写，表示结束方法

方法有返回值：必须要写，表示结束方法和返回结果

### 方法的重载

在同一个类中，定义多个同名的方法，这些同名的方法具有同种功能。

每个方法具有不同的参数类型或参数个数，这写同名的方法，就构成了重载关系

简单记：同一个类中，方法名相同，参数不同的方法。与返回值无关/

参数不同：个数不同、类型不同、顺序不同

Java虚拟机会通过参数的不同来区分同名的方法

### 方法的练习

#### 遍历，求最大值，查找

```java
public class test1 {
    public static void main(String[] args) {
        int [] Array={1,2,3,4,5};
        traverse(Array);
    }

    public static void traverse(int[] array){
        System.out.print('[');
        for (int i = 0; i < array.length-1; i++) {
            System.out.print(array[i]+",");
        }
        System.out.print(array[array.length-1]);
        System.out.print(']');
    }

}
```

```java
public class test2 {
    public static void main(String[] args) {
        int [] array={1,2,3,4,5};
        System.out.println(fmax(array));
    }
    public static int fmax(int [] array){
        int max=array[0];
        for (int j : array) {
            max = Math.max(max, j);
        }
        return max;
    }
}
```

```java
public class test3 {
    public static void main(String[] args) {
        int[] array={1,2,3,4,5};
        System.out.println(find(array,4));
    }
    public static int find(int[] array,int num){
        for (int i = 0; i < array.length; i++) {
            if(num==array[i]) {
                return i+1;
            }
        }
        return -1;
    }
}
```



#### 拷贝数组

```java
public class test4 {
    public static void main(String[] args) {
        int []array={1,2,3,4,5,6 };
        int c[] =copy(array,2,5);
        for (int i = 0; i < c.length; i++) {
            System.out.println(c[i]);
        }
    }
    public static int[] copy(int[] array,int start,int end){
        int [] a= new int [end-start];
        for (int i = 0; i < end-start; i++) {
            a[i]=array[i+start];
        }
        return a;
    }
}
```



### 方法的内存

#### 方法调用的基本内存原理

栈内存

基本数据类型：数据值时存储在自己空间中

特点：赋值给其他变量，也是复真实的值

引用数据类型：数据值是存储在其他空间中，自己空间中存储的是地址值

特点：赋值给其他变量，赋的地址值

#### 方法传递基本数据类型的内存原理

传递基本数据类型是，传递的是真实的数值，形参的改变，不影响实参的值

#### 方法传递引用数据类型的内存原理

传递引用数据类型，传递的是地址值，形参的改变，影响实参的值

## 综合案例

### 案例1：买飞机票

`ctrl+p`显示参数

`ctrl+alt+m`抽取方法

```java
import java.util.Scanner;
public class test1 {
    public static void main(String[] args) {
        Scanner sc= new Scanner(System.in);
        double price=sc.nextDouble();
        int month=sc.nextInt();
        String category=sc.next();
        System.out.println(cost(price,month,category));
    }
    public static double cost(double price,int month,String category){
        if(month>=5 &&month<=10)
        {
            if(category=="头等舱")
                price*=0.9;
            else price*=0.85;
        }
        else{
            if(category=="头等舱")
                price*=0.7;
            else price*=0.65;
        }
        return price;
    }
}
```

### 案例2：找素数

```java
import java.util.Scanner;
public class test2 {
    public static void main(String[] args) {
            Scanner sc=new Scanner(System.in);
            int num=sc.nextInt();
            if(isprime(num)) {
                System.out.println(num+"是质数");
            }
            else {
                System.out.println(num+"不是质数");
            }
    }
    public static boolean isprime(int num){
        for (int i = 2; i < Math.sqrt(num); i++) {
            if(num%i==0){
                return false;
            }
        }
        return true;
    }
}
```

### 案例3：开发验证码

方法：在以后如果要在一堆没有什么关系的数据中随机抽取，可以先把数据放到数组中，再随机抽取一个索引

```java
import java.util.Random;
public class test3 {
    public static void main(String[] args) {
        System.out.println(code());
    }
    public static String code(){
        char[] ASCII = new char[52];
        String cluster = "";
        for (int i = 0; i < ASCII.length; i++) {
            if(i<26){
                ASCII[i]=(char)('a'+i);
            }else{
                ASCII[i]=(char)('A'+i-26);
            }
        }
        Random r= new Random();
        for (int i = 0; i < 4; i++) {
            cluster=cluster+ASCII[r.nextInt(52)];
        }
        cluster=cluster+r.nextInt(10);
        return cluster;
    }
}
```

### 案例4：数组元素复制

```java
public class test4 {
    public static void main(String[] args) {
        int[] array={1,2,3,4,5};
        int[] copy= new int[array.length];
        for (int i = 0; i < array.length; i++) {
            copy[i]=array[i];
        }
        for (int i = 0; i < copy.length; i++) {
            System.out.print(copy[i]);
        }
    }
}
```

### 案例5：评委打分

```java
import java.util.Scanner;
public class test5 {
    public static void main(String[] args) {
        int[] array=evaluate();
        del_max(array);
        del_min(array);
        System.out.println(average(array));
    }
    public static int[] evaluate(){
        int[] array=new int[6];
        Scanner sc =new Scanner(System.in);
        for (int i = 0; i < 6; ) {
            int s=sc.nextInt();
            if(s<=100&&s>=0){
                array[i]=s;
                i++;
            }else{
                System.out.println("输出不合理");
            }
        }
        return array;
    }
    public static void del_max(int[] array){
        int max=array[0];
        for (int i = 0; i < array.length; i++) {
            max=max>array[i]?max:array[i];
            System.out.println(array[i]);
        }
        for (int i = 0; i < array.length-1; i++) {
            if(max==array[i])
            {
                array[i]=array[i+1];
            }
        }
    }
    public static void del_min(int[] array){
        int min=array[0];
        for (int i = 0; i < array.length; i++) {
            min=min<array[i]?min:array[i];
        }
        for (int i = 0; i < array.length-2; i++) {
            if(min==array[i])
            {
                array[i]=array[i+1];
            }
        }
    }
    public static double average(int[]array){
        double sum=0;
        for (int i = 0; i < array.length; i++) {
            sum+=array[i];
        }
        return sum/array.length-2;
    }

}
```

### 案例6：数字加密

加5，对10取余，将数字反转

```java
import java.util.Scanner;
public class test6 {
    public static void main(String[] args) {
        Scanner sc=new Scanner(System.in);
        int num=sc.nextInt();
        int[] array=split(num);
        array=secret(array);
        print(array);
    }
    public static int[] split(int num){
        int count=0;
        int s=num;
        while(s!=0){
            count++;
            s/=10;
        }
        int[] array=new int[count];
        for (int i = 0; i < array.length; i++) {
            array[i]=num%10;
            num/=10;

        }
//        for (int i = 0,j=array.length-1; i < j; i++,j--) {
//            int tmp =array[i];
//            array[i]=array[j];
//            array[j]=tmp;
//        }
        return array;
    }
    public static int[] secret(int[] array){
        for (int i = 0; i < array.length; i++) {
            array[i]=array[i]+5;
            array[i]%=10;
        }
        return array;
    }
    public static void print(int[] array){
        int num=0;
        for (int i = 0; i < array.length; i++) {
            num=num*10+array[i];
        }
        System.out.println(num);
    }

}
```

### 案例7：数字解密

```java
import java.util.Scanner;
public class test7 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int num = sc.nextInt();
        int[] array=reverse(num);
        System.out.println(decode(array));
    }
    public static int [] reverse(int num){
        int s=num,count=0;
        while(s!=0){
            count++;
            s/=10;
        }
        int [] array=new int[count];
        for (int i = 0; i < array.length; i++) {
            array[i]=num%10;
            num/=10;
        }
        return array;
    }
    public static int decode(int[]array){
        for (int i = 0; i < array.length; i++) {
            array[i]-=5;
            if (array[i]<0)
            {
                array[i]+=10;
            }
        }
        int num=0;
        for (int i = 0; i < array.length; i++) {
            num=num*10+array[i];
        }
        return num;
    }
}
```

### 案例8：抢红包

```java
import java.util.Random;
public class test8 {
    public static void main(String[] args) {
        int[] array={2,588,888,1000,100000};
        Random r=new Random();

        for (int i = 0; i < array.length; i++) {
            int index=r.nextInt(array.length);
            int tmp = array[i];
            array[i]=array[index];
            array[index]=tmp;
        }
        for (int i = 0; i < array.length; i++) {
            System.out.print(array[i]+" ");
        }
    }
}
```

### 案例9：模拟双色球

```java
import java.util.Scanner;
import java.util.Random;
public class test9 {

    public static void main(String[] args) {
        int[] a=generate();
        int[] b=choice();
        prize(b,a);
    }
    public static int [] generate(){
        int[] array=new int[7];
        Random r=new Random();
        for (int i = 0; i < array.length-1; ) {
            int x=r.nextInt(33)+1;
            if(exist(array, x)) {
                array[i] = x;
                i++;
            }
            else{
                System.out.print("请重新输入");
            }
        }
        array[array.length-1]=r.nextInt(16)+1;
        for (int i = 0; i < array.length; i++) {
            System.out.print(array[i]+" ");
        }
        return array;
    }
    public static int [] choice(){
        Scanner sc=new Scanner(System.in);
        int[] array= new int[7];
        for (int i = 0; i < array.length-1;) {
            int x=sc.nextInt();
            if(x<=33&&x>=0 && exist(array, x)){
                array[i]=x;
                i++;
            }
            else{
                System.out.println("请重新输入");

        }
        }
        int x=sc.nextInt();
        while(true) {
            if (x <= 16 && x >= 0)
            {array[array.length - 1] = x;
            break;

            }
            else {
                System.out.println("请重新输入");
                x=sc.nextInt();
            }

        }
        return array;
    }
    public static  void prize (int []array,int []compose){
        int count_red=0,count_blue=0;
        for (int i = 0; i < compose.length; i++) {
            System.out.print(compose[i]+" ");
        }
        System.out.println();
        for (int i = 0; i < array.length-1; i++) {
            for (int j = 0; j < compose.length-1; j++) {
                if(array[i]==compose[j])
                {
                    count_red++;
                }
            }
        }
        if(array[array.length-1]==compose[compose.length-1]) count_blue++;
        System.out.println(count_red);
        System.out.println(count_blue);
        if(count_red==6 && count_blue==1)
        {
            System.out.println("1000万");
        } else if (count_red==6) {
            System.out.println("500万");
        } else if (count_red==5&&count_blue==1) {
            System.out.println("3000");
        } else if ((count_red==5&&count_blue==0)|| (count_red==4&&count_blue==1)) {
            System.out.println("200");
        } else if ((count_red==4&&count_blue==0)|| (count_red==3&&count_blue==1)|| (count_red==2&&count_blue==1)) {
            System.out.println("10");
        } else if ((count_red==1&&count_blue==1)|| (count_red==0&&count_blue==1)) {
            System.out.println("5");
        }
    }
    public static boolean exist(int[] array,int number){
        for (int i = 0; i < array.length; i++) {
            if(number==array[i])
                return false;
        }
        return true;
    }


}
```

### 案列10：二维数组

当我们需要数据分组管理的时候，就需要二维数组

#### 静态初始化

格式：数据类型[\][\]数组名=new 数据类型[\][\]{{元素1，元素2},{元素1，元素2}};

简化格式：数据类型[\][\]数组名={{元素1，元素2},{元素1，元素2}};

每一个一位数组单独写成一行

每个一维数组就是二维数组中的一个元素，所以每一个一维数组需要用逗号隔开，最后一个数组后面不需要逗号

#### 获取元素

arr[i][j\]

i:二维数组的索引，获取出来的是里面的一维数组

j:表示一维数组中的索引，获取的是真正的元素

#### 数组遍历

二重循环，一重获得数组行数，二重获得元素

#### 动态初始化

格式：数组类型[][\]数组名=new数据类型[m\][n\]

m表示这个二维数组，可以存放多少个一位数组

n表示每一个一位数组，可以存放多少个元素

```java
public class test10 {
    public static void main(String[] args) {
        int [][]arr={{22,66,44},
                {77,33,88},
                {25,45,65},
                {11,66,99}};
        int []s=new int [4];
        int sum=0;
        for (int i = 0; i < arr.length; i++) {
            for (int j = 0; j < arr[i].length; j++) {
                s[i]+=arr[i][j];
            }
        }
        for (int i = 0; i < s.length; i++) {
            System.out.print(s[i]+" ");
            sum+=s[i];
        }
        System.out.println();
        System.out.println(sum);
    }
}
```

## 面向对象

### 设计对象并使用

#### 类和对象

- 类（设计图）：是对象共同特征的描述
- 对象：是真实存在的具体东西

再java中，必须设计类，才能获得对象

定义类

```java
public class 类名{
    1、成员变量（代表属性，一般是名词）;
    2、成员方法（代表行为，一般是动词）;
    3、构造器;
    4、代码块;
    5、内部类;  
}
```

得到类的对象

```java
类名 对象名 = new 类名();
```

使用对象

- 访问属性：对象名.成员变量
- 访问行为：对象名.方法名(...)

#### 类的几个补充注意事项

- 用来描述一类事物的类，专业叫做：javabean类
    在JavaBean类中是不写main方法的

- 在以前，编写main方法的类，叫做测试类。
    我们可以在测试类中创建JavaBean类的对象进行赋值调用

- 类名首字母建议大写，需要见名知义，驼峰样式

- 一个Java文件可以定义多个class类，且只有一个类是public修饰，而且public修饰的类名必须称为代码文件名。
    实际开发建议还是一个文件定义一个class类

- 成员定义的完整格式是：修饰符 数据类型 变量名称 = 初始化值，一般无需指定初始化值，存在默认值

- 对象的成员变量的默认值规则

    | 数据类型 | 明细                   | 默认值 |
    | -------- | ---------------------- | ------ |
    | 基本类型 | byte、short、int、long | 0      |
    | 基本类型 | float、double          | 0.0    |
    | 基本类型 | boolean                | false  |
    | 引用类型 | 类、接口、数组、String | null   |

### 封装

正确设计对象的属性和方法

对象代表什么，就得封装对应的数据，并提供数据对应的行为

封装的好处

让编程变得简单，有什么是，找对象，调方法就行

降低我们的学习成本，可以少学，少记，或者压根不用学，不用急对象有哪些方法，有需要去找就行

#### private关键字

- 是一个权限修饰符

- 可以修饰成员变量（成员变量和成员方法）

- 被private修饰的成员只能在本类中访问

    

分隔到一个屏幕

`Ctrl + Alt + L`格式化代码

### this关键字

#### 成员变量与局部变量

成员变量定义在类里面

局部变量定义在类的方法里面

#### 就近原则

谁离我近，我就用谁

#### this作用

区分成员变量和局部变量

### 构造方法

构造方法也叫构造器，构造函数

创建对象的时候，虚拟机会自动调用构造方法，作用是给成员变量进行初始化的

作用：在创建对象的时候给成员变量进行初始化的

```java
public class Student{
    修饰符 类名(参数){
        方法体;
    }
}
```

特点：

1. 方法名与类名相同，大小写也要一致
2. 没有返回值类型，连viod也没有
3. 没有具体的返回值（不能有return带回返回结果的数据）
4. 分空参构造与带参构造

执行时机：

1. 创建的时候有虚拟机调用，不能手动的调用构造方法
2. 每创建一次对象，就会调用一次构造方法

注意事项

1. 构造方法的定义
    - 如果没有定义构造方法，系统将给出一个默认的无参数的构造方法
    - 如果定义了构造方法，系统将不在提供默认的构造方法
2. 构造方法的重载
    - 带参构造方法，和无参数构造方法，两者方法名相同，但是参数不同，这叫做构造方法的重载
3. 推荐的使用方式
    - 无论是否使用，都手动的书写无参数的构造方法，和带全部参数的构造方法

### 标准JavaBean

1. 类名需要见名知义
2. 成员变量使用private修饰
3. 提供至少两个构造方法
    - 无参数的构造方法
    - 带全部参数的构造方法
4. 成员方法
    - 提供每一个成员变量对应的setXxx()/getXxx()
    - 如果还有其他行为，也需要写上

快捷键：

`alt + insert`

`alt + Fn + insert`

插件PTG 1秒生成标准Javabean

### 对象内存图

#### Java内存分配介绍

![image-20250531220652348](images/image-20250531220652348.png)

#### 一个对象的内存图

1. 加载class文件
2. 申明局部变量
3. 在堆内存中开辟一个空间
4. 默认初始化
5. 显示初始化
6. 构造方法初始化
7. 将堆内存中的地址值赋值给左边的局部变量

#### 基本数据类型和引用数据类型

基本数据类型：数据值是存储在自己的空间中

特点：赋值给其他变量，也是赋的真实的值

引用数据类型：数据值是存储在其他空间中，自己空间中存储的是地址值

特点：赋值给其他变量，赋的地址值

#### this的本质

代表方法调用者的地址值

### 补充知识：成员变量、局部变量的区别

成员变量

类中方法外的变量

局部变量

方法中的变量

| 区别         | 成员变量                                   | 局部变量                                   |
| ------------ | ------------------------------------------ | ------------------------------------------ |
| 类中位置不同 | 类中，方法外                               | 方法内，方法申明上                         |
| 初始化值不同 | 有默认给初始值                             | 没有，使用之前完成赋值                     |
| 内存位置不同 | 堆内存                                     | 栈内存                                     |
| 生命周期不同 | 随着对象的创建而存在，随着对象的消失而消失 | 随着对象的创建而存在，随着方法的结束而消失 |
| 作用域       | 整个类中有效                               | 当前方法有效                               |

## 面向对象综合练习

### 文字版格斗游戏

```java
import java.util.Random;

public class Role {
    private String name;
    private  int blood;

    public Role() {
    }

    public Role(String name, int blood) {
        this.name = name;
        this.blood = blood;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getBlood() {
        return blood;
    }

    public void setBlood(int blood) {
        this.blood = blood;
    }

    public void attack(Role role){
        Random r = new Random();
        int harm=r.nextInt(20)+1;
        int remainblood=role.getBlood()-harm;
        role.setBlood(remainblood<0?0:remainblood);
        System.out.println(this.getName()+"举起拳头，打了"+role.getName()+"一下，"+"造成了"+harm+"点伤害"+"还剩"+role.getBlood()+"血量");
    }
}
```

```java
package com.yuanshenligong;

import java.util.Scanner;

public class game {
    public  static void main(String[] args){
        Scanner sc= new Scanner(System.in);
        Role character1= new Role(sc.next(),sc.nextInt());
        Role character2= new Role(sc.next(),sc.nextInt());
        while(true){
            character1.attack(character2);
            if(character2.getBlood()==0){
                System.out.println(character1.getName()+"KO了"+character2.getName());
                break;
            }
            character2.attack(character1);
            if(character1.getBlood()==0){
                System.out.println(character2.getName()+"KO了"+character1.getName());
                break;
            }
        }
    }
}
```

两部分参数

第一部分参数：要输出的内容%s（占位）

第二部分参数：填充的数据

### 对象数组练习

#### 对象数组1

```java
public class array1 {
    private int id;
    private String name;
    private int count;

    public array1(int id, String name, int count) {
        this.id = id;
        this.name = name;
        this.count = count;
    }

    public array1() {
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getCount() {
        return count;
    }

    public void setCount(int count) {
        this.count = count;
    }
}
```

```java
public class arraytest1 {
    public static void main(String[] args) {
        array1[] good = new array1[3];
        array1 g1 = new array1(1, "手机", 3);
        array1 g2 = new array1(4, "电脑", 6);
        array1 g3 = new array1(7, "平板", 9);
        good[0]=g1;
        good[1]=g2;
        good[2]=g3;
        for (int i = 0; i < good.length; i++) {
            System.out.println("序号"+good[i].getId()+"的"+good[i].getName()+"还剩"+good[i].getCount());
        }
    }
}
```

#### 对象数组2

键盘录入：

第一套体系：

nextInt();接受整数

nextDouble();接受小数

next();接受字符串

遇到空格，制表符，回车停止接受，这些符号后面就不会接受

第二套体系：

nextLine();接受字符串

可以接受空格，制表符，遇到回车才停止接受数据

```java
public class Car {
    private String brand;
    private int price;
    private String color;

    public Car(String brand, int price, String color) {
        this.brand = brand;
        this.price = price;
        this.color = color;
    }

    public Car() {
    }

    public String getBrand() {
        return brand;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }

    public int getPrice() {
        return price;
    }

    public void setPrice(int price) {
        this.price = price;
    }

    public String getColor() {
        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }
}
```

```java
import java.util.Scanner;

public class Car_test {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        Car [] cars = new Car[3];

        for (int i = 0; i < cars.length; i++) {
            Car c = new Car();
            c.setBrand(sc.next());
            c.setPrice(sc.nextInt());
            c.setColor(sc.next());
            cars[i]=c;
        }
        for (int i = 0; i < cars.length; i++) {
            Car car0 = cars[i];
            System.out.println(car0.getBrand()+"的"+car0.getColor()+"色"+"的价格是"+car0.getPrice());
        }
    }
}
```

#### 对象数组3

```java
public class Phone {
    private String brand;
    private int price;
    private String color;

    public Phone(String brand, int price, String color) {
        this.brand = brand;
        this.price = price;
        this.color = color;
    }

    public Phone() {
    }

    public String getBrand() {
        return brand;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }

    public int getPrice() {
        return price;
    }

    public void setPrice(int price) {
        this.price = price;
    }

    public String getColor() {
        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }
}
```

```java
public class phone_test {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Phone[] phones = new  Phone[3];
        for (int i = 0; i < phones.length; i++) {
            Phone p = new Phone();
            p.setBrand(sc.next());
            p.setPrice(sc.nextInt());
            p.setColor(sc.next());
            phones[i]=p;
        }
        int sum=0;
        for (int i = 0; i < phones.length; i++) {
            sum+=phones[i].getPrice();
        }
        double average=sum/phones.length;
        System.out.printf("%.5s",average);
    }
}
```

#### 对象数组4

```java
public class GirlFriend {
    private String name;
    private int year;
    private String gender;
    private String love;

    public GirlFriend() {
    }

    public GirlFriend(String name, int year, String gender, String love) {
        this.name = name;
        this.year = year;
        this.gender = gender;
        this.love = love;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getYear() {
        return year;
    }

    public void setYear(int year) {
        this.year = year;
    }

    public String getGender() {
        return gender;
    }

    public void setGender(String gender) {
        this.gender = gender;
    }

    public String getLove() {
        return love;
    }

    public void setLove(String love) {
        this.love = love;
    }
}
```

```java
public class GirlFriendTest {
    public static void main(String[] args) {
        GirlFriend [] girlFriends=new  GirlFriend[4];
        girlFriends[0]=new GirlFriend("小美",18,"女","打球");
        girlFriends[1]=new GirlFriend("小玲",19,"女","游戏");
        girlFriends[2]=new GirlFriend("小琪",20,"女","睡觉");
        girlFriends[3]=new GirlFriend("小烨",21,"女","干饭");

        int sum=0;
        for (int i = 0; i < girlFriends.length; i++) {
            sum+=girlFriends[i].getYear();
        }
        double average=1.0*sum/girlFriends.length;

        for (int i = 0; i < girlFriends.length; i++) {
            if(girlFriends[i].getYear()<average)
            {
                System.out.println(girlFriends[i].getName());
            }
        }
    }
}
```

#### 对象数组5

```java
public class Student {
    private int id;
    private String name;
    private int old;

    public Student() {
    }

    public Student(int id, String name, int old) {
        this.id = id;
        this.name = name;
        this.old = old;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getOld() {
        return old;
    }

    public void setOld(int old) {
        this.old = old;
    }
}
```

```java
public class StudentTest {
    public static void main(String[] args) {
        int len=3;
        Student[] students = new Student[len];
        students[0] = new Student(1, "小明", 18);
        students[1] = new Student(2, "小亮", 18);
        students[2] = new Student(3, "小红", 18);

        Student student = new Student(4, "小王", 18);
        boolean flag = false;
        for (int i = 0; i < students.length; i++) {
            if (students[i] == null) {
                if (student.getId() == students[i].getId()) {
                    flag = true;
                }
            }
        }
        if (flag) {
            System.out.println("以重复，请重新输入");
        } else {
            Student[] array;
            array = new  Student[6];
            if(students.length<len){
                
                students[students.length+1]=student;
                array = students;
            }
            else {
                System.arraycopy(students,0,array,0,students.length);
                array[students.length]=student;

            }
            for (int i = 0; i < array.length; i++) {
                if(array[i]!=null) System.out.println(array[i].getId()+","+array[i].getOld()+","+array[i].getName());
            }
        }
        int id=4;
        int in=index( students, id);
        if(in>=0)students[in]=null;
        for (int i = 0; i < students.length; i++) {
            System.out.println(students[i].getId()+","+students[i].getOld()+","+students[i].getName());
        }
        int s=0;
        for (int i = 0; i < students.length; i++) {
            if(students[i].getId()==s){
                students[i].setOld(students[i].getOld()+1);
            }
        }

    }

    public static int  index(Student[] students,int id){
        for (int i = 0; i < students.length; i++) {
            if(id==students[i].getId()){
                return i;
            }
        }
        return -1;

    }
}
```

## 字符串

### String

java.lang.String类代表字符串，Java程序中所有字符串文字都为此类的对象

字符串的内容是不会发生改变的，它的对象在创建后不能更改

#### 创建String对象的两种方式

1. 直接赋值

2. new

    | 构造方法                       | 说明                             |
    | ------------------------------ | -------------------------------- |
    | public String()                | 创建空白字符串，不含任何内容     |
    | public String(String original) | 根据传入的字符串，创建字符串对象 |
    | public String(char[] chs)      | 根据字符数组，创建字符串对象     |
    | public String(byte[] chs)      | 根据字节数组，创建字符串对象     |

当使用双引号进行赋值时，系统会检查该字符串在串池中是否存在

不存在：创建新的

存在：复用

#### 比较

==基本数据类型比较的是数据值

引用数据类型比较的是地址值

| 字符串比较                                 | 结果                          |
| ------------------------------------------ | ----------------------------- |
| boolean equals方法（要比较的字符串）       | 完全一样才是true，否则为false |
| boolean equalsIgnoreCase（要比较的字符串） | 忽略大小写的比较              |

#### 遍历

| 方法                          | 结果               |
| ----------------------------- | ------------------ |
| public char charAt(int index) | 根据索引返回字符   |
| public int length()           | 返回此字符串的长度 |
| 数组名.length                 | 数组的长度         |
| 字符串对象.length             | 字符串长度         |

#### 截取

| 方法                                           | 结果       |
| ---------------------------------------------- | ---------- |
| String substring(int beginIndex ,int endIndex) | 截取       |
| String substring(int beginIndex)               | 截取到末尾 |

注意点：包头不包尾，包左不包右，只有返回值才是截取的小串

#### 替换

| 方法                      | 结果 |
| ------------------------- | ---- |
| String replace(旧值,新值) | 替换 |

注意点：只有返回值才是替换后的结果

#### 添加

| 方法              | 结果 |
| ----------------- | ---- |
| String append(值) | 添加 |

#### 案例

##### 用户登录

```java
import java.util.Scanner;

public class test1 {
    public static void main(String[] args) {
        String password = "123456";
        String account="lyz";
        Scanner sc=new Scanner(System.in);
        boolean flag = false;
        for (int i = 0; i < 3; i++) {
            if(sc.next().equals(account)){
                if(sc.next().equals(password)) {
                    System.out.println("输入正确");
                    flag=true;
                    break;
                }
            }
            System.out.println("输入错误");
        }
        if(!flag){
            System.out.println("你已累计输错达三次");
        }

    }
}
```

##### 遍历字符串

```java
import java.util.Scanner;

public class test2 {
    public static void main(String[] args) {
        Scanner sc= new Scanner(System.in);
        String x=sc.next();
        for (int i = 0; i < x.length(); i++) {
            System.out.println(x.charAt(i));
        }
    }
}
```

##### 统计字符数量

```java
import java.util.Scanner;

public class test3 {
    public static void main(String[] args) {
        Scanner sc= new Scanner(System.in);
        String x=sc.next();
        int small_count=0;
        int big_count=0;
        int number_count=0;
        for (int i = 0; i < x.length(); i++) {
            char c = x.charAt(i) ;
            if((c>= 'a' ) && (c<='z')){
                small_count++;
            }
            else if((c>='A')&&(c<='Z')){
                big_count++;
            }
            else if((c<='9')&&(c>='1')){
                number_count++;
            }
        }
        System.out.println(small_count);
        System.out.println(big_count);
        System.out.println(number_count);
    }
}
```

##### 字符拼接

```java
public class test4 {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3};
        String s="[";
        for (int i = 0; i < arr.length-1; i++) {
            s+=arr[i]+",";
        }
        s+=arr[arr.length-1]+"]";
        System.out.println(s);
    }
}
```

##### 字符反转

```java
import java.util.Scanner;

public class test5 {
    public static void main(String[] args) {
        Scanner sc= new Scanner(System.in);
        System.out.println(reverse(sc.next()));
    }
    public static String reverse(String s){
        String a="";
        for (int i = s.length()-1; i >= 0; i--) {
            a+=s.charAt(i);
        }
        return a;
    }
}
```

##### 金额转换

```java
import java.util.Scanner;

public class test6 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String x;
        int num;
        while (true) {
            num = sc.nextInt();
            if(num<9999999&&num>=0)
            {
                break;
            }
            else {
                System.out.println("请重新输入");
            }
        }
        x=converse(num);
        x=supply_zero(x);
        x=insert(x);
        System.out.println(x);
    }
    public static String converse(int num){
        char[] character = {'零','壹','贰','叁','肆','伍','陆','柒','捌','玖'};

        String s="";
        while (num!=0)
        {
            char p =character [num%10];
            num/=10;
            s+=p;
        }
        return s;
    }
    public static String supply_zero(String s){

        String a="";
        for (int i = 0; i < 7-s.length(); i++) {
            a+='零';
        }
        for (int i = s.length()-1; i >= 0 ; i--) {
            a+=s.charAt(i);
        }
        return a;
    }
    public static String insert(String a){
        char[] big_character={'佰','拾','万','仟','佰','拾','元'};
        String h="";
        for (int i = 0; i < a.length(); i++) {
            h+=a.charAt(i);
            h+=big_character[i];
        }
        return h;
    }
}
```

##### 手机号屏蔽

```java
import java.util.Scanner;

public class test7 {
    public static void main(String[] args) {
        Scanner sc= new Scanner(System.in);
        long num;
        while (true) {
            num = sc.nextLong();
            if (num < 99999999999L && num > 10000000000L) break;
            else System.out.println("请重新输入");
        }
        System.out.println(number(num));
    }
    public static String number(long num){
        String s="";
        while (num!=0){
            s+=num%10;
            num/=10;
        }
        String a="";
        for (int i = s.length()-1; i>=0; i--) {
            if(i<4||i>7) a+=s.charAt(i);
            else a+="*";
        }
        return a;
    }

}
```

##### 身份证号信息查询

```java
public class test8 {
    public static void main(String[] args) {
        String s = "140781200606300010";
        System.out.println( find(s));
    }
    public static String find(String s)
    {
        String x,y,z,k;
        x=s.substring(6,10)+"年";
        y=s.substring(10,12)+"月";
        z=s.substring(12,14)+"日";
        if((s.charAt(16)-48)%2==0)
            k="女";
        else k="男";
        x=x+y+z+k;
        return x;
    }
}
```

##### 敏感词替换

```java
public class test9 {
    public static void main(String[] args) {
        System.out.println(replace("Tmd,ma"));
    }
    public static String replace(String s){
        s=s.replace("Tmd","***");
        return s;
    }
}
```

### StringBuilder

可以看成一个容器，创建之后是可变的

作用：提高字符串的操作效率

| 方法名                         | 说明                                                |
| ------------------------------ | --------------------------------------------------- |
| public StringBuilder append()  | 添加数据，并返回对象本身                            |
| public StringBuilder reverse() | 反转容器中的内容                                    |
| public int length()            | 返回长度（字符出现的次数）                          |
| public String toString()       | 通过toString()就可以实现把StringBuilder转化为String |

普及：

因为StringBuilder是Java已经写好的类，Java底层对他进行了些特殊处理，打印对象不是地址值，而是属性值

链式编程：

当我们在调用一个方法的时候，不需要用变量接受他的结果，可以继续调用其他方法

### StringJoiner

StringJoiner跟StringBuilder一样，也可以卡成是一个容器，创建之后里面的内容是可变的

作用：提高字符串的操作效率，而且代码编写特别简洁

JDK8出现的

| 方法名                    | 说明                                       |
| ------------------------- | ------------------------------------------ |
| public StringJoiner add() | 添加数据，并返回对象本身                   |
| public int length()       | 返回长度(字符出现的次数)                   |
| public String toString()  | 返回一个字符串(该字符串就是拼接之后的结果) |

在拼接的时候，可以指定间隔符号，结束符号

### 字符串原理

#### 字符串存储的内存原理

- 直接赋值会复用字符串常量池中的
- new出来不会复用，而是开辟一个新空间

#### ==号比较的是什么

- 基本数据类型比较数据值
- 引用数据类型比较地址值

#### 字符串拼接的底层原理

拼接的时候没有变量，都是字符串

触发字符串的优化机制

在编译的时候就已经是最终结果了

`Ctrl+N`查找

`Ctrl+F12`查找方法

一个加号，堆内存中俩对象

字符串拼接的时候有常量参与：

在内存中创建了很多对象，浪费空间，时间也非常慢

很多字符串拼接，不要直接+

JDK8版本：系统会预估要字符串拼接之后的总大小，把要拼接的内容都放在数组中，此时也是产生了一个新字符串

- 如果没有变量参与，都是字符串直接相加，编译之后就是拼接之后的结果，会复用串池中的字符串
- 如果有变量的参与，每一行拼接的代码，都会在内存中创建新的字符串，浪费内存

#### StringBuilder提高效率原理图

-  所有要拼接的内容都会往StringBuilder中放，不会创建很多无用空间，节约内存

#### StringBuilder源码分析

- 默认创建一个长度为16的字节数组
- 添加的内容长度小于16，直接存
- 添加内容大于16会扩容（原来的容量*2+2）
- 如果扩容之后还不够，以实际长度为准

### 综合练习

#### 转化罗马数字

```java
import java.util.Scanner;

public class test12 {


    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String x;
        while (true) {
            x = sc.next();
            if(check(x)) break;
            else System.out.println("请重新输入");
        }
        String y=converse(x);
        System.out.println(y);

    }
    public static String converse(String s){
        String str="";
        char [] a ={' ','Ⅰ','Ⅱ','Ⅲ','Ⅳ','Ⅴ','Ⅵ','Ⅶ','Ⅷ','Ⅸ'};
        for (int i = 0; i < s.length(); i++) {
            int j = s.charAt(i)-48;
            str+=a[j];

        }

        return str;
    }
    public static boolean check(String s){
        if(s.length()>9){
            return false;
        }
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if(c<'1' || c>'9')
                return false;
        }
        return true;
    }
}
```

#### 旋转字符串

```java
import java.util.Scanner;

public class test13 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String a = sc.next();
        String b = sc.next();
        System.out.println( overturn(a,b));
    }
    public static boolean overturn(String a,String b){
        String x=a;
        for (int i = 0; i < a.length(); i++) {
            a = a.substring(1) + a.charAt(0);
            if(a.equals(b)) return true;
        }
        return false;
    }
}
```

#### 打乱字符串

```java
import java.util.Random;
import java.util.Scanner;

public class test14 {
    //键盘输入字符串，打乱其中的内容
    public static void main(String[] args) {
        Scanner sc = new  Scanner(System.in);
        String x = sc.next();
        String s = disorganize(x);
        System.out.println(s);
    }

    public static String disorganize(String s){
        Random r = new Random();
        char[] c= s.toCharArray();
        for (int i = 0; i < s.length(); i++) {
            int x = r.nextInt(s.length());
            char tmp = c[i];
            c[i]=c[x];
            c[x]=tmp;

        }
        s="";
        for (int i = 0; i < c.length; i++) {
            s+=c[i];
        }
        return s;
    }
}
```

#### 验证码（进阶）

```java
import java.util.Random;

public class test15 {
    //生成随机验证码，数字可以出现在任意位上
    public static void main(String[] args) {
        Random r = new Random();
        int x = r.nextInt(4);
        String s="";
        char [] c=new char[52];
        for (int i = 0; i < c.length; i++) {
            if(i<26) c[i]= (char) ('a'+i);
            else c[i]= (char) ('A'+i-26);
        }

        for (int i = 0; i < 4; i++) {
            if(i==x) s+=r.nextInt(10);
            s+=c[r.nextInt(52)];

        }
        System.out.println(s);
    }
}
```

#### 字符串计算

```java
public class test16 {
    //字符串形式的num1和num2返回乘积 结果也用字符串表示
    public static void main(String[] args) {
        Scanner sc=  new Scanner(System.in);
        String num1 = sc.next();
        String num2 = sc.next();
        int j=0,k=0;
        for (int i = 0; i < num1.length(); i++) {
            j=j*10+num1.charAt(i);
        }
        for (int i = 0; i < num2.length(); i++) {
            k=k*10+num2.charAt(i);
        }
        int x= k*j;
        String num="";
        while (x!=0)
        {
            num+=x%10;
            x/=10;
        }
        String s="";
        for (int i = num.length()-1; i >=0 ; i--) {
            s+=num.charAt(i);
        }
        System.out.println(s);
    }
}
```

#### 返回最后一个单词的长度

```java
import java.util.Scanner;

public class test17 {
    //返回字符串最后一个单词的长度
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String x = sc.nextLine();
        int count=0;
        for (int i = x.length()-1; i >=0 ; i--) {
            System.out.println(x.charAt(i));
            if(x.charAt(i)==' ') break;
            count++;
        }
        System.out.println(count);
    }
}
```

## 集合

### 为什么要有集合

集合与数组对比

- 长度：集合可变，数组不可变
- 存储类型：数组既可以存储可变数据类型，又可以存储不可变数据类型
                      集合可以存引用数据类型，基础数据类型要转化为包装类可存

### 集合

##### ArrayList成员方法

|      | 方法名               | 说明                                 |
| ---- | -------------------- | ------------------------------------ |
| 增   | boolean add(E e)     | 添加元素，返回值表示添加是否成功     |
| 删   | boolean remove(E e)  | 删除指定元素，返回值表示是否删除成功 |
|      | E remove(int index)  | 删除指定索引的元素，返回被删除元素   |
| 改   | E set(int index,E e) | 修改指定索引下的元素，返回原来的元素 |
| 查   | E get(int index)     | 获取指定索引的元素                   |
|      | int size()           | 集合的长度，也就是集合中元素的个数   |

### 综合练习

#### 添加字符串并输出

```java
import java.util.ArrayList;
import java.util.List;
import java.util.StringJoiner;

public class test1 {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();

        list.add("123");
        list.add("456");
        list.add("789");

        StringJoiner sj = new StringJoiner(",", "[","]");
        for (int i = 0; i < list.size(); i++) {
            sj.add(list.get(i));
        }
        System.out.println(sj);

    }
}
```

| 基本数据类型 | 包装类    |
| ------------ | --------- |
| byte         | Byte      |
| short        | Short     |
| char         | Character |
| int          | Integer   |
| long         | Long      |
| float        | Float     |
| double       | Double    |
| boolean      | Boolean   |

#### 添加学生对象并输出信息

```java
public class Student {
    private String name;
    private int age;

    public Student() {
    }

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

```java
import java.util.ArrayList;
import java.util.Scanner;
import java.util.StringJoiner;

public class test2 {
    public static void main(String[] args) {
        ArrayList<Student> list = new ArrayList<>();
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入学生的个数");
        int n = sc.nextInt();
        for (int i = 0; i < n; i++) {
            Student student = new Student();
            student.setName(sc.next());
            student.setAge(sc.nextInt());
            list.add(student);
        }
        for (int i = 0; i < list.size(); i++) {
            System.out.print (list.get(i).getName()+" ");
            System.out.println( list.get(i).getAge());
        }
    }
}
```

#### 查找用户是否存在

```java
    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }
}
```

```java
import java.util.ArrayList;
import java.util.Scanner;

public class test3 {
    public static void main(String[] args)
    {
        ArrayList<User> list = new ArrayList<>();
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        for (int i = 0; i < n; i++) {
            User user = new User();
            user.setId(sc.next());
            user.setUsername(sc.next());
            user.setPassword(sc.next());
            list.add(user);
        }

        String x = sc.next();
        System.out.print(seek(list,x));


    }
    public static boolean seek(ArrayList<User> list ,String ID){
        for (int i = 0; i < list.size(); i++) {
            if(list.get(i).getId().equals(ID))return true;
        }
        return false;
    }
}
```

#### 返回多个数据

```java
public class Phone {
    private String brand;
    private int price;

    public Phone() {
    }

    public Phone(String brand, int price) {
        this.brand = brand;
        this.price = price;
    }

    public String getBrand() {
        return brand;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }

    public int getPrice() {
        return price;
    }

    public void setPrice(int price) {
        this.price = price;
    }
}
```

```java
import java.util.ArrayList;
import java.util.Scanner;

public class test4 {
    public static void main(String[] args) {
        ArrayList<Phone> list = new ArrayList<>();
        Phone p1 = new Phone("小米", 1000);
        Phone p2 = new Phone("苹果", 8000);
        Phone p3 = new Phone("锤子", 2999);
        list.add(p1);
        list.add(p2);
        list.add(p3);
        ArrayList<Phone> k=ret(list);
        for (int i = 0; i < k.size(); i++) {
            System.out.print(k.get(i).getBrand()+" ");
        }
    }
    public static ArrayList<Phone> ret (ArrayList<Phone> list){
        ArrayList<Phone> k = new ArrayList<>();
        for (int i = 0; i < list.size(); i++) {
            if(list.get(i).getPrice()<3000) k.add(list.get(i));
        }
        return k;
    }
}
```

### 学生管理系统

```java
public class Student {
    private String ID;
    private String Name;
    private int year;
    private String Home;

    public Student() {
    }

    public Student(String ID, String name, int year, String home) {
        this.ID = ID;
        Name = name;
        this.year = year;
        Home = home;
    }

    public String getID() {
        return ID;
    }

    public void setID(String ID) {
        this.ID = ID;
    }

    public String getName() {
        return Name;
    }

    public void setName(String name) {
        Name = name;
    }

    public int getYear() {
        return year;
    }

    public void setYear(int year) {
        this.year = year;
    }

    public String getHome() {
        return Home;
    }

    public void setHome(String home) {
        Home = home;
    }
}
```

```java
public class Main {
    static Scanner sc = new Scanner(System.in);
    static boolean flag=true;
    public static void main(String[] args) {
        while (flag) {
            System.out.println("-----------------欢迎来到学生管理系统-----------------");
            System.out.println("1：添加学生");
            System.out.println("2：删除学生");
            System.out.println("3：修改学生");
            System.out.println("4：查看学生");
            System.out.println("5：退出系统");
            System.out.println("请输入你的选择");
            int choose = sc.nextInt();
            switch (choose) {
                case 1 -> add();
                case 2 -> delete();
                case 3 -> change();
                case 4 -> seek();
                case 5 -> exit();
                default -> System.out.println("请重新输入");
            }
        }
    }
    static ArrayList<Student> s = new ArrayList<>();
    public static void add(){
        String ID=sc.next();
        String name = sc.next();
        int year = sc.nextInt();
        String home = sc.next();
        Student student = new Student(ID,name,year,home);
        boolean flag = true;
        for (Student value : s) {
            if (value.getID().equals(ID)) {
                flag = false;
                break;
            }
        }
        if(flag) s.add(student);
    }
    public static void delete(){
        String ID=sc.next();
        boolean flag = true;
        for(int i =0;i<s.size();i++){
            if(s.get(i).getID().equals(ID)) {
                s.remove(i);
                flag = false;
                break;
            }
        }
        if(flag) System.out.print("学生不存在");
    }
    public static void change(){
        String ID=sc.next();
        boolean flag = true;
        for(int i =0;i<s.size();i++){
            if(s.get(i).getID().equals(ID)) {
                s.get(i).setHome(sc.next());
                flag = false;
                break;
            }
        }
        if(flag) System.out.print("学生不存在");
    }
    public static void seek(){
        String ID=sc.next();
        boolean flag = true;
        for(int i =0;i<s.size();i++){
            if(s.get(i).getID().equals(ID)) {
                System.out.println(s.get(i).getName());
                System.out.println(s.get(i).getID());
                System.out.println(s.get(i).getYear());
                System.out.println(s.get(i).getHome());
                flag = false;
                break;
            }
        }
        if(flag) System.out.print("学生不存在");
    }
    public static void exit(){
        flag=false;
    }
}
```

## 面向对象进阶

### static

static表示静态，是Java中的一个修饰符，可以修饰成员方法，成员变量

#### 静态变量

被static修饰的成员变量，叫做静态变量

特点：

- 被该类的所有对象共享
- 不属于对象，属于类
- 随着类的加载而加载，优先于对象的存在

调用方式：

- 类名调用（推荐）
- 对象名调用

#### 静态方法

被static修饰的成员方法

特点：

- 多用在测试类和工具类中
- JavaBean类中很少会用

调用方式：

- 类名调用（推荐）
- 对象名调用

#### 类的分类

javabean：用来描述一类事物的类

测试类：用来检查其他类是否书写正确，带有main方法的类，是程序的主入口

工具类：不是用来描述事物的，而是帮我们做一写事情的类

1. 类名见名知义
2. 私有化构造方法
3. 方法定义为静态

```java
import java.util.StringJoiner;

public class ArrayUtil {
    private ArrayUtil(){}
    public static String printArr(int [] a){
        StringJoiner sj = new StringJoiner(",","[","]");
        String k ="";
        for (int i = 0; i < a.length; i++) {
            k+=a[i];
        }
        CharSequence charSequence=k;
        for (int i = 0; i < k.length(); i++) {
            String cs= String.valueOf(k.charAt(i));
            sj.add(cs);
        }
        k=sj.toString();
        return k;
    }
    public static double getAverage(double[] a){
        double sum=0;
        for (int i = 0; i < a.length; i++) {
            sum+=a[i];
        }
        return sum/a.length;
    }

}
```

```java
public class test {
    public static void main(String[] args) {
        int[] a = {1, 2, 3};
        System.out.println(ArrayUtil.printArr(a));
        double[] b = {1.0,2.0,3.0};
        System.out.println(ArrayUtil.getAverage(b));
    }
}
```

```java
public class Student {
    private String name;
    private int age;
    private String gender;

    public Student(String string, int age, String gender) {
        this.name = string;
        this.age = age;
        this.gender = gender;
    }

    public Student() {
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getGender() {
        return gender;
    }

    public void setGender(String gender) {
        this.gender = gender;
    }
}
```

```java
import java.util.ArrayList;

public class StudentTool {
    private StudentTool(){}
    public static int maxAge(ArrayList<Student> list){
        int max = list.get(0).getAge();
        for (int i = 0; i < list.size(); i++) {
            if(max<list.get(i).getAge()) max = list.get(i).getAge();
        }
        return max;
    }
}
```

```java
import java.util.ArrayList;

public class test {
    public static void main(String[] args) {
        ArrayList<Student> list = new ArrayList<>();

        Student s1 = new Student("LiHua",18,"男");
        Student s2 = new Student("小明",16,"男");
        Student s3 = new Student("小鹏",20,"男");
        list.add(s1);
        list.add(s2);
        list.add(s3);

        System.out.println(StudentTool.maxAge(list));
    }
}
```

#### static注意事项

- 静态方法只能访问静态变量和静态方法
- 非静态方法可以访问静态变量或者静态方法，也可以访问非静态的成员变量和非静态成员方法
- 静态方法中没有this关键字

总结：静态方法，只能访问静态。非静态方法可以访问所有，静态方法中没有this关键字

#### 重新认识main方法

- public：被JVM调用，访问权限足够大
- static：被JVM调用，不用直接创建对象，直接类名访问，因为main方法是静态的，所以测试类中其他方法也需要静态的
- void：被JVM调用，不需要给JVM返回值
- main：一个通用名称，虽然不是关键字，但是被JVM识别
- String[] args：用于接受键盘录入数据的现在没用

### 继承

#### 继承与继承的好处

- Java中提供一个关键字extends，用这个关键字，我们可以让一个类和另一个类建立起继承关系

    ```java
    public class student extends Person{}
    ```

- Student称为子类(派生类)，Person称为父类（基类或超类）

- 使用继承的好处：

    - 可以把多个子类中重复的代码抽取到父类，提高代码的复用性
    - 子类可以在父类的基础上，增加其他的功能，使子类更加强大

- 什么时候使用继承

- 当类与类之间，存在相同（共性）的内容，并满足子类是父类中的一种，就可以考虑使用继承来优化代码。

####  继承的特点

Java只支持单继承，一个类只能继承一个直接父类

java不支持多继承，但支持多层继承、

每一个类都直接或间接继承object类

子类只能访问父类中非私有成员

```java
public class Animal {
    public static void eat(){
        System.out.println("吃饭");
    }
    public static void drink(){
        System.out.println("喝水");
    }
}
```

```java
public class Cat extends Animal{
    public static void catchMouse(){
        System.out.println("抓老鼠");
    }
}
```

```java
public class Dog extends Animal{
    public static void watchHome(){
        System.out.println("看家");
    }
}
```

```java
public class BuOuCat extends Cat{
}
```

```java
public class ChinaLiHuaCat extends Cat{
}
```

```java
public class HaShiQi extends Dog{
    public static void Divorce(){
        System.out.println("拆家");
    }
}
```

```java
public class TaiDi extends Dog{
    public static void Rub(){
        System.out.println("蹭一蹭");
    }
}
```

#### 子类能继承父类中的那些内容

![image-20250608210011599](images/image-20250608210011599.png)

![image-20250608211249138](images/image-20250608211249138.png)

#### 继承中成员变量的访问特点

就近原则：谁离我近，我就用谁

现在局部位置找，本类成员位置找，父类成员位置找，逐级往上

变量：从局部位置往上找

this.变量：从本类成员位置开始往上找

super.变量：从父类成员位置开始往上找

#### 继承中成员方法的访问特点

##### 方法的重写

当父类的方法不能满足子类现在的需要，需要进行方法重写

书写格式

在继承体系中，子类出现了和父类一模一样的方法声明，我们就称子类这个方法是重写的方法

@Override重新注释

1. @Override是放在重写后的方法上，检验子类重写是语法是否正确
2. 加上注释后，如果有红色波浪线，表示语法错误
3. 建议重写方法都加@Override注解，代码安全，优雅！

如果发生了重写，则会覆盖原方法

方法重写注意事项和要求

1. 重写方法的名称、形参列表必须与父类保持一致
2. 子类重写父类方法时，访问权限子类必须大于等于父类（空着不写<protected<public）
3. 子类重写父类方法时，返回值类型子类必须小于等于父类
4. 建议：重写的方法尽量和父类保持一致
5. 只有被添加到虚方法表中的方法才能被重写

```java
public class Dog {
    public  void eat(){

    }
    public static void drink(){
        System.out.println("喝水");
    }
    public static void watchHome(){
        System.out.println("看家");
    }

}
```

```java
public class HaShiQi extends Dog {
    @Override
    public  void eat(){
        System.out.println("吃狗粮");
    }
    public static void Divorce(){
        System.out.println("拆家");
    }
}
```

```java
public class ShaPi extends Dog{
    @Override
    public void eat(){
        System.out.println("吃狗粮");
        System.out.println("吃骨头");
    }
}
```

```java
public class ZhongHuaTianYuanQuan {
    public void Eat(){
        System.out.println("吃剩饭");
    }
}
```

方法重写的本质

覆盖虚方法表中的方法

#### 继承中构造方法的特点

父类中的构造方法不会被子类继承

子类中所有的构造方法默认先访问父类中的无参构造，在执行自己

为什么

子类在初始化的时候，有可能会使用到父类中的数据，如果父类没有完成初始化，子类将无法使用父类的数据

子类初始化之前，一定要调回用父类的构造方法先完成父类数据空间的初始化

子类构造方法的第一行默认是：super(),不写也存在，且必须在第一行

如果想调用父类有参构造，必须手动写super进行调用

#### this，super使用总结

this：理解为一个变量，表示当前方法调用者的地址值 

super：父类的存储空间

| 关键字 | 访问成员变量                         | 访问成员方法                                | 访问构造方法                         |
| ------ | ------------------------------------ | ------------------------------------------- | ------------------------------------ |
| this   | this.成员变量<br />访问本类成员变量  | this.成员方法（...）<br />访问本类成员方法  | this（...）<br />访问本类构造方法    |
| super  | super.成员变量<br />访问父类成员变量 | super.成员方法（...）<br />访问父类成员方法 | super（...）<br />访问父类的构造方法 |

案例1：

```java
public class Employer {
    private String ID;
    private String Name;
    private int price;

    public void work(){

    }

    public static void eat(){
        System.out.println("吃饭");
    }

    public Employer() {
    }

    public Employer(String ID, String name, int price) {
        this.ID = ID;
        Name = name;
        this.price = price;
    }

    public String getID() {
        return ID;
    }

    public void setID(String ID) {
        this.ID = ID;
    }

    public String getName() {
        return Name;
    }

    public void setName(String name) {
        Name = name;
    }

    public int getPrice() {
        return price;
    }

    public void setPrice(int price) {
        this.price = price;
    }
}
```

```java
public class Manager extends Employer {
    private int manage_price;

    public Manager(String ID, String name, int price,int manage_price) {
        super(ID, name, price);
        manage_price=this.manage_price;
    }

    public Manager() {
    }

    public int getManage_price() {
        return manage_price;
    }

    public void setManage_price(int manage_price) {
        this.manage_price = manage_price;
    }

    @Override
    public void work(){
        System.out.println("管理其他人");
    }


}
```

```java
public class Chef extends Employer {
    public Chef() {
    }

    public Chef(String ID, String name, int price) {
        super(ID, name, price);
    }
    @Override
    public void work(){
        System.out.println("炒菜");
    }

}
```

```java
public class test {
    public static void main(String[] args) {
        Manager manager=new Manager ("1","k",1000,10000);
        Chef chef = new Chef("2","c",1000);

        manager.work();
        Manager.eat();

        chef.work();
        Chef.eat();

    }
}
```

案例2：

```java
public class Employee {
    private String ID;
    private String Name;
    public void work(){

    }

    public Employee() {
    }

    public Employee(String ID, String name) {
        this.ID = ID;
        Name = name;
    }

    public String getID() {
        return ID;
    }

    public void setID(String ID) {
        this.ID = ID;
    }

    public String getName() {
        return Name;
    }

    public void setName(String name) {
        Name = name;
    }

}
```

```java
public class Teacher extends Employee {
    public Teacher() {
    }

    public Teacher(String ID, String name) {
        super(ID, name);
    }
}
```

```java
public class AdminStaff extends Employee{
    public AdminStaff() {
    }

    public AdminStaff(String ID, String name) {
        super(ID, name);
    }
}
```

```java
public class Lecturer extends Teacher{
    public Lecturer() {
    }

    public Lecturer(String ID, String name) {
        super(ID, name);
    }
    @Override
    public void work(){
        System.out.println("讲课");
    }
}
```

```java
public class Tutor extends Teacher{
    public Tutor() {
    }

    public Tutor(String ID, String name) {
        super(ID, name);
    }

    @Override
    public void work(){
        System.out.println("帮助讲课");
    }
}
```

```java
public class Maintainer extends AdminStaff{
    public Maintainer() {
    }

    public Maintainer(String ID, String name) {
        super(ID, name);
    }
    @Override
    public void work(){
        System.out.println("维修");
    }
}
```

```java
public class Buyer extends AdminStaff{
    public Buyer() {
    }

    public Buyer(String ID, String name) {
        super(ID, name);
    }
    @Override
    public void work(){
        System.out.println("购买");
    }
}
```

### 多态

#### 认识多态

同类型的对象，表现处的不同形态

##### 表现形式

```java
父类类型 对象名称 = 子类对象;
```

##### 多态的前提

- 有继承关系
- 有父类引用指向子类对象
- 有方法重写

#### 多态调用成员的特点

变量调用：编译看左边，运行也看左边

方法调用：编译看左边，运行看右边

#### 多态的优势

- 在多态的形势下，右边对象可以实现解耦合，便于扩展和维护
- 定义一个方法的时候，使用父类型作为参数，可以接受所有子类对象，体现多态的拓展性与便利

#### 多态的弊端

不能调用子类的特有功能

原因：编译看左边，运行看右边

编译时检测父类中是否有这个方法，如果没有，直接报错

解决方案：变回子类型就可以了

细节：转换的时候不能瞎转，如果转成其他类的类型，就会报错

#### 综合练习

```java
public class Animal {
    private int year;
    private String color;

    public Animal(int year, String color) {
        this.year = year;
        this.color = color;
    }

    public Animal() {
    }

    public int getYear() {
        return year;
    }

    public void setYear(int year) {
        this.year = year;
    }

    public String getColor() {
        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }

    public void eat(String something){

    }

}
```

```java
public class Dog extends Animal{
    public Dog(int year, String color) {
        super(year, color);
    }

    public Dog() {
    }

    @Override
    public void eat(String something){
        System.out.println(super.getYear()+"岁的"+super.getColor()+"的狗两只前脚死死的抱住"+something+"猛吃");
    }
    public static void lookHome(){
        System.out.println("看家");
    }
}
```

```java
public class Cat extends Animal{
    public Cat(int year, String color) {
        super(year, color);
    }

    public Cat() {
    }

    @Override
    public void eat(String something){
        System.out.println(super.getYear()+"岁的"+super.getColor()+"的猫眯着眼睛侧着头吃"+something);
    }
    public static void catchMouse() {
        System.out.println("抓老鼠");
    }
}
```

```java
public class Person {
    private String name;
    private int year;

    public Person(String name, int year) {
        this.name = name;
        this.year = year;
    }

    public Person() {
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getYear() {
        return year;
    }

    public void setYear(int year) {
        this.year = year;
    }

    public  void keepPet(Animal animal, String something){
        if(animal instanceof Dog){
            animal = (Dog) animal;
            System.out.println("年龄为"+getYear()+"岁的"+getName()+"养了一只"+animal.getColor()+"的"+animal.getYear()+"岁的狗");
            animal.eat(something);
        }else{
            animal = (Cat) animal;
            System.out.println("年龄为"+getYear()+"岁的"+getName()+"养了一只"+animal.getColor()+"的"+animal.getYear()+"岁的猫");
            animal.eat(something);
        }
     }
}

```

```java
public class test {
    public static void main(String[] args) {
        Dog dog = new Dog(2,"黑");
        Cat cat = new Cat(3,"灰");
        Person person = new Person("老王",30);

        person.keepPet(dog,"骨头");
        person.keepPet(cat,"鱼");
    }
}
```

### 包、final、权限修饰符、代码块

#### 包

包就是文件夹。用来管理不同功能的Java类，方便后期维护管理

- 包名的规则：公司的域名反写+包的作用，需要全部英文小写，见名知意

```java
package com.yuanshenligong.类名
```

全类名，全限定名

使用其他类时，需要使用全域名

```java
import 域名.类名
```

使用其他类的规则

- 使用同一个包中的类时，不需要导包
- 使用java.lang包中的类时，不需要导包
- 其他情况都需要导包
- 如果同时使用两个包中的同名类，需要全类名

#### final

方法：表明该方法是最终方法，不能被重写

类：表明该类是最终类，不能被继承

变量：叫做常量，只能被赋值一次

##### 常量

实际开发中，常量一般作为系统的配置信息，方便维护，提高可读性

常量的命名规范：

- 单个单词：全部大写
- 多个单词：全部大写，单词之间用下滑线隔开

细节：

- final修饰的变量是基本类型：那么变量存储的数据值不能发生改变
- final修是的变量是引用类型：那么变量存储的地址值不能发生改变，对象内部的可以改变

#### 权限修饰符

- 权限修饰符：是用来控制一个成员能够被访问的范围的
- 可以修饰成员变量，方法构造方法，内部类

##### 权限修饰符的分类

有四种范围由小到大（private<空着不写（缺省/默认）<protected<public）

| 修饰符    | 同一个类中 | 同一个包中其他类 | 不同包下的子类 | 不同包下的无关类 |
| --------- | ---------- | ---------------- | -------------- | ---------------- |
| private   | √          |                  |                |                  |
| 空着不写  | √          | √                |                |                  |
| protected | √          | √                |                |                  |
| public    | √          | √                | √              | √                |

##### 权限修饰符的使用规则

实际开发中一般只用private和public 			

-  成员变量私有
- 方法公开

特例：如果方法中的代码时抽取其他方法中的共性代码，这个方法一般也私有

#### 代码块

局部代码块

提前结束变量的生命周期（已淘汰）

构造代码块

抽取构造方法中重复的代码（不够灵活）

静态代码块

数据初始化（重点）

格式：static{}

特点：通过通过static关键字，随着类的加载而加载，并且自动触发、只执行一次

### 抽象类

- 抽象方法：将共性的行为（方法）抽取到父类之后。由于每一个子类执行的内容是不一样，所以，在父类中不能确定具体的方法体，该方法就可以定义为抽象的方法

    ```java
    public abstract 返回值类型 方法名(参数列表);
    ```

- 抽象类：如果一个类中存在抽象的方法，那么该类就必须声明为抽象类

    ```java
    public abstract class 类名{}
    ```

    

##### 注意事项

- 抽象方法不能实例化
- 抽象类中不一定有抽象方法，有抽象方法的一定是抽象类
- 可以有构造方法
- 抽象类的子类
    - 要么重写抽象类中的抽象方法
    - 要么是抽象类

```java
public abstract class Animal {
    private String name;
    private int year;
    public abstract void eat();
    public  void drink(){
        System.out.println("喝水");
    };

    public Animal() {
    }

    public Animal(String name, int year) {
        this.name = name;
        this.year = year;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getYear() {
        return year;
    }

    public void setYear(int year) {
        this.year = year;
    }
}
```

```java
public interface swim {
    public abstract void swim ();

}
```

```java
public class Dog extends Animal implements swim{
    @Override
    public void eat() {
        System.out.println("吃骨头");
    }

    public Dog() {
    }

    public Dog(String name, int year) {
        super(name, year);
    }

    @Override
    public void swim() {
        System.out.println("蛙泳");
    }
}
```

```java
public class Frog extends Animal implements swim{
    @Override
    public void eat() {
        System.out.println("吃虫子");
    }

    public Frog() {
    }

    public Frog(String name, int year) {
        super(name, year);
    }

    @Override
    public void swim() {
        System.out.println("蛙泳");
    }
}
```

```java
public class Sheep extends Animal{
    @Override
    public void eat() {
        System.out.println("吃艹");
    }

    public Sheep() {
    }

    public Sheep(String name, int year) {
        super(name, year);
    }
}
```

```java
public class test {
    public static void main(String[] args) {
        Frog frog = new Frog("frog",1);
        Dog dog = new Dog("dog",2);
        Sheep sheep = new Sheep("sheep",3);

        frog.eat();
        frog.drink();
        frog.swim();
        dog.eat();
        dog.drink();
        dog.swim();
        sheep.eat();
        sheep.drink();
    }
}

```



### 接口

就是一种规则

#### 接口的定义和使用

- 接口使用关键字interface来定义

    ```java
    public interface 接口名{}
    ```

- 接口不能实例化

- 接口和类之间的实例关系，通过implements关键字表示

    ```java
    public class 类名 implements 接口名
    ```

- 接口的子类（实现类）
    要么重写接口中所有抽象方法
    要么是抽象类

注意1：接口和类的实现关系，就可以单实现，也可以多实现

```java
public class 类名 implements 接口名1，接口名2{}
```

注意2：实现类还可以在继承一个 类的同时实现多个接口

```java
public class 类名 extends 父类 implements 接口1，接口2{}
```

#### 接口中成员的特点

- 成员变量

    只能是常量

    默认修饰符：public static final

- 构造方法

    没有

- 成员方法

    只能是抽象方法

    默认修饰符：public abstract

JDK7以前：接口中只能定义抽象方法

#### 接口与类的关系

- 类和类的关系

    继承关系，只能单继承，不能多继承，但是可以多重继承

- 类和接口的关系

    实现关系，可以单实现，也可以多实现，还可以在继承一个类的同时多个接口

- 接口与接口的关系

    可以单继承也可以多继承

```java
public class SportMan {
    private String name;
    private int year;

    public SportMan() {
    }

    public SportMan(String name, int year) {
        this.name = name;
        this.year = year;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getYear() {
        return year;
    }

    public void setYear(int year) {
        this.year = year;
    }
}
```

```java
public interface SpeakEnglish {
    public abstract void speakEnglish();
}
```

```java
public interface Study {
    public abstract void study();
}
```

```java
public interface Teach {
    public abstract void teach();
}
```

```java
public class TennisCoach extends SportMan implements SpeakEnglish,Teach{

    public TennisCoach() {
    }

    public TennisCoach(String name, int year) {
        super(name, year);
    }

    @Override
    public void speakEnglish() {
        System.out.println("说英语");
    }

    @Override
    public void teach() {
        System.out.println("教打乒乓球");
    }
}
```

```java
public class TennisPlayer extends SportMan implements SpeakEnglish ,Study {
    public TennisPlayer() {
    }

    public TennisPlayer(String name, int year) {
        super(name, year);
    }

    @Override
    public void speakEnglish() {
        System.out.println("说英语");
    }

    @Override
    public void study() {
        System.out.println("打乒乓球");
    }
}
```

```java
public class BasketballCoach extends SportMan implements Teach{
    public BasketballCoach() {
    }

    public BasketballCoach(String name, int year) {
        super(name, year);
    }

    @Override
    public void teach() {
        System.out.println("教打篮球");
    }
}
```

```java
public class BasketballPlayer extends SportMan implements Study{
    public BasketballPlayer() {
    }

    public BasketballPlayer(String name, int year) {
        super(name, year);
    }

    @Override
    public void study() {
        System.out.println("打篮球");
    }
}
```

```java
public class test {
    public static void main(String[] args) {
        BasketballCoach basketballCoach= new BasketballCoach("li",10);
        BasketballPlayer basketballPlayer= new BasketballPlayer("zhao",12);
        TennisCoach tennisCoach = new TennisCoach("qian",14);
        TennisPlayer tennisPlayer = new TennisPlayer("sun",16);

        basketballCoach.teach();
        basketballPlayer.study();
        tennisPlayer.speakEnglish();
        tennisPlayer.study();
        tennisCoach.speakEnglish();
        tennisCoach.teach();
    }
}
```

#### 接口的新特性

##### JSK8新增的接口的新方法

###### JDK8

- JDK8中以后接口新增的方法，需要使用default修饰

作用：解决接口的升级的问题

接口中默认方法的定义格式：

- 格式：

    ```java
    public default 返回值类型 方法名(参数列表){}
    ```

接口中默认方法的注意事项：

- 默认方法不是抽象方法，所以不强制重写。但是如果被重写，重写的时候必须去掉default关键字
- public可以省略，default不可省略
- 如果实现了多个接口，多个接口中存在相同名字的默认方法，子类就必须对改方法进行重写

- 允许在接口中定义静态方法，需要用static修饰

接口中静态方法的定义格式：

- 格式：

    ```java
    public static 返回值类型 方法名(参数列表){}
    ```

接口的注意事项：

- 静态方法只能通过接口名调用，不能通过实现类名或者对象名调用
- public可以省略，static不能省略

##### JDK9

接口中私有方法的定义格式

格式1：

```java
private 返回值类型 方法名(参数列表){}
```

格式2：

```java
private static 返回值类型 方法名(参数列表){}
```

##### 接口的应用

1. 接口代表规则，是行为的抽象。想让哪个类拥有一个行为，就让这个类实现对应的接口就行了
2. 当一个方法的参数是一个接口的时候，可以传递接口所有实现类的对象，这种方式称之为接口的多态

##### 适配器设计模式

1. 当一个接口中抽象方法过多，但是我只要使用其中一部分的时候，就可以适配器模式
2. 书写步骤
    编写中间类XXXAdapter，实现对应接口
    让接口中的抽象方法进行空实现
    让真正的实现类继承中间类，并重写需要用的方法
    为避免其他类创建适配器类对象，中间的适配器类
    用abstract修饰

### 内部类

类的五大成员：

属性、方法、构造方法、代码块、内部类

在一个类里面，再定义一个类

内部类表示的事物是外部类的一部分

内部类的单独出现没有任何意义

内部类的访问特点：

- 内部类可以直接访问外部类的成员，包括私有
- 外部类要访问内部类的成员，必须创建对象

#### 成员内部类

##### 内部类的注意点

- 写在成员位置的，属于外部类的成员
- 成员内部类可以被一些修饰符所修饰，比如：private，默认，protected，public，static等
- 再内部类里面，JDK16之前不能定义静态变量，JDK16开始才可以定义静态变量

##### 获取成员内部类对象

方式1：

再外部类中编写方法，对外提供内部类的对象;

方式2：

直接创建格式：外部类名.内部类名 对象名=外部类对象.内部类对象;

##### 成员内部类获取外部类的对象

外部类成员变量和内部类重名时，内部类如何访问

#### 静态内部类

静态内部类只能访问外部类中静态变量和静态方法，如果想要访问非静态的需要创建对象

创建静态内部类对象的格式：

```java
外部类名.内部类名 对象名 = new 外部类名.内部类名();
```

调用静态方法的格式

```java
外部类.内部类名.方法名();
```

注意事项：

1. 静态内部类也是成员内部类的一种
2. 静态内部类只能访问外部类中静态变量和静态方法，如果要访问非静态的需要创建对象

创建静态内部类的对象，只要时静态的东西都可以用类名直接获取

#### 局部内部类

1. 将内部类定义再方法里面就叫做局部内部类，类似于方法里面的局部变量
2. 外界是无法直接使用局部内部类，需要在方法内部创建对象并使用
3. 该类可以直接访问外部类的成员，也可以访问方法内的局部变量

#### 匿名内部类

匿名内部类本质上是隐藏了名字的内部类，可以写在成员位置，也可以写在局部位置

```java
new 类名或接口名(){
	重写方法
};
```

##### 格式的细节

包含了继承或实现，方法重写，创建对象

整体就是一个类的子类对象或者接口的实现类对象

##### 使用场景

当方法的参数是接口或者类时，

以接口为例，可以传递这个接口的实现类对象，

如果实现类只要使用一次，就可以匿名内部类简化代码

### 拼图游戏

#### GUI

##### 组件

JFrame：最外面的窗体

JMenuBar：最上层的菜单

JLabel：管理文字和图片的容器

`Ctrl+Alt+M`快速抽取方法

#### 事件

事件时可以被组件识别的操作

当你对组件干了某件事情之后，就会执行对应的代码

- 事件源：按钮 图片 窗体
- 事件：某些操作
- 绑定监听：当事件源上发生了某个事件，则执行某段代码

KeyListener：键盘监听

MouseListener：鼠标监听

ActionListener：动作监听

监听一个按钮的单机事件：

- 动作监听
- 鼠标监听中的单击事件
- 鼠标监听中的松开事件

键盘监听机制-Key Listener

| 方法                      | 描述               |
| ------------------------- | ------------------ |
| keypressed（KeyEvent e）  | 按下键时调用       |
| keyReleased（KeyEvent e） | 当键已被释放时调用 |
| keyTyped（KeyEvent e）    | 键入键时调用       |

#### 美化界面

先加载的图片在上方，后加载的图片在下方

#### 上下左右移动

1. 本类实现keylistener接口，并重写所有抽象方法
2. 给整个界面添加键盘监听事件
3. 统计一下空白方块对应的数字0在二维数组中的位置
4. 在keyRealsed方法中实现移动的逻辑
5. Bug修复：
    1. 空白方块在最下方式，无法上移
    2. 空白方块在最上方式，无法下移、
    3. 空白方块在最左方式，无法右移
    4. 空白方块在最右方式，无法左移

#### 查看完整图片功能

a

#### 作弊码

w

#### 判断胜利

victory

#### 计步功能



#### 重新开始

#### 关闭游戏

#### 关于我们

## API

API（Application Programming Interface）:应用程序编程接口

简单理解：API就是别人已经写好的东西，我们不需要自己编写，直接使用即可

Java API：指的就是JDK中提供的各种功能的Java类，这些类将地产的实现封装起来，我们不需要关心这些类是如何实现的，只需要学习这些类如何使用即可

API帮助文档：帮助开发人员更好的使用API和查询API的一个工具

使用帮助文档：

1. 打开API帮助文档
2. 点击显示，并找到索引下面的输入
3. 在输入框中输入类名并点击显示
4. 查看类所在的包
5. 查看的类的描述
6. 查看构造方法
7. 查看成员方法

### Math

- 是一个帮助我们用于数学计算的工具类
- 私有化构造方法，所有方法都是静态的

#### 常用方法

| 方法名                                      | 说明                                  |
| ------------------------------------------- | ------------------------------------- |
| public static int abs(int a)                | 获取参数的绝对值                      |
| public static double celi(double a)         | 向上取整                              |
| public static double floor(double a)        | 向下取整                              |
| public static int round(float a)            | 四舍五入                              |
| public static int max(int a,int b)          | 求最大值                              |
| public static double pow(double a,double b) | 求a的b次幂的值                        |
| public static double random()               | 返回职位double的随机值，范围[0.0,1.0) |
| public static double cbrt(double a)         | 返回a的立方根                         |
| public static double sqrt(double a)         | 返回a的平方根                         |

### System

System也是一个工具类，提供了一些与系统相关的方法

| 方法名                                                       | 说明                         |
| ------------------------------------------------------------ | ---------------------------- |
| public static void (int status)<br />0是正常停止<br />1是异常停止 | 终止当前运行的Java虚拟机     |
| public static long currentTimeMillis()                       | 返回当前系统的时间的毫秒形式 |
| public static void arraycopy(数据源数组，起始索引，目的地数组，起始索引，拷贝个数) | 数组拷贝                     |

数据源，从拷贝的数据从那个数组而来

从数据源的第几个索引开始拷贝

目的地，我要把数据拷贝到哪一个数组中

目的地数组的索引

拷贝的个数

细节：

1. 如果数据源数组和目的地数组都是基本数据类型，那么两者的类型必须保持一致，否则会报错
2. 在拷贝是考虑数组的长度，如果超出范围也会报错
3. 如果数据源数组和目的地数组都是引用数据类型，那么子类型可以赋值给父类型

#### 计算机中的事件源点

1970年1月1日 00:00:00

### Runtime

 Runtime表示当前虚拟机的运行环境

| 方法名                               | 说明                                        |
| ------------------------------------ | ------------------------------------------- |
| public static Runtime getRuntime     | 当前系统的运行环境对象                      |
| public void exit(int status)         | 停止虚拟机                                  |
| public int availableProcessors()     | 获得CPU线程数                               |
| public long maxMemory()              | JVM能从系统中获取总内存大小（单位byte）     |
| public long toatalMemory()           | JVM已经从系统中获取的总内存大小（单位byte） |
| public long freeMemory()             | JVM剩余内存大小（单位byte）                 |
| public Process exec (String command) | 运行cmd命令                                 |

shutdown：关机

-s：默认一分钟后管家

-s -t指定事件：指定关机时间

-a 取消关机操作

-r 关机并重启

### Object和Objects

#### Object

Object是Java中的顶级父类，所有的类都直接或简接的继承于Object类

Object类中的方法可以被所有子类访问，所以我们要学习Object类和其中的方法

| 方法名                            | 说明                     |
| --------------------------------- | ------------------------ |
| public Object                     | 空参构造                 |
| public String toString            | 返回对象的字符串表示形式 |
| public boolean equals(Object obj) | 比较两个对象是否相等     |
| protected Object clone(int a)     | 对象克隆                 |

##### toString

System：类名

out：静态变量

System.out：获取打印的对象

println():方法

参数：表示打印的内容

当我们打印一个对象的时候，底层会调用对象toString方法，把对象变成字符串。

然后再打印在控制台上，打印完毕换行处理

toString方法的结论：

如果我们打印一个对象，想要看到属性值的话，那么就重写toString方法就可以了

在重写的方法中，把对象的属性值进行拼接

##### equals

1. 如果没有重写equals方法，那么默认使用Object中的方法进行比较，比较的是地址值是否相等
2. 一般来讲地址值对我们意义不大，所以我们会重写，重写之后比较的就是对象内部的属性值

##### clone

把A的对象的属性值完全拷贝给B对象，也叫对象拷贝，对象复制

Cloneable

如果一个接口里面没有抽象方法

表示当前的接口是一个标记性接口

现在Cloneable表示一旦了实现，那么当前类的对象就可以被克隆

如果没有实现，当前类的对象就不能克隆

克隆对象

默认浅克隆

细节：

方法在底层帮我们创建一个对象，并把原对象中的数据拷贝过去

书写细节：

1. 重写Object中的clone方法
2. 让javabean类是西安Cloneable接口
3. 创建原对象并调用clone就可以了

第三方工具

1. 第三方法写的代码导入到项目中

#### Objects

Objects是一个工具类，提供了一些方法去完成一些功能

| 方法名                                          | 说明                                     |
| ----------------------------------------------- | ---------------------------------------- |
| public static boolean equals(Object a,Object b) | 先做非空判断，比较两个对                 |
| public static boolean isNull(Object obj)        | 判断对象是否为null，为null返回true，反之 |
| public static boolean nonNull(Object obj)       | 判断对象是否为null，跟isNull的结果相反   |

1. 方法底层会判断是否为null，如果为null，直接返回false

2. 如果s1不为null，那么就利用s1再次调用equals方法

3. 此时s1是Student类型，所以最终还是会调用Student中的equals方法

    如果没有重写，比较地址值，如果重写了，就比较属性值

### BigInteger和BigDecimal 

#### BigInteger

在Java中，整数有四种类型：byte，short，int，long。

在底层战役字数：byte1个字节、short2个字节、int4个字节、long8个字节

| 方法名                                     | 说明                                     |
| ------------------------------------------ | ---------------------------------------- |
| public BigInteger(int num,Random rnd)      | 获取随机大整数，范围[0~2的num次方-1]     |
| public BigInteger(String val)              | 获取指定的大整数                         |
| public BigInteger(String val,int radix)    | 获取指定进制的大整数                     |
| public static BigInteger valueOf(long val) | 静态方法获取BigInteger的对象，内部有优化 |

1. 获取一个随机的大整数
2. 获取一个指定的大整数
    必须为整数，否则会报错
3. 获取指定进制的大整数
    1. 字符串中的数字必须为整数
    2. 字符串中的数字必须要跟进制吻合
4. 静态方法获取BigInteger的对象，内部有优化
    1. 能表示范围比较小，只能在long的取值范围，如果超出long的范围就不行了
    2. 在内部对常用的数字：-16~16进行了优化

对象一旦创建，内部记录的值不能发生改变	

BigInteger构造方法小结

1. 如果BigInteger表示的数字没有超出long的范围，可以用静态方法获取
2. 如果BigInteger表示的超出long的范围，可以用构造方法获取
3. 对象一旦创建，BigInteger内部记录大的值不能发生改变
4. 只要进行计算都会产生一个新的BigInteger对象

BigInteger

| 方法名                                                 | 说明                              |
| ------------------------------------------------------ | --------------------------------- |
| public BigInteger add(BigInteger val)                  | 加法                              |
| public BigInteger subtract(BigInteger val)             | 减法                              |
| public BigInteger multiply(BigInteger val)             | 乘法                              |
| public BigInteger divide(BigInteger val)               | 除法，获取商                      |
| public BigInteger[] divideAndRemainder(BigInteger val) | 除法，获取商和余数                |
| public boolean equals(Object x)                        | 比较是否相同                      |
| public BigInteger pow(int exponent)                    | 次幂                              |
| public BigInteger max/min(BigInteger val)              | 返回较大值/较小值                 |
| public int intvalue(BigInteger val)                    | 转为int类型整数，超出范围数据有误 |

##### BigInteger底层存储方式

1. 对于计算机而言，其实是没有数据类型的概念的
2. 数据类型是变成语言自己规定的

##### BigInteger存储上限

存储方式：[1,-2147483648,0]

数组中最多能存储的元素个数：21亿多

数组中每一位能表示的数字：42亿多

BigInteger能表示的最大数字为：42亿的21亿次方

#### BigDecimal

##### 计算机中的小数

| 类型   | 占用字节数 | 总bit位数 | 小数部分bit位数 |
| ------ | ---------- | --------- | --------------- |
| float  | 4个字节    | 32个bit位 | 23个bit位       |
| double | 8个字节    | 64个bit位 | 52个bit位       |

```java
BigDecimal bd1 = new BigDecimal("较大的小数");
BigDecimal bd2 = BigDecimal.valueof(0.1);
```

细节：

1. 如果要表示的数字不大，没有超过double的取值范围，建议使用静态方法
2. 如果要表示的数字比较大，超过了double的取值范围，建议使用构造方法
3. 如果我们传递的是0~10之间的整数，半酣0和10，那么方法会返回已经那个创建号的对象，不会重新new

##### BigDecimal的使用

| 方法名                                                      | 作用 |
| ----------------------------------------------------------- | ---- |
| public BigDecimal add(BigDecimal val)                       | 加法 |
| public BigDecimal subtract(BigDecimal val)                  | 减法 |
| public BigDecimal multiply(BigDecimal val)                  | 乘法 |
| public BigDecimal divide(BigDecimal val)                    | 除法 |
| public BigDecimal divide(BigDecimal val,精确几位，舍入模式) | 除法 |

四舍五入：RoundingMode.HALF_UP

##### BigDecima底层存储方式



### 正则表达式

#### 正则基础

正则表达式可以校验字符串是否满足一定的规则，并且检验数据格式的合法性

在一段文本中查找满足一定要求的内容

字符类（只匹配一个字符）

| 类             | 作用                                   |
| -------------- | -------------------------------------- |
| [abc]          | 只能是a,b,c                            |
| [^abc]         | 除了a，b，c之外的任何字符              |
| [a-zA-Z]       | a到z，A到Z，包括（范围）               |
| [a-d[m-p]]     | a到d，或m到p                           |
| [a-z&&[def]]   | a-z和def的交集，为：d、e、f            |
| [a-z&&\[^bc]]  | a-z和非bc的交集（等同与[ad-z]）        |
| [a-z&&\[^m-p]] | a到z和除了m到p的交集（等同于[a-lq-z]） |

预定义字符

| 类   | 作用                           |
| ---- | ------------------------------ |
| .    | 任何字符                       |
| \d   | 一个数字：[0-9]                |
| \D   | 非数字：\[^0-9]                |
| \s   | 一个空白字符:[\t\n\x0B\f\r]    |
| \S   | 非空白字符：\[^\s]             |
| \w   | [a-zA-Z_0-9]英文、数字、下划线 |
| \W   | \[^\w]一个非单词字符           |

```java
public boolean matches(String regex)
```

判断是否与正则表达式匹配，匹配则返回true

如果要写两个之间的交集需要两个&

\表示转义字符，改变后面那个字符原本的含义

数量词

| 类     | 作用               |
| ------ | ------------------ |
| X?     | X,一次或0次        |
| X*     | X,零次或多次       |
| X+     | X,一次或多次       |
| X{n}   | X,正好n次          |
| X{n,}  | X,至少n次          |
| X{n,m} | X,至少n但不超过m次 |

(?i)忽略数据的大小写

((?i)x)只忽略指定字母的大小写

|写在方括号外面表示并集

#### 爬虫

Pattern：表示正则表达式

```java
Pattern p = Pattern.compile("");
```

Matcher：文本匹配器，作用按照正则表达式规则去读取字符串，从头开始读取。在大串中去找符号匹配规则的字符串

```java
Matcher m = p.matcher(str);
boolean b = m.find();
```

拿着文本匹配器从头开始读取，寻找是否满足规则的子串

如果没有，方法返回false

如果有，返回true，在底层记录子串的其实索引和结束索引+1

？代表前面的数据，=java后面跟随的数据

只写+和*表示贪婪匹配

+? 非贪婪匹配

*? 非贪婪匹配

贪婪爬取：在爬取时尽可能多的获取数据

非贪婪爬取：在爬取数据的时候尽可能少的获取数据

Java默认的是贪婪爬取

| 方法                                                 | 作用                               |
| ---------------------------------------------------- | ---------------------------------- |
| public String[] matches(String regex)                | 判断字符串是否满足正则表达式的规则 |
| public String replaceAll(String regex,String newStr) | 按照正则表达式的规则进行替换       |
| public String[] split (String regex)                 | 按照正则表达式进行切割字符串       |

#### 分组

分组就是一个小括号

捕获分组：

可以获取组中的数据反复使用

每组是有组号的，也就是序号

规则1：从1开始，连续不间断

规则2：以左括号为基准，最左边的是第一组，其次为第二组，以此类推

非捕获分组

\\\组号表示把第X组内容再出来用一次

正则内部使用：\\\组号

正则外部使用：$组号

非捕获分组

不占用组号

| 符号     | 含义                       | 举例              |
| -------- | -------------------------- | ----------------- |
| (?:正则) | 获取所有                   | Java(?:8\|11\|17) |
| (?=正则) | 获取前面的部分             | Java(?=8\|11\|17) |
| (?!正则) | 获取不是指定内容的前面部分 | Java(?!8\|11\|17) |

### JDK7以前时间相关类

#### Date

全世界的时间有一个统一的计算标准

格林尼治时间简称GMT

计算核心：地球自转一天是24个小时，太阳直射时为正午12点

原子钟：利用铯原子的震动频率计算出来的时间，作为世界标准时间（UTC）

中国标准时间=十九届标准时间+8小时

Data类是JDK写好的一个JavaBean类，用来描述时间，精确到毫秒

利用空参构造创建的对象，默认表示系统当前时间

利用有参构造创建的对象，表示指定的时间

创建对象

| 方法                   | 作用                       |
| ---------------------- | -------------------------- |
| public Date()          | 创建Date对象，表示当前时间 |
| public Date(long date) | 创建Date对象，表示指定时间 |

调用方法

| 方法                           | 作用                 |
| ------------------------------ | -------------------- |
| public void setTime(long time) | 设置/修改毫秒值      |
| public long getTime()          | 获取时间对象的毫秒值 |

#### SimpleDateFormat

- 格式化：把时间变成我们喜欢的格式
- 解析：把字符串表示的时间变成Date对象

| 构造方法                                | 说明                                  |
| --------------------------------------- | ------------------------------------- |
| public SimpleDateFormat()               | 构造一个SimpleDateFormat,使用默认格式 |
| public SimpleDateFormat(String Pattern) | 构造一个SimpleDateFormat,使用指定格式 |

| 常用方法                              | 说明                         |
| ------------------------------------- | ---------------------------- |
| public final String format(Date date) | 格式化（日期对象 -> 字符串） |
| public Date parse(String source)      | 解析(字符串 ->日期对象)      |



#### Calendar

- Calendar代表了系统当前时间的日历对象，可以单独修改、获取时间中的年、月、日
- 细节：Calendar是一个抽象类，不能直接创建对象

获取calendar日历类对象的方法

| 方法名                               | 说明                   |
| ------------------------------------ | ---------------------- |
| public static Calendar getInstance() | 获取当前时间的日历对象 |

Calendar常用方法

| 方法名                                   | 说明                        |
| ---------------------------------------- | --------------------------- |
| public final Date getTime()              | 获取日期对象                |
| public final setTime(Date date)          | 给日历设置日期对象          |
| public long getTimeInMillis()            | 拿到时间毫秒值              |
| public void setTimeInMillis(long millis) | 给日历设置时间毫秒值        |
| public int get(int field)                | 去日历中的某个字段信息      |
| public void set(int field,int value)     | 修改日历中的某个字段信息    |
| public void add(int field,int amount)    | 为某个字段增减/减少指定的值 |

### JDK8新增的时间相关类

好处：

代码层面：

简单

判断的方法

计算时间间隔的方法

安全层面：

时间日期对象都是不可变的，解决了这个问题

#### Data类

##### Zoneld时区

| 方法名                                    | 说明                   |
| ----------------------------------------- | ---------------------- |
| static Set\<String> getAvailableZoneIds() | 获取Java支持的所有时区 |
| static ZoneId systemDefault()             | 获取系统默认时区       |
| static ZoneId of (String zoneId)          | 获取一个指定时区       |

##### Instant

| 方法名                                  | 说明                                |
| --------------------------------------- | ----------------------------------- |
| static Instant now()                    | 获取当前时间的Instant对象(标准时间) |
| static Instant ofxxx(long epochMilli)   | 根据（秒/毫秒/纳秒）获取Instant对象 |
| ZonedDateTime atZone(ZoneId zone)       | 指定时区                            |
| boolean isXXX(Instant otherInstant)     | 判断系列方法                        |
| Instant minusXxx(long millisToSubtract) | 减少时间系列方法                    |
| Instant plusXxx(long millisToSubtract)  | 增加时间系列方法                    |

##### ZoneDateTime带时区的时间

| 方法名                      | 说明                           |
| --------------------------- | ------------------------------ |
| static ZoneDateTime now()   | 获取当前时间的ZoneDateTime对象 |
| staic ZoneDateTime ofxxx()  | 获取指定时间的ZoneDateTime对象 |
| ZoneDateTime withxxx(时间)  | 修改时间的系列方法             |
| ZoneDateTime minusXxx(时间) | 减少时间的系列方法             |
| ZoneDateTime plusXxx(时间)  | 增加时间的系列方法             |

#### SimpleDateFormat类

##### DateTimeFormatter用于时间的格式化与解析

| 方法名                                   | 说明               |
| ---------------------------------------- | ------------------ |
| static DateTimeFormatter ofPattern(格式) | 获取格式对象       |
| String format(时间对象)                  | 按照指定方式格式化 |

#### Calendar类

##### localDate、localTime、localDateTime

| 方法名             | 说明                                     |
| ------------------ | ---------------------------------------- |
| static XXX now()   | 获取当前时间的对象                       |
| static XXX of(...) | 获取指定时间的对象                       |
| get                | 获取日历中的年、月、日、时、分、秒等信息 |
| isBefore,isAfter   | 比较两个LocalDate                        |
| with开头的         | 修改时间系列的方法                       |
| minus开头的        | 减少时间系列的方法                       |
| plus开头的         | 增加时间系列的方法                       |

#### 工具类

##### Duration、period、ChronoUnit

Duration

计算两个时间间隔（秒，纳秒）

Period

用于计算两个日期的间隔（年、月、日）

ChronoUnit

用于计算两个日期间隔

### 包装类

基本数据类型对应的引用数据类型

#### Integer

##### 获取Integer对象

| 方法名                                            | 说明                                      |
| ------------------------------------------------- | ----------------------------------------- |
| public Integer(int value)                         | 根据传递的整数创建一个integer对象         |
| public Integer(String s)                          | 根据传递的字符串创建一个Integer对象       |
| public static Integer valueOf(int i)              | 根据传递的整数创建一个Integer对象         |
| public static Integer valueof(String s)           | 根据传递的字符串创建一个Integer对象       |
| public static Integer valueOf(String s,int radix) | 根据传递的字符串和进制创建一个Integer对象 |

在JDK5的时候提出一个机制：自动装箱和自动拆箱

自动装箱：把基本数据类型会自动变成对应的包装类

自动拆箱：把包装类自动变成其对象的基本数据类型

不需要new，不需要调用方法，直接赋值即可

##### 成员方法

| 方法名                                     | 说明                                |
| ------------------------------------------ | ----------------------------------- |
| public static String toBinaryString(int i) | 得到二进制                          |
| public static String toOctalString(int i)  | 得到八进制                          |
| public static String toHexString(int i)    | 得到十六进制                        |
| public static int parselent(String s)      | 将字符串类型的整数转成int类型的整数 |

强类型语言：每种数据在Java中都有各自的数据类型

在计算的时候，如果不是同一种数据类型，是无法直接计算的

在类型转换的时候，括号中的参数只能是数字不能是其他，否则代码会报错

8种包装类当中，除了Character都有对应的parseXxx方法，进行类型转换

### 综合练习

## 常见的算法和lambda表达式

### 常见算法

#### 查找算法

##### 基本查找

从0索引开始挨个往后查找，查询某个元素是否存在

参数：数组，查找元素

返回值：元素是否存在

二分查找/折半查找

如果返回多个数据，把数据放入集合或数组中

##### 二分查找/折半查找

前提条件：数组中的数据必须是有序的

如果数据是乱的，线排序再用二分查找得到的索引没有实际意义，只能确定当前数字在数组中是否存在，因为排序之后的数字的位置可能就要发生变化了

核心逻辑：每次排除一半的查找范围

1. min和max表示当前要查找的范围
2. mid是在min和max之间的
3. 如果要查找的元素在mid的左边，缩小范围时，min不变，max等于mid减1
4. 如果要查找的元素在mid的右边，缩小范围时，max不变，min等于mid加1

##### 插值查找

二分查找的改进型

mid尽量靠近要查找的数据，但是要求数据尽可能的分布均匀

要求数据有序且分布均匀

mid=min+((key-arr[min])/(arr[max]-arr[min]))*(max-min)

##### 斐波那契查找

根据黄金分割点来计算mid指向的位置

1：0.618

mid = min + 黄金分割点左半边长度-1

##### 分块查找

分块的原则1：前一块中的最大数据，小于后一块中所有数据（块内无序，块间有序）

分块的原则2：块数数量一般等于数字的个数开根号。比如：16个数字一般分为4块

核心思路：先确定要查找的元素在哪一块，然后在块内挨个查找

块

```java
class Block{//块
    int max;	//块中的最大值
    int startIndex;	//起始索引
    int endIndex;	//结束索引
}
```

核心思想：

块内无序，块间有序

实现步骤：

1. 创建数组blockArr存储每一块对象的细腻些
2. 先查找blockArr确定数据属于那一块
3. 在单独遍历这一块数据即可

拓展

```java
class Block{
    int min;
    int max;
    int startIndex;
    int endIndex;
}
```

##### 树表查找

##### 哈希查找

#### 排序算法

##### 冒泡排序

相邻的数据两两比较，小的放前面，大的放后面

1. 相邻的元素两两我比较，大的放右边，小的放左边
2. 第一轮循环结束，最大值已经找到，在数组的最右边
3. 第二轮循环只要在剩余元素找最大值就可以了
4. 第二轮循环结束，次大值已经确定，第三轮循环继续在剩余数据中循环

1. 相邻的元素两两比较，大的放右边，小的放左边
2. 第一轮比较完毕后，最大值就已经确定，第二轮可以少循环一次，后面一次类推
3. 如果数组中有n个数据，总共我们只要执行n-1轮代码就可以

`shift+F6`选中重命名

##### 选择排序

从0索引开始，拿着每一个索引上的元素跟后面的元素进行比较，小的放前面，大的放后面，以此类推

1. 从0索引开始，跟后面的元素一一比较
2. 小的放前面，大的放后面
3. 第一轮循环结束后，最小的数据已经确定
4. 第二轮循环从1索引开始以此类推
5. 第三轮循环从2索引开始以此类推

##### 插入排序

插入排序：将0索引对策元素到N搜因的元素看作是有序的，把N+1搜因的元素到最后一个当成是无序的，遍历无序的数据，将遍历的元素插入有序序列中适当的位置，如遇相同数据，插在后面

N的范围：0~最大索引

##### 快速排序

###### 递归算法

递归指的是方法中调用方法本身的现象

把一个复杂的问题层层转化为一个与原问题相似的规模较小的问题来求解

递归策略只需少量程序就可描述出接替过程需要的多次重复计算

书写递归的两个核心：

- 找出口：什么时候不在调用方法
- 找规则：如何把大问题变成规模较小的问题

###### 快速排序

第一轮：把0索引的数字作为基准数，确定基准数在数组中正确的位置。比基准数小的全部在左边，比基准数的全部在右边

- 将排序范围范围中的第一个数字作为基准数，在定义两个变量start，end
- start从前往后找比基准数大的，end从后往前找比基准数小的
- 找到之后交换start和end指向的元素，并循环这一过程，直到start和end处于同一个位置，改位置是基准数在数组中应存入的位置，在让基准数归位
- 归为后的效果，基准数左边的，比基准数小，基准数右边的，比基准数大

##### 希尔排序

##### 归并排序

##### 堆排序

##### 计数排序

##### 桶排序

##### 基数排序

### Arrays

操作数组的工具类

| 方法名                                                      | 说明                     |
| ----------------------------------------------------------- | ------------------------ |
| public static String toString(数组)                         | 把数组拼接成一个字符串   |
| public static int binarySearch(数组，查找的元素)            | 二分查找法查找元素       |
| public static int[] copyOf(原数组，新数组的长度)            | 拷贝数组                 |
| public static int[] copyOfRange(原数组，起始索引，结束索引) | 拷贝数组（指定范围）     |
| public static void fill(数组，元素)                         | 填充数组                 |
| public static void sort(数组)                               | 按照默认方式进行数组排序 |
| public static void sort(数组，排序规则)                     | 按照指定的规则排序       |

二分查找

细节1：二分查找的前提:数组中的元素必须是有序，数组中的元素必须是升序的

细节2：如果要查找的元素是存在的，那么返回的是真实的索引

但是：如果要查找的元素是不存在的，返回的是 -插入点-1

如果查找的是0就会造成疏解

copyof：拷贝数组

参数1：老数组

参数2：新数组的长度

方法的底层会根据第二个参数来创建新的数组

如果新数组的长度是小于老数组的长度，会部分拷贝

如果新数组的长度是等于老数组的长度，会完全拷贝

如果新数组的长度是大于老数组的长度，会补上默认初始值

copyOfRange：拷贝数组（指定范围）

包头不包尾，包左不包右

sort，在默认情况下，给基本数据类型进行升序排列，底层使用的是快速排序

参数1：要排序的数组

参数2：排序的规则

细节：

只能是引用数据类型的数组进行排序

如果数组是基本数据类型的额，需要变成对于的包装类

底层原理：

利用插入排序+二分查找方式进行排序的

默认把0索引的数据当做是有序的序列，1索引到最后认为是无序的序列

遍历无序的序列得到里面的每一个元素，假设当前遍历得到的元素是A元素

把A网有序序列中进行插入，在插入的时候，是利用二分查找确定A元素的插入点

拿着A元素，跟插入点的元素进行比较，比较的规则就是compare方法的方法体

如果方法的返回值是负数，拿着A和前面的数据继续比较

如果方法的返回值是正数，拿着A和后面的数据继续比较

如果方法的返回值是0，拿着A和后面的数据继续比较

直到确定A的最终位置位置

compare方法的形式参数：

参数1 o1：表示在无序序列中，遍历得到每一个元素

参数2 o2：有序序列中的元素

返回值：

负数：表示当前要插入的元素是小的，放在前面

正数：表示当前要插入的元素是大的，放在后面

0：表示当前要插入的元素跟现在的元素比一样的也会放在后面

### Lambda表达

#### 函数式编程

函数式编程是一种思想特点

面向对象：先找对象，让对象做事情

函数是编程忽略面向对象的复杂语法，强调做什么，而不是谁去做

lambda表达式是JDK8开始后的一种新语法形式

```java
()->{
    
}
```

- （）对于着方法的形参
- ->固定格式

注意点：

- lambda表达式可以用来简化匿名内部类的书写

- lambda表达式只能简化函数式接口的匿名内部类的书写

- 函数式接口：

    有且仅有一个抽象方法的接口叫做函数式接口，接口上方可以加@FunctionalInterface

1. 利用匿名内部类的形式去调用以下方法

    调用一个方法的时候，如果方法的形参只是一个接口，那么我们要传递这个接口的实现类对象

    如果实现类对象只用用到以此，就可以用匿名内部类的形式进行书写

2. 利用lambda表达式进行改写

lambda是一个匿名函数，我们可以把lambda表达式理解尾是一段可以传递的代码，它可以写出更简洁，更灵活的代码，作为一种更紧凑的代码风格，是java语言的表达能力得到了提升

lambda的省略规则

省略核心：可推导，可省略

1. 参数类型可以省略不写
2. 如果只有一个参数，参数类型可以省略，同时()也可以省略
3. 如果lambda表达式的方法体只有一行，大括号，分号，return都可以省略不写需要同时省略

### 综合练习

#### 女朋友排序

```java
public class GirlFriend {
    private String name;
    private int year;
    private int height;

    public GirlFriend() {
    }

    public GirlFriend(String name, int year, int height) {
        this.name = name;
        this.year = year;
        this.height = height;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getYear() {
        return year;
    }

    public void setYear(int year) {
        this.year = year;
    }

    public int getHeight() {
        return height;
    }

    public void setHeight(int height) {
        this.height = height;
    }
}
```

```java
import java.util.Arrays;

public class main {
    public static void main(String[] args) {
        GirlFriend g1 =new GirlFriend("li",18,160);
        GirlFriend g2 =new GirlFriend("hi",19,190);
        GirlFriend g3 =new GirlFriend("zi",20,180);

        GirlFriend[] girlFriends= {g1,g2,g3};
        Arrays.sort(girlFriends,(o1, o2) -> o1.getHeight()- o2.getHeight());
        for (int i = 0; i < girlFriends.length; i++) {
            System.out.println(girlFriends[i].getName());
        }
    }

}
```

#### 斐波那契数列

```java
public class Main {
    public static void main(String[] args) {
        System.out.println(rabbits(3));
    }
    public static int rabbits(int num){
        if(num==1||num==2) return 1;
        else return rabbits(num-1)+rabbits(num-2);
    }
}
```

#### 猴子吃桃

```java
public class peach {
    public static void main(String[] args) {
        System.out.println(monkey(1));
    }

    public static int monkey(int day){
        if(day==10) return 1;
        else return monkey(day+1)*2;
    }
}
```

#### 爬楼梯

```java
class Solution {
    public int climbStairs(int n) {
        int[] dp = new int[46];
        dp[0]=1;
        dp[1]=1;
        for(int i = 2 ;i<dp.length;i++)
        {
            dp[i]=dp[i-1]+dp[i-2];
        }
        return dp[n];
    }
}
```

## 集合进阶

### 集合体系结构

![image-20250618221938476](images/image-20250618221938476.png)

List系列集合：添加的元素是有序、可重复、有索引

Set系列即可：添加的元素是无序、不重复、无索引

### Collection集合

Collection是单列集合的祖宗集合，它的功能是全部单列集合都可以继承使用的

| 方法名称                            | 说明                             |
| ----------------------------------- | -------------------------------- |
| public boolean add(E e)             | 把给定的元素添加到当前集合当中   |
| public void clear()                 | 清空集合中所有的元素             |
| public boolean remove(E e)          | 把给定的对象在当前集合中删除     |
| public boolean contains(Object obj) | 判断当前集合中是否包含给定的对象 |
| public boolean isEmpty()            | 判断当前对象是否为空             |
| public int size()                   | 返回集合中元素的个数/集合的长度  |

Collection是一个接口，我们不能直接创建他的对象

所以我们学习他的方法是，只能创建它实现类的对象

1. 添加元素

    细节1:如果我们要往List系列集合中添加数据，那么方法永远返回true，因为list系类是允许重复的

    细节2:如果我们要往Set系列集合中添加数据，如果当前要添加元素不存在，方法返回true，表示添加成功，如果当前添加的元素已经存在，方法返回false，表示添加失败

2. 清空

3. 删除

    细节1：因为Collection里面定义的是共性的方法，所以此时不能通过索引进行删除，只能通过元素的对象进行删除。

    细节2：方法会有一个布尔类型的返回值，删除成功返回true，删除失败返回false

    如果要删除的元素不存在就会删除失败

4. 判断元素是否包含
    底层依赖equals方法进行判断是否存在的
    集合存储的是自定义对象，也想通过contains方法来判断是否包含，那么在JavaBean类中，一定要重写equals方法

5. 判断集合是否为空

6. 获取集合的长度

#### Collection的遍历方式

##### 迭代器遍历

迭代器不依赖索引

迭代器在Java中的类是Iterator，迭代器是集合专用的遍历方式

Collection集合获取迭代器

| 方法名                  | 说明                                            |
| ----------------------- | ----------------------------------------------- |
| Iterator\<E> iterator() | 判断当前位置是否有元素，默认指向当前集合的0索引 |

Iterator中的常用方法

| 方法名            | 说明                                                      |
| ----------------- | --------------------------------------------------------- |
| boolean hasNext() | 判断当前位置是否有元素，有元素返回true，没有元素返回false |
| E next()          | 获取当前位置的元素，并将迭代器对象一项下一个位置          |

创建指针

判断是否有元素

获取元素 移动指针

1. 创建集合并添加元素
2. 获取迭代器元素
3. 利用循环不断的去获取集合中的每一个元素
4. next方法的两件事情：获取元素并移动指针

细节注意点：

1. 报错NoSuchElementExeception
2. 迭代器遍历完毕，指针不会复位
3. 循环中只能用一次next方法
4. 迭代器遍历的时，不能用集合的方法进行增加或者删除
    可以使用迭代器提供的remove方法进行删除

##### 增强for遍历

- 增强for的底层逻辑就是迭代器，为了简化迭代器的代码书写的
- 它是JDK5之后出现的，其内部原理就是一个Iterator迭代器
- 所有单列集合和数组才能用增强for进行遍历

```java
for(元素的数据类型 变量名:数组或者集合){
}
```

1. 创建集合并添加元素
2. 利用增强for进行遍历

注意点

s起始就是一个第三方变量，循环的过程中依次表示表示集合中的每一个数据

快速生成方式

集合的名字+for 回车

增强for的细节

- 修改增强for中的变量，不会改变集合中原本的数据

##### Lambda表达式遍历

得益于JDK8开始的新技术Lambda表达式，提供了一种更简单，更直接的集合遍历集合的方式

| 方法名称                                           | 说明               |
| -------------------------------------------------- | ------------------ |
| default void forEach (Consumer<? super T> action): | 结合lambda遍历集合 |

1. 闯进集合并添加元素
2. 利用匿名内部类的形式
    底层原理：
    起始也会自己遍历集合，依次得到每个元素
    把得到的每一个元素，传递给下面的accept方法
    s依次表示集合中的每一个数据

### List集合

- 有序：存和取的元素顺序一致
- 有索引：可以通过索引操作元素
- 可重复：存储的元素可以重复

#### List集合的特有方法

- Collection的方法List都继承了
- List集合因为有索引，所以多了很多索引操作的方法

| 方法名称                      | 说明                                   |
| ----------------------------- | -------------------------------------- |
| void add(int index,E element) | 在此集合中的指定位置插入指定元素       |
| E remove(int index)           | 删除指定索引处的元素，返回被删除的元素 |
| E set(int index,E element)    | 修改指定索引处的元素，返回被修改的元素 |
| E get(int index)              | 返回指定索引处的元素                   |

add

细节：原来的元素会依次往后移

remove

List系列集合中的两个删除的方法

1. 直接删除元素
2. 通过索引进行删除

调用方法的时候，如果方法进行了重载现象

优先调用，实参跟形参类型一致的那个方法

#### List集合的遍历方式

1. Iterator迭代器

2. 增强for循环

3. lambda表达式

4. 普通for循环

5. 列表迭代器

    获取一个列表迭代器的对象，里面的指针也是默认指向0索引的
    在遍历的时候，可以添加元素

对比

| 方式         | 场景                                         |
| ------------ | -------------------------------------------- |
| 迭代器遍历   | 在遍历过程中需要删除元素，请使用迭代器       |
| 列表迭代器   | 在遍历的过程中需要添加元素，请使用列表迭代器 |
| 增强for遍历  | 仅仅想遍历，那么使用增强for或Lambda表达式    |
| Lambda表达式 | 仅仅想遍历，那么使用增强for或Lambda表达式    |
| 普通for      | 如果遍历的时候想操作索引，可以使用普通for    |

### 数据结构（线性表）

计算机存储、组织数据的方式

是指数据相互之间是以什么方式排列在一起的

数据结构是为了更加方便的管理和使用数据，需要结合具体的业务场景来进行选择

一般情况下，精心选择的数据结构可以带来更高的运送或存储效率‘

#### 栈

栈的特点：后进先出，先进后出

![image-20250619210611046](images/image-20250619210611046.png)

数据进入栈模型的过程称为：压/进栈

数据离开栈模型的过程称为：弹/出栈

![image-20250619210720034](images/image-20250619210720034.png)

#### 队列

队列的特点：先进先出，后进后出

![image-20250619211023040](images/image-20250619211023040.png)

数据从后端进入队列的模型的过程称为：入队列

数据从前端离开队列的模型的过程称为：出队列

#### 数组

![image-20250619211243800](images/image-20250619211243800.png)

数组是一种查询快，增删慢的模型

- 查询速度快：查询数据通过地址值和索引定位，查询任意数据耗时相同。（元素在内存中是连续存储的）
- 删除效率低：要将原始数据删除，同时将每个数据前移
- 添加效率极低：添加位置后的每个数据后移，在添加元素

数组：内存连续区域，查询快，增删慢

#### 链表

链表中的结点时独立的对象，在内存中时不连续的，每个结点包含数据值和下一个结点的地址

链表查询满，无论查询那个数据都要从头开始找

链表增删相对较快

链表：元素是游离的，查询慢，首尾操作极快

![image-20250619211621883](images/image-20250619211621883.png)

![image-20250619211807898](images/image-20250619211807898.png)

![image-20250619212138422](images/image-20250619212138422.png)

### ArrayList集合

#### ArrayList集合底层原理

1. 利用空参创建集合，底层创建一个默认长度为0的数组
2. 添加第一个元素时，底层会创建一个长度为10的数组
3. 存满时，会扩容1.5倍
4. 如果一次添加多个元素，1.5倍还放不下，则新创建数组的长度一实际为准

`Alt + 7`罗列方法

10以内

![image-20250619214805939](images/image-20250619214805939.png)

扩容

![image-20250619214705858](images/image-20250619214705858.png)

### LinkedList集合

- 底层数据结构是双链表，查询慢，增删快，但是如果操作的是首尾元素，速度是极快的

底层数据结构是双链表，查询慢，增删快，所以多了很多首位操作的API

| 特有方法                  | 说明                             |
| ------------------------- | -------------------------------- |
| public void addFirst(E e) | 在该列表开头插入指定的元素       |
| public void addLast(E e)  | 将指定元素追加到此列表的末尾     |
| public E getFirst()       | 返回此列表中的第一个元素         |
| public E getLast()        | 返回此列表中的最后一个元素       |
| public E removeFirst()    | 从此列表中删除并返回第一个元素   |
| public E removeLast()     | 从此列表中删除并返回最后一个元素 |

#### LinkedList的底层实现原理

![image-20250619220449427](images/image-20250619220449427.png)

#### 迭代器的底层实现原理

![image-20250619221232925](images/image-20250619221232925.png)

### 泛型深入

泛型：是JDK5中引入的特性，可以在编译阶段约束操作的数据类型，并进行检查

泛型的格式：<数据类型>

注意：泛型只能支持引用数据类型

如果我们没有给集合指定类型，默认所有数据类型都是Object类型，此时可以往集合添加任意数据类型，带来一个坏处：我们获取数据的时候，无法使用他的特有行为

这时候添加了泛型，可以在添加数据的时候就把类型进行统一

泛型的好处

- 统一数据类型
- 把运行时期的问题提前到了编译期间，避免强制类型转换可能出现的异常，因为在编译阶段就能确定下来

拓展知识点：Java中的泛型是伪泛型

泛型的细节：

- 泛型不能写基本数据类型
- 指定泛型的具体类型，传递数据时，可以传入该类类型或者其子类型
- 如果不写泛型，类型默认是Object

#### 泛型类

使用场景：但一个类，某个变量的数据类型不确定的时候，就可以定义带有泛型

```java
修饰符 class 类名<类型>{
}
```

E：表示是不确定的类型，该类型在类名后面已经定义过了

e：形参的名字，变量名

#### 泛型方法

方法中形参类型不确定时，

1. 可以使用类名后面定义的泛型\<E>（所有方法都能用）

2. 在方法申明定义自己的泛型（只有本方法能用）

```java
修饰符<类型>返回值类型 方法名(类型 变量名){
    
}
```



#### 泛型接口

```java
修饰符 interface 接口名<类型>{

}
```

方法名1：实现类给出具体类型

方法名2：实现类延续泛型，创建对象时，再确定

#### 泛型的通配符

泛型不具备继承性，但是数据具备继承性

泛型里写的时什么类型，就只能传递什么类型

就可以使用泛型的通配符：

- ？也表示不确定类型，他可以进行类型的限定
- ？extends E：表示可以传递E或者E所有的子类型
- ？super E：表示可以传递E或者E所有的父类类型

### 数据结构（树）

![image-20250620153308678](images/image-20250620153308678-17504047913331.png)

![image-20250620155057204](images/image-20250620155057204.png)

![image-20250620153523291](images/image-20250620153523291.png)

度：每一个结点的子节点的数量

二叉树中，任意结点的度<=2

树高：树的总层数

根节点：最顶层的结点

左子节点：左下方的结点

右子节点：右下方的结点

根结点的左子树：蓝色虚线

根节点的右子树：绿色虚线

![image-20250620153843222](images/image-20250620153843222.png)

#### 二叉树

![image-20250620153942644](images/image-20250620153942644.png)

##### 遍历方式

###### 前序遍历

从根节点开始，然后按照当前结点，左子节点，右子节点的顺序遍历

###### 中序遍历、

从最左边的子节点开始，然后按照左子节点，当前结点，右子节点的顺序遍历

###### 后序遍历

从最左边的子节点开始，然后按照左子节点，右子节点，当前节点的顺序遍历

###### 层序遍历

从根节点开始一层一层遍历

#### 二叉查找树

![image-20250620153958408](images/image-20250620153958408.png)

二叉查找树，又称二叉排序树或者二叉搜索树

特点

- 每一个结点上最多有两个子节点
- 任意结点左子树上的值都小于当前结点
- 任意结点右子树上的值都大于当前结点

##### 添加结点

按照下列规则将下列结点添加到二叉查找树中

规则：

小的存左边

大的存右边

一样的不存

##### 查找结点

判断大小

大了向右

小了向左

##### 弊端

![image-20250620155312196](images/image-20250620155312196.png)

#### 平衡二叉树

规则：任一结点的左右左子树高度差不超过1

![image-20250620155757506](images/image-20250620155757506.png)

##### 旋转机制

规则1：左旋

规则2：右旋

触发时机：当添加一个结点之后，该树不再是一颗平衡二叉树

###### 左旋

![image-20250620160524416](images/image-20250620160524416.png)

![image-20250620160544391](images/image-20250620160544391.png)

确定支点：从添加的结点开始，不断的往父节点找到不平衡的结点

步骤：

- 以不平衡的点作为支点
- 把支点左旋降级，变为左子节点
- 晋升原来的右子节点

![image-20250620160647700](images/image-20250620160647700.png)

![image-20250620160943473](images/image-20250620160943473.png)

步骤：

- 以不平衡的结点作为支点
- 将根节点的右侧往左拉
- 原先的右子节点变成新的父节点，并把多余子结点出让，给已经降级的根节点当右子节点

###### 右旋

![image-20250620161048737](images/image-20250620161048737.png)

![image-20250620161402003](images/image-20250620161402003.png)

确定支点：从添加的结点开始，不断的往父节点找不平衡的结点

步骤：

- 以不平衡的点作为支点
- 把支点右旋降级，变为右子节点
- 晋升原来的左子节点

![image-20250620161440713](images/image-20250620161440713.png)

![image-20250620161717143](images/image-20250620161717143.png)

确定支点：从添加的结点开始，不断的往父节点找不平衡的结点

步骤：

- 以不平衡的点作为支点
- 就是将根节点的左侧往右拉
- 原来的左子节点变成新的父节点，并把多余的右子节点出让，给已经降级的根节点当左子节点

##### 需要旋转的四种情况

###### 左左

当根结点左子树的左子树有结点插入，导致二叉树不平衡

![image-20250620164847251](images/image-20250620164847251.png)

![image-20250620164918431](images/image-20250620164918431.png)

一次右旋

###### 左右

当根节点左子树的右子树有节点插入，导致二叉树不平衡

![image-20250620165048694](images/image-20250620165048694.png)

![image-20250620165134582](images/image-20250620165134582.png)

局部左旋

![image-20250620165336860](images/image-20250620165336860.png)

整体右旋

![image-20250620165418790](images/image-20250620165418790.png)

先局部左旋，再整体右旋

###### 右右

右右：当根结点右子树有结点插入，导致二叉树不平衡

一次左旋

![image-20250620165636214](images/image-20250620165636214.png)

![image-20250620165711968](images/image-20250620165711968.png)

###### 右左

右左：当根结点右子树的左子树有结点插入，导致二叉树不平衡

![image-20250620165850562](images/image-20250620165850562.png)

局部右旋

![image-20250620165933916](images/image-20250620165933916.png)

整体左旋

![image-20250620165949500](images/image-20250620165949500.png)

#### 红黑树

- 红黑树是一种自平衡的二叉查找树，是计算机科学中用到的一种数据结构
- 1972年出现，当时被称之为平衡二叉B树，后来，1978年修改为如今的“红黑树”。
- 他是一种特殊的二叉查找树，红黑树的每一个结点上都有存储位表示颜色
- 每一个结点都可以是红或者黑，红黑树不是高度平衡的，它的平衡是通过“红黑规则”进行实现的

##### 红黑规则

1. 每一个结点或是红色的，或者是黑色的
2. 根节点必须是黑色
3. 如果一个结点没有子节点或者父节点，则节点相应的指针属性值为Nil，这些Nil视为叶节点，每个叶节点（Nil）是黑色的
4. 如果某一个结点时红色的，那么它的子节点必须时黑色（不能出现两个红色结点想连的情况）
5. 对每一个结点，从该结点，从该结点到其所有后代的叶节点的简单路径，均包含相同数目的黑色结点

##### 添加结点的规则

默认颜色：添加结点默认是红色的（效率高）

黑色：添加三个结点，调整两次

红色：添加三个结点，调整一次

![image-20250620173111099](images/image-20250620173111099.png)

红黑树增删改查的性能都很好

### Set系列集合

- 无序：存取顺序不一致
- 不重复：可以去除重复
- 无索引：没有带索引的方法，所以不能使用普通for循环遍历，也不能通过索引来获取元素

Set集合的实现类

- HashSet：无序、不重复、无索引
- LinkedHashSet：有序、不重复、无索引
- TreeSet：可排序、不重复、无索引

Set接口中的方法上基本上与Collection的API一致

利用Set系列集合，添加字符串，并使用多种方式遍历

迭代器

增强for

Lambda表达式

### HashSet

#### HashSet的底层原理

- HashSet集合底层使用哈希表存储数据
- 哈希表是一种对于增删改查性能都标胶好的结构

![image-20250620180534783](images/image-20250620180534783.png)

1. 创建一个默认长度为16，默认加载因为0.75的数组，数组名table

2. 根据元素的哈希值跟数组的长的计算出应存入的位置

3. 判断当前位置是否为null，如果是null直接存入

4. 如果位置不为null，表示有元素，则调用equals方法比较属性值

5. 一样：不存
    不一样：存入数组

    JDK8以前：新元素存入数组，老元素挂在新元素下面

    JDK8以后：新元素直接挂在老元素下面

JDK8以后，当链表长度超过8，而且数组长度大于64的时候，自动转换为红黑树

如果集合存储的是自定义对象，必须重写hashCode和equals方法

#### 哈希表组成

+ JDK8之前：数组+链表
+ JDK8之后：数组+链表+红黑树

#### 哈希值

哈希值：对象的整数表现形式

- 依据hashCode方法算出来的int类型整数
- 该方法定义在Object类中，所有对象都可以调用，默认使用地址值进行计算
- 一般情况下，会重写hashCode方法，利用对象内部属性值计算哈希值

特点

- 如果没有重写hashCode方法，不同对象计算出的哈希值是不同的
- 如果已经重写hashCode方法，不同对象只要属性值相同，计算出的哈希值就是一样的
- 在小部分情况下，不同属性值或者不同地址值计算出来的哈希值也有可能一样（哈希碰撞）

eclipse`alt+shift+s`

### LinkedHashSet

#### LinkedHashSet底层原理

- 有序、不重复、无索引
- 这里的有序指得是保证存储和取出的元素顺序一致
- 原理：底层数据结构依然是哈希表，只是每个元素又额外多一个双链表的机制记录存储的顺序

去重默认使用HashSet

如果要求取值且存取有序，才使用LinkedHashSet

### TreeSet

- 无索引、无索引、可排序
- 可排序：按照元素的默认规则（有大有小）排序
- TreeSet集合底层是基于红黑树的数据结构实现排序的，增删改查性能都比较好

#### TreeSet集合默认的规则

- 对于数值类型：Integer，Double，默认按照从小到大的顺序排序
- 对于字符、字符串类型：按照字符在ASCii码表中的数字升序排列

字符和字符串默认的排序都剖视按照字典的顺序进行排列

方式1

默认排序/自然排序：JavaBean类实现Comparable接口指定比较规则

![image-20250620193614365](images/image-20250620193614365.png)

方式2：

比较器排序：创建TreeSet对象时候，传递比较器Comparator指定规则

使用规则：默认使用第一种，如果第一种不能满足当前需求，就使用第二种

创建集合

o1：表示执勤要添加的元素

o2：表示之前已经在红黑树存在的元素

返回值：

负数：认为要添加的元素是小的，存左边

正数：认为要添加的元素是大的，存右边

0：认为还要添加的元素已经存在，舍弃

### 场景分析

1. 如果想要集合中的元素可重复
    - 用ArrayList集合，基于数组的（用的最多）
2. 如果想要集合中的元素可重复，而且当前的增删操作明显多于查询
    - 用LinkedList集合，基于链表的
3. 如果相对集合中的元素可重复，而且当前的增删操作明显多于查询
    - 用HashSet集合，基于哈希表的（用的最多）
4. 如果相对集合中的元素去重，而且保证存取顺序
    - 用LinkedHashSet集合，基于哈希表和双链表，效率低于HashSet
5. 如果相对集合中的元素进行排序
    - 用TreeSet集合，基于红黑树。后续也可以用List集合实现排序

### 双列集合的特点

1. 双列集合一次需要村一堆数据，分别为键和值
2. 键不能重复，值可以重复
3. 键和值是一一对应的，每一个键只能找到自己对应的值
4. 键+值这个整体我们称之为"键值对"或"键值对对象",在Java中叫做"Entry对象"

### Map

#### Map的常见API

Map是双列集合的顶层接口，它的功能是全部双列集合都是可以继承使用的

| 方法名称                            | 说明                                 |
| ----------------------------------- | ------------------------------------ |
| V put(K key,V value)                | 添加元素                             |
| V remove(Object key)                | 根据键删除键值对元素                 |
| void clear()                        | 移出所有的键值对元素                 |
| boolean containsKey(Object key)     | 判断集合是否包含指定的键             |
| boolean containsValue(Object value) | 判断集合是否包含指定的值             |
| boolean isEmpty()                   | 判断集合是否为空                     |
| int size()                          | 集合的长度，也就是集合中键值对的个数 |

`Ctrl + Alt + L`补齐代码

put方法的细节：

添加/覆盖

在添加数据的时候，如果键不存在，那么直接把键值对对象添加到map集合中，方法返回null

在添加数据的时候，如果键是存在的，那么会把原有的键值对对象覆盖，会把被覆盖的值进行返回

#### Map集合遍历方式

##### 键找值

通过键找值，把这些键放在单列集合中

遍历单列集合，得到每一个键

利用map集合中的键值对来获取对应的值

##### 键值对

创建Map集合对象

添加元素

map.entrySet返回一个set集合

`Ctrl+Alt+v`自动生成左边

遍历这个Set集合去获取每一个键值对对象

利用entry调用个体方法获取值

##### Lambda表达式

| 方法名                                                       | 说明                  |
| ------------------------------------------------------------ | --------------------- |
| default void forEach(BiConsumer\<? super K,? super V>action) | 结合lamnda遍历Map集合 |

1. 创建Map集合对象
2. 添加元素
3. 利用lambda表达式进行遍历
    底层：
    forEach起始就是利用第二种方式进行遍历，依次得到每一个键和值
    在调用accept方法

### HashMap

1. HashMap是Map里面的一个实现类
2. 没有额外需要学习的特有方法，直接使用Map里面的方法就可以了
3. 特点是由键决定的：无序、不重复、无索引
4. HashMap跟HashSet底层原理是一模一样的，都是哈希表结构

总结

1. HashMap底层是哈希表结构的
2. 依赖hashCode方法和equals方法保证键的唯一
3. 如果建存储是自定义对象，需要重写hashCode和equals方法
    如果值存储自定义对象，不需要重写hashCode和equals方法

```java
import java.util.Objects;

public class Student {
    private String name;
    private int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public Student() {
    }

    public String getName() {

        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public boolean equals(Object o) {
        if (o == null || getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return age == student.age && Objects.equals(name, student.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }
}
```

```java
import java.util.HashMap;

public class test {
    public static void main(String[] args) {
        Student s1 = new Student("li", 18);
        Student s2 = new Student("wang", 18);
        Student s3 = new Student("zhao", 18);
        HashMap<Student, String> site = new HashMap<Student, String>();
        site.put(s1, "介休");
        site.put(s2,"灵石");
        site.put(s3,"介休");

        site.forEach((key,value)->{
            System.out.println(key.equals(s1)&value.equals("介休"));

        });

    }
}
```

```java
import java.util.HashMap;
import java.util.Map;
import java.util.Random;
import java.util.Set;

public class test {
    static Random r = new Random();

    public static void main(String[] args) {
        HashMap<Character,Integer> hashMap = new HashMap<>();
        int a=0,b=0,c=0,d=0;
        hashMap.put('A',a);
        hashMap.put('B',b);
        hashMap.put('C',c);
        hashMap.put('D',d);
        for (int i = 0; i < 80; i++) {
            int x = r.nextInt(4)+1;
            switch (x){
                case 1 -> hashMap.put('A',a++);
                case 2 -> hashMap.put('B',b++);
                case 3 -> hashMap.put('C',c++);
                case 4 -> hashMap.put('D',d++);
            }
        }
        int max=0;
        Set<Map.Entry<Character, Integer>> entries = hashMap.entrySet();
        for (Map.Entry<Character,Integer> entry:entries) {
            int count = entry.getValue();
            if (count > max) max = count;

        }
        final int s=max;
        hashMap.forEach((key,value)->{
            if(s==value) System.out.println(value);
        });
    }
}
```



```java
map.merge(num, 1, Integer::sum)
```



### LinkedHashMap

- 由键决定：有序、不重复、无索引
- 这里的有序指的是保证存储和取出的元素顺序一致
- 原理：底层结构依然是哈希表，只是每个键值对元素由额外多了一个双链表机制记录存储顺序

### TreeMap

- TreeMap跟TreeSet底层原理一样，都是红黑树结构
- 由键决定的特性：无重复、无索引、可排序
- 可排序：对键的大小进行排序
- 注意：默认按照键的从小到大进行排序，也可以自己规定排序规则

代码书写两种排序规则

- 实现Comparable接口，指定比较规则
- 创建集合是传递Comparator比较器对象，指定比较规则

```java
import java.util.*;

public class test3 {
    public static void main(String[] args) {
        TreeMap<Integer, String> treeMap = new TreeMap<>(new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2){
                return o1-o2;
            }
        });
        treeMap.put(1,"v");
        treeMap.put(2,"b");
        treeMap.put(3,"n");
        treeMap.put(4,"m");

        treeMap.forEach((key,value)->System.out.println(key+value));

    }

}
```

```java
import java.util.Objects;

public class Student {
    private String name;
    private int age;

    public Student() {
    }

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }


    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public boolean equals(Object o) {
        if (o == null || getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return age == student.age && Objects.equals(name, student.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

```java
import java.util.Comparator;
import java.util.TreeMap;

public class test4 {
    public static void main(String[] args) {
        Student li = new Student("li", 18);
        Student wang = new Student("wang", 18);
        Student zhao = new Student("zhao", 18);

        TreeMap<Student, String> treeMap = new TreeMap<>(new Comparator<Student>() {
            @Override
            public int compare(Student o1, Student o2) {
                int i = o2.getAge()-o1.getAge();
                if(i==0) i= o2.getName().compareTo(o1.getName());
                return i;
            }
        });

        treeMap.put(li,"介休");
        treeMap.put(wang,"灵石");
        treeMap.put(zhao,"介休");

        treeMap.forEach((key,value)->{
            System.out.println(key+value);
        });
    }
}
```

```java
import java.util.Scanner;
import java.util.TreeMap;

public class test5 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String s= sc.next();
        TreeMap<Character,Integer> treeMap = new TreeMap<>();
        for (int i = 0; i < s.length(); i++) {
            if(!treeMap.containsKey(s.charAt(i)))
                treeMap.put(s.charAt(i),1);
            else {
                int count = treeMap.size();
                count++;
                treeMap.put(s.charAt(i),count);
            }
        }
        treeMap.forEach((key,value)->{
            System.out.print(key+"("+value+")"+" ");
        });
    }
}
```

### 源码分析

```java
1.看源码之前需要了解的一些内容

Node<K,V>[] table   哈希表结构中数组的名字

DEFAULT_INITIAL_CAPACITY：   数组默认长度16

DEFAULT_LOAD_FACTOR：        默认加载因子0.75



HashMap里面每一个对象包含以下内容：
1.1 链表中的键值对对象
    包含：  
			int hash;         //键的哈希值
            final K key;      //键
            V value;          //值
            Node<K,V> next;   //下一个节点的地址值
			
			
1.2 红黑树中的键值对对象
	包含：
			int hash;         		//键的哈希值
            final K key;      		//键
            V value;         	 	//值
            TreeNode<K,V> parent;  	//父节点的地址值
			TreeNode<K,V> left;		//左子节点的地址值
			TreeNode<K,V> right;	//右子节点的地址值
			boolean red;			//节点的颜色
					


2.添加元素
HashMap<String,Integer> hm = new HashMap<>();
hm.put("aaa" , 111);
hm.put("bbb" , 222);
hm.put("ccc" , 333);
hm.put("ddd" , 444);
hm.put("eee" , 555);

添加元素的时候至少考虑三种情况：
2.1数组位置为null
2.2数组位置不为null，键不重复，挂在下面形成链表或者红黑树
2.3数组位置不为null，键重复，元素覆盖



//参数一：键
//参数二：值

//返回值：被覆盖元素的值，如果没有覆盖，返回null
public V put(K key, V value) {
    return putVal(hash(key), key, value, false, true);
}


//利用键计算出对应的哈希值，再把哈希值进行一些额外的处理
//简单理解：返回值就是返回键的哈希值
static final int hash(Object key) {
    int h;
    return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
}

//参数一：键的哈希值
//参数二：键
//参数三：值
//参数四：如果键重复了是否保留
//		   true，表示老元素的值保留，不会覆盖
//		   false，表示老元素的值不保留，会进行覆盖
final V putVal(int hash, K key, V value, boolean onlyIfAbsent,boolean evict) {
	    //定义一个局部变量，用来记录哈希表中数组的地址值。
        Node<K,V>[] tab;

		//临时的第三方变量，用来记录键值对对象的地址值
	    Node<K,V> p;
	    
		//表示当前数组的长度
		int n;
		
		//表示索引
	    int i;
		
		//把哈希表中数组的地址值，赋值给局部变量tab
		tab = table;
	
	    if (tab == null || (n = tab.length) == 0){
			//1.如果当前是第一次添加数据，底层会创建一个默认长度为16，加载因子为0.75的数组
			//2.如果不是第一次添加数据，会看数组中的元素是否达到了扩容的条件
			//如果没有达到扩容条件，底层不会做任何操作
			//如果达到了扩容条件，底层会把数组扩容为原先的两倍，并把数据全部转移到新的哈希表中
			tab = resize();
			//表示把当前数组的长度赋值给n
	        n = tab.length;
	    }
	
		//拿着数组的长度跟键的哈希值进行计算，计算出当前键值对对象，在数组中应存入的位置
		i = (n - 1) & hash;//index
		//获取数组中对应元素的数据
		p = tab[i];



    if (p == null){
		//底层会创建一个键值对对象，直接放到数组当中
        tab[i] = newNode(hash, key, value, null);
    }else {
        Node<K,V> e;
        K k;
		
		//等号的左边：数组中键值对的哈希值
		//等号的右边：当前要添加键值对的哈希值
		//如果键不一样，此时返回false
		//如果键一样，返回true
		boolean b1 = p.hash == hash;
		
        if (b1 && ((k = p.key) == key || (key != null && key.equals(k)))){
            e = p;
        } else if (p instanceof TreeNode){
			//判断数组中获取出来的键值对是不是红黑树中的节点
			//如果是，则调用方法putTreeVal，把当前的节点按照红黑树的规则添加到树当中。
            e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
        } else {
			//如果从数组中获取出来的键值对不是红黑树中的节点
			//表示此时下面挂的是链表
            for (int binCount = 0; ; ++binCount) {
                if ((e = p.next) == null) {
					//此时就会创建一个新的节点，挂在下面形成链表
                    p.next = newNode(hash, key, value, null);
					//判断当前链表长度是否超过8，如果超过8，就会调用方法treeifyBin
					//treeifyBin方法的底层还会继续判断
					//判断数组的长度是否大于等于64
					//如果同时满足这两个条件，就会把这个链表转成红黑树
                    if (binCount >= TREEIFY_THRESHOLD - 1)
                        treeifyBin(tab, hash);
                    break;
                }
				//e：			  0x0044  ddd  444
				//要添加的元素： 0x0055   ddd   555
				//如果哈希值一样，就会调用equals方法比较内部的属性值是否相同
                if (e.hash == hash && ((k = e.key) == key || (key != null && key.equals(k)))){
					 break;
				}

                p = e;
            }
        }
		
		//如果e为null，表示当前不需要覆盖任何元素
		//如果e不为null，表示当前的键是一样的，值会被覆盖
		//e:0x0044  ddd  555
		//要添加的元素： 0x0055   ddd   555
        if (e != null) {
            V oldValue = e.value;
            if (!onlyIfAbsent || oldValue == null){
				
				//等号的右边：当前要添加的值
				//等号的左边：0x0044的值
				e.value = value;
			}
            afterNodeAccess(e);
            return oldValue;
        }
    }
	
    //threshold：记录的就是数组的长度 * 0.75，哈希表的扩容时机  16 * 0.75 = 12
    if (++size > threshold){
		 resize();
	}
    
	//表示当前没有覆盖任何元素，返回null
```

![HashMap源码超详细讲解](images/HashMap源码超详细讲解.png)

1.TreeMap中每一个节点的内部属性
K key;					//键
V value;				//值
Entry<K,V> left;		//左子节点
Entry<K,V> right;		//右子节点
Entry<K,V> parent;		//父节点
boolean color;			//节点的颜色




2.TreeMap类中中要知道的一些成员变量
public class TreeMap<K,V>{

    //比较器对象
    private final Comparator<? super K> comparator;
    
    //根节点
    private transient Entry<K,V> root;
    
    //集合的长度
    private transient int size = 0;

   

























3.空参构造
	//空参构造就是没有传递比较器对象
	 public TreeMap() {
        comparator = null;
    }
	
	
	
4.带参构造
	//带参构造就是传递了比较器对象。
	public TreeMap(Comparator<? super K> comparator) {
        this.comparator = comparator;
    }
	
	
5.添加元素
	public V put(K key, V value) {
        return put(key, value, true);
    }

参数一：键
参数二：值
参数三：当键重复的时候，是否需要覆盖值
		true：覆盖
		false：不覆盖
		
	private V put(K key, V value, boolean replaceOld) {
		//获取根节点的地址值，赋值给局部变量t
	    Entry<K,V> t = root;
		//判断根节点是否为null
		//如果为null，表示当前是第一次添加，会把当前要添加的元素，当做根节点
		//如果不为null，表示当前不是第一次添加，跳过这个判断继续执行下面的代码
	    if (t == null) {
			//方法的底层，会创建一个Entry对象，把他当做根节点
	        addEntryToEmptyMap(key, value);
			//表示此时没有覆盖任何的元素
	        return null;
	    }
		//表示两个元素的键比较之后的结果
	    int cmp;
		//表示当前要添加节点的父节点
	    Entry<K,V> parent;
		
		//表示当前的比较规则
		//如果我们是采取默认的自然排序，那么此时comparator记录的是null，cpr记录的也是null
		//如果我们是采取比较去排序方式，那么此时comparator记录的是就是比较器
	    Comparator<? super K> cpr = comparator;
		//表示判断当前是否有比较器对象
		//如果传递了比较器对象，就执行if里面的代码，此时以比较器的规则为准
		//如果没有传递比较器对象，就执行else里面的代码，此时以自然排序的规则为准
	    if (cpr != null) {
	        do {
	            parent = t;
	            cmp = cpr.compare(key, t.key);
	            if (cmp < 0)
	                t = t.left;
	            else if (cmp > 0)
	                t = t.right;
	            else {
	                V oldValue = t.value;
	                if (replaceOld || oldValue == null) {
	                    t.value = value;
	                }
	                return oldValue;
	            }
	        } while (t != null);
	    } else {
			//把键进行强转，强转成Comparable类型的
			//要求：键必须要实现Comparable接口，如果没有实现这个接口
			//此时在强转的时候，就会报错。
	        Comparable<? super K> k = (Comparable<? super K>) key;
	        do {
				//把根节点当做当前节点的父节点
	            parent = t;
				//调用compareTo方法，比较根节点和当前要添加节点的大小关系
	            cmp = k.compareTo(t.key);
				
	            if (cmp < 0)
					//如果比较的结果为负数
					//那么继续到根节点的左边去找
	                t = t.left;
	            else if (cmp > 0)
					//如果比较的结果为正数
					//那么继续到根节点的右边去找
	                t = t.right;
	            else {
					//如果比较的结果为0，会覆盖
	                V oldValue = t.value;
	                if (replaceOld || oldValue == null) {
	                    t.value = value;
	                }
	                return oldValue;
	            }
	        } while (t != null);
	    }
		//就会把当前节点按照指定的规则进行添加
	    addEntry(key, value, parent, cmp < 0);
	    return null;
	}	


​	
​	
​	 private void addEntry(K key, V value, Entry<K, V> parent, boolean addToLeft) {
​	    Entry<K,V> e = new Entry<>(key, value, parent);
​	    if (addToLeft)
​	        parent.left = e;
​	    else
​	        parent.right = e;
​		//添加完毕之后，需要按照红黑树的规则进行调整
​	    fixAfterInsertion(e);
​	    size++;
​	    modCount++;
​	}


​	
​	
```java
private void fixAfterInsertion(Entry<K,V> x) {
	//因为红黑树的节点默认就是红色的
    x.color = RED;

	//按照红黑规则进行调整
	
	//parentOf:获取x的父节点
	//parentOf(parentOf(x)):获取x的爷爷节点
	//leftOf:获取左子节点
    while (x != null && x != root && x.parent.color == RED) {

			//判断当前节点的父节点是爷爷节点的左子节点还是右子节点
			//目的：为了获取当前节点的叔叔节点
	        if (parentOf(x) == leftOf(parentOf(parentOf(x)))) {
				//表示当前节点的父节点是爷爷节点的左子节点
				//那么下面就可以用rightOf获取到当前节点的叔叔节点
	            Entry<K,V> y = rightOf(parentOf(parentOf(x)));
	            if (colorOf(y) == RED) {
					//叔叔节点为红色的处理方案
					
					//把父节点设置为黑色
	                setColor(parentOf(x), BLACK);
					//把叔叔节点设置为黑色
	                setColor(y, BLACK);
					//把爷爷节点设置为红色
	                setColor(parentOf(parentOf(x)), RED);
					
					//把爷爷节点设置为当前节点
	                x = parentOf(parentOf(x));
	            } else {
					
					//叔叔节点为黑色的处理方案


		//表示判断当前节点是否为父节点的右子节点
                if (x == rightOf(parentOf(x))) {
					
					//表示当前节点是父节点的右子节点
                    x = parentOf(x);
					//左旋
                    rotateLeft(x);
                }
                setColor(parentOf(x), BLACK);
                setColor(parentOf(parentOf(x)), RED);
                rotateRight(parentOf(parentOf(x)));
            }
        } else {
			//表示当前节点的父节点是爷爷节点的右子节点
			//那么下面就可以用leftOf获取到当前节点的叔叔节点
            Entry<K,V> y = leftOf(parentOf(parentOf(x)));
            if (colorOf(y) == RED) {
                setColor(parentOf(x), BLACK);
                setColor(y, BLACK);
                setColor(parentOf(parentOf(x)), RED);
                x = parentOf(parentOf(x));
            } else {
                if (x == leftOf(parentOf(x))) {
                    x = parentOf(x);
                    rotateRight(x);
                }
                setColor(parentOf(x), BLACK);
                setColor(parentOf(parentOf(x)), RED);
                rotateLeft(parentOf(parentOf(x)));
            }
        }
    }
	
	//把根节点设置为黑色
    root.color = BLACK;
}

```

6.1TreeMap添加元素的时候，键是否需要重写hashCode和equals方法？
此时是不需要重写的。

6.2HashMap是哈希表结构的，JDK8开始由数组，链表，红黑树组成的。
既然有红黑树，HashMap的键是否需要实现Compareable接口或者传递比较器对象呢？
不需要的。
因为在HashMap的底层，默认是利用哈希值的大小关系来创建红黑树的

6.3TreeMap和HashMap谁的效率更高？
如果是最坏情况，添加了8个元素，这8个元素形成了链表，此时TreeMap的效率要更高
但是这种情况出现的几率非常的少。
一般而言，还是HashMap的效率要更高。

6.4你觉得在Map集合中，java会提供一个如果键重复了，不会覆盖的put方法呢？
此时putIfAbsent本身不重要。
传递一个思想：
	代码中的逻辑都有两面性，如果我们只知道了其中的A面，而且代码中还发现了有变量可以控制两面性的发生。
	那么该逻辑一定会有B面。
习惯：
		boolean类型的变量控制，一般只有AB两面，因为boolean只有两个值
		int类型的变量控制，一般至少有三面，因为int可以取多个值。

6.5三种双列集合，以后如何选择？
	HashMap LinkedHashMap TreeMap

默认：HashMap（效率最高）
如果要保证存取有序：LinkedHashMap
如果要进行排序：TreeMap

### 可变参数

JDK5

可变参数

方法形参的个数是可以发生变化的,0,1,2,3

格式:属性类型...名字

int...args

底层

可变参数底层就是一个数组

只不过不需要我们自己创建,java会帮我们创建好

细节:

1. 在方法的形参中只能写一个可变参数
2. 在方法当中,如果出了可变参数以外,还有其他形参,那么可变参数要写在最后

### Collections

- java.util.Collections:是集合工具类
- 作用:Collection不是集合,而是集合的工具类

Collections常用API

| 方法名称                                                     | 说明                            |
| ------------------------------------------------------------ | ------------------------------- |
| public static \<T> boolean addAll(Collection\<T> c,T...elements) | 批量添加元素                    |
| public static void shuffle (List\<?> list)                   | 打乱List集合元素的顺序          |
| public static \<T> void sort(List\<T> list)                  | 排序                            |
| public static \<T> void sort(List\<T> list,Comparator\<T> c) | 根据指定的规则进行排序          |
| public static \<T> int binarySearch (List\<T> list, T key)   | 以二分查找法查找元素            |
| public static \<T> void copy(List\<T> dest, List\<T> src)    | 拷贝集合中的元素                |
| public static \<T> int fill(List\<T> list, T obj)            | 使用指定的元素填充集合          |
| public static \<T> void max/min(Collection\<T> coll)         | 根据默认的自然排序获取最大/小值 |
| public static \<T> void swap(List\<?> list, int i,int j)     | 交换集合中指定位置的元素        |

### 综合案例

```java
import java.util.ArrayList;
import java.util.Collections;

public class test1 {
    public static void main(String[] args) {
        ArrayList<String> name = new ArrayList<>();
        Collections.addAll(name,"a","b","c","d","e","f");
        Collections.shuffle(name);
        System.out.println(name.getFirst());
    }
}
```

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Random;

public class test2 {
    public static void main(String[] args) {
        Random r = new Random();
        int [] arr = {1,1,1,1,1,1,1,0,0,0};
        int x = r.nextInt(10);
        ArrayList<String> boyList = new ArrayList<>();
        ArrayList<String> girlList= new ArrayList<>();
        Collections.addAll(boyList,"a","b","c","d","e","f","g");
        Collections.addAll(girlList,"A","B","C");
        Collections.shuffle(boyList);
        Collections.shuffle(girlList);
        if(arr[x]==1) System.out.println(boyList.getFirst());
        else System.out.println(girlList.getFirst());
    }
}
```

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Random;

public class test3 {
    public static void main(String[] args) {
        Random r = new Random();
        ArrayList<String> name = new ArrayList<>();
        Collections.addAll(name, "a", "b", "c", "d", "e", "f");
        ArrayList<String> list = new ArrayList<>();
        for (int i = 0; i < 10; i++) {
            System.out.println("===========================i==========================");
            int count = name.size();
            for (int j = 0; j < count; j++) {
                int index = r.nextInt(name.size());
                String x = name.remove(index);
                list.add(x);
                System.out.println(x);
            }

            name.addAll(list);
            list.clear();
        }
    }
}
```

```java
import java.util.*;

public class test6 {
    public static void main(String[] args) {
        HashMap<String, ArrayList<String>> hashMap = new HashMap<>();

        ArrayList<String> city1 = new ArrayList<>();
        city1.add("a");
        city1.add("a");
        city1.add("a");
        city1.add("a");
        city1.add("a");
        city1.add("a");

        ArrayList<String> city2 = new ArrayList<>();
        city2.add("b");
        city2.add("b");
        city2.add("b");
        city2.add("b");
        city2.add("b");
        city2.add("b");

        ArrayList<String> city3 = new ArrayList<>();
        city3.add("c");
        city3.add("c");
        city3.add("c");
        city3.add("c");
        city3.add("c");
        city3.add("c");

        hashMap.put("A",city1);
        hashMap.put("B",city2);
        hashMap.put("C",city3);
        String s ="";
        Set<Map.Entry<String,ArrayList<String>>> entries = hashMap.entrySet();
        for (Map.Entry<String,ArrayList<String>>entry:entries){
            String key=entry.getKey();
            ArrayList<String> value = entry.getValue();
            StringJoiner sj =new StringJoiner (",","","");
            for (String city : value) sj.add(city);

            System.out.println(key+" = "+ sj);
        }



    }
    }
```

#### 微服务

![image-20250622220642554](images/image-20250622220642554.png)

#### 斗地主

```java
import java.util.ArrayList;
import java.util.Collections;

public class PokerGame {
    static ArrayList<String> list = new ArrayList<>();
    static {
        String[] color = {"♦","♣","♥","♠"};
        String[] number = {"3","4","5","6","7","8","9","10","J","Q","K","A","2"};


        for (String c:color){
            for (String n: number){
                list.add(n+c);
            }
        }
        list.add("大王");
        list.add("小王");
    }

    public PokerGame(){
        Collections.shuffle(list);

        ArrayList<String> lord = new ArrayList<>();
        ArrayList<String> player1 = new ArrayList<>();
        ArrayList<String> player2 = new ArrayList<>();
        ArrayList<String> player3 = new ArrayList<>();

        for (int i = 0; i < list.size(); i++) {
            String poker = list.get(i);
            if(i<=2){
                lord.add(poker);
                continue;
            }

            if(i%3==0){
                player1.add(poker);
            } else if (i%3==1) {
                player2.add(poker);
            } else  {
                player3.add(poker);
            }
        }
        lookPoker("底牌",lord);
        lookPoker("地主",player1);
        lookPoker("农民",player2);
        lookPoker("农民1",player3);

    }
    public void lookPoker (String name,ArrayList<String> list){
        System.out.println(name+"：");
        for(String poker : list){
            System.out.print(poker+" ");
        }
        System.out.println();
    }
}
```

```java
public class App {
    public static void main(String[] args) {
        new PokerGame();
    }
}
```

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.HashMap;
import java.util.TreeSet;

public class PokerGame {
    static HashMap<Integer,String> hm = new HashMap<>();
    static ArrayList<Integer> list = new ArrayList<>();
    static {
        String[] color = {"♦","♣","♥","♠"};
        String[] number = {"3","4","5","6","7","8","9","10","J","Q","K","A","2"};

        int serialNumber = 1;
        for (String c:number){
            for (String n: color){
                hm.put(serialNumber,n+c);
                list.add(serialNumber);
                serialNumber++;
            }
        }
        hm.put(serialNumber,"大王");
        list.add(serialNumber);
        serialNumber++;
        list.add(serialNumber);
        hm.put(serialNumber,"小王");
    }
    public PokerGame(){
        Collections.shuffle(list);
        TreeSet<Integer> lord = new TreeSet<>();
        TreeSet<Integer> player1 = new TreeSet<>();
        TreeSet<Integer> player2 = new TreeSet<>();
        TreeSet<Integer> player3 = new TreeSet<>();
        for (int i = 0; i < list.size(); i++) {
            Integer poker = list.get(i);
            if(i<=2){
                lord.add(poker);
                continue;
            }

            if(i%3==0){
                player1.add(poker);
            } else if (i%3==1) {
                player2.add(poker);
            } else  {
                player3.add(poker);
            }
        }
        lookPoker("底牌",lord);
        lookPoker("地主",player1);
        lookPoker("农民",player2);
        lookPoker("农民1",player3);

    }
    public void lookPoker (String name,TreeSet<Integer> list){
        System.out.println(name+"：");
        for(Integer serialNumber : list){
            String poker = hm.get(serialNumber);
            System.out.print(poker+" ");
        }
        System.out.println();
    }


}
```

```java
public class App {
    public static void main(String[] args) {
        new PokerGame();
    }
}
```

```java
import java.util.*;


public class PokerGame {
    static ArrayList<String> list = new ArrayList<>();
    static HashMap<String,Integer> hm = new HashMap<>();
    static {
        String[] color = {"♦","♣","♥","♠"};
        String[] number = {"3","4","5","6","7","8","9","10","J","Q","K","A","2"};


        for (String c:color){
            for (String n: number){
                list.add(c+n);
            }
        }
        list.add(" 大王");
        list.add(" 小王");

        hm.put("J",11);
        hm.put("Q",12);
        hm.put("K",13);
        hm.put("A",14);
        hm.put("2",15);
        hm.put("小王",50);
        hm.put("大王",100);
    }

    public PokerGame(){
        Collections.shuffle(list);

        ArrayList<String> lord = new ArrayList<>();
        ArrayList<String> player1 = new ArrayList<>();
        ArrayList<String> player2 = new ArrayList<>();
        ArrayList<String> player3 = new ArrayList<>();

        for (int i = 0; i < list.size(); i++) {
            String poker = list.get(i);
            if(i<=2){
                lord.add(poker);
                continue;
            }

            if(i%3==0){
                player1.add(poker);
            } else if (i%3==1) {
                player2.add(poker);
            } else  {
                player3.add(poker);
            }
        }

        order(lord);
        order(player1);
        order(player2);
        order(player3);


    }
    public void order(ArrayList<String> list){
        Collections.sort(list, new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                String color1=o1.substring(0,1);
                String color2=o2.substring(0,1);
                int value1 = getValue(o1);
                int value2 = getValue(o2);

                int i = value1-value2;
                return i==0?color1.compareTo(color2):i;

            }
        });
    }

    public int getValue(String poker){
        String number = poker.substring(1);

        if(hm.containsKey(number)){
            return  hm.get(number);
        }else{
            return Integer.parseInt(number);
        }
    }


}
```

```java
public class App {
    public static void main(String[] args) {
        new PokerGame();
    }
}
```

### 创建不可变集合

#### 引用场景

- 如果某个数据不能被修改，把它防御性的拷贝到不可变集合中是个很好的实践
- 或者当集合的对象被不可信的库调用时，不可变的形式是安全的

简单理解：不想让别人修改集合中部的内容

#### 创建不可变集合的书写形式

在List、Set、Map接口中，都存在静态的of方法，可以获取一个不可变的集合

| 方法名称                                    | 说明                               |
| ------------------------------------------- | ---------------------------------- |
| static \<E> List\<E> of(E ... Elements)     | 创建一个具有指定元素的List集合对象 |
| static \<E> Set\<E> of(E ... Elements)      | 创建一个具有指定元素的Set集合对象  |
| static \<K,V> Map\<K,V> of (E ... Elements) | 创建一个具有指定元素的Map集合对象  |

注意：这个集合不能添加，不能删除，不能修改

创建Map的不可变集合

细节1：

键是不能重复的

细节2：

Map中的of方法，参数是有上线的，最多只能传递20个参数，10个键值对

细节3：

如果我们要传递多个键值对对象，数量大于10个，在Map接口中还有一个方法

```java
static <K,V> Map<K,V> ofEntries (Entry <? extends K,? extends V> ... enries)
```

JDK10中有CopyOf方法

### Stream流

#### Stream流的作用

结合lambda表达式，简化集合，数组的操作

#### Stream流的使用步骤

1. 先得的一条Stream(流水线),并把数据放上去
2. 利用Stream流中的API进行各种操作

过滤	转换	中间方法	方法调用完毕后，还可以调用其他方法

统计	打印	终结方法	最后一步，调用完毕后，不能调用其他方法

1. 先得到一条stream流水线，并把数据放上去

    | 获取方式     | 方法名                                     | 说明                   |
    | ------------ | ------------------------------------------ | ---------------------- |
    | 单列集合     | default Stream\<E> Stream                  | Collection中的默认方法 |
    | 双列集合     | 无                                         | 无法直接使用Stream流   |
    | 数组         | public static Stream\<T> Stream(T[] array) | Arrays工具中的静态方法 |
    | 一堆零散数据 | public static Stream\<T> of(C)             | Stream接口中的静态方法 |

    Stremof接口中的静态方法of的细节

    方法的形参是一个可变的参数，可以传递一堆零散的数据，也可以传递数组

    但是数组，必须是引用数据类型的，如果传递基本数据类型，是会把整个数组当作一个元素，放到Stream当中

2. | 名称                                               | 说明                                       |
    | -------------------------------------------------- | ------------------------------------------ |
    | Stream\<T> filter(Predicate\<? super T> predicate) | 过滤                                       |
    | Stream\<T> limit(long maxSize)                     | 获取前几个元素                             |
    | Stream\<T> skip(long n)                            | 跳过前几个元素                             |
    | Stream\<T> distinct()                              | 元素去重，依赖（hashCode方法和equals方法） |
    | static \<T> Stream\<T> concat(Stream a,Stream b)   | 合并a和b两个流为一个流                     |
    | Stream\<R> map(Function<T,R>mapper)                | 转化流的数据类型                           |

    注意1：中间方法，返回新的Stream流，原来的Stream流只能使用一次，建议使用链式编程

    注意2：修改Stream流中的数据，不会影响原来集合或者数组中的数据

    Predicate接口：如果返回值为true，表示当前数据留下，如果返回值为false，表示当前数据舍弃不要

3. 终结方法

    | 名称                          | 说明                       |
    | ----------------------------- | -------------------------- |
    | void forEach(Consumer action) | 遍历                       |
    | long count()                  | 统计                       |
    | toArray()                     | 收集流中的数据，放到数组中 |
    | collect(Collector collector)  | 收集流中的数据，放到集合中 |

    Consumer的泛型:表示流里面的每一个数据类型

    accept方法中的形参s：依次表示流里面的每个数据

    方法体：对每一个数据的处理操作

    ToMap：

    参数一表示键的生成规则

    参数二表示值的生成规则

    参数一：

    Function

    泛型一：表示流中每一个数据的数据类型

    泛型二：表示Map集合中键的数据类型

    方法apply的形参：依次表示流中的每一个数据

    方法体：生成键的代码

    返回值：已经生成的键

    参数二：

    Function

    泛型一：表示流中每一个数据的数据类型

    泛型二：表示Map集合中值的数据类型

    方法apply的形参：依次表示流中的每一个数据

    方法体：生成值的代码

    返回值：已经生成的值

#### 综合案例

数据过滤

```java
public class test1 {
    public static void main(String[] args) {
        int [] a={1,2,3,4,5,6,7,8,9,10};
        Arrays.stream(a).filter(d->d%2==0).forEach(d->System.out.println(d));
    }
}
```

数据操作

```java
import java.util.ArrayList;
import java.util.Map;
import java.util.function.Function;
import java.util.stream.Collector;
import java.util.stream.Collectors;

public class test2 {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("zhangsan,23");
        list.add("lisi,24");
        list.add("wangwu,25");
        Map<String,Integer> map=list.stream()
                .filter(s->Integer.parseInt(s.split(",")[1])>=24)
                .collect(Collectors.toMap(new Function<String, String>() {
                    @Override
                    public String  apply(String s) {
                        return s.split(",")[0];
                    }
                }, new Function<String, Integer>() {
                    @Override
                    public Integer apply(String s) {
                        return Integer.parseInt(s.split(",")[1]);

                    }
                }));
        System.out.println(map);
    }
}
```

数据操作

```java
import java.util.ArrayList;
import java.util.List;
import java.util.function.Function;
import java.util.stream.Collectors;
import java.util.stream.Stream;

public class test3 {
    public static void main(String[] args) {
        ArrayList<String> manList =new ArrayList<>();
        ArrayList<String> womanList =new ArrayList<>();

        Stream<String> man = manList.stream()
                .filter(s -> s.split(",")[0].length() == 3)
                .limit(2);
        Stream<String> woman = womanList.stream()
                .filter(s->s.split(",")[0].startsWith("杨"))
                .skip(1);
        List<Actor> list = Stream.concat(man, woman).map(new Function<String, Actor>() {
            @Override
            public Actor apply(String s) {
                String name = s.split(",")[0];
                int age = Integer.parseInt(s.split(",")[1]);
                return new Actor(name, age);
            }
        }).collect(Collectors.toList());
        System.out.println(list);
    }
}
```

### 方法引用

把已经有的方法拿过来用，当作函数是接口中抽象方法的方法体

`::`方法引用符

要求：

1. 引用处必须是函数式接口
2. 被引用的方法必须已经存在
3. 被引用方法必须已经存在，需要跟抽象方法保持一致
4. 被引用方法的功能满足当前要求

####  方法引用分类

##### 引用静态方法

类名::静态方法

##### 引用成员方法

对象::成员方法

###### 引用其他类的成员方法

其他类对象::方法名

###### 引用本类的成员方法

引用处不能是静态方法

this::方法名

###### 引用父类的成员方法

引用处不是静态方法

super::方法名

##### 引用构造方法

类名::new

##### 使用其他调用方式

###### 使用类名引用成员方法

类名::成员方法

抽象参数形参的详解：

第一个参数：表示被引用方法的调用者，决定了可以引用那些类的方法

在stream流中，第一个参数一般表示流里面的每一个数据

假设列里面都是字符串，那么使用这种方式进行方法引用，只能使用String这个类中的方法

第二个参数到最后一个参数：跟被引用方法的形参保持一致，如果没有第二个参数，说明被引用的方法需要的是无参的成员方法

局限性：

不能引用所有类中的成员方法

如果抽象方法的第一个参数是A类型的

只能引用A类中的方法

###### 使用数组的构造方法

数组类型[]::new

## 异常、File、综合案例

### 异常

异常就是代表程序出现的问题

![image-20250626203357854](images/image-20250626203357854.png)

Error：代表系统级别错误（属于严重问题）系统一旦出现问题，sun公司就把这些错误封装为Error对象。Error是给sun自己用的，不是给程序员用的

Exception：叫做异常，代表程序可能出现的问题。我们通常会用Exception以及他的子类来封装程序出现的问题

运行时异常：RuntimeException及其子类，编译阶段不会出现异常提醒，运行时出现的异常（如：数组索引越界异常）

编译时异常：编译阶段就会出现的异常提醒。（如：日期解析异常）

![image-20250626204152351](images/image-20250626204152351.png)

Java不会运行代码，只会检查语法是否错误，或者做一些性能优化

#### 异常的作用

作用1：异常是用来查询bug的关键信息

作用2：异常可以作为方法内部的一种特殊返回值，以便通知调用者底层的情况

#### 异常的处理方式

##### JVM默认的处理方式

- 把异常的名称，异常原因及异常处理的位置等信息输出在了控制台
- 程序停止执行，下面的代码不会再执行

##### 自己处理（捕获异常）

```java
try{
    可能出现异常代码;
}catch(异常类名 变量名){
    异常的处理代码;
}
```

目的：当代码出现异常时，可以让程序继续往下执行1

###### 细节

try中没有遇到问题

会把try里面所有的代码全部执行完毕，不会执行catch里面的代码

注意：

只有出现了异常才会执行catch里面的代码

try中可能遇到多个问题，怎么执行

会写多个catch与之对应

细节：

如果我们要捕获多个异常，这些异常中如果存在多个父子关系，那么父类一定要写下面

理解：

再JDK7之后，我们再catch中同时捕获多个异常，中间使用|进行隔开

表示如果出现了A异常或者B异常，采取同一种处理方案

如果try没有捕获异常

相当于try...catch的代码白写了，最终还是会交给虚拟机进行处理

如果try遇到了问题，那么try下面的代码还会执行

下面的代码就不会执行了，直接跳转到对应的catch当中，执行catch中的语句体

但是如果没有catch与之对应，那么还是会交给虚拟机处理

##### 异常中的常见的成员方法

| 方法名称                      | 说明                            |
| ----------------------------- | ------------------------------- |
| public String getMessage()    | 返回此throwable的详细消息字符串 |
| public String toString()      | 返回此可抛出的简单描述          |
| public void printStackTrace() | 把异常的错误信息输出在控制台    |

在底层是利用System.err.println进行输出把异常的错误信息输出在控制台

细节：仅仅是打印信息，不会停止程序的运行

##### 抛出异常

throws

注意：写在方法定义处，表示声明一个异常，告诉调用者，使用本方法可能会有那些异常

```java
public void 方法()throws 异常类名1,异常类名2...{
    ...
}
```

- 编译时异常：必须要写
- 运行时异常：可以不写

throw

注意：写在方法内，结束方法

手动抛出异常对象，交给调用者

方法下面的代码就不在执行了

```java
public void 方法(){
    throw new NullPointerException();
}
```

#### 自定义异常

1. 定义异常类
2. 写继承关系
3. 空参构造
4. 带参构造

意义：就是为了让控制台的报错信息更加的见名知义

### File

file对象就表示一个路径，可以是文件的路径，也可以是文件夹的路径

这个路径可以是存在的，也可以是不存在的

| 方法名                                   | 说明                                               |
| ---------------------------------------- | -------------------------------------------------- |
| public File(String pathname)             | 根据文件路径创建对象                               |
| public File(String parent ,String child) | 根据父路径名字符串和子路径字符串创建文件对象       |
| public File(File parent,String child)    | 根据父路径对应文件对象和子路径名字符串创建文件对象 |

父级路径：除了文件名称以外的路径

自己路径：文件名

\：转义字符（windows）

/：转移字符（linux）

### 综合练习

#### File中常见的成员方法

##### 判断

| 方法名称                     | 说明                             |
| ---------------------------- | -------------------------------- |
| public boolean isDirectory() | 判断此路径名表示的file是否是文件 |
| public boolean isFile()      | 判断此路径名表示的file是否是文件 |
| public boolean exists()      | 判断此路径名表示的file是否存在   |

##### 获取

| 方法名称                        | 说明                                 |
| ------------------------------- | ------------------------------------ |
| public long length()            | 返回文件的大小（字节数量）           |
| public String getAbsolutePath() | 返回文件的绝对路径                   |
| public String getPath()         | 返回文件的名称，带后缀               |
| public long lastModified()      | 返回文件的最后修改时间（时间毫秒值） |

length只能返回文件的大小单位是字节

如果单位是M或G，可以不断的除以1024

这个方法无法获取文件夹的大小

如果我们要获取文件夹的大小，需要把这个文件夹里面所有文件大小都累加在一起

##### 创建

| 创建                           | 说明                 |
| ------------------------------ | -------------------- |
| public boolean createNewFile() | 创建一个新的空文件夹 |
| public boolean mkdie()         | 创建单极文件夹       |
| public boolean mkdirs()        | 创建多级文件夹       |
| public boolean delete()        | 删除文件、空文件夹   |

delete方法默认只能删除文件和文件夹，delete方法直接删除不走回收站

细节1：如果当前路径表示的文件是不存在的，则创建成功，方法返回true

如果当前文件时存在的，则创建失败，方法返回false

细节2：如果父级路径是不存在的，那么会有方法异常IOException

细节3：createNewFile方法创建的一定是文件，如果路径中不包含后缀名，则创建一个没有后缀的文件

如果删除的是文件，则直接删除，不走回收站

如果删除的是文件夹，则直接删除，不走回收站

如果删除的是有内容的文件夹，则删除失败

##### 删除

| 方法名称                  | 说明                     |
| ------------------------- | ------------------------ |
| public File[] listFiles() | 获取当前该路径下所有内容 |

##### 获取并遍历

| 方法名称                                       | 说明                                       |
| ---------------------------------------------- | ------------------------------------------ |
| public static File[] listRoots()               | 列出可用的文件系统根                       |
| public String[] list()                         | 获取当前路径下所有内容                     |
| public String[] list(FilenameFilter filter)    | 利用文件名过滤器获取当前改路径下的所有内容 |
| public File[] listFiles()                      | 利用当前改路径下所有内容                   |
| public File[] listFiles(FileFilter filter)     | 利用文件名过滤器获取当前该路径下所有内容   |
| public File[] listFiles(FilenameFilter filter) | 利用文件名获取当前该路径下所有内容         |

要删除一个有文件的文件夹：

1. 删除文件夹中所有的内容
2. 在删除自己

## IO流

存储和读取数据的解决方案

File类只能对文件本身进行操作，不能读写文件里面存储的数据

IO流

用于读写文件中的数据（可以读写文件或网络中的数据）

### IO流的分类

![image-20250704202644557](images/image-20250704202644557.png)

纯文本文件

用windows系统自带的记事本打开并且可以正确编码的文件

### IO流的体系

![image-20250706213901383](images/image-20250706213901383.png)

### 字节流

#### FileOutputStream

操作本地文件的字节输出流，可以把程序中的数据写到本地文件

书写步骤：

1. 创建字节输出流对象
    参数是字符串表示的路径或者是File对象都是可以的
    如果文件不存在会创建一个新的文件，但是要保证父级路径是存在的
    如果文件已经存在，则会清除文件

2. 写数据
    write方法的参数是整数，但是实际上写到本地文件的是整数在ASCII码表上的对应的字符

3. 释放资源

    每次使用完流后都要释放资源

##### 写数据的三种方式

| 方法名称                              | 说明                         |
| ------------------------------------- | ---------------------------- |
| void write(int b)                     | 一次写一个字节的数据         |
| void write(byte[] b)                  | 一次写一个字节数组的数据     |
| void write(byte[] b,int off ,int len) | 一次写一个字节数组的部分数据 |

参数：

1. 数组
2. 起始索引
3. 个数

##### 换行写

在写出一个换行符即可

- Windows：\r\n
- Linux：\n
- Mac：\r

细节：

在window是操作系统中Java会对回车换行进行了优化

虽然完整的是\r\n，但是我们写其中一个\r或者\n

Java也可以实现换行，因为Java在底层中补齐

建议：

不要省略，还是不全了

##### 续写（追加）

 如果想要续写，打开续写开关即可

开关位置，创建对象的第二个参数

默认false：表示关闭续写，此时创建对象会清空文件

手动传递true：表示打开续写，此时创建对象不会清空文件

#### FileInputStream

 操作本地文件的字节输入流，可以把本地文件中的数据读取到程序中来

书写步骤：

1. 创建字节流输入对象
    如果文件不存在，直接报错
2. 读数据
    一次读取一个字节，读出来是ASCII上对应的数字
    找到文件末尾了，read方法返回-1
3. 释放资源
    每次使用完流后都要释放资源

##### 字节输入流的循环读取

```java
int b;
while(b=文件对象.read()!=-1){
    语句体;
}
```

##### 拷贝大文件

![image-20250707173003104](images/image-20250707173003104.png)

弊端：一次读取一个字节

| 方法名称                       | 说明                     |
| ------------------------------ | ------------------------ |
| public int read()              | 一次读取一个字节的数据   |
| public int read(byte[] buffer) | 一次读一个字节数组的数据 |

注意：一次读一个字节数组的数据，每次读取会尽可能把数组装满
返回值：本次读取了多少字节数据

##### try...catch异常处理

基本方法

```java
try{
    可能出现异常的代码;
}catch(异常类名 变量名) {
    异常处理代码;
} finally{
    执行所有资源释放操作;
}
```

JDK7的方案

实现AutoCloseable接口

```java
try(创建流对象1;创建流对象2){
    可能出现异常的代码;
}catch(异常类名 变量名) {
    异常处理代码;
}
```

资源用完最终自动释放

JDK8的方案

```java
创建流对象1;
创建流对象2;
try(流1;流2){
    可能出现异常的代码;
}catch(异常类名 变量名) {
    异常处理代码;
}
```



### 字符集

#### 编码规则

在计算机中，任意数据都是以二进制的形式来存储的

计算机中最小的存储单元是一个字节

##### ASCII字符集

一个英文占一个字节

##### GBK

简体中文windows默认编码规则

核心：

1. GBK中，一个英文字母一个字节，二进制第一位是0
2. GBK中，一个汉字两个字节，二进制的第一位是1

##### Unicode

![image-20250707181616372](images/image-20250707181616372.png)

###### 英文

兼容ASCII码表

UTF-16编码规则：用2~4个字节保存

UTF-32编码规则：固定使用四个字节保存

UTF-8编码规则：用1~4个字节进行保存

###### 中文

三个字节

第一个字节首位是1

#### 不产生乱码

1. 不要使用字节流读取文本文件
2. 编码解码的时候使用同一个码表，同一个编码方式

#### Java中的编码方法

| String类中的方法                           | 说明                 |
| ------------------------------------------ | -------------------- |
| public byte[] getBytes()                   | 使用默认方式进行编码 |
| public byte[] getBytes(String charsetName) | 使用指定方式进行编码 |

#### Java中的解码方法

| String类中的方法                         | 说明                 |
| ---------------------------------------- | -------------------- |
| String(byte[] bytes)                     | 使用默认方式进行解码 |
| String(byte[] bytes, String charsetName) | 使用指定方式进行解码 |

### 字符流

字符类底层其实就是字节流

![image-20250714094131680](images/image-20250714094131680.png)

特点：

- 输入流：一次读取一个字节，遇到中文时，一次读取多个字节
- 输出流：底层会把数据按照指定的编码方式进行编码，编程字节在写到文件当中

使用场景

对于纯文本文件进行读写

#### FileReader

1. 创建字符输入对象

    | 构造方法                           | 说明                       |
    | ---------------------------------- | -------------------------- |
    | public FileReader(File file)       | 创建字符输入流关联本地文件 |
    | public FileReqder(String pathname) | 创建字符输入流关联本地文件 |

2. 读取文件

    | 成员方法                        | 说明                         |
    | ------------------------------- | ---------------------------- |
    | public int read()               | 读取数据，读到末尾返回-1     |
    | public int read(char [] buffer) | 读取多个数据，读到末尾返回-1 |

    细节1：按字节继续读取，遇到中文，一次读取多个字节，读取后解码，返回一个整数

    细节2：读到文件末尾了，read方法返回-1

3. 释放资源

    | 成员方法           | 说明          |
    | ------------------ | ------------- |
    | public int close() | 释放资源/关流 |

#### FileWriter

##### 构造方法

| 构造方法                                    | 说明                             |
| ------------------------------------------- | -------------------------------- |
| public FileWriter(File file)                | 创建字符输出流关联本地文件       |
| public FileWriter(String pathname)          | 创建字符输出流关联本地文件       |
| public FileWriter(File file,boolean append) | 创建字符输出流关联本地文件，续写 |
| public FileWirter(File file,boolean append) | 创建字符输出流关联本地文件，续写 |

##### 成员方法

| 成员方法                                  | 说明                   |
| ----------------------------------------- | ---------------------- |
| void write(int c)                         | 写出一个字符           |
| void write(String str)                    | 写出一个字符串         |
| void write(String str , int off ,int len) | 写出一个字符串的一部分 |
| void write(char[] cbuf)                   | 写出一个字符数组       |
| void write(char[] cbuf, int off ,int len) | 写出字符数组的一部分   |

#### 底层原理

![image-20250714105054841](images/image-20250714105054841.png)

#### 缓冲区

flush和close

| 成员方法            | 说明                             |
| ------------------- | -------------------------------- |
| public void flush() | 将缓冲区中的数据，刷新到本地文件 |
| public void close() | 释放资源，关流                   |

flush刷新：刷新之后，还可以继续往文件中写入数据

close关流：断开通道，无法再往文件中写入数据

#### 字节流和字符流的使用场景

字节流

拷贝任意类型的文件

字符流 

读取纯文本文件中的数据

往纯文本文件中写出数据

### 缓冲流

![image-20250803181814455](images/image-20250803181814455.png)

#### 字节缓冲流

原理：底层自带了长度为8192的缓冲区提高性能

| 方法名称                                     | 说明                                     |
| -------------------------------------------- | ---------------------------------------- |
| public BufferedInputStream(InputStream is)   | 把基本流包装成高级流，提高读取数据的性能 |
| public BufferedOutputStream(OutputStream os) | 把基本流包装成高级流，提高写出数据的性能 |

#### 字符缓冲流

| 方法名称                        | 说明                 |
| ------------------------------- | -------------------- |
| public BufferedReader(Reader r) | 把基本流包装成高级流 |
| public BufferedWriter(Writer r) | 把基本流包装成高级流 |

| 字符缓冲输入流特有方法 | 说明                                       |
| ---------------------- | ------------------------------------------ |
| public String readline | 读取一行数据，如果没有数据可读了会返回null |

| 字符缓冲输出流      | 说明       |
| ------------------- | ---------- |
| public void newLine | 跨平台换行 |

### 转换流

是字符流和字节流之间的桥梁

作用1：指定字符集读写

作用2：字节流中想要使用字符流中的方法

![image-20250804162345366](images/image-20250804162345366.png)

`Ctrl+b`查看类的的代码

### 序列化流

![image-20250809180732979](images/image-20250809180732979.png)

#### 序列化流（对象操作输出流）

可以将序列化流写到本地文件中

| 构造方法                                    | 说明                 |
| ------------------------------------------- | -------------------- |
| public ObjectOutputStream(OutputStream out) | 把基本流包装成高级流 |

| 成员方法                             | 说明                         |
| ------------------------------------ | ---------------------------- |
| public final writeObject(Object obj) | 把对象序列化(写出)到文件中去 |

#### 序列化流的小细节

1.  使用对象输出流将对象保存到文件时会出现NotSerializableException异常
    解决方案：需要让JavaBean类实现Serializable接口
    一旦实现了这个接口，那么表示当前的Student类可以序列化
2. 序列化流写到文件中的数据是不能修改的，一旦修改就无法再次读回来了、
3. 序列化对象后，修改了JavaBean类，再次反序列化会出问题，抛出InvalidClassExecption异常
    给JavaBean类添加serialVersionUID(序列号、版本号)
4. 如果一个人对象中某个成员变量的值不想被序列化
    给该成员变量transient关键字修饰，该关键字transient关键字修饰，该关键字标记的成员变量不参与序列化过程

#### 反序列化流（对象输入操作流）

可以把序列化流到本地文件中的对象，读取到程序中来

| 构造方法                                  | 说明               |
| ----------------------------------------- | ------------------ |
| public ObjectInputStream(InputStream out) | 把基本流变成高级流 |

| 成员方法                   | 说明                                       |
| -------------------------- | ------------------------------------------ |
| public Object readObject() | 将序列化到本地文件中的对象，读取到程序中来 |

#### 报错

原因：文件中的版本号，跟JavaBean的版本号不匹配

方法：固定版本号

```java
private static final long serialVersionUID =1L;
```

### 打印流

分类：打印流一般是指：PrintStream，PrintWriter两个类

特点1：打印流只操作文件的目的地

特点2：特有的写出方法可以实现，数据的原样写出

特点3：特有的写出方法，可以实现自动刷新自动换行

#### 字节打印流

| 构造方法                                                     | 说明                         |
| ------------------------------------------------------------ | ---------------------------- |
| public PrintStream(OutputStream/File/String)                 | 关联字节输出流/文件/文件路径 |
| public PrintStream(String fileName, Charset charset)         | 指定字符编码                 |
| public PrintStream(OutputStream out，boolean autoFlush)      | 自动刷新                     |
| public PrintStream(OutputStream out, boolean autoFlush , String encoding) | 指定字符集且自动刷新         |

字符流底层没有缓冲区，开不开自动刷新一样

| 成员方法                                         | 说明                                       |
| ------------------------------------------------ | ------------------------------------------ |
| public void write(int b)                         | 常规方法：规则跟之前一样们将指定字节写出   |
| public void println(Xxx xx)                      | 特有方法：打印任意数据，自动刷新，自动换行 |
| public void print(Xxx xx)                        | 特有方法：打印任意数据，不换行             |
| public void printf(String format,Object... args) | 特有方法：带有占位符的打印语句，不换行     |

#### 字符打印流

| 构造方法                                                     | 说明                         |
| ------------------------------------------------------------ | ---------------------------- |
| public PrintWriter(OutputStream/File/String)                 | 关联字节输出流/文件/文件路径 |
| public PrintWriter(String fileName, Charset charset)         | 指定字符编码                 |
| public PrintWriter(OutputStream out，boolean autoFlush)      | 自动刷新                     |
| public PrintWriter(OutputStream out, boolean autoFlush , String encoding) | 指定字符集且自动刷新         |

| 成员方法                                         | 说明                                       |
| ------------------------------------------------ | ------------------------------------------ |
| public void write(int b)                         | 常规方法：规则跟之前一样们将指定字节写出   |
| public void println(Xxx xx)                      | 特有方法：打印任意数据，自动刷新，自动换行 |
| public void print(Xxx xx)                        | 特有方法：打印任意数据，不换行             |
| public void printf(String format,Object... args) | 特有方法：带有占位符的打印语句，不换行     |

### 解压缩流/压缩流

#### 解压缩流

解压本质：把每一个ZipEntry按照层级拷贝到本地的另一个文件夹

#### 压缩流

压缩本质：把每一个（文件/文件夹）看成ZipEntry对象放到压缩包中

参数一：表示要压缩的文件

参数二：表示压缩包的位置

1. 创建压缩流关联压缩包
2. 创建ZipEntry对象，表示压缩包李米娜每一个文件和文件夹
3. 把ZipEntry对象放进压缩包中
4. 把src文件的数据写进压缩包中

### Commons-io

Commons-io是apache开源基金组织提供的一组有关IO操作的开源工作包

作用：提高IO流的开发效率

#### 使用步骤：

1. 在项目中创建一个文件夹：lib
2. 将jar包复制粘贴到lib文件夹
3. 右键jar包，选择Add as Libary -> 点击OK
4. 在类中导包使用

| FileUtils类（文件/文件夹相关）                               | 说明                       |
| ------------------------------------------------------------ | -------------------------- |
| static void copyFile(File srcFile. File destFile)            | 复制文件                   |
| static void copyDirectory(File srcDir, File destDir)         | 复制文件夹                 |
| static void copyDirectoryToDirectory(File,File destDir)      | 复制文件夹                 |
| static void deleteDirectory(File directory)                  | 删除文件夹                 |
| static String readFileToString(File file,CharSet enconding)  | 读取文件中的数据变成字符串 |
| static void write(File file,CharSequence data,String encoding) | 写出数据                   |

| IOUtils                                                      | 说明       |
| ------------------------------------------------------------ | ---------- |
| public static int copy(InoutStream input, OutputStream output) | 复制文件   |
| public static int copyLarge(Reader input, Writer)            | 复制大文件 |
| public static String readline(Reader input)                  | 读取数据   |
| public static void write(String Data ,OutputStream output)   | 写出数据   |

### Hutool工具包

| 相关类            | 说明                          |
| ----------------- | ----------------------------- |
| IoUtil            | 流操作工具类                  |
| FileUtil          | 文件读写和操作的工具类        |
| FileTypeUtil      | 文件类型判断类                |
| WatchMontior      | 目录、文件监听                |
| ClassPathResource | 针对ClassPath中资源访问的封装 |
| FileReader        | 封装文件读取                  |
| FileWriter        | 封装文件写入                  |

### 综合练习

#### 制造假数据

需求：在各个网络上爬取数据，是其中的一个方法

#### 随机点名器

![image-20250813183918768](images/image-20250813183918768.png)

![image-20250813183936809](images/image-20250813183936809.png)

![image-20250813184016234](images/image-20250813184016234.png)

![image-20250813184027642](images/image-20250813184027642.png)

![image-20250813184145827](images/image-20250813184145827.png)

每个数据的权重占比

#### 登录注册

![image-20250814154216130](images/image-20250814154216130.png)

![image-20250814154241793](images/image-20250814154241793.png)

![image-20250814154258789](images/image-20250814154258789-17551573796851.png)

![image-20250814154317871](images/image-20250814154317871.png)

#### 游戏存档和读档

#### 游戏配置

好处

1. 可以把软件的设置永久化存储
2. 如果我们要修改参数，不需要改动代码，直接修改配置文件就好了

properties是一个双列集合，拥有Map集合所有的特点

重点：有一些特有方法，可以把集合的数据，按照键值对的形式写到配置文件当中

也可以到配置文件中的数据，读取到集合中来

#### 每日一记

## 多线程

### 什么是多线程

#### 线程

线程是操作系统能够进行运算调度的最小单位，它被包含在进程之中，是进程中的实际操作单位

简单理解：应用软件中互相独立，可以同时运行的功能

#### 进程

进程是程序的基本执行实体

#### 应用场景

拷贝、迁移大文件

加载大量资源文件

### 多线程的两个概念

#### 并发与并行

并发：在同一时刻，有多个指令在单个CPU上交替执行

并行：在同一时刻，有多个指令在多个CPU上同时执行

### 多线程的实现方式

#### 继承Thread类的方式实现

1. 自己定义一个类降继承Thread
2. 重写run方法
3. 创建子类的对象，并启动线程

#### 实现Runnable接口的实现方式

1. 自己定义一个类实现Runnable接口
2. 重写里面的run方法
3. 创建自己的类的对象
4. 创建一个Thread类的对象，并开启线程

#### 利用Callable接口和Future接口方式实现

1. 创建一个类实现callable接口
2. 重写call（是有返回值的，表示多线程运行的结果)
3. 创建类的对象（表示多线程要执行的任务）
4. 创建FutureTask的对象（表示管理多线程运行的结果）
5. 创建Thread类的对象，并启动（表示线程）

#### 多线程的三种实现方式对比

|                  | 优点                                       | 缺点                                       |
| ---------------- | ------------------------------------------ | ------------------------------------------ |
| 继承Thread类     | 编程比较简单，可以直接使用Thread类中的方法 | 可以拓展性差，不能再继承其他的类           |
| 实现Runnable接口 | 拓展性强，实现该接口的同时还可以继承其他类 | 编程相对复杂，不能直接使用Thread类中的方法 |
| 实现Callable接口 | 拓展性强，实现该接口的同时还可以继承其他类 | 编程相对复杂，不能直接使用Thread类中的方法 |

### 常见的成员方法

| 方法名称                          | 说明                                   |
| --------------------------------- | -------------------------------------- |
| String getName()                  | 返回此线程的名称                       |
| void serName(String name)         | 设置线程的名字(构造方法也可以设置名字) |
| static Thread currentThread()     | 获取当前线程的对象                     |
| static void sleep(long time)      | 让线程休眠指定的时间，单位为毫秒       |
| setPriority(int newPriority)      | 设置进程优先级                         |
| final int getPriority()           | 获取进程的优先级                       |
| final void setDaemon (boolean on) | 设置为守护进程                         |
| public static void yield()        | 出让线程/礼让线程                      |
| public static void join()         | 插入线程/插队线程                      |

```java
String getName()

void setName(String name)
```

细节：

1. 如果我们没有给线程设置名字时，线程也是有默认名字的

    格式：Thread-X（X是序号，从0开始的）

2. 如果我们要给线程设置名字，可以使用set方法进行设置，也可以使用构造方法设置

```java
static Thread currentThread()
```

细节：

1. 当JVM虚拟机启动之后，会自动启动多条线程，其中有一条线程就叫做main线程，它的作用就是就是调用main方法，并执行里面的代码，在以前，我们写的所有代码，其实都是运行在main线程中

```java
static void sleep(long time)
```

细节：

1. 哪条线程执行到这个方法，那么哪条线程就会在这里停留对应的时间
2. 方法的参数：表示睡眠的时间，单位毫秒
3. 当时间到了之后，线程会自动醒来，继续执行下面的其他代码

```java
setPriority(int newPriority)
final int getPriority()
```

java虚拟机采取抢占式调度，是随机的

```java
final void setDaemon(boolean on)
```

细节：

1. 当其他非守护线程执行完毕后，守护线程会陆续结束

    通俗理解
    女神线程结束后，备胎也没有存在的必要了

```java
public static void yield()
```

```java
public final void join()
```

### 线程安全的问题

#### 线程的生命周期

![image-20250814223904324](images/image-20250814223904324.png)

#### 同步代码块

```java
synchronized(锁){
	操作共享数字的代码
}
```

特点：

1. 锁默认打开，有一个线程进去了，锁自动关闭
2. 里面的代码全部执行完毕，线程出来，锁自动打开

细节：

1. 锁对象是唯一的
2. 共享一个代码

#### 同步方法

就是把synchronized关键字加到方法上

格式

```java
修饰符  synchronized 返回值类型 方法名(方法参数) {...}
```

特点：

1. 同步方法是锁住方法里面所有的代码
2. 锁对象自己不能锁定

方法：

1. 循环
2. 同步代码块
3. 判断共享数据是否到了末尾，如果到了末尾
4. 判断共享数据是否到了末尾，如果没到末尾，执行核心逻辑

#### Lock锁

虽然我们可以理解同步代码和同步方法的锁对象问题，但是我们并没有直接看到哪里加上了锁，在哪里释放了锁，为了更清晰的表达如何加锁和释放锁，JDK5以后提供了一个新的锁对象Lock

Lock实现提供比使用synchronized方法和语句可以获得更广泛的锁定操作，Lock中并提供了获得锁和释放锁的方法

手动上锁、手动释放锁

| 方法          | 作用   |
| ------------- | ------ |
| void lock()   | 获得锁 |
| void unlock() | 释放锁 |

Lock是接口不能直接实例化，这里采用它的实现类ReentrantLock来实例化

ReentrantLock的构造方法

ReentrantLock():创建一个ReentrantLock的实例

### 死锁

### 生产者和消费者

#### 等待唤醒机制

#### 生产者等待机制

#### 常见方法

| 方法名称         | 说明                             |
| ---------------- | -------------------------------- |
| void wait()      | 当前线程等待，直到被其他线程唤醒 |
| void notfy()     | 随即唤醒单个线程                 |
| void notifyAll() | 唤醒所有线程                     |

#### 阻塞队列方式实现

put数据时：放不进去，会等着，也叫做阻塞

take数据时：取出第一个数据，取不到会等着，也叫做阻塞

##### 阻塞队列的继承结构

![image-20250815193844172](images/image-20250815193844172.png)

### 线程状态

![image-20250815194646392](images/image-20250815194646392.png)

![image-20250815194736056](images/image-20250815194736056.png)

### 综合练习

![image-20250815194937149](images/image-20250815194937149.png)

![image-20250815195235130](images/image-20250815195235130.png)

![image-20250815195300942](images/image-20250815195300942.png)

![image-20250815195321226](images/image-20250815195321226.png)

![image-20250815195336551](images/image-20250815195336551.png)

![image-20250815195352197](images/image-20250815195352197.png)

![image-20250815195408727](images/image-20250815195408727.png)

![image-20250815195433238](images/image-20250815195433238.png)

### 线程池

#### 线程池的核心原理 

1. 创建一个池子，池子中是空的
2. 提交任务时，池子会创建新的线程对象，任务执行完毕，线程归还给池子，下回再次提交任务时，不需要创建新的线程，直接复用已有的线程即可
3. 但是如果提交任务时，池子中没有空闲线程，也无法创建新的线程，任务就会排队等待

#### 线程池代码实现

1. 创建线程池
2. 提交任务
3. 所有的任务全部执行完毕，关闭线程池

Executors：线程池的工具类通过调用方法返回不同类型的线程池对象

| 方法名称                                                     | 说明                     |
| ------------------------------------------------------------ | ------------------------ |
| public static ExecutorService newCachedThreadPool()          | 创建一个没有上限的线程池 |
| public static ExecutorService newFixedThreadPool(int nThreads) | 创建有上限的线程池       |

#### 自定义线程池

##### 任务拒绝策略

| 任务拒绝策略                          | 说明                                                   |
| ------------------------------------- | ------------------------------------------------------ |
| ThreadPoolExector.AbortPolicy         | 默认策略：丢弃任务并抛出RejectedExecutionException异常 |
| ThreadPoolExector.DiscardPolicy       | 丢弃任务，但是不抛出异常，这是不推荐的做法             |
| ThreadPoolExector.DiscardOldestPolicy | 抛弃队列中等待最久的任务，然后把当前任务加入队列中     |
| ThreadPoolExector.CallerRunsPolicy    | 调整任务的run()方法绕过线程池直接执行                  |

```java
ThreadPoolExecutor threadPoolExecutor = new ThreadPoolExecutor(核心线程数量,最大线程数,空闲线程最大存活时间,任务队列,创建线程工厂,任务的拒绝策略)
```

1. 核心线程数量
    不能小于0
2. 最大线程数
    不能小于0，最大数量 >= 核心线程数量
3. 空闲线程最大存活时间
    不能小于0
4. 时间单位
    用TimeUnit指定
5. 任务队列
    不能为null
6. 创建线程工厂
    不能为null
7. 任务的拒绝策略
    不能为null

#### 线程池多大合适

![image-20250815220650409](images/image-20250815220650409.png)

![image-20250815215741546](images/image-20250815215741546.png)

## 网络编程

### 什么是网络编程

在网络通信协议下，不同计算不同计算机上运行的程序

- 应用场景：即使通信、网游对战、金融证券、国际贸易、邮件、等等。

不管是什么场景，都是计算机跟计算机之间通过网络进行数据传输

- Java中可以使用java.net包下的技术轻松开发出常见的网络应用程序

#### 常见的软件架构

##### C/S：Client/Server 客户端/服务器

在用户本地需要下载并安装客户端程序，在远程有一个服务器端程序

##### B/S：Browser/Server浏览器/服务器

只需要一个浏览器，用户通过不同的网址。客户访问不同的服务器

##### BS架构优缺点

1. 不需要开发客户端，只需要页面+服务端
2. 用户不需要下载，打开浏览器就能使用
3. 如果应用过大，用户体验就会受影响

##### CS架构的优缺点

1. 画面可以做的很精美，用户体验好
2. 需要开发客户端，也需要开发服务端
3. 用户需要下载和更新的时候太麻烦

### 网络编程三要素

#### IP

全称：Internet Protocol，是互联网协议地址，也称IP地址

是分配给上网设备的数字标签

通俗理解：

上网设备在网络中的地址，是唯一的

##### IPv4

全称：Internet Protocol version 4，互联网通信协议第四版。

有2^32次方个IP

采用32位地址长度，分成4组，点分十进制表示法

##### IPv6

全称：Internet Protocol version 5，互联网通信协议第四版。

有2^128次方个IP

由于互联网的蓬勃发展，IP地址的需求量愈来愈大，而IPv4的模式下的IP的总数量是有限的

采用128位地址长度分为8组，冒分十六进制表示法

##### IPv4细节

IPv4的地址分类形式

- 公网地址（万维网使用）和私有地址（局域网使用）
- 192.168.开头就是私有地址，范围即为192.168.0.0--192.168.255.255，专门位组织机构内部使用，以此节省IP

特殊IP地址

127.0.0.1.也可以是localhost：是回送地址也称本地回环地址，也称本地IP，永远只会寻找当前所在本机

常见CMD命令

- ipconfig：查看本机的IP地址
- ping：检查网络是否联通

InetAddress使用

| 方法                                      | 作用                                                       |
| ----------------------------------------- | ---------------------------------------------------------- |
| static InetAddress getByName(String host) | 确定主机名称的IP地址，主机名称可以是机器名称，也可是IP地址 |
| String getHostName()                      | 获取此IP地址的主机名                                       |
| String getHomeAddress()                   | 返回文本显示中的IP地址字符串                               |

#### 端口号

应用程序在设备中唯一的标识

端口号：由两个字节表示的整数，取值范围：0~65535

其中0~1023之间的端口号用于一些知名的网络服务或者应用

使用1024以上的端口号就可以了 

一个端口号只能被一个应用程序使用

#### 协议

计算机网络中，连接和通信的规则被称为网络通信协议

- OSI参考模型：世界互联协议标准，全球通信规范，单模型过于理想化，未能在因特网上进行广泛推广‘
- TCP/IP参考模型（或TCP/IP协议）：事实上的国际标准

| OSI参考模型 | TCP/IP参考模型  | TCP/IP参考模型各层对应协议      | 面向那些                                                     |
| ----------- | --------------- | ------------------------------- | ------------------------------------------------------------ |
| 应用层      | 应用层          | HTTP、FTP、Telent、DNS          | 一般是应用程序需要关注的。如浏览器、邮箱。程序员一般在这一层开发 |
| 表示层      |                 |                                 |                                                              |
| 会话层      |                 |                                 |                                                              |
| 传输层      | 传输层          | TCP、UDP                        | 选择传输使用的TCP、UDP协议                                   |
| 网络层      | 网络层          | IP、ICMP、ARP                   | 封装自己的IP，对方的IP等信息                                 |
| 数据链路层  | 物理+数据链路层 | 硬件设备。010100101010100101010 | 转换成二进制利用物理设备传输                                 |
| 物理层      |                 |                                 |                                                              |

##### UDP协议

- 用户数据报协议（User Datagram Protocol）

- UDP是面向无连接通信协议。

    速度快，有大小限制一次最多发送64K，数据不安全，易丢失数据

##### TCP协议

- 传输控制协议TCP（Transmission Control Protocol）

- TCP协议是面向连接的通信协议

    速度慢，没有大小限制，数据安全

### UDP通信程序

#### 发送数据

1. 创建发送端DatagramSocket对象
    细节：
    绑定端口，以后我们就是通过端口往外发送
    空参：所有可用的端口中随机一个进行使用
    有参：指定端口号进行绑定
2. 数据打包（DatagramPacket）
3. 发送数据
4. 释放资源

#### 接收数据

1. 创建接收端DatagramSocket对象
    细节：

    在接受数据的时候，一定要绑定端口

    而且绑定的端口一定要跟发送的端口保持一致

2. 接受打包好的数据

3. 解析数据包

4. 解放资源

#### 三种通信方式

1. 单播
    以前的代码就是单播
2. 组播
    组播地址：224.0.0.0~239.255.255.255
    其中224.0.0.0~224.0.0.255为预留的组播地址
3. 广播
    广播地址：255.255.255.255

### TCP通信程序

TCP通信协议是一种可靠的网络协议，他在通信协议的两端各建议一个Socket对象

通信之前要保持连接已经建立

通过Socket产生IO流来网络通信

![image-20250817173641760](images/image-20250817173641760.png)

发送

1. 创建客户端的Socket对象（Socket）与指定服务端连接
    Socket(String host, int port)
    细节：
    在创建对象的同时会连接服务端
    如果连接不上，代码会报错

2. 获取输出流，写数据

    OutputStream getOutputStream()

3. 释放资源
    void close()

接受

1. 创建服务器端的Socket对象(ServerSocket)
    ServerScoket(int port)
2. 监听客户端连接，返回一个Socket对象
    Socket accept()
3. 获取输入流，读数据，并把数据显示在控制台
    InputStream getInputStream()
4. 释放资源
    void close()

#### 三次握手

![image-20250817180012013](images/image-20250817180012013.png)

#### 四次挥手

![image-20250817180155611](images/image-20250817180155611.png)

### 综合练习

![image-20250817180234132](images/image-20250817180234132.png)

![image-20250817180251990](images/image-20250817180251990.png)

![image-20250817180312177](images/image-20250817180312177.png)

![image-20250817180402721](images/image-20250817180402721.png)

![image-20250817180421843](images/image-20250817180421843.png)

![image-20250817180446199](images/image-20250817180446199.png)

![image-20250817180501697](images/image-20250817180501697.png)

![image-20250817180510187](images/image-20250817180510187.png)

## 反射

### 反射的概述

反射允许对成员变量，成员方法和构造方法的信息进行编程访问

![image-20250817190244203](images/image-20250817190244203.png)

### 获取class对象的三种方式

1. Class.forName("全类名");
    全类名：包名+类名

    最为常用

2. 类名.class
    一般更多的是当作参数进行传递

3. 对象.getClass();
    当我们已经有了这个类的对象时，才可以使用

### 利用反射获取构造方法

Class类中用于获取构造方法的方法

Constructor<?>[] getConstructors()：返回所有公共构造方法对象的数组

Constructor<?>[] getDeclaredConstructors()：返回所有构造方法对象的数组

Constructor\<T> getConstructor(Class<?>...parameterTypes)：返回单个公共构造方法对象

Constructor\<T> getDeclaredConstructor(Class<?>...parameterTypes)：返回单个构造方法对象

Constructor类中用于创建对象的方法

T newInstance(Object... initargs)： 根据指定的构造方法创建对象

setAccessible(boolean flag)：设置为true，表示取消访问检查

### 利用反射获取成员变量

Class类中获取成员变量的方法

Field[] getFields()：返回所有公共成员变量的数组

Field[] getDeclaredFields()：返回所有成员变量对象的数组

Field getField(String name)：返回单个成员变量对象

Field getDeclaredField(String name)：返回单个成员变量对象

Field类中用于创建对象的方法

void set(Object obj,Object value)：赋值

Object get(Object obj) 获取值

### 利用反射获取成员方法

Class类中获取成员方法的方法

Method[] getMethods()：返回所有公共成员方法对象的数组，包括继承的

Method[] getDeclaredMethods()：返回所有成员方法对象的数组

Method getMethod(String name,Class<?>...parameterTypes)：返回单个公共成员方法对象

Method getDeclaredMethod(String name,Class<?>...parameterTypes)：返回单个成员方法对象

Method类中用于创建对象的方法

Object invoke(Object obj,Object...args)：运行方法

参数一：用obj对象调用该方法

参数二：调用方法的传递的参数(如果没有就不写)

返回值：方法的返回值(如果没有就不写)

### 反射作用

1. 获取一个类里面所有的信息，获取到了之后，再执行其他业务逻辑
2. 结合配置文件，动态创建对象并调用方法

get：获取

Costructor：构造方法

Field：成员变量

Method：方法

set：设置

Parameter：参数

Modifiers：修饰符

Declared：私有的

## 动态代理

特点：无侵入式的给代码增加额外的功能

将所有被代理的方法定义在接口中

类的作用：创建一个代理

- java.lang.reflect.Proxy类：提供了为对象产生代理对象的方法

```java
public static Object newProxyInstance(ClassLoader loader,Class<?>[] interfaces, InvocationHandler h)
```

参数一：用于指定用哪个类加载器，去加载生产的代理类

参数二：指定接口，这些接口用于指定生成的代理长什么，也就是有哪些方法

参数三：用来指定生成代理对象要干你什么事情
