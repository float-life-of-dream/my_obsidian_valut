[TOC]

# python

## pythonIDE

### pycharm

#### 常用快捷键

CTRL+d复制本行

CTRL+p调用方法，提示类型注解

## 面向对象

### 初识对象



 使用对象组织数据

1. 设计类（class）

			    2.  创建对象
			    2.  对象属性赋值



### 成员变量



类的使用语法：

```python
class 类名称:			
    类的属性
    
	类的行为
```

- class是关键字，表示定义类
- 类的属性，即定义在类中的变量（成员变量）
- 类的行为，即定义在类中的函数（成员方法）



常见类对象的语法：

```python
对象=类名称（）
```



 类中:

- 不仅可以定义属性来记录数据，类中定义的属性，称为：成员变量
- 也可以定义函数，用来记录行为，类中定义的方法，称为：成员方法



成员方法的定义语法:

```python
def 方法名（self,形参1，形参2，......,形参N）
```

self关键字是成员方法定义的时候，必须填写的。

- 它用来表示类对象本身的意思
- 当我们使用类对象调用方法的时，self会自动被python传入
- 在方法内部，想要访问类的成员变量，必须使用self



### 类和对象



面向对象编程就是适用对象进行编程。

设计类，基于类创建对象，并使用对象完成具体工作



### 构造方法



python类可以使用：<u>__</u>init()<u>__</u>方法,称为构造方法

可以实现：

- 在创建类对象（构造类）的时候，会自动实行
- 在创建类对象（构造类）的时候，传入参数自动传递给<u>__</u>init()<u>__</u>方法使用

注意事项：

- 构造方法不要忘记self关键字
- 在方法内使用成员变量需要使用self



### 其他内置方法



<u>__</u>str<u>__</u>字符串方法

当类对象需要被转化为字符串之时，会输出地址

通过<u>__</u>str<u>__</u>方法，控制类转化为字符串的行为

- 方法名：<u>__</u>str<u>__</u>
- 返回值：字符串
- 内容：自行定义



<u>__</u>lt<u>__</u>小于符号比较方法

直接对两个对象进行比较是不可以的，但是在类中实现<u>__</u>lt<u>__</u>方法，同时完成小于符号与大于符号两种比较

- 方法名：<u>__</u>lt<u>__</u>

- 传入参数：other,另一个类对象

- 返回值：True或False

- 内容：自行定义

  

<u>__</u>le<u>__</u>

<u>__</u>le<u>__</u>可用于：<=、>=两种比较运算符上

- 方法名：<u>__</u>le<u>__</u>
- 传入参数：other、另一个·类对象
- 返回值：True或False
- 内容：自行定义



<u>__</u>eq<u>__</u>，比较运算符实现方法

- 方法名：<u>__</u>eq<u>__</u>
- 传入参数：other，另一个类对象
- 返回值：True或False
- 内容：自行定义

不实现<u>__</u>eq<u>__</u>方法，对象之间可以比较，但是是比较内存地址，也即是：不同对象==比较一定是False结果

实现<u>__</u>eq<u>__</u>方法，就可以按照自己的想法决定两个对象是否相等了



### 封装

面向对象的三大特性

基于模板（类）去创建实体（对象），使用对象完成功能开发。

面向对象包含三大特性：

* 封装
* 继承
* 多态



私有成员

类中提供了私有成员的形式来支持

- 私有成员变量
- 私有成员方法

定义私有成员的方式非常简单，只需要：

- 私有成员变量：变量名以__开头（2个下划线)
- 私有成员方法：方法名以__开头（2个下划线)

即可完成私有成员设置



使用私有成员

私有方法无法直接被类对象使用

私有变量无法赋值，也无法获取值

私有成员无法被类对象使用，但可以被其他成员使用



### 继承

#### 继承的基础语法

继承的基础语法

```py
class 类名(父类名):
	类内容体
```



单继承

继承分为单继承与多继承

继承表示：将从父类那里继承（复制）来成员变量和成员方法（不含私有）



多继承

python的类支持多继承，即一个类，可以继承多个父类

```python
class 类名(父类1,......,父类N):
    类内容体
```



多继承的注意事项

多个父类中，如果有同名的成员，那么默认以继承顺序（从左到右）为优先级

即：先继承的保留，后继承的覆盖 

pass是占位语句，用来保证函数（方法）或类定义的完整性，表示无内容，空的意思



#### 复写和使用父类成员

复写

子类继承父类的成员属性和成员方法后，如果对其”不满意“，那么可以进行复写

即：在子类中重新定义同名属性或方法即可



调用父类同名成员

一旦复写父类成员，那么类对象调用成员的时候，就会调用复写后的新成员

如果需要使用被复写的父类成员，需要特殊的调用方式

方式1：

- 调用父类成员

​	使用成员变量：父类名.成员变量

​	使用成员方法：父类名.成员方法（self）

方式2：

- 使用super()调用父类成员

  使用成员变量：super().成员变量

  使用成员方法：super().成员方法()

注意：

只可以在子类内部调用父类的同名成员，子体的实体类对象调用默认是调用子类复写的



### 类型注解

#### 变量的类型注解

类型注解

python在3.5版本的时候引入了类型注解，以方便静态类型检查工具，IDE等第三方工具

类型注解：在代码中设计数据交互的地方，提供数据类型的注解（显示的说明）

主要功能：

- 帮助第三方IDE工具对代码类型进行判断，协助做代码提示
- 帮助开发者自身对变量进行类型注释

支持：

- 变量的类型注解
- 函数（方法）形参列表和返回值类型注解



为变量设置类型注解

基础语法：

```python
变量：类型
```

注意：

- 元组类型设置类型详细注解，需要将每一个元素标记出来
- 字典类型设置类型详细注解，需要两个类型，第一个是Key，第二个是Value



类型注解的语法

语法：

```python
#type:类型
```

在注释中进行类型注解

为变量设置注解，显示变量的定义，一般无需注解：

一般，无法直接看出变量类型只是会添加变量的类型注解

注意： 

类型注解并不会真正的对类型做验证和判断，也就是，类型注解仅仅是提示性的，不是决定性的



#### 函数（方法）的类型注解

形参注释

函数(方法)的类型注解语法：

```python
def 函数方法名(形参名：类型，......):
    pass
```

函数(方法)的返回值也是可以添加类型注解

```python
def 函数方法名(形参：类型，......，形参：类型)->返回值类型：
	pass	
```



#### Union类型

语法：

```python
from typing import Union
	Union[类型,......,类型]
```

定义联合类型注解



### 多态

多态：

多态，指的是：多种状态，即完成某个行为时，使用不同的对象会得到不同的状态

多态常作用在继承关系

比如

- 函数(方法)形参声明接受父类对象
- 实际传入父类的子类对象进行工作

即：

- 以父类做声明定义
- 以子类做实际工作
- 用以获得同一行为，不同状态



抽象类（接口）

父类的同名功能是空实现，含义是：

- 父类用来确定有哪些方法
- 具体的方法实现，由子类自行决定

这种写法，就叫做抽象类（也可称之为接口）

抽象类：含有抽象方法的类称之为抽象类

抽象方法：方法体是空实现的（pass）称之为抽象方法

抽象类就好比定义了一个标准，包含了一些抽象的方法，要求子类必须实现

配合多态，完成

- 抽象的父类设计（设计标准）
- 具体的子类标准（实现标准）



## SQL基础

###  数据库介绍

数据库

数据库就是指数据存储的库，作用就是组织数据并存储数据



数据库组织数据

按照：库->表->数据 三个层级进行组织



数据库软件

数据库软件就是提供库->表->数据，这种数据组织形式的工具软件，也称之为数据库管理系统

常见的数据库软件有：

Oracle，MySQL，SQL sever，PostgreSQL，SQLite，



数据库与SQL的关系

数据库（软件）提供数据组织存储的能力

SQL语句则是操作数据、数据库的工具语言



### MySQL的入门使用

在命令提示符中使用MySQL

打开：命令提示符程序，输入：

```cmd
mysql -u root -p
```

然后再回车后输入密码，即可进入命令行环境

在MySQL命令行环境下，可以通过：

- show databases    查看有那些数据库
- use数据库名           使用某个数据库
- show tables           查看数据库中有那些表
- exit                          退出MySQL命令行环境

等基础命令。



### SQL基础与DDL

SQL语言的分类

由于数据库管理系统（数据库软件）功能非常多，不仅仅是存储数据，还包括数据的管理，表的管理，库的管理，账户管理全乡管理等

操作数据库中SQL语言，也基于功能，可划分为4类：

- 数据定义：DDL
  - 库的创建删除、表的创建删除

- 数据操纵：DML
  - 新增数据、删除数据、修改数据等

- 数据控制：DCL
  - 新增用户、删除用户、密码修改、权限管理

- 数据查询：DQL
  - 基于需求查询和计算数据



SQL语法特征

- SQL语言，大小写不敏感
- SQL可以单行或多行书写，最后以;号结束
- SQL支持注释：
  - 单行注释：-- 注释内容（--后一定有一个空格）
  - 单行注释：# 注释内容（#后面可以不加空格，推荐加上）
  - 多行注释：/* 注释内容 */



DDL-库管理

查看数据库

``` mysql
SHOW DATABASE;
```

使用数据库

``` mysql
USE 数据库名称;
```

创建数据库

``` mysql
CREATE DATABASE 数据库名称 [CHARST UTF8];
```

删除数据库

``` mysql
DROP DATABASE 数据库名称;
```

查看当前使用数据库

``` mysql
SELECT DATABASE();
```



DDL-表管理

查看有那些表

```mysql
SHOW TABLES;
```

注意：需要先选择数据库

删除表

```mysql
DROP TABLE 表名称;
DROP TABLE IF EXISTS 表名称;
```

创建表

``` mysql
CREATE TABLE 表名称（
	列名称 列类型,
	列名称 列类型,
	......
);
```



### SQL-DML

DML

DML是指数据操作语言，英语全称是Data Manipulation Language,用来对数据库中表的数据记录进行更新

关键字：

- 插入INSERT
- 删除DELETE
- 更新UPDATE



数据插入 INSERT

基础语法：

```mysql
INSERT INTO 表[(列1，列2，......，列N)] VALUES(值1，值2，......，值N)[,(值1，值2，......，值N)，......，(值1，值2，......，值N)]
```



数据删除

基础语法：

```mysql
DELETE FROM 表名称 [WHERE 条件判断]
```

条件判断：列 操作符 值

操作符：= < > <= >= !=



数据更新

基础语法

```mysql
UPDATE 表名 SET 列=值 [WHERE 条件判断];
```



注意事项

字符串的值，出现在SQL语句中，必须用单引号包围起来



### SQL-DQL

#### 基础查询

基础数据查询

在SQL中，通过SELECT关键字开头的SQL语句，来进行数据的查询

基础语法：

```mysql
SELECT 字段列表|* FROM 表
```

含义就是：

从（FROM）表中，选择（SELECT）某些列进行展示



基础数据查询-过滤

```mysql
SELECT 字段列表|* FROM 表 WHERE 条件判断
```



#### 分组聚合

分组聚合场景：

- 特征分组
- 处理数据

基础语法：

```mysql
SELECT 字段|聚合函数 FROM 表 [WHERE 条件]GROUP BY 列
聚合函数有：
- SUM(列) 求和
- AVG(列) 求平均值
- MIN(列) 求最小值
- MAX(列) 求最小值
- COUNT(列|*) 求数量
```

注意：

GROUP BY中出现了那个列，那个列才能出现在SELECT中的非聚合中



#### 排序分页

结果排序

可以对查询的结果，使用ORDER BY 关键字，指定某个列进行排序，语法：

``` mysql
SELECT 列|聚合函数|* FROM 表
WHERE ...
GROUP  BY ...
ORDER  BY ... [ASC| DESC]
```



结果分页限制

同样，可以使用LIMIT关键字，对查询结果进行限制或分页显示，语法：

```mysql
SELECT 列|聚合函数|* FROM 表
WHERE ...
GROUP  BY ...
ORDER  BY ... [ASC| DESC]
LIMIT  n[,m]
```



注意：

- WHERE、GROUP BY、OREDER BY、LIMIT均可按要求省略
- SELECT和FROM是必写的
- 执行顺序：

​		FROM->WHERE->GROUP BY 和聚合函数->SELECT->ORDER BY ->LIMIT



### Python & MySQL

#### 基础使用

pymysql

可以使用编程语言来执行SQL从而操作数据库

Python中使用第三方库：pymysql来完成对MySQL数据库的操作

安装：

``` cmd
pip install pymysql
```



创建到MySQL的数据库链接

代码如下：
```python
from pymysql import Connection
#获取数据库链接对象
conn = Connection(
	host='localhost',	#主机名（或IP地址）
	port=3306,			#端口，默认3306
	user='root',		#账户名
    password=''			#密码
)
#打印MySQL数据库软件信息
print(conn.get_server_info())
#关闭到数据库的链接
conn.close()
```



执行SQL语句

执行非查询性质的SQL语句：

```python
from pymysql import Connection
#获取数据库链接对象
conn = Connection(
	host='localhost',	#主机名（或IP地址）
	port=3306,			#端口，默认3306
	user='root',		#账户名
    password=''			#密码
)
#获取游标对象
cursor = conn.cursor()
conn.select_db("test")	#先选择数据库
#使用游标对象，执行sql语句
cursor.excute("CREATE TABLE test_pymysql(id INT, info VARCHAR(255))")
#关闭到数据库的链接
conn.close()
```

执行查询性质的SQL语句：

```python
from pymysql import Connection
#获取数据库链接对象
conn = Connection(
	host='localhost',	#主机名（或IP地址）
	port=3306,			#端口，默认3306
	user='root',		#账户名
    password=''			#密码
)
#获取游标对象
cursor = conn.cursor()
conn.select_db("test")	#先选择数据库
#使用游标对象，执行sql语句
cursor.excute("SELECT * FROM student")
#获取查询结果
result: tuple= cursor.fetchall()
for r in results:
    print(r)
#关闭到数据库的链接
conn.close()
```

通过连接对象调用cursor()方法，得到游标对象

- 游标对象.execute()执行SQL语句
- 游标对象.fetchall()得到全部查询结果封装入元组内



#### 数据插入

commit提交

pymysql在执行数据插入或其他产生数据更改的SQL语句时,默认时需要提交更改的，即需要通过代码"确认"这种更改行为。

通过链接对象.commit()即可确认此行为



自动提交

```python
#获取数据库链接对象
conn = Connection(
	host='localhost',	#主机名（或IP地址）
	port=3306,			#端口，默认3306
	user='root',		#账户名
    password=''			#密码
    aurocommit=TRUE		#设置自动提交
)
```



## Pyspark

### spark与pyspark

spark

spark是Apache基金会旗下顶级的开源项目，用于对海量数据进行分布式计算

 

Pyspark

Pyspark是spark的python实现，是spark为python开发者提供的编程入口，用于以python代码完成spark任务开发

pyspark不仅可以作为python的第三方库使用，也可以将程序提交的Spark集群环境中，调度大规模集群进行执行



### 基础准备

Pyspark库的安装

```cmd
pip install pyspark
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple pyspark
```



构建Pyspark执行环境入口对象

想要使用Pyspark库完成数据处理，首先要构造一个执行环境入口的对象

Pyspark的执行环境入口对象是：类SparkContext的类对象

```python
#导包
from pyspark import SparkConf,SparkContext

#创建SparkConf类对象
conf=SparkConf().setMaster("local[*]").\setAppName("test_spark_app")
#基于SparkConf类对象创建SparkContext类对象
sc= SparkContext(conf=conf)

#打印Pyspark的运送版本
print(sc.version)

#停止SparkContext对象的运行(停止PySpark程序)
sc.stop()
```



Pyspark的编程模型是

- 数据输入：通过SparkContext完成数据读取
- 数据计算：读取到的数据转化为RDD对象，调用RDD成员方法完成计算
- 数据输出：调用RDD的数据输出相关成员方法，将结果输出到list，原则，字典，文本文件，数据库等

 ### 数据输入

RDD对象

Pyspark支持多种数据的输入，在输入完成后，都会得到一个RDD类的对象

RDD全称弹性分布式数据集(Resilient Distributed Datasets)

Pyspark针对数据的处理，都啊hi以RDD对象作为载体，即：

- 数据存储在RDD中
- 各类数据的计算方法，也都是RDD的成员方法
- RDD的数据计算方法，返回值依旧是RDD对象 



python数据容器转RDD对象

Pyspark支持通过SparkCOntext对象的parallelize将：

- list
- tuple
- set
- dict
- str

转化为Pyspark的RDD对象

语法：

```python
from pyspark import SparkConf ,Sparkcontext
conf= SparkConf().setMaster("local[*]").\setAppName("test_spark_app")
sc=SparkContext(conf=conf)

sdd= sc.parallelize(数据容器对象)

#输出RDD对象
print(rdd.collect())
```

注意：

- 字符串会被拆分成一个个的字符，存入RDD对象
- 字典经由Key会被存入RDD对象



读取文件转RDD对象

Pyspark支持通过SparkContect入口对象，来读取对象，来构建出RDD对象

```python
from pyspark import SparkConf ,Sparkcontext

conf= SparkConf().setMaster("local[*]").\setAppName("test_spark_app")
sc=SparkContext(conf=conf)

sdd= sc.textfile(文件路径)

#输出RDD对象
print(rdd.collect())
```



### 数据计算

#### map方法

map方法

Pyspark的数据计算依赖，RDD对象内置丰富的：成员方法(算子)



map算子

是将RDD数据一条条处理（处理的逻辑基于map算子接受的处理函数），返回新的RDD

- 接受一个处理函数，可用lambda表达式快速缩写
- 对RDD内的元素逐个处理，并返回一个新的RDD

```python
rdd.map(func)
# func: f(T) ->U
#f: 表示这是一个函数（方法）
# (T) -> U 表示的是方法的定义：
#  () 表示传入参数， (T)表示传入一个参数， () 表示没有传入参数
# T U 都是反省的代称，在这里表示任意类型

#-> U 表示返回值

#(T) -> U 总结起来的意思是：这是一个方法，这个方法接受一个参数传入，传入参数类型不限，返回一个返回值，返回值的类型不同

#(A) -> A 总结起来的意思是：这是一个方法。这个方法接受一个参数传入，传入参数类型不限，返回一个返回值，返回值和传入参数类型一致
```



链式调用

对于返回值是新的RDD算子，可以通过链式调用大的方法多次调用算子



#### flatMap方法

flatMap算子

功能：对RDD执行map操作，然后进行接触嵌套操作

演示代码

```python
#coding:utf8
#演示rdd的flatMap算子

from pyspark import SparkConf， SparkContext、

if __name__ == '__main__':
    #构建Spark执行环境
    conf = SparkConf().setAppName("create rdd").\setMaster("local[*]")
    sc= SparkContext(conf=conf)
    
    rdd=sc.parallelize(嵌套数据容器)
    
    #按照空格切分数据，接触嵌套
    print(rdd.flatMap(lambda x: x.split(" ")).collect())
```



#### reduceByKey方法

reduceByKey算子

功能：针对KV型RDD，自动按照key分组，然后根据你提供的聚合逻辑，完成组内数据（value)的聚合操作

用法：\

```python
rdd.reduceByKey(func)
# function：(V,V)-> V
# 接受2个传入参数(类型要一致)，返回一个类型值，类型和传入要求一致
```

代码

```py
rdd=sc.parallelize(ky型数据容器)
result=rdd.reduceByKey(func)
print(result.collect())
```

注意：reduceByKey中接受的函数，只负责聚合，不理会分组

分组是自动by key来分组



#### filter方法

功能：过滤想要的数据进行保留

语法

```python
rdd.filiter(func)
# func:(T) -> bool 传入一个参数来随意类型，返回值必须是True or False
```

返回是True的数据被保留，False数据丢弃



#### distinct方法

distinct算子

功能：对RDD数据进行去重，返回新的RDD

语法：

``` python
rdd.distinct() #无需传参
```



#### Sortby方法

sortBy算子

功能：对RDD数据进行排序，基于你指定的排序依据

语法：

```python
rdd.sortBy(func, ascending=False,numPartitions=1)
# func:(T) -> U:告知按照rdd中的那个数据进行排序，比如 lambda x:x[1] 表示按照rdd中第二列元素进行排序
#ascending True升序 False降序
#numPartitons:用多少分区排序
```

全局排序需要设置分区数为1



### 数据输出

#### 输出为Python对象

collect算子

功能：

将RDD各个分区内的数据，统一收集到Driver中，形成一个list对象

用法：
rdd.collect()

返回值是一个列表



reduce算子

功能：

对RDD数据集按照你传入的逻辑进行聚合

语法：

```python
rdd.reduce(func)
#func(T,T)->T
#2参数传入一个返回值，返回值与参数要求类型一致
```

返回值等同于计算函数的返回值



take算子

功能：取出RDD的前N个元素，组合成list返回给你



count算子

功能：计算RDD有多少条数据，返回值是一个数字



#### 输出为文件对象

功能：将RDD数据写入文本文件

支持本地写出，hdfs等文件系统



## Python高阶技巧

### 闭包

闭包

定义双层嵌套函数，内层函数可以访问外层函数的变量

将内层函数作为外层函数的返回，此内层函数就是闭包函数

在前腰函数的前提下，内部函数使用了外部函数的变量，并且外部函数返回了内部函数，我们把这个使用外部函数变量的内部函数称为闭包

修改外部函数变量的值

需要使用nonlocal关键字修饰外部函数的变量才可以在内部函数中修改它

注意事项

优点,使用闭包可以得到：

- 无需定义全局变量即可实现通过函数，持续的访问，修改某个值
- 闭包使用的变量的所用于在函数内，难以被错误的调用修改

缺点：

- 由于内部函数持续引用外部函数的值，所以会导致者一部分内存空间不被释放，一致占用内存



nonloacl关键字作用

在闭包函数(或内部函数中)想要修改外部函数的变量值

需要用nonlocal声明这个外部变量



### 装饰器

装饰器

在不破坏目标函数原有的代码和功能的前提下，为目标函数增加新功能



装饰器的一般写法

定义一个闭包函数,在闭包函数内部：

- 执行目标函数
- 并完成功能的添加

语法糖写法：

使用@outer

定义在目标函数的sleep之上



### 设计模式

#### 单例模式

单例模式

单例模式是一种常见的软件的设计模式，该模式的主要目的是确保某一个类只有一个实例存在

在整个系统中，某个类只能出现一个实例时，单例对象就能派上用场

- 定义：保证一个类中只有一个实例，并提供一个访问它的全局访问点
- 使用场景：当一个类只有一个实例，而客户可以从一个众所周知的访问的访问它时

单例的实现模式：

```python
class StrTolls:
    pass

str_tool=StrTools()
```

在一个文件中定义如上代码

```python
from test import str_tool

s1=str_tool
s2=str_tool
```

在另一个文件中导入对象



### 工厂模式

工厂模式

当需要常见大量一个类的实例的时候，可以使用工厂模式

特点：

- 使用工厂类的get_person()方法去创建具体类对象

优点：

- 大批量创建对象的时候有统一的入口，易于代码维护
- 当发生修改时，仅修改工厂类的创建方法
- 符合现实世界的模式，即由工厂来制作产品（对象）



### 多线程

#### 进程、线程和并行执行

进程、线程

进程：就是一个程序，运行在系统之上，那么便称之这个程序为一个运行进程，并分配ID方便系统管理

线程：线程时归属于进程的，一个进程可以开启多个线程，执行不同的工作，是进程的实际工作最小单位

操作上系统中可以运行多个进程，即多任务运行

一个进程内可以运行多个线程，即多线程运行

注意点：

进程之间是内存隔离的

相乘之间是内存共享的



并行执行

同一时间做不同的工作

多任务并行执行

多线程并行执行



#### 多线程编程

python的多线程通过threading模块实现

```python
import threading

thread_obj = threading.Thread([group[,target[,name[,args[,kwargs]]]]])
- group:暂时无用，未来功能的预留参数
- target:执行目标任务名
- args:以元组的方式给执行任务传参
- kwargs:以字典的方式给执行任务传参
- name:线程名，一般不用设置

#启动线程，让线程开始工作
rhread_obj.start()
```



### 网络编程

#### 服务端开发

Socket

Socket（简称套接字）是进程之间通信的一个工具，进程间通信需要Socket

Socket负责进程间网络数据传输



客户端与服务端

2个进程通过Socket进行相互通讯，就必须有服务端与客户端

Socket服务端：等待其他进程的连接、可接受发来的信息、可以回复消息

Socket客户端：主动连接服务端、可以发送消息、可以接受回复



Socket服务端编程

主要分为如下几个步骤：

1.创建Socket对象

```python
import socket
socket_server = socket.socket()
```

2.绑定socket_server到指定IP和地址

```python
socket_server。bind(host,port)
```

3.服务端开始监听接口

```python
socket_server.listen(backlog)
# backlog为int整数，表示允许连接的数量，超出的会等待，可以不填，不填会自动设置一个合理值
```

4.接受客户端连接，活得连接对象

```python
conn, address = socket_server.accept()
print(f"接受到客户端连接，连接来自：{address}")
# accept方法是阻塞方法，如果没有连接，会卡在对当前这一行不向下执行代码
# accept返回的是一个二元元组，可以使用上述形式，用两个变量接受二元元组的两个元素
```

5.客户端连接后通过recv方法，接受客户端发送的信息

```python
while True：
	data=conn.recv(1024).decode("UTF-8")
    # recv方法的返回值是字节数组（Bytes），可以通过decode使用UTF-8解码为字符串
    # recv方法的传参是buffsize，缓冲区大小，一般设置为1024即可
    if data == 'exit':
        break
    print("接收发送到的数据："，data)
# 可以通过while True无限循环来持续和客户端进行数据交互
# 可以通过判定客户端发来的特殊标记，如exit，来退出无限循环
```

6.通过conn（客户端当次连接对象），调用send方法可以回复消息

```python
	conn.send("你好呀哈哈哈".encode("UTF-8"))
```

7.conn(客户端当次连接对象)和socket_server对象调用close方法，关闭连接

 

#### 客户端开发

1.创建socket对象

```python
import socket
socket_client = socket.socket()
```

2.连接到服务端

```python
socket_client.connect(("localhost",8888))
```

3.发送消息

```python
while True:		#可以无限循环确保持续发送消息给服务端
    send_msg = input("请输入要发送的信息")
    if send_msg == 'exit':
        # 通过特殊标记确保可以推出无限循环
        break
    socket_client.send(send_msg.encode("UTF-8"))		#消息需要编码为字节数组（UTF-8编码）
```

4.接受返回消息

```python
while True :
    send_msg=input("请输入要发送的消息").encode("UTF-8")
    socket_client.send(send_msg)
    
    recv_data=socket_client.recv(1024)		#1024是缓冲区大小，一般1024即可
    # recv方法是阻塞式的，即不接受到返回，就卡在这里等待
    print("服务端回复消息为：",recv_data.decode("UTF-8"))	#接受消息需要通过UTF-8解码为字符串
```

5.关闭连接

```python
socket_client.close()	#最后通过close关闭连接
```



###  正则表达式

#### 基础使用

 正则表达式

正则表达式又称规则表达式，使用单个字符串来描述，匹配某个句法规则的字符串，常被用来检索，替换那些符合某个模式（规则）的文本

简单来说，正则表达式就是使用：字符串定义规则，并通过规则去验证字符串是否匹配



正则三个基础方法

python中的正则表达式,使用re模块，并给予re模块的三个基础方法做匹配

分别是：match、search、findall三个基础方法

- re.match(匹配规则,被匹配字符串)

从被匹配字符串开头进行匹配，匹配成功返回匹配对象(包含匹配信息)，匹配不成功返回空

- re.search(匹配规则,被匹配字符串)

搜索整个字符串，找出匹配的。从前向后，找到第一个后，就停止，不会继续向后

整个字符串找不到，返回None

- re.findall(匹配规则，被匹配字符串)

匹配整个字符串，找出全部匹配项

找不到返回空list：[]



#### 元字符匹配

元字符匹配

| 字符 | 功能                                     |
| ---- | ---------------------------------------- |
| .    | 匹配任意一个字符（除了\n）,\\.匹配点本身 |
| []   | 匹配[]中列举的字符                       |
| \d   | 匹配数字，即0-9                          |
| \D   | 匹配非数字                               |
| \s   | 匹配空白，即空格、tab键                  |
| \S   | 匹配非空白                               |
| \w   | 匹配单词字符，即a-z、A-Z、0-9、_         |
| \W   | 匹配非单词字符                           |

字符串的r标记，表示当前字符串是原始字符串，即内部的转移字符串无效而是普通字符串

[]内可以写:[a-zA-Z0-9]这三种范围组合或指定字符

数量匹配

| 字符  | 功能                            |
| ----- | ------------------------------- |
| *     | 匹配前一个规则字符出现0至无数次 |
| +     | 匹配前一个规则字符出现1至无数次 |
| ？    | 匹配前一个规则字符出现0至1次    |
| {m}   | 匹配前一个规则字符出现m次       |
| {m,}  | 匹配前一个规则字符至少m次       |
| {m,n} | 匹配前一个规则字符出现m次到n次  |

边界匹配

| 字符 | 功能               |
| ---- | ------------------ |
| ^    | 匹配字符串开头     |
| $    | 匹配字符串结尾     |
| \b   | 匹配一个单词的边界 |
| \B   | 匹配非单词边界     |

分组匹配

| 字符 | 功能                       |
| ---- | -------------------------- |
| \|   | 匹配左右任意一个表达式     |
| ()   | 将括号中的字符作为一个分组 |



### 递归

递归

递归在编程中是一种非常重要的算法

递归：即方法（函数）自己调用自己的一种特殊编程写法

```python
def func():
    if ……:
        func()
    return ……
```



注意

- 退出的条件，否则容易变成无限递归
- 注意返回值的传递，确保从最内层，层层传递到最外层



os模块的使用方法

- os.listdir列出目录下的指定内容
- os.path.isdir,判断给定路径是否是文件夹，是返回True，否返回False
- os.path.exists,判断给定路径是否存在，是返回True，否返回False 
