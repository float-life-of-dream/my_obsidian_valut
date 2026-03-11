[TOC]

# MySQL

## 基础篇

### MySQL概述

#### 数据库相关概念

| 名称           | 全称                                                         | 简称                                |
| -------------- | ------------------------------------------------------------ | ----------------------------------- |
| 数据库         | 存储数据的仓库，数据是有组织的进行存储                       | DataBase（DB）                      |
| 数据库管理系统 | 操纵和管理数据库的大型软件                                   | DataBase Management System （DBMS） |
| SQL            | 操作关系型数据库的编程语言，定义了一套操作关系型数据库统一标准 | Structured Query Language（SQL）    |

- 主流的关系型数据库管理系统
  - Oracle
  - MySQL
  - Microsoft SQL Server
  - PostgreSQL

#### MySQL数据库

MySQL提供两种版本：社区版与商业版

- 启动与停止

  - 启动

    ```cmd
    net start mysql80
    ```

  - 停止

    ```cmd
    net stop mysql80
    ```

- 客户端连接

  - 方式一：使用MySQL提供的命令行工具

  - 方式二：系统中自带命令行工具执行指令

    ```cmd
    mysql [-h 127.0.0.1] [-p 3306] -u root -p
    ```

    ```
    mysql -u root -p
    ```
    
    注意：使用这种方式是，需要配置PATH环境变量

#### 数据模型

- 关系型数据库（RDBMS）

概念：建立在关系模型基础上，由多张相互连接的二维表组成的数据库。

特点：

1. 使用表存储数据，格式统一，便于维护
2. 使用SQL语言操作，标准统一，使用方便

包括数据库与表

#### 图形化工具——Datagrip



### SQL

#### SQL的通用语法

1. SQL语句可以单行或多行书写以分号结尾
2. SQL语句可以使用空格/缩进来增强语句的可读性
3. MYSQL数据库的SQL语句不区分大小写，关键字建议大写
4. 注释：
    - 单行注释：--注释内容或#注释内容（MySQL特有）
    - 多行注释：/*注释内容\*/

#### SQL语句分类

| 分类 | 全称                       | 说明                                                   |
| ---- | -------------------------- | ------------------------------------------------------ |
| DDL  | Data Definition Language   | 数据定义语言，用来定义数据对象（数据库、表、字段）     |
| DML  | Data Manipulation Language | 数据操作语言、用来对数据库中的数据进行增删改           |
| DQL  | Data Query Language        | 数据查询语言，用来查询数据库中表的记录                 |
| DCL  | Data Control Language      | 数据控制语言，用来创建数据库用户、控制数据库的访问权限 |

#### DDL

- DDL-数据库操作

    - 查询

        查询所有数据库

        ```sql
        SHOW DATABASES;
        ```

        查询当前数据库

        ```sql
        SELECT DATABASE();
        ```

    - 创建

        ```sql
        CREATE DATABASE [IF NOT EXISTS]数据库名 [DEFAULT CHARSET 字符集][COLLATE 排序规则];
        ```

        推荐字符集使用`utf8mb4`

    - 删除

        ```sql
        DROP DATABASE[IF EXISTS] 数据库名;
        ```

    - 使用

        ```sql
        USE 数据库名
        ```

- DDL-表操作-查询

    - 查询当前数据库所有表

        ```sql
        SHOW TABLES;
        ```

    - 查询表结构

        ```sql
        DESC 表名;
        ```

    - 查询指定表的建表语句

        ```sql
        SHOW CREATE TABLE 表名称
        ```

- DDL-表操作-创建

    - 创建

        ```sql
        CREATE TABLE 表明(
        	字段1 字段1类型[COMMENT 字段1注释],
            字段2 字段2类型[COMMENT 字段2注释],
        	字段3 字段3类型[COMMENT 字段3注释],
        	……
        	字段n 字段n类型[COMMENT 字段n注释]
        )[COMMENT 表注释];
        ```

        注意：[……]为可选参数，最后一个字段后面没有逗号

- DDL-表操作-数据类型

    MySQL中的数据类型有很多，主要分为三类：数值类型、字符串类型、日期时间类型

    - 数值类型

        | 类型         |大小| 有符号（SIGNED）范围 | 无符号（UNSIGNED）范围 | 描述 |
        | ------------ |------	 |-------------------- | ---------------------- | ---- |
        | TINYINT      | 1 byte | (-128,127) | (0,255) |小整数值|
        | SMALLINT     | 2 bytes | (-32768,32767) | (0,65535) |大整数值|
        | MEDIUMINT    | 3 bytes | (-8388608,8388607) | (0,16777215) |大整数值|
        | INT或INTEGER | 4 bytes | (-2147483648,21747483647) | (0,4294967295) |大整数值|
        | BIGINT       | 8 bytes | (-2^63,2^63-1) | (0,2^64-1) |极大整数值|
        | FLOAT        | 4 bytes | (-3.402823466 E-38,-3.402823466351 E+38) | 0和(1.175494351E-38,-3.402823466351 E+38) |单精度浮点数值|
        | DOUBLE       | 8 bytes | (-1.797E-308，1.797E308) | 0和（2.225E-308，1.797E+308） |双精度浮点数值|
        | DECIMAL      |  | 依赖于M（精度）和D（标度）的值 | 依赖于M（精度）和D（标度）的值 |小数值（）|

        精度值表示整个长度

        标度值表示小数点后长度

    - 字符串类型

        | 类型       | 大小              | 描述                        |
        | ---------- | ----------------- | --------------------------- |
        | CHAR       | 0-255 bytes       | 定长字符串                  |
        | VARCHAR    | 0-65535bytes      | 变长字符串                  |
        | TINYBLOB   | 0-255bytes        | 不超过255个字符的二进制数据 |
        | TINYTEXT   | 0-255bytes        | 短文本字符串                |
        | BLOB       | 0-65535bytes      | 二进制形式长文本数据        |
        | TEXT       | 0-65535bytes      | 长文本数据                  |
        | MEDIUMBLOB | 0-16777215bytes   | 二进制形式中等长度文本数据  |
        | MEDIUMTEXT | 0-16777215bytes   | 中等长度文本数据            |
        | LONGBLOB   | 0-4294967295bytes | 二进制形式的极大文本数据    |
        | LONGTEXT   | 0-4294967295bytes | 极大文本数据                |
    
    - 日期时间类型
    
      | 类型      | 大小 | 范围                                       | 格式                | 描述                     |
      | --------- | ---- | ------------------------------------------ | ------------------- | ------------------------ |
      | DATE      | 3    | 1000-01-01至 9999-12-31                    | YYYY-MM-DD          | 日期值                   |
      | TIME      | 3    | -838:59:59至838:59:59                      | HH:MM:SS            | 时间值或持续时间         |
      | YEAR      | 1    | 1901至2155                                 | YYYY                | 年份值                   |
      | DATETIME  | 8    | 1000-01-01 00:00:00 至 9999-12-31 23:59:59 | YYYY-MM-DD HH:MM:SS | 混合日期和是兼职         |
      | TIMESTAMP | 4    | 1970-01-01 00:00:01 至 2038-01-19 03:14:07 | YYYY-MM-DD HH:MM:SS | 混合日期和时间值、时间戳 |
    
- 例：设计员工信息表

    设计一张员工信息表，要求如下：

    1. 编号（纯数字）
    2. 员工工号（字符串类型，长度不超过10位）
    3. 员工姓名（字符串类型，长度不超过10位）
    4. 性别（男/女，存储一个汉字）
    5. 年龄（正常人年龄，不可能存负数）
    6. 身份证号（二代身份证号均为18位，身份证中有X的字符）
    7. 入职年月（输入年月日即可）

    ```sql
    create table emp{
    	id int comment "编号",
    	workno varchar(10) comment "工号",
        name varchar(10) comment "姓名",
        gender char(1) comment "性别",
        age tinyint unsigned comment "年龄",
        idcard char(18) comment "身份证号"，
        entrydate date comment "特质时间"
    }comment '员工表';
    ```

- DDL-表操作-修改

    - 添加字段

        ```sql
        ALTER TABLE 表名 ADD 字段名 类型(长度) [COMMENT 注释][约束];
        ```

    - 修改数据类型

        ```sql
        ALTER TABLE 表名 MODIFY 字段名 新数据类型(长度);
        ```

    - 修改字段名和字段类型

        ```sql
        ALTER TABLE 表名 CHANGE 旧字段名 新字段名 类型(长度) [COMMENT 注释] [约束];
        ```

        例：

        将emp表中nickname修改位username，类型为varchar(30)

        ```sql
        ALTER TABLE emp CHANGE nicname username varchar(30) COMMENT "昵称";
        ```

    - 删除字段

        ```sql
        ALTER TABLE 表名 DROP 字段名;
        ```

        例：

        将emp表的字段username删除

        ```sql
        ALTER TABLE emp DROP username;
        ```

    - 修改表名

        ```sql
        ALTER TABLE 表名 RENAME TO 新表名;
        ```

        例：

        将emp表的表名修改为emploee

        ```sql
        ALTER TABLE emp RENAME TO employee;
        ```

- DDL-表操作-删除

    - 删除表

        ```sql
        DROP TABLE [IF EXISTS] 表名;
        ```

    - 删除指定表, 并重新创建该表

        ```sql
        TRUNCATE TABLE 表名;
        ```

        注意：删除表时，表中的数据也会被删除


#### DML

- 介绍

    DML英文全称是Data Manipulation Language（数据操作语言），用来对数据库中表的数据记录进行增删改的操作

    - 添加数据（INSERT）
    - 修改数据（UPDATE）
    - 删除数据（DELETE）

- 添加数据

    - 给指定字段添加数据

        ```sql
        INSERT INTO 表名(字段名1，字段名2，……)VALUES(值1，值2，……);
        ```

    - 给全部字段添加数据

        ```sql
        INSERT INTO 表名 VALUES(值1，值2，……);
        ```

    - 批量添加数据

        ```sql
        INSERT INTO 表名(字段名1,字段名2,……)VALUES(值1,值2,……)(值1,值2,……)(值1,值2,……);
        ```

        ```sql
        INSERT INTO 表名 VALUES (值1,值2,……),(值1,值2,……),(值1,值2,……);
        ```

        - 注意

    		- 插入数据时，指定的字段顺序要与值得顺序是一一对应的
- 字符串和日期型数据应该包含在引号中
    		- 插入的数据的大小，应该在字段的规定范围内

- 修改数据

    - 修改数据

        ```sql
        UPDATE 表名 SET 字段名1=值1,字段名2=值2,...[WHERE 条件];
        ```

        注意：修改语句的条件可以有，也可以没有，如果没有条件，则会修改整张表的所有数据

- 删除数据

    - 删除数据

        ```sql
        DELETE FROM 表名 [WHERE 条件]
        ```

        注意：

        - DELETE语句可以有，也可以没有，如果没有条件，会删除整张表的所有数据
        - DELETE语句不能删除某一个字段的值（可以使用UPDATE）

#### DQL

- DQL-介绍

    DQL的英文全称是Data Query Language（数据查询语言），数据查询语言，用来查询数据库中表的记录。

    查询关键字：SELECT

- DQL-语法

    ```SQL
    SELECT 
    		字段列表
    FROM	
    		表名列表
    WHERE	
    		条件列表
    GROUP BY	
    		分组字段列表
    HAVING	
    		分组后条件列表
    ORDER BY	
    		排序字段列表
    LIMIT
    		分页参数
    ```

    - 基本查询
    - 条件查询（WHERE）
    - 聚合函数（count、max、min、avg、sum）
    - 分组查询（GROUP BY）
    - 排序查询（ORDER BY）
    - 分页查询（LIMIT）

- DQL-基本查询

    1. 查询多个字段

        ```sql
        SELECT 字段1,字段2,字段3,…… FROM 表名;
        ```

        ```sql
        SELECT * FROM表名 ;
        ```

    2. 设置别名

        ```sql
        SELECT 字段1 [AS 别名1],字段2 [AS 别名2]…… FROM 表名;
        ```

    3. 去除重复记录

        ```sql
        SELECT DISTINCT FROM 表名;
        ```

- DQL-条件查询

    1. 语法

        ```sql
        SELECT 字段列表 FROM 表名 WHERE 条件列表
        ```

    2. 条件

        | 比较运算符       | 功能                                     |
        | ---------------- | ---------------------------------------- |
        | >                | 大于                                     |
        | >=               | 大于等于                                 |
        | <                | 小于                                     |
        | <=               | 小于等于                                 |
        | =                | 等于                                     |
        | <>或!=           | 不等于                                   |
        | BETWEEN...AND... | 在某个范围之内(感最小、最大值)           |
        | IN(...)          | 在in之后的列表中的值多选一               |
        | LIKE 占位符      | 模糊匹配(_排配单个字符，%匹配任意个字符) |
        | IS NULL          | 是NULL                                   |
        | AND 或 &&        | 并且（多个条件同时成立）                 |
        | OR 或 \|\|       | 或者（多个条件任意一个成立）             |
        | NOT 或 !         | 非，不是                                 |


#### DCL

DCL全称是Data Control Language(数据控制语言)，用来控制数据库用户，控制数据库的访问权限

DCL-管理用户

1. 查询用户

    ```sql
    USE mysql;
    SELECT * FROM user;
    ```

2. 创建用户

    ```sql
    CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';
    ```

3. 修改用户密码

    ```sql
    ALTER USER '用户名'@'主机名' IDENTIFIED WITH  mysql_native_password BY '密码';
    ```

4. 删除用户

    ```sql
    DROP USER '用户名'@'主机名';
    ```

注意：

- 主机名可以使用%通配
- 这类SQL开发人员用的较少，主要是DBA（Database Administrator 数据库管理员）使用。

DCL-权限控制

| 权限               | 说明               |
| ------------------ | ------------------ |
| ALL,ALL PRIVILEGES | 所有权限           |
| SELECT             | 查询数据           |
| INSERT             | 插入数据           |
| UPDATE             | 修改数据           |
| DELETE             | 删除数据           |
| ALTER              | 修改表             |
| DROP               | 删除数据库/表/视图 |
| CREATE             | 创建数据库/表      |



1. 查询权限

    ```sql
    SHOW GRANTS FOR '用户名'@'主机名';
    ```

2. 授予权限

    ```sql
    GRANT 权限列表 ON 数据库名.表名 TO '用户名'@'主机名'
    ```

3. 撤销权限

    ```sql
    REVOKE 权限列表 ON 数据库名.表名 FROM '用户名'@'主机名'
    ```

    

### 函数

函数是指一段可以直接被另一段程序调用的程序或代码

#### 字符串函数

| 函数                     | 功能                                                      |
| ------------------------ | --------------------------------------------------------- |
| CONCAT(S1,S2,..Sn)       | 字符串拼接，将S1,S2,...Sn拼接成一个字符串                 |
| LOWER(str)               | 将字符串str全部转换为小写                                 |
| UPPER(str)               | 将字符串str全部转化为大写                                 |
| LPAD(str,n,pad)          | 左填充，用字符串pad对str的左边进行填充，达到n个字符串长度 |
| RPAD(str,n,pad)          | 右填充，用字符串pad对str的右边进行填充，达到n个字符串长度 |
| TRM(str)                 | 去掉字符串头部和尾部                                      |
| SUBSTRING(str,start,len) | 返回从字符串str从start位置起的len个长度的字符串           |

```sql
SELECT 函数名称(参数)
```

#### 数值函数

| 函数       | 功能                               |
| ---------- | ---------------------------------- |
| CELI(x)    | 向上取整                           |
| FLOOR(x)   | 向下取整                           |
| MOD(x,y)   | 返回x/y的模                        |
| RAND()     | 返回0~1之间的随机数                |
| ROUND(x,y) | 求参数x的四舍五入的值，保留y位小数 |

#### 日期函数

| 函数                              | 功能                                              |
| --------------------------------- | ------------------------------------------------- |
| CURDATE()                         | 返回当前日期                                      |
| CURTIME()                         | 返回当前时间                                      |
| NOW()                             | 返回当前的时间和日期                              |
| YEAR(date)                        | 获取指定date的年份                                |
| MONTH(date)                       | 获取指定date的月份                                |
| DAY(date)                         | 获取指定date的日期                                |
| DATE ADD(date,INILRVAL_expr type) | 返回一个日期/时间值加上一个时间间隔expr后的时间值 |
| DATEDIFF(date1,date2)             | 返回起始时间date1和结束时间date2之间的天数        |

#### 流程函数

| 函数                                                      | 功能                                                    |
| --------------------------------------------------------- | ------------------------------------------------------- |
| IF(value,t,f)                                             | 如果value为true，则返回t，否则返回f                     |
| IFNULL(value1,value2)                                     | 如果value1不为空，返回value1，否则返回value2            |
| CASE WHEN [val1] THEN [res1] ... ELSE [default] END       | 如果val1为true，返回res1，...否则返回default默认值      |
| CASE [expr] WHEN [val1] THEN [res1] ...ELSE [default] END | 如果expr的值为val1，返回res1，。。否则返回default默认值 |

### 约束

概念：约束是作用与表中字段上的规则，用于限制存储在表中的数据

目的：保证数据库中的数据的正确、有效性和完整性

分类

| 约束                     | 描述                                                 | 关键字      |
| ------------------------ | ---------------------------------------------------- | ----------- |
| 非空约束                 | 限制该字段的数据不能为null                           | NOT NULL    |
| 唯一约束                 | 保证该字段的所有数据都是唯一、不重复的               | UNIQUE      |
| 主键约束                 | 主键是一行数据的唯一标识，要求非空且唯一             | PRIMARY KEY |
| 默认约束                 | 保存数据是，如果未指定该字段的值，则采用默认值       | DEFAULT     |
| 检查约束(8.0.16版本以后) | 保证字段满足某一条件                                 | CHECK       |
| 外键约束                 | 用来让两张表的数据建立连接，保证数据的一致性和完整性 | FOREGIN KEY |

约束是作用与表中字段上的，可以在创建表/修改表的时候添加约束

#### 外键约束

外键用来让两张表的数据建立连接，从而保证数据的一致性和完整性g

语法

```sql
CREATE TABLE 表名(
	字段名 数据类型，
	...
	[CONSTRANT][外键名称] FOREIGN KEY(外键字段名) REFENCES主表(主表列名);
	)
```

```sql
ALTER TABLE 表名 ADD CONSTRANT 外键名称 FOREGIN KEY(外键字段名) REFERENCES 主表名(主表列名);
```

删除更新行为

| 行为        | 说明                                                         |
| ----------- | ------------------------------------------------------------ |
| NO ACTION   | 当父表中删除/更新对应记录时，首先应该检查该记录是否有对应外键，如果有则不允许删除/更新(与RESTIRCT一致) |
| RESTRICT    | 当父表中删除/更新对应记录时，首先应该检查该记录是否有对应外键，如果有则不允许删除/更新(与NO ACTION一致) |
| CASCADE     | 当父表中删除/更新对应记录时，首先应该检查该记录是否有对应外键，如果有，则也删除。更新外键在子表中的记录 |
| SET NULL    | 当在父表删除对应的记录时，首先检查该记录是否有对应外键，如果有则设置子表中该外键的值为null(这就要求外键允许去null) |
| SET DEFAULT | 父表有变更时，子表将外键列设置成一个默认值(Innodb)不支持     |

```sql
ALTER TABLE 表名 ADD CONSTRANT 外键名称 FOREGIN KEY(外键字段名) REFERENCES 主表名(主表列名) ON UPDATE CASCADE ON DELETE CASCADE;
```

### 多表查询

#### 多表关系

项目开发中，在进行数据库表结构的设计时，会根据 业务需求及业务模块之间的关系，分析并设计表结构，由于业务之间互相关联，所以各个表结构之间存在着各种联系，基本上分三种

- 一对多（多对一）
    实现：在多的一方建立外键，指向一的一方主键
- 多对多
    建立第三张中间表，中间表至少包含两个外键。分别关联两方主键
- 一对一
    在任意一方加入外键，关联另外一方的主键，并且设置外键为唯一的(UNIQUE)

#### 多表关系查询

只从多张表中查询数据

笛卡尔积：笛卡尔积是指在数学中，两个集合A集合和B集合的所有组合情况（在多表查询时，需要消除无效的笛卡尔积

多表查询分类

内连接：相当于查询A、B交集部分的数据

外连接：

左外连接：查询左表的所有数据，以及两张表的交集部分的数据

右外连接：查询右表的所有数据，以及两张表交集部分

子连接：当时表与自身连接查询，自连接必须使用表别名

#### 内连接

内连接查询语法：

隐式内连接

```sql
SELECT 字段列表 FROM 表1，表2 WHERE 条件...;
```

显示内连接

```sql
SELECT 字段列表 FROM表1[INNER] JOIN 表2 ON 连接条件...;
```

内连接查询的时两张表交集的部分

#### 外连接

外连接查询语法

左外连接

```sql
SELECT 字段列表 FROM 表1 LEFT[OUTER]JOIN 表2 ON 条件...;
```

相当于查询表一(左表)的所有数据包含表1和表2交集部分的数据

右外连接

```sql
SELECT 字段列表 FROM 表1 RIGHT [OUTER] JOIN 表2 ON 条件 ...;
```

相当与查询表二(右表)的所有数据包含表1和表2交集部分的数据

#### 自连接

自连接查询语法

```sql
SELECT 字段列表 FROM 表A 别名A JOIN 表A 别名B ON 条件...;
```

自连结查询，可以是内连接查询，也可以是外连接查询

#### 联合查询

对于union查询，就是把多此查询的结果合并起来，形成一个新的查询结果集。

```sql
SELECT 字段列表 FROM 表A ...
UNION[ALL]
SELECT 字段列表 FROM 表B ...;
```

对于联合查询的多张表的列数必须保持一致，字段类型也需要保持一致

union all 会将全部的数据合并到一起，union会对合并之后的数据进行查看

#### 子查询

概念：SQL语句嵌套SELECT语句，称为嵌套查询，又称子查询

```sql
SELECT * FROM l1 WHERE column1 = (SELECT column1 FROM l2);
```

子查询外部语句可以是INSERT/UPDATE/DELETE/SELECT的任何一个

根据子查询结果不同，分为：

- 标量子查询(子查询的结果为单个值)
- 列子查询(子查询的结果为一列)
- 行字查询(子查询的结果为一行)
- 表子查询(子查询结果为多行多列)

根据子查询的位置，分为WHERE之后、FROM之后、SELECT之后

##### 标量子查询

子查询返回的结果是单个值(数字、字符串、日期等)，最简单的形式，这种子查询成为标量子查询

常用的操作符:= <> > >= < <=

##### 列子查询

 子查询返回的结果是一列(可以是多行)，这种子查询成为列子查询

常用的操作符:IN、NOT IN、ANY、SOME、ALL

| 操作符 | 描述                                   |
| ------ | -------------------------------------- |
| IN     | 在指定的集合范围之内，多选一           |
| NOT IN | 不在指定的集合范围内                   |
| ANY    | 子查询返回的列表中，有任意一个满足即可 |
| SOME   | 与ANY相同,使用SOME的地方都可以使用ANY  |
| ALL    | 子查询返回列表的所有值都必须满足       |

##### 行子查询

子查询返回的结果是一行(可以是多行),这种子查询称为行子查询	

常用的操作符: = 、<> 、IN、NOT IN

##### 表子查询

子查询返回的是多行多列，这种子查询称为表子查询

常用的操作符:IN


#### 多表查询案例

### 事务

#### 事务简介

事务是一种操作的集合，他是一格不可分割的工作单位，事务会把所有的操作作为一格整体一起向系统提交或撤销操作，及这些操作要么同时成功，要么同时失败

![image-20250913104725404](images/image-20250913104725404.png)

默认MySQL的事务是自动提交的，也就是说，当执行一条DML语句，MySQL会立即隐式的提交事务

#### 事务操作

方式1

- 查看/设置事务的提交方式

    ```SQL
    SELECT @@ autocommit;
    ```

- 提交事务

    ```sql
    COMMIT;
    ```

- 回滚事务

    ```sql
    ROLLBACK
    ```

方式2

- 开启事务

    ```sql
    START TRRANSACTION 或 BEGIN;
    ```

- 提交事务

    ```sql
    COMMIT;
    ```

- 回滚事务

    ```sql
    ROLLBACK;
    ```

#### 事务的四大特性(ACID)

- 原子性(Atomicity)：事务时不可分割的最小操作单元，要么全部成功，要么全部失败
- 一致性(Consistency)：事务完成时，必须使所有数据都保持一致的状态
- 隔离性(Isolation)：数据库系统提供的隔离机制，保证事务 不受外部并发操作影响的独立环境下运行
- 持久性(Durablity):事务一旦提交或回滚，他对数据库的数据的改变就是永久的

#### 并发事务的问题

| 问题       | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| 脏读       | 一个事务读到另一个事务还没有提交的数据                       |
| 不可重复读 | 一格事务先后读取同一条记录，但两次读取的数据不同，称之为不可重复读· |
| 幻读       | 一个事务按照条件查询数据时，没有对应数据行，但在插入数据时，又发现这行数据已经存在，好像出现了"幻影"; |

#### 事务的隔离级别

| 隔离级别                   | 脏读 | 不可重复读 | 幻读 |
| -------------------------- | ---- | ---------- | ---- |
| Read uncommited            | √    | √          | √    |
| Read commited(Orcale默认)  | ×    | √          | √    |
| Repeatable Read(MySQL默认) | ×    | ×          | √    |
| Serializable               | ×    | ×          | ×    |

-- 查看事务的隔离级别

```sql
SELECT @@ TRANSACTION_ISOLATION;
```

-- 设置事务的隔离级别

```sql
SET [SESSION|GLOBAL] TRANSACTION ISOLATION LEVEL [READ UNCOMMITTED|READ COMMITTED| REPEATABLE |SERIALIZABLE]
```

## 进阶篇

### 存储引擎

#### MySQL的体系结构

![image-20250913171625344](images/image-20250913171625344.png)

- 连接层

    最上层时一些客户端和连接服务，主要完成一些类似于连接处理、授权认证、即相关的安全方案。服务器也会为安全接入的每个客户端验证它所具有操作权限

- 服务层
    第二层架构主要完成大多数核心服务功能，如SQL接口。并完成缓存的查询，SQL的分析与优化，部分内置函数的执行。所有跨存储引擎的功能也在这一层实现，如过程、函数等

- 引擎层
    存储引擎真正负则了MySQL中数据的存储与提取，服务器通过API和存储引擎进行通信。不同的引擎具有不同的功能，这样我们可以根据自己的需要，来选取合适的存储引擎

- 存储层
    主要是将数据存储在文件系统之上，并完成与存储引擎的交互

#### 存储引擎简介

存储引擎就是存储数据、建立索引、更新、查找数据等技术的实现方式，存储引擎是基于表的，而不是基于库的，所以存储引擎可被称为表类型

1. 创建表的时候，指定存储引擎

    ```sql
    CREATE TABLE 表名(
    	字段1 字段1类型 [COMMENT 字段1注释],
        ...
        字段n 字段n类型 [COMMENT 字段n注释]
    )ENGINE = INNODB[COMMENT 表注释];
    ```

2. 查看当前数据库支持的存储引擎

    ```sql
    SHOW ENGINES;
    ```

#### 存储引擎特点

- InnoDB

    - 介绍
        InnoDB是一种兼顾高可靠和高性能的通用存储引擎，在MySQL 5.5之后，InnoDB是默认的MySQL存储引擎

    - 特点
        DML操作遵循ACID模型，支持事务；
        行级锁，提高并发性能
        支持外键FOREIGN KEY约束，保证数据的完整性，和正确性

    - 文件
        xxx.ibd：xxx代表的是表名，innoDB引擎的每张表都回对应这样一个表空间文件，存储该表的表结构(frm、sdi)、数据和索引。
        参数：innodb_file_per_table

        ![image-20250913175243347](images/image-20250913175243347.png)

- MyISAM

    - 介绍
        MyISAM是MySQL早期默认存储引擎

    - 特点
        不支持事务，不支持外锁
        支持表锁，不支持行锁
        访问速度快

    - 文件
        xxx.sdi：存储表结构的信息
        xxx.MYD:存储数据

        xxx.MYI：存储索引

- Memory

    - 介绍
        Memory引擎的表数据是存储在内存中的，由于受到硬件问题、或断电问题的影响，只能将这些表作为临时表或缓存使用

    - 特点
        内存存放
        hash索引(默认)

    - 文件

        xxx.sdi：存储表结构信息

| 特点         | InnoDB            | MyISAM | Memory |
| ------------ | ----------------- | ------ | ------ |
| 存储限制     | 64TB              | 有     | 有     |
| 事务安全     | 支持              | -      | -      |
| 锁机制       | 行锁              | 表锁   | 表锁   |
| B+tree索引   | 支持              | 支持   | 支持   |
| Hash索引     | -                 | -      | 支持   |
| 全文索引     | 支持(5.6版本之后) | 支持   | -      |
| 空间使用     | 高                | 低     | N/A    |
| 内存使用     | 高                | 低     | 中等   |
| 批量插入速度 | 低                | 高     | 高     |
| 支持外键     | 支持              | -      | -      |

#### 存储引擎选择

在选择存储引擎应该根据应用特点选择合适的存储引擎。对于复杂系统的应用，还可以根据多种存储引擎进行组合

- InnoDB：MySQL的默认存储引擎、支持事务、外键。如果应用对事务的完整性有比较高的请求，在并发条件要求数据的一致性，数据操作出来插入和查询之外，还包含很多的更新删除操作、那么InnoDB存储引擎是比较合适的选择
- MyISAM：如果应用是以读操作和插入操作为主，只有很少的更新和删除操作，并且对事务的完整性、并发性要求不是很高，那么选择这个引擎是很合适的（MogoDB取代）
- MEMORY：将所有数据保存在内存中，访问速度快通常用于临时表即缓存。MEMORY的缺陷是对表的大小有限制，太大的表无法缓存在内存当中，而且无法保障数据的安全性(Redis取代)

### 索引

#### 索引概述

索引(index)是帮助MySQL高效获取数据的数据结构(有序)。在数据之外，数据库系统还维护着满足特定查找算法的数据结构，这些数据结构以某种方式指向引用数据，这样就可以在这些数据结构上实现高级查找算法，这种数据结构就是索引

优缺点

| 优势                                                    | 劣势                                                         |
| ------------------------------------------------------- | ------------------------------------------------------------ |
| 提高数据的检索效率，降低数据库的IO成本                  | 索引列也是要占用空间的                                       |
| 通过索引列对数据进行排序，降低排序的成本，降低CPU的消耗 | 索引大大提高了查询效率，同时也降低了更新表的速度，如对表进行INSERT、UDATE、DELETE时，效率降低 |

#### 索引结构

MySQL的索引时在存储引擎层实现的，不同存储引擎有不同的结构、主要有以下几种

| 索引结构            | 描述                                                         |
| ------------------- | ------------------------------------------------------------ |
| B+Tree索引          | 最常见的索引类型，大部分引擎都支持B+树索引                   |
| Hash索引            | 底层数据结构是用哈希表实现的，只有精确匹配索引列的查询才有效，不支持查询范围 |
| R-tree(空间索引)    | 空间索引是MyISAM引擎的一个特殊索引类型，主要用于地理空间数据类型，通常使用较少 |
| Full-text(全文索引) | 是一种通过建立倒排索引，快速匹配文档的方式，类似与Lucence，Solr，ES |

| 索引结构            | InnoDB        | MyISAM | Memory |
| ------------------- | ------------- | ------ | ------ |
| B+Tree索引          | 支持          | 支持   | 支持   |
| Hash索引            | 不支持        | 不支持 | 支持   |
| R-tree(空间索引)    | 不支持        | 支持   | 不支持 |
| Full-text(全文索引) | 5.6版本后支持 | 支持   | 不支持 |

若没有特别指明，都是指B+树结构组织的索引

- 二叉树
    缺点：顺序插入时，会形成一个链表，查询性能大大降低。大数据量的情况下，层级较深，检索速度慢
    红黑树：大数据量情况下，层级较深，检索速度慢

- B-Tree(多路平衡查找树)
    以一颗最大度数(max-degree)为5(5阶)的b-tree为例(每个节点最多存储4个key，5个指针)

    ![image-20250913213608565](images/image-20250913213608565.png)树的度是指得时一格节点的子节点个数

- B+Tree
    ![image-20250913214136552](images/image-20250913214136552.png)
    与B树的区别

    1. 所有数据都会出现在叶子节点
    2. 叶子节点形成一个单向链表

    MySQL索引结构回检点的B+Tree进行了优化，在原B+Tree的基础上，增加了一个指向相邻叶子节点的链表指针，就形成了带有顺序指针的B+Tree，提高区间访问性能
    ![image-20250913214602054](images/image-20250913214602054.png)

- Hash
    哈希索引就是采用一定的hash算法，将键值换算成新的hash值，映射到对应的曹魏上，然后存储在哈希表中
    特点：

    1. Hash索引只能用于对等比较(=,in)不支持范围查询(between,>，<,...)
    2. 无法利用索引完成排序操作
    3. 查询效率高，通常只需要一次检索就可以了，效率通常要高于B+tree索引

- 为什么InnoDB存储引擎选择使用B+tree索引结构

    - 相对于二叉树结构，层级更少，搜索效率高
    - 对于B-tree，无论是叶子节点还是非叶子节点，都会保存数据，这样导致一页中存储的键值减少，指针跟着减少，要同样保存大量数据，只能增加树的高度，导致性能降低
    - 相对Hash索引，B+tree支持范围匹配及排序操作

#### 索引分类

| 分类     | 含义                                                 | 特点                       | 关键字   |
| -------- | ---------------------------------------------------- | -------------------------- | -------- |
| 主键索引 | 针对于表中主键创建的索引                             | 默认自动创建吗，只能有一个 | PRIMARY  |
| 唯一索引 | 避免同一个表中某数据列中的值重复                     | 可以有多个                 | UNIQUE   |
| 常规索引 | 快速定位特定数据                                     | 可以有多个                 |          |
| 全文索引 | 全文索引查找的是文本中的关键词，而不是比较索引中的值 | 可以有多个                 | FULLTEXT |

在InnoDB存储引擎中，根据索引的存储形式，又可以分为以下两种

| 分类                      | 含义                                                       | 特点                      |
| ------------------------- | ---------------------------------------------------------- | ------------------------- |
| 聚焦索引(Clustered Index) | 将数据于索引放到了一块，索引结构的叶子节点保存了行数据     | 必须有，而且有且只有一个· |
| 二级索引(Secondary Index) | 将数据于索引分开存储，索引结构的叶子节点关联的是对应的主键 | 可以存在多个              |

聚集索引的选取规则：

- 如果存在主键，主键索引就是聚集索引
- 如果不存在主键，将使用第一个唯一(UNIQUE)索引作为聚焦索引
- 如果表没有主键，或没有合适的唯一索引,则InnoDB会自动生成一个rowid作为隐藏的聚焦索引

回表查询

指通过二级索引查询聚焦索引，在查询表

InnoDB主键素银的B+tree高度为多高

假设：

一行数据大小为1k，一页数据可以存储16行这样的数据。InnoDB的指针占用6个字节的空间，主键即使为bigint，占用字节数为8

高度为2

n*8+(n+1)\*6=16\*1024,算出n约为1170

1171*16 = 18736

高度为3

在此基础上乘以1171

#### 索引语法

- 创建索引

    ```sql
    CREATE [UNIQUE|FULLTEXT] INDEX index name ON table_name(index_col_name,...);
    ```

- 查看索引

    ```sql
    SHOW INDEX FROM table_name;
    ```

- 删除索引

    ```sql
    DROP INDEX index_name ON table_name;
    ```

#### SQL性能分析

- SQL执行频率
    MySQL客户端连接成功后，通过show[session|global] status命令可以提供服务器状态信息。通过如下指令，可以查看当前数据库的INSERT、UPDATE、DELETE、SELECT的访问频次

    ```sql
    SHOW GLOBAL STATUS LIKE "Com____";
    ```

- 慢查询日志
    慢查询日志记录了所有执行时间超过指定参数(long_query_time,单位：秒，默认10秒）的所有SQL语句的日志。
    MySQL的慢查询日志默认没有开启，需要在MySQL的配置文件(/etc/my.conf)中配置如下信息

    ```shell
    #开启MySQL慢日志查询开关
    slow_query_log = 1;
    #设置慢日志的时间为2秒，SQL语句执行时间超过2秒，就会视为慢查询，记录慢查询日志
    long_query_time = 2;
    ```

    配置完成后，通过以下指令重新启动MySQL服务器进行测试，查看慢日志文件中记录的信息/var/lib/mysql/localhost-slow.log

- profile详情
    show profiles能够在SQL优化时帮助我们了解时间都耗费到哪里去了。通过have_profiling参数
    profile操作：

    ```sql
    SELECT @@have_profiling;
    ```

    默认profiling是关闭的，可以通过set语句session/global级别开启profiling

    ```sql
    SET profiling = 1；
    ```

- explain执行计划
    EXPLAN 或者 DESC命令 MySQL如何执行SELECT语句的信息，包括在SELECT语句执行过程中表如何连接和连接的顺序

    ```sql
    # 直接在select语句之前关键字explain/desc
    EXPLAIN SELECT 字段列表 FROM 表名 WHERE 条件;
    ```

    EXPLAIN执行计划的各字段含义

    - id
        select查询的序列号，表示中执行select子句或者是操作表的顺序(id相同，执行顺序从上到下；id不同，值越大，越先执行)
    - select_type
        表示SELECT类型。常见的取值有SIMPLE(简单表，既不使用表连接或者子查询)、PRIMARY(主查询，即外层的查询)、UNION(UNION中的第二个或陪着后面的查询语句)、SUBQUERY(SELECT/WHERE之后包含了子查询)等；
    - type
        表示连接类型，性能由好到差连接类型为NULL、system、const、eq_ref、ref、range、index、all
    - possible__key
        显示可能应用在这张表上的索引，一个或多个
    - Key
        实际使用的索引，如果为NULL，则没有使用索引
    - Key_len
        表示该索引中所使用的字节数，该值为索引字段最大可能长度，并非实际使用长度，再不损失精确性的前提下，长度越短越好
    - rows
        MySQL认为必须执行查询的行数，在Innodb引擎的表中，是一个估计值，可能并不总是准确的
    - filtered
        表示返回结果的行数占须读取行数的百分比，filtered的值越大越好

#### 索引使用

- 验证索引使用效率
    在未建立索引之前，执行如下SQL语句，查看SQL耗时

    ```sql
    SELECT *FROM tb_sku WHERE sn = '100000003145001'; 
    ```

    针对字段创建索引

    ```sql
    create index idx_sku_sn on tb_sku;
    ```

    然后执行相同的SQL语句，再次查看SQL的耗时

    ```sql
    SELECT * FROM tb_sku WHERE sn = '100000003145001';
    ```

- 最左前缀法则
    如果索引了多列(联合索引)，要遵循最左前缀法则。最左前缀发展指的是查询从许哦因的最右列开始，并且不能跳过索引中的列。如果跳跃索引中的某一列，索引将部分失效(后面的索引字段失效)

- 范围查询
    联合索引中，出现范围查询(>,<),范围查询右侧的列索引失效

- 索引列运算
    不要再索引列上进行运算操作，索引将失效

- 字符串不加引号
    字符串类型字段使用时，不加引号，索引将失效

- 模糊查询
    如果仅仅是尾部模糊匹配，索引不会失效。如果是头部模糊匹配，索引失效

- or连接条件
    用or分割开的条件，如果or前的条件中的列有索引，而后面的列中没有索引，那么涉及的索引均不会用到

- 数据分布影响
    如果MySQL评估使用索引比全表更慢，则不使用索引

- SQL提示
    SQL提示，是优化数据库的一个重要手段，简单来说，就是在SQL语句中加入一些人为的提示来达到哟话操作的目的
    use index

    ```sql
    explain select *from tb_user use index(idx_user_pro) where...;
    ```

    ignore index

    ```sql
    explain select *from tb_user ignore index(idx_user_pro) where...;
    ```

    froce index

    ```sql
    explain select *from tb_user force index(idx_user_pro) where...;
    ```

- 覆盖索引
    尽量使用覆盖索引(查询使用了索引，并且返回需要的列，在该索引多种已全部找到)，select *。
    using index condition ：查找使用了索引，但是需要回表查询数据
    using where;using index ：查找使用了索引，但是需要的数据都在索引列中能找到，所以不需要回表查询数据

- 覆盖索引
    ![image-20250914170515596](images/image-20250914170515596.png)

- 前缀索引
    当前缀索引为字符串(varchar,text等)时，有时候需要索引很长的字符串，这会让索引变得很大，查询时，浪费大量磁盘IO，影响查询效率。此时可以将字符串的一部分前缀，建立索引，这样可以大大节约空间，从而提升索引效率

    - 语法

        ```sql
        create index idx_xxxx on table_name(column(n));
        ```

    - 前缀长度
        可以根据索引的选择性来决定，而选择性是指不重复的索引值(基数)和数据表记录的总数的比值，索引选择性越高则查询效率越高，
        唯一索引的选择性是1，这是最好的所配音选择性，性能也是最好的

        ```sql
        select count(distinct email)/count(*) from tb_user;
        select count(distinct substring(email,1,5))/count(*) from tb_user;
        ```

- 单列索引与联合索引
    单列索引：即一个索引只包含单个列
    联合索引：即一个索引包含了多个列
    在业务场景中，如果存在多个查询条件，考虑针对于查询字段建立索引时，建议联合索引，而非单列索引
    多条件联合查询，MySQL优化器会评估哪个字段的索引效率更高，会选择该索引完成本次查询

#### 索引设计原则

1. 针对于数据量较大，且查询比较频繁的表建立索引
2. 针对于常作为查询条件(where)、排序(order by)、分组(group by)操作的字段建立索引
3. 尽量选择区分度高的列作为索引，尽量建立唯一索引，区分度越高、使用索引的效率越高、
4. 如果是字符串类型的字段，字段的长度越长，可以针对字段的特点，建立前缀索引
5. 如果使用联合索引，减少单列索引，查询时，联合索引很多时候可以覆盖索引，节省存储空间、避免回表、提高查询效率
6. 要控制索引的数量，索引并不是多多益善，索引越多，维护索引结构的代价越大，会影响增删改的效率
7. 如果索引不能存储NULL值，请在创建表时使用NOT NULL约束它。当优化器直到每列是否包含NULL值时，它可以更好地确定那个索引最有效地用于查询

### SQL优化

#### 插入数据

- insert优化

    - 批量插入
    - 手动提交事务
    - 主键顺序插入

- 大批量插入数据
    如果一次性需要插入大量的数据，使用insert语句插入性能较低，此时可以使用MySQL数据库提供的load指令进行插入

    ```sql
    #客户端连接服务端时，加上参数 -local-infile
    mysql -local-infile -u root -p
    #设置全局参数local_infile为1，开启从本地加载文件导入数据的开关
    set global local_infile =1 ;
    #执行load命令将准备好的数据，加载到表结构中
    load data local infile "/root/sql1.log" into table "tb_user" fields terminated by ',' lines terminated by "\n"
    ```

    主键顺序插入的性能高于乱序插入

#### 主键优化

- 数据组织方式
    在InnoDB存储引擎中，表数据都是根据主键顺序组织存放的，这种存储方式的表称为索引组织表(Index organized table IOT)
    ![image-20250914190352205](images/image-20250914190352205.png)
    ![image-20250914190452084](images/image-20250914190452084.png)
- 页分类
     页可以为空，也可以填充一半，也可以填充100%。每个页包含了2-N行数据(如果一行数据多大，会行溢出)，根据主键排列
- 页合并
    当删除一行记录，实际上据路并没有被物理删除，只是记录被标记(flaged)为删除并且它的空间允许被其他记录声明使用
    当页中的删除记录达到MERGE_THRESHOLD(默认为页的50%)，InnoDB会开始寻找最靠近的页(前或后)看看是否可以将两个页合并优化空间使用
    MERGE_THRESHOLD：合并页的阈值，可以自己设置，在创建表或者创建索引时指定

#### order by优化

1. Using filesort：通过表的索引或全表扫描，读取满足条件的数据行，然后再排序缓冲区sort buffer中完成排序操作，所有不是通过索引直接返回排序结果的排序都叫Filesort排序

2. Using index：通过有序索引顺序扫描直接返回有序数据，这种情况即为using index，不需要额外排序，操作效率高、

    ```sql
    #没有创建索引时，根据age，phone进行排序
    explain select id,age,phone from tb_user order by age ,phone;
    #创建索引
    create index idx_user_age_phone_aa on tb_user(age,phone);
    #创建索引后，根据age，phone进行升序降序排列
    explain select id,age,phone from tb_user order by age,phone;
    #创建索引后，根据age，phone进行降序排序
    explain select id,age,phone from tb_user order by age desc ，phone desc;
    #根据age，phone进行降序一个升序，一个降序
    explain select id,age,phone from tb_user order by age asc ，phone desc;
    #创建索引
    create index idx_user_age_phone_ad on tb_user(age asc,phone desc);
    #根据age,phone进行一个升序一个降序
    explain select id,age,phone from tb_user order by age asc ，phone desc;
    ```

- 根据排序字段建立合适的索引，多字段排序时，也遵循最左前缀法则
- 尽量使用覆盖索引
- 多字段排序，一个升序一个降序，此时需要注意联合索引在创建时的规则(ASC/DESC)
- 如果不可避免的出现filesort，大数据量排序时，可以适当增大排序缓冲区大小sort_buffer_size(默认256K)

#### group by优化

```sql
#删除掉目前的联合索引 idx_user_pro_age_sta
drop index idx_user_pro_age_sta on tb_user;
#执行分组操作
explain select profession,count(*) from tb_user group by profession;
#创建索引
Create index idx_user_pro_age_sta on tb_user(profession,age,status);
#执行分组操作，根据profession字段分组
explain select profession ,count(*) from tb_user group by profession;
#执行分组操作
explain select profession ，count(*)from tb_user group by profession,age;
```

在分组操作时，可以通过索引提高效率

分组操作时，索引的使用也是满足最左前缀法

#### limit优化

一个常见又非常头疼的问题是就是limit 200000 ，10此时MySQL需要排序前2000010记录，仅仅返回200000~200010的记录，其他记录丢弃，查询排序的代价非常大

优化思路：一般分页查询时，通过创建 覆盖索引 能够比较好地提高性能，可以通过覆盖索引加子查询形式进行优化

```sql
explain select *from tb_sku t,(select id from tb_sku order by id limit 200000,10) a where t.id = a.id;
```

#### count优化

```sql
explain select count(*) from tb_user;
```

- MyISAM引擎把一个表的总行数存在了磁盘上，因此执行count(*)的时候会直接返回这个数，效率很高
- InnoDB引擎就麻烦了。它执行count(*)的时候，需要把数据一行一行地从引擎里面读出来，然后积累基数

优化思路：自己计数

- count的几种用法

    - count(）是一个聚合函数，对于返回的结果集，一行行的判断，如果count函数的参数不是NULL，累计值就加1，否则不加，最后返回累加值

    - 用法：

        - count(*)
            InnoDB引擎并不会把全部字段取出来，而是专门做了优化，不取值，服务层直接按行进行累加

        - count(主键)
            InnoDB引擎会遍历整张表，把每一行的主键id值都取出来，返回给服务层。服务层拿到主键后，直接按行累加(主键不可能是null)

        - count(字段)

            没有not null约束：innoDB引擎会遍历整张表把每一行的字段值都取出来，返回服务层，服务层判断是否为null，不为null，计数累加。
            有not null约束：innoDB引擎遍历整张表把每一个字段值都取出来，返回给服务层，直接按行进行累加

        - count(1)

            InnoDB引擎遍历整张表，但不取值。服务层对于返回的每一行，放一个数字"1"进去，直接按行进行累加

    - 效率排序：
        count(字段)<count(主键 id)<count(1)$\approx$count(*),所以尽量使用count(\*);

#### update优化

InnoDB的行锁是针对索引加的锁，不是针对记录加的锁，并且该索引，不能失效，否则会从行锁升级成表锁

### 视图/存储过程/触发器

#### 视图

视图是一种虚拟存在的表，视图中的数据并不在数据库中实际存在，行和列数据来自自定义视图中查询中使用的表，并且视使用视图时动态生成的

通俗的讲，视图只保存了查询的SQL逻辑，不保存查询结果，所以我们在创建视图时候，主要工作就落在创建这条SQL语句的基础上

- 创建

    ```sql
    CREATE [OR REPLACE] VIEW 视图名称[(列表名称)] AS SELECT语句 [WITH[CASCADED|LOCAL] CHECK OPTION];
    ```

- 查询

    ```sql
    查询创建视图语句: SHOW CREATE VIEW 视图名称;
    查看视图数据：SELECT * FROM 视图名称 ......;
    ```

- 修改

    ```sql
    方式一:CREATE [OR REPLACE] VIEW 视图名称[(列表名称)] AS SELECT语句 [WITH[CASCADED|LOCAL]CHECK OPTION];
    方式二:ALTER VIEW 视图名称[(列表名称)]AS SELECT语句[WITH[CASCADED|LOCAL]CHECK OPTION];
    ```

- 删除

    ```sql
    DROP VIEW [IF EXISTS] 视图名称 [,视图名称] ...
    ```

- 视图的检查选项
    当使用WITH CHECK OPTION子句创建视图时，MySQL会通过视图检查正在更改的每个行，例如：插入，更新，删除，以使其符合视图的定义。MySQL允许基于另一个视图创建视图，他还会依赖视图的规则以保证一致性，为了确定检查的范围，mySQL提供了两个选项：CACADED和LOCAL，默认值为CASCAED

- 视图的更新
    要使视图可更新，视图中的行与基础表之间必须存在一对一的关系。如果视图包含以下任何一项，则该视图不可更新

    1. 聚合函数或窗口函数(SUM()、MIN()、MAX()、COUNT()等)
    2. DISTINCT
    3. GROUP BY
    4. HAVING
    5. UNION 或者 UNION ALL

- 作用

    - 简单
        视图不仅可以简化用户对数据的理解，也可以简化他们的操作。那些被经常使用的查询可以被定义为视图，从而使得用户不必为以后操作每次指定全部的条件
    - 安全
        数据库可以授权，但不能授权到数据库特定行和特定列上。通过视图用户只能查询和修改他们所能见到的数据
    - 数据独立
        视图可帮助用户屏蔽真实表结构变化带来的影响

#### 存储过程

存储过程是事先经过编译并存储在数据库中的一段SQL语句的集合，调用存储过程可以简化应用开发人员的很多工作，减少数据在数据库和应用服务器之间的传输，对于提高数据处理的效率是有好处的

存储过程在思想上很简单，就是数据库SQL语言层面的代码封装与重用

- 特点

    - 封装复用
    - 可以接受参数，也可以返回数据
    - 减少网络交互，效率提升

- 创建

    ```sql
    CREATE PROCEDURE 存储过程名称([参数列表])
    BEGIN 
    	--SQL语句
    END;
    ```

- 调用

    ```sql
    CALL 名称([参数]);
    ```

- 查看

    ```sql
    SELECT * FROM INFORMATION_SCHEMAROUTINES WHERE ROUTINE_SCHEMA = 'xxx'; ---查询指定数据库的存储过程及状态信息
    SHOW CREATE PROCEDURE 存储过程名称; --查询某个存储过程的定义
    ```

- 删除

    ```SQL
    DROP PROCEDURE [IF EXISTS] 存储过程名称;
    ```

- 注意：在命令行中，执行创建存储过程的SQL时，需要通过关键字delimiter指定SQL语句的结束符

- 变量
    系统变量是MySQL服务器提供，不是用户定义的，属于服务器层面。分为全局变量(GLOBAL)、会话变量(SESSION)

    - 查看系统变量

        ```sql
        SHOW [SESSION|GLOBAL] VARIABLES;			-- 查看所有系统变量
        SHOW [SESSION|GLOBAL] VARIABLES LIKE '...';	 -- 可以通过LIKE模糊匹配方式查找变量
        SELECT @@[SESSION|GLOBAL];				    -- 查看指定变量的值
        ```

    - 设置系统变量

        ```sql
        SET [SESSION|GLOBAL] 系统变量名=值;
        SET @@[SESSION|GLOBAL] 系统变量名= 值;
        ```

    用户自定义变量是用户根据需要自己定义的变量，用户变量不用提前声明在用的时候直接用"@变量名"使用就可以，其作用域为当前连接

    - 赋值

        ```sql
        SET @var_name = expr[@var_name = expr]..;
        SET @var_name := expr[@var_name = expr]..;
        ```

        ```sql
        SELECT @var_name := expr[,@var_name := expr]...;
        SELECT 字段名 INTO @var_name FROM 表名;
        ```

    - 使用

        ```sql
        SELECT @var_name;
        ```

    - 注意
        用户自定义的变量无需对其进行声明或初始化，只不过获取的值为NULL

    局部变量是根据需要定义在局部生效的变量，访问之前需要DECLARE声明。可用于存储过程内局部变量的范围是在其内声明的BEGIN ...END块

    - 声明

        ```sql
        DECLARE 变量名 变量类型[DEFAULT];
        ```

        变量类型就是数据库字段类型：INT，BIGHT，CHAR，VARCHAR，DATE，TIME等

    - 赋值

        ```sql
        SET 变量值 = 值;
        SET 变量值 := 值;
        SELECT 字段名 INTO 变量名 FROM 表名 ...;
        ```

- if
    语法:

    ```sql
    IF 条件1 THEN
    	...
    ELSEIF 条件2 THEN
    	...
    ELSE
    	...
    END IF;
    ```

- 参数

    | 类型  | 含义                                         | 备注 |
    | ----- | -------------------------------------------- | ---- |
    | IN    | 该类参数作为输入，也就是需要调用时传入值     | 默认 |
    | OUT   | 该类参数作为输出，也就是该参数可以作为返回值 |      |
    | INOUT | 既可以作为输入参数，页可以作为输入参数       |      |

    用法

    ```sql
    CREATE PROCEDURE 存储过程名称([IN/OUT/INOUT 参数名 参数类型] )
    BEGIN
    	--SQL语句
    END;
    ```

- 循环
    - case

    - 语法一

        ```sql
        CASE case_value
        	WHEN when_value1 THEN statement_list1
        	[WHEN when_value2 THEN statement_list2] ...
        	[ELSE statement_list]
        END CASE;
        ```

    - 语法二

        ```sql
        CASE
        	WHEN search_condition1 THEN statement_list1
        	[WHEN search_condition2 THEN statement_list2]...
        	[ELSE statement_list]
        END CASE;
        ```

    - while
        while循环是有条件的循环控制语句。满足条件后，再执行循环体中的SQL语句。具体语法为:

    ```sql
    #先判定条件，如果条件为true，则执行逻辑，否则不执行逻辑
    WHILE 条件 DO
    	SQL 逻辑...
    END WHILE;
    ```

    - repeat
        repeat是有条件的循环语句，当满足条件时推出循环。具体语法为

    ```sql
    REPEAT
    	SQL逻辑
    	UNTIL 条件
    END REPEAT;
    ```

    - loop
        LOOP实现简单循环，如果不在SQL逻辑中增加退出循环的条件，可以用其来实现简单的死循环。LOOP可以配合以下两个语句使用

    - LEAVE:配合循环使用，退出循环

    - ITERATE：必须使用在循环中，作用时跳过当前循环剩下的语句，直接进入下一次循环

        ```sql
        [begin_label:]LOOP
        	SQL逻辑...
        END LOOP [end_label];
        ```

        ```sql
        LEAVE label;	退出指定标记的循环体
        ITERATE label;	--直接进入下一次循环
        ```

- 游标
    游标(CURSOR)是用来存储查询结果集的数据类型，在存储过程中和函数中可以使用游标对数据进行循环的处理，游标的使用包括游标的声明、OPEN、FETCH和CLOSE，其语法如下

    - 声明游标

        ```sql
        DECLARE 游标名称 CURSOR FOR 查询语句;
        ```

    - 打开游标

        ```sql
        OPEN 游标名称;
        ```

    - 获取游标记录

        ```sql
        FETCH 游标名称 INTO 变量[,变量];
        ```

    - 关闭游标

        ```sql
        CLOSE 游标名称;
        ```

- 条件处理程序
    条件处理程序(Handler)可以用来定义在流程控制结构执行过程中遇到问题时相应的处理步骤

    ```sql
    DECLARE hanlder_action HANDLER FOR condition_value [,condition_value]... statement;
    
    handler_action
    		CONTINUE:继续执行当前程序
    		EXIT:终止执行当前的程序
    condition_value
    		SQLSTATE sqlstate_value:状态码,如02000
    		SQLWARNING：所有以01开头的SQLSTATE代码的简写
    		NOT FOUND：所有以02开头的SQLSTATE代码的简写
    		SQLEXCEPTION：所有没有被SQLWARNING或NOT FOUND捕获的SQLSTATE代码的简称
    ```

#### 存储函数

存储函数是由返回值的过程，存储函数的参数只能是IN类型的。具体语法如下:

```sql
CREATE FUNCTION 存储函数名称([参数名称])
RETURNS type[characteristic...]
BEGIN 
	--SQL语句
	RETURN...;
END;

characteristic说明:
DETERMINSTIC:相同的输入参数总是产生相同的结果
NO SQL：不包含SQL语句
READS SQL DATA:包含读取数据的语句，但不包含写入数据的语句
```

#### 触发器

- 介绍
    触发器是与表有关的数据库对象，指在insert/update/delete之前或之后触发并执行触发器中定义的SQL语句集合。触发器的这种特殊性可以协助应用在数据库端确保数据的完整性，日志记录，数据校验等操作
    使用别名OLD和NEW来引用触发器中发生变化的记录内容，这与其他数据库是相似的。现在触发器还只支持行级触发，不支持语句触发

    | 触发器类型     | NEW和OLD                                               |
    | -------------- | ------------------------------------------------------ |
    | INSERT型触发器 | NEW表示将要或者已经新增的数据                          |
    | UPDATE型触发器 | OLD表示修改之前的数据，NEW表示将要或者已经修改后的数据 |
    | DELETE型触发器 | OLD表示将要或者已经删除的数据                          |

- 语法

    - 创建

        ```sql
        CREATE TRIGGER trigger_name
        BEFORE/AFTER INSERT/UPDATE/DELETE
        ON tbl_name FOR EACH ROW --行级触发器
        BEGIN 
        	trigger_stmt;
        END;
        ```

    - 查看

        ```sql
        SHOW TRIGGER;
        ```

    - 删除

        ```sql
        DROP TRIGGER [schema_name.]trigger_name; 如果没有指定schema_name,默认当前数据库
        ```

        

### 锁

#### 概述

锁是计算机协调多个线程或线程并发访问某一资源的控制。在数据库中。出传统的计算机资源(CPU、RAM、I/O)的争用外，数据也是一种供许多用户共享的资源。如何保证数据并发访问的一致性、有效性是所有数据库必须解决的问题，所冲突也是影响数据库并发访问性能的一个重要因素，从这个角度上来说，所对于数据库而言显得尤其重要，也更加复杂

MySQL中的锁，按照所得粒度分，分为以下三类：

1. 全局锁：锁定数据库中的所有表
2. 表级锁：每次操作锁住整张表
3. 行级锁：每次操作锁住对应的行数据

#### 全局锁

- 介绍
    全局锁就是对整个数据库实例加锁，枷锁后整个实例属于只读状态，后续写DML语句，DDKL语句，已经更新操作的事务都将被阻塞
    其典型的使用场景是做全库的逻辑备份，对所有的表进行锁定，从而获取一致性视图，保证数据的完整性

- 语法

    ```sql
    flush tables with read lock;
    mysqldump -h 主机地址 -u root -p password 数据库>文件路径
    unlock tables;
    ```

- 特点

    数据库中加全局锁，是一个比较重的操作，存在以下问题：

    1. 如果在主库上备份，那么备份期间都不能执行更新，业务基本上就得停摆
    2. 如果在从库上备份，那么在备份期间从库不能执行主库同步过来的二进制日志(binlog)，会导致主从延迟

    在InnoDB引擎中，我们可以备份时加上参数 --single-transaction参数来完成不加锁的一致性数据备份

    ```sql
    mysqldump --single-transaction -h 主机地址 -u root -p password 数据库>文件路径
    ```

#### 表级锁

- 介绍
    表级锁，每次操作锁住整张表。锁定粒度大，发生锁冲突的概率最高，并发度最低，应用在MyISAM、InnoDB，BDB等存储引擎中
    对于表级锁，主要分为以下三类:

    1. 表锁
    2. 元数据锁(meta data lock,MDL)
    3. 意向锁

- 表锁
    分为两类：

    1. 表共享读锁(read lock)
    2. 表独占写锁(write lock)

    语法：

    1. 加锁：lock tables 表名 ... read/write
    2. 释放锁：unlock tables / 客户端断开连接

    ![image-20250921173735988](images/image-20250921173735988.png)

    读锁不会阻塞其他客户端的读，但会阻塞写。写锁即会阻塞其他用户端的读，又会阻塞其他用户端的写

- 元数据锁(meta data lock,MDL)

    MDL加锁过程中是系统自动控制，无需显示使用，在访问一张表的时候自动加上。MDL锁主要作用是维护表元数据的一致性，在表上有活动事务的时候，不可以对元数据进行写入操作。为了避免DML与DDL冲突。保证读写的正确性
    在MySQL5.5中引入MDL，当对一张表进行增删改查的时候，加MDL读锁(共享);当对表结构进行变更操作时候，加MDL写锁(排他)

    | 对应SQL                                     | 所类型                                | 说明                                             |
    | ------------------------------------------- | ------------------------------------- | ------------------------------------------------ |
    | lock table xxx read/write                   | SHARED_READ_ONLY/SHARED_NO_READ_WRITE |                                                  |
    | select、select...lock in share mode         | SHARE_READ                            | 与SHARED_READ、SHARED_WRITE兼容，与EXCLUSIVE互斥 |
    | insert、update、delete、select...for update | SHARED_WRITE                          | 与SHARED_READ、SHARED_WRITE兼容，与EXCLUSIVE互斥 |
    | alter table                                 | EXCLUSIVE                             | 与其他的MDL都互斥                                |

    查看元数据锁

    ```sql
    select object_type,object_name,lock_type,lock_duration from performance_schema.metadata_locks;
    ```

- 意向锁
    为了避免DML执行时，加的行锁与表锁的冲突，在InnoDB中引入了意向锁，使得表锁不用检查每行数据是否加锁，使用意向锁来减少表锁的检查

    1. 意向共享锁(IS)：与表锁共享锁(read)兼容，与表锁其他锁(write)都互斥。
    2. 意向排他锁(IX)：与表锁共享锁(read)及其他锁(read互斥。意向锁之间不会互斥。

    通过以下SQL，查看意向锁及行锁的加锁情况：

    ```sql
    select object_schema,object_name,index_name,lock_type,lock_mode,lock_data from performance_schema.data_locks;
    ```

#### 行级锁

行级锁，每次操作锁住对应的行数据 ，锁定力度最小，发生锁冲突d额概率最低，并发度最高。应用在InnoDB存储引擎中

InnoDB的数据是基于索引组织的，行锁是通过对索引上的索引项加锁实现的，而不是对记录家的锁。对于行级锁，主要分为以下三类:

1. 行锁(Record Lock)：锁定单个记录的锁，防止其他事务对此行进行update和delete。在RC、RR隔离级别下都支持
2. 间隙锁(Gap Lock)：锁定索引记录的间隙(不含该记录)，确保索引记录间隙不变，防止其他事务在这个间隙进行insert，产生幻读。在RR隔离级别下都支持
3. 临键锁(Next-Key Lock)：行锁与间隙锁的结合，同时锁住数据，并锁住数据前面的间隙Gap。在RR隔离级别下支持

- 行锁
    InnoDB实现了以下两种类型的行锁：

    1. 共享锁(S)：允许一个事务读一行，阻止其他事务活得相同数据集的排他锁
    2. 排他锁(X)：允许获取排他锁的事务更新数据，阻止其他事务获得相同数据集的共享锁和排他锁

    | 当前\请求 | S(共享锁) | X(排他锁) |
    | --------- | --------- | --------- |
    | S(共享锁) | 兼容      | 冲突      |
    | X(排他锁) | 冲突      | 冲突      |

    | SQL                         | 行锁类型   | 说明                                     |
    | --------------------------- | ---------- | ---------------------------------------- |
    | INSERT...                   | 排他锁     | 自动加锁                                 |
    | UPDATE...                   | 排他锁     | 自动加锁                                 |
    | DELETE                      | 排他锁     | 自动加锁                                 |
    | SELECT(正常)                | 不加任何锁 |                                          |
    | SELECT...FOR UPDATE         | 排他锁     | 需要手动在SELECT之后加FOR UPDATE         |
    | SELECT...LOCK IN SHARE MODE | 排他锁     | 需要手动在SELECT之后加LOCK IN SHARE MODE |

    默认情况下，InnoDB在REPEATABLE READ事务隔离级别运行，InnoDB使用next-key锁进行搜索和索引扫描，以防止幻读

    1. 针对唯一索引进行检索时，对已存在的记录进行等值匹配时，将会自动优化行锁
    2. InnoDB的行锁是针对于索引加的锁，不通过索引条件检索数据，那么InnoDB将对表中的记录加锁，此时就会升级为表锁

- 间隙锁/临建锁
    默认情况下，InnoDB在REPEATABLE READ事务隔离级别运行，InnoDB使用next-key锁进行搜索和索引扫描，以防止幻读

    1. 索引上的等值查询(唯一索引)，给不存在的记录加锁时，优化为间隙锁
    2. 索引上的等值查询(普通索引)，向右遍历时最后一个值不满足查询需求时，next-key lock 退化为间隙锁
    3. 索引上的范围查询(唯一索引)，会访问到不满足条件的第一个值为止

    注意：间隙锁唯一目的是防止其他事务插入间隙。间隙锁可以共存，一个事务采用的间隙锁不会阻止另一个事务在同一间隙上采用间隙锁 

### InnoDB引擎



#### 逻辑存储引擎

![image-20250921212911376](images/image-20250921212911376.png)

#### 架构

##### 内存架构

​	![image-20250921213224325](images/image-20250921213224325.png)

![image-20250921213435582](images/image-20250921213435582.png)

![image-20250921213525426](images/image-20250921213525426.png)

![image-20250921213716089](images/image-20250921213716089.png)

##### 磁盘结构

![image-20250921213944111](images/image-20250921213944111.png)

![image-20250921214210445](images/image-20250921214210445.png)

![image-20250921214312250](images/image-20250921214312250.png)

##### 后台线程

![image-20250921214707424](images/image-20250921214707424.png)

1. Master Thread
    核心后台线程，负责调度其他线程，还负责将缓冲池中的数据异步刷新到磁盘中，保持数据的一致性，还包括脏页的刷新，合并插入缓存、undo页的回收

2. IO Thread
    在InnoDB存储引擎中大量使用了AIO来处理IO请求，这样可以极大地提高数据库的性能，而IO Thread主要负责这些IO请求的回调

    | 线程类型             | 默认个数 | 职责                         |
    | -------------------- | -------- | ---------------------------- |
    | Read thread          | 4        | 负责读操作                   |
    | Write thread         | 4        | 负责写操作                   |
    | Log thread           | 1        | 负责将日志缓冲区刷新到磁盘   |
    | Insert buffer thread | 1        | 负责将写缓冲区内容刷新到磁盘 |

3. Purge Thread
    主要用于回收事务已经提交了的undo log,在事务提交之后,undo log可能不用了，就用它来回收

4. Page Cleaner Thread
    协助Master Thread 刷新脏页到磁盘的线程，它可以减轻Master Thread 的工作压力，减少阻塞

#### 事务原理

- 事务
    事务是一组操作的集合，它是不可分割的工作单位，事务会把所有的操作作为一个整体一起向系统提交或撤销操作，即这些操作要么同时成功，要么同时失败
- 特性
    - 原子性(Atomicity)：事务是不可分割的最小单元，要么全部成功，要么全部失败
    - 一致性(Consistency)：事务完成时，必须使所有数据都保持一致的状态
    - 隔离性(Isolation)：数据库提供的的隔离机制，保证事务在不受外部并发操作影响的人独立环境运行
    - 持久性(Durability)：事务一旦提交或回滚，他对数据库中的数据改变就是永久的
- readlog
    重做日志，记录的是事务提交时数据也的物理修改，用来实现事务的持久性
    该日志由两部分组成:重做日志缓存(read log buffer)以及重做日志文件(redo log file)，前者是在内存中，后者是在磁盘中。当事务提交之后会把所有修改信息都存到该日志文件中，用于刷新脏页到磁盘，发生错误时，进行数据回复使用
    ![image-20250922202806532](images/image-20250922202806532.png)
- undo log
    回滚日志，用于记录数据被修改前的信息，作用包含两个：提供回滚和MVCC(多版本并发控制)
    undo log 和redo log记录的物理日志不一样，他是逻辑日志，可以认为当delete一条记录时，undo log中会记录一条对应的insert记录,反之亦然，当update一条记录，它记录一条对应相反的update记录。当执行rollback时，就可以从undo log中的逻辑记录读取到相应的内容进行回滚
    Undo log销毁：undo log在事务执行时产生，事务提交时，并不会立即删除undo log，因为这些日志还可能用于MVCC
    Undo log存储：undo log采用段的方式进行管理和记录，存放在前面介绍的roll back segment 回滚段中，内部包含1024个undo log segment

#### MVCC

##### 基本概念

- 当前读
    读取记录的最新版本，读取时爱要保证其他并发事务不能修改当前记录，会对读取的记录加锁。对于我们日常的操作，如：sleect...lock in share mode(共享锁),select for update 、insert、delete(排他锁)都是一种当前读
- 快照读
    简单select(不加锁)就是快照读，快照读，读取的是记录数据的可见版本，有可能是历史数据，不加锁，是非阻塞读
    - Read Committed：每次select，都生成一个快照读
    - Repeatable Read：开启事务后第一个select语句才是快照读的地方
    - Serializable：快照读会退化为当前读
- MVCC
    全称Multi-Version Concurrency Control,多版本并发控制。只维护一个数据的多个版本，使得读写操作没有冲突，快照读为MySQL实现 MVCC提供了一个非阻塞读功能。MVCC的具体实现。还需要依赖于数据库记录中的三个隐式字段、undo log日志，readView

###### 隐藏字段

- 记录中的隐藏字段

    | 隐藏字段    | 含义                                                         |
    | ----------- | ------------------------------------------------------------ |
    | DB_TRX_ID   | 最近修改事务ID，记录插入这条记录或最后一次修改该记录的事务ID |
    | DB_ROLL_PTR | 回滚指针，指向这条记录的上一个版本，用于配合undo log，指向上一个版本 |
    | DB_ROW_ID   | 隐藏主键，如果表结构没有指定主键，将会生成隐藏字段           |

##### 实现原理

- undo log

    回滚日志，在insert、update、delete的时候产生的便于数据回滚的日志

    在Insert的时候，产生的undo log日志只在回滚时需要，在事务提交后，可立即被删除
    而update、delete的时候，产生的undo log日志不仅在回滚时需要，在快照读时也需要，不会立即被删除

- undo log版本链
    不同事务或相同事务对同一条记录进行修改，会导致 记录的undolog生成一条记录版本链表，链表的头部时最新的旧纪录，链表的尾部时最早的旧纪录

- readview
    ReadView(读视图)是快照读SQL执行时MVCC提取数据的根据，记录并维护系统当前活跃的事务(未提交的)id
    ReadView中包含了四个核心字段

    | 字段           | 含义                                                 |
    | -------------- | ---------------------------------------------------- |
    | m_ids          | 当前活跃的事务ID集合                                 |
    | min_trx_id     | 最小活跃事务ID                                       |
    | max_trx_id     | 预分配事务ID、当前最大事务ID+1(因为事务的ID是自增的) |
    | creator_trx_id | Readview创建者的事务ID                               |

    版本数据链访问规则
    ![image-20250923213914874](images/image-20250923213914874.png)

    不同的隔离级别，生成ReadView的时机不同

    - READ COMMITTED：在事务中每一次执行快照时生成ReadView

    - REPEATABLE READ：仅在事务中第一次执行快照时生成ReadView，后续复用该ReadView

        ![image-20250923214659454](images/image-20250923214659454.png)

### MySQL管理

#### 系统数据库

MySQL数据库安装完成后，自带了四个数据库

| 数据库             | 含义                                                         |
| ------------------ | ------------------------------------------------------------ |
| mysql              | 存储MySQL服务器正常运行所需要各种时区信息(时区、主从、用户、权限等) |
| information_schema | 提供了访问数据库元数据的各种表和视图，包含数据库、表、字段类型及访问权限 |
| performance_schema | 为MySQL服务器运行时提供了一个底层监控功能，主要用于收集数据库服务器性能参数 |
| sys                | 包含了一系列方便DBA和开发人员利用performance_schema性能数据库进行性能调优和诊断的视图 |

#### 常用工具

- mysql
    该mysql不是指mysql服务，而是指mysql的客户端工具

    ```shell
    语法:
    	mysql [options] [database]
    选项：
    	-u,-user=name			#指定用户名
    	-p,-password[=name]		#指定密码
    	-h,-host=name			#指定服务器ip或域名
    	-P,--port=port			#指定连接端口
    	-e,-execute=name		#执行SQL语句并退出 
    ```

    -e选项可以在Mysql客户端执行SQL，而不用连接到MySQL数据库中在执行，对于一些批处理脚本，这种方式尤其方便

    ```shell
    mysql -uroot -p123456 db01 -e"select*from_stu";
    ```

- mysqladmin
    mysqladmin是一个执行管理操作的客户端程序，可以用它来检查服务器的配置和当前状态并删除数据库等

    ```shell
    通过帮助文档查看选项
    	mysqladmin --help
    ```

- mysqlbinlog
    由于服务器生成的二进制日志文件以二进制的格式保存，所以如果想要检验这些文本的文本格式，就会使用到mysqlbinlog 日志管理工具

    ```shell
    语法：
    	mysqlbinlog[options] log-file1 log-files2 ...
    选项：
    	-d,--database=name		#指定数据库名称,只列出指定数据库
    	-o,--offset=#			#忽略掉日志中前n行的命令
    	-r,--result file=name	#将输出的文本格式日志输出到指定文件
    	-s,--short-form			#显示简单格式，省略掉一些信息
    		start datatime-date1 stop datatime-date2 			指定日期间隔内的日志
    		stop postions-pos1 stop position-pos2				指定位置间隔内的日志
    ```

- mysqlshow
    mysqlshow客户端对象查找工具，用来很快的查找存在那些数据库、数据库中的表、表中的列或者索引

    ```shell
    语法:
    	mysqlshow [options][db_name[table_name[col_name]]
    选项：
    	--count		显示数据库及表的统计信息(数据库，表均不可以指定)
    	-i			显示指定数据库或者指定表的状态信息
    ```

- mysqldump
    mysqldump客户端工具用来备份数据库或在不同数据库之间进行数据迁移，备份内容包含创建表，及插入表的SQL语句

    ```sql
    语法：
    	mysqldump[options]db_name[tables]
    	mysqldump[options]--database/-B db1[db2 db3...]
    	mysqldump[options]--all-databases/-A
    连接选项:
    	-u,--user=name			指定用户名
    	-p,--password[=name]	指定密码
    	-h,--host=name			指定服务器ip或域名
    	-P,--port=#				指定连接端口
    输出选项：
    	add drop database		在每个数据库创建语句加上drop database语句
    	--add-drop-table		在每个表创建语句drop table语句，默认开启;不开启(--skip-add-drop-table)
        -n,--no-create-db		不包含数据库的创建语句
        -t,--no-create-into		不包含数据表的创建语句
        -d --no-data			不包含数据
        -T,-tab=name			自动生成两个文件：一个sql文件，创建表结构的语句；一个.txt文件，数据文件
    ```

- mysqlimport/source
    mysqlimport是数据库导入工具，用来导入mysqldump加-T参数后导出的文本文件

    ```sql
    语法
    	mysqlimport [options] db_name textfile1 [textfile2]
    ```

    如果需要导入sql文件，可以使用mysql中的source指令

    ```sql
    语法：
    	source /root/xxx.sql
    ```

## 运维篇

### 日志

#### 错误日志

错误日志是MySQL中最重要的日志之一，他记录了当mysql的启动或停止时，以及服务器在运行过程中发生任何严重的错误时的相关信息。当数据库出现任何故障导致无法使用时，建议先查看此日志

该日志是默认开启的，默认存放在目录/var/log/，默认的日志文件名为mysqld.log。查看日志位置

```sql
show variables like '%log_error'
```

#### 二进制日志

二进制日志(BINLOG)记录了所有的DDL(数据定义语言)语句和DML(数据操控语言)语言,但不包括数据查询(SELECT、SHOW)语句

作用:1. 灾害时的数据恢复2. MySQL的主从复制。在MySQL8版本中，默认二进制日志时开启着的，涉及到的参数如下

```sql
show variables like '%log_bin%'
```

- 日志格式
    MySQL服务器中提供了多种格式记录二进制日志，具体格式及特点如下

    | 日志格式  | 含义                                                         |
    | --------- | ------------------------------------------------------------ |
    | STATEMENT | 基于SQL语句的日志记录，记录的是SQL语句，对数据进行修改的SQL都会记录在日志文件中 |
    | ROW       | 基于行的日志记录，记录的是每一行的数据变更                   |
    | MIXED     | 混合了STATEMENT和ROW两种格式默认采用STATEMENT，在某些特殊情况下会自动切换为ROW进行记录 |

    ```sql
    show variables like '%binlog_format'
    ```

- 日志查看
    由于日志是以二进制方式的存储的，不能直接读取，需要通过二进制日志查询工具mysqlbinlog来查看，具体语法

    ```
    mysqlbinlog [参数选项] logfilename
    
    参数选项
    	-d,--database=name		#指定数据库名称,只列出指定数据库
    	-o,--offset=#			#忽略掉日志中前n行的命令
    	-v						#将行事件(数据变更)重构为SQL语句
    	-w 						#将行时间(数据变更)重构为SQL语句，并输出注释信息
    ```

- 日志删除
    对于业务比较繁忙的系统，每天生成的binlog数据巨大，如果长期不清除，将会占用大量的磁盘空间。可以通过以下几种方式清理日志

    | 指令                                             | 含义                                                         |
    | ------------------------------------------------ | ------------------------------------------------------------ |
    | reset master                                     | 删除全部binlog日志，删除之后，日志编号，将从binlog.0000001重新开始 |
    | purge master logs to 'binlog.********'           | 删除******编号之前的所有日志                                 |
    | purge master logs brfore 'yyyy-mm-dd hh24:mi:ss' | 删除日志为'yyyy-mm-dd hh24:mi:ss'之前所产生的所有日志        |

    也可以在mysql的配置文件中配置二进制日志的过期时间，设置了之后，二进制文件过期后会自动删除

    ```sql
    show variables like '%binlog_expire_logs_seconds%';
    ```

#### 查询日志

查询日志中记录了客户端所有操作语句，而二进制日志不包含查询数据的SQL语句，默认情况下，查询日志是未开启的。如果要开启查询日志，可以设置以下配置

修改MySQL的配置文件/etc/my.cnf文件，添加如下内容

```shell
#该选项用来开启查询日志,可选值：0或1，0代表关闭，1代表开启
general log = 1
#修改日志的文件，如果没有指定，默认的文件名为host_name.log
general log file=mysql.query.log
```



#### 慢查询日志

慢查询日志记录了所有执行事件超过参数long_query_time设置值并且扫描记录数不小于min_examined_row_limit的所有SQL语句的日志，默认未开启。long_query_time默认为10秒，最小为0，精度可以精确到微秒

```shell
#慢查询日志
slow_query_log=1
#执行时间参数
long_query_time=2
```

默认情况下，不会记录管理语句，也不会记录不使用进行查找的查询，可以使用log_show_admin_statements和更改此后为log_queries_not_using_indexes

```shell
#记录执行较慢的管理语句
log_slow_admin_statments=1
#记录执行较慢的未使用索引的语句
log_queries_not_using_indexes=1
```



### 主从分离

#### 概述

主从复制是指将主数据库的DDL和DML操作通过二进制日志传到从库服务器，然后再从库上对这些日志重新执行(也叫重做)，从而使得从库与主库的数据保持同步

MySQL支持一台主库同时向多台从库进行复制，从库同时也可以作为其他从服务器的主库，实现链状复制

![image-20250926201937173](images/image-20250926201937173.png)

MySQL复制的优点主要包括以下三个方面

1. 主库出现问题，可以快速切换到从库提供服务
2. 实现读写分离，降低主库的访问压力
3. 可以再从库中执行备份，以避免备份期间影响主库的服务

#### 原理

![image-20250926202318019](images/image-20250926202318019.png)

从上图来看主要分三步：

1. Master主库在事务提交时，会把数据变更的记录在二进制文件Binlog中
2. 从库读取主库的二进制日志文件Binlog，写入到从库的中级日志Relay Log
3. slave重做中级日志中的文件，将改变反应它自己的数据

#### 搭建

- 服务器准备
    ![image-20250926202714461](images/image-20250926202714461.png)

    ```shell
    #开放指定的3306端口
    firewall-cmd --zone=public --add-port=3306/tcp-permanent
    firewall-cmd -reload
    
    #关闭服务器防火墙
    systemctl stop firewalld
    systemctl disable firewalld
    ```

    在上述两台服务器之后，在上述的两台服务器中分别安装好MySQL,并完成基础的初始化准备工作

- 主库配置

    1. 修改配置文件 /etc/my.cnf

        ```shell
        #mysql服务ID，保证整个集群环境中唯一，取值范围:1-2**32-1，默认为1
        server-id=1
        #是否只读，1代表只读，0代表读写
        read-only=0
        #忽略的数据，只不需要同步的数据库
        #binlog-ignore-db=mysql
        #指定同步数据库
        #binlog-do-db=db01
        ```

    2. 重启MySQL服务器

        ```shell
        systemctl restart mysqld
        ```

    3. 登录mysql，创建远程连接的账户，并授予主从复制的权限

        ```sql
        #创建用户，并设置密码，该用户可在任意主机上连接该MySQL服务
        create user 'name'@'%'IDENTIFED WITH mysql_native_password'BY'Root@password';
        #为用户创建用户分配主从复制的权限
        GRANT REPLICATION SLAVE ON '.'TO user 'name'@'%';
        ```

- 从库配置

    1. 修改配置文件 /etc/my.cnf

        ```shell
        #mysql服务ID，保证整个集群环境中唯一，取值范围:1-2**32-1，默认为1
        server-id=2
        #是否只读，1代表只读，0代表读写
        read-only=1
        ```
        
    2. 重启MySQL服务器
    
        ```shell
        systemctl restart mysqld
        ```
    
    3. 登录mysql，设置主库配置
    
        ```sql
        CHANGE PEPLICATION SOURCE TO SOURCE_HOST='xxx.xxx',SOURCE_USER='xxx',SOURCE_PASSWORD='xxx',SOURCE_LOG_FILE='xxx',SOURCE_LOG_POS=xxx;
        ```
    
        上述是8.0.23中的语法，如果是mysql是8.0.23之前的版本，执行如下SQL：
    
        ```sql
        CHANGE MASTER TO MASTER_HOST='xxx.xxx',MASTER_USER='xxx',MASTER_PASSWORD='xxx',MASTER_LOG_FILE='xxx',MASTER_LOG_POS=xxx;
        ```
    
        | 参数名          | 含义               | 8.0.23之前      |
        | --------------- | ------------------ | --------------- |
        | SOURCE_HOST     | 主库的IP地址       | MASTER_HOST     |
        | SOURCE_USER     | 连接主库的用户名   | MASTER_USER     |
        | SOURCE_PASSWORD | 连接主库的密码     | MASTER_PASSWORD |
        | SOURCE_LOG_FILE | binlog的日志文件名 | MASTER_LOG_FILE |
        | SOURCE_LOG_POS  | binlog日志文件位置 | MASTER_LOG_POS  |
    
    4. 开启同步操作
    
        ```sql
        start replica; 	#8.0.22之后
        start slave;	#8.0.22之前
        ```
    
    5. 查看主从复制的状态
    
        ```sql
        show replica status; 	#8.0.22之后
        show slave status;	#8.0.22之前
        ```

### 分库分表

#### 介绍

随着互联网以及移动互联网的发展，应用系统的数据也是成指数式增长，若采用单数据库进行数据存储，存在以下性能瓶颈

1. IO瓶颈：热点数据太多，数据库缓存不足，产生大量磁盘IO，效率较低。请求数据太多，带宽不够，网络瓶颈
2. CPU瓶颈：排序、分组、连接查询、聚合统计等SQL会耗费大量的CPU资源，请求书太多，CPU出现瓶颈

分库分表的中新思想是将数据分散存储，使得单一数据库/表的数据量变小来缓解单一数据库的性能问题，从而达到提升数据库性能的目的

- 拆分策略
    ![image-20250927103520286](images/image-20250927103520286.png)

- 垂直拆分

    ![image-20250927103644953](images/image-20250927103644953.png)

    垂直分库以表为依据，根据业务将不同的表拆分到不同数据库中
    特点：

    1. 每个库的表结构都不一样
    2. 每个库的数据也不一样
    3. 所有库的并集是全量数据

    ![image-20250927103911478](images/image-20250927103911478.png)

    垂直分表：以字段为依据，根据字段的不同属性将不同字段拆分到不同的表上
    特点：

    1. 每个表的结构也不一样
    2. 每个表的数据也不一样，一般通过一列(主键/外键)关联
    3. 所有表的并集是全量数据

- 水平拆分

    ![image-20250927104254406](images/image-20250927104254406.png)

    水平分库：以字段为依据，按照一定的策略，将一个库拆分到多个库中
    特点：
    
    1. 每个库的表结构都不一样
    
    2. 每个库的数据都不一样

    3. 所有库的病及数据是全量数量	
    
        ![image-20250927104722479](images/image-20250927104722479.png)
    
    水平分表：以字段为依据，按照一定策略，将一个表的数据拆分到多个表中
    特点：
    
    1. 每个表的结构都一样
    2. 每个表的数据都一样
    3. 所有的表的并集是全量数据
    
- 实现技术
  
  - shardingJDBC：基于AOP原理，在应用程序中本地执行的SQL进行拦截，解析、改写、路由处理。需要自行编码配置实现，只支持java语言，性能较高
  - MyCat：数据库分库分表的中间件，不用调整代码即可实现分库分表，支持多种语言，性能不及前者   
  
  ![image-20250927105508742](images/image-20250927105508742.png)

#### Mycat概述

- 介绍
    MyCat是开源的，活跃的，基于java语言编写的MySQL数据库中间件。可以像使用mysql一样使用mycat，对于开发人员感受不到mycat的存在

    优势：

    - 性能可靠稳定
    - 强大技术团队
    - 体系完整
    - 社区活跃

- 安装
    mycat是采用Java语言开发的开源数据库中间件，支持Windows和Linux运行环境，下面介绍MyCat的Linux中环境的搭建,我们在准备好的服务器中安装如下软件

    - MySQL
    - JDK
    - Mycat

- 目录结构
    bin：存放可执行文件用于启动停止mycat
    conf：存放mycat的配置文件
    lib：存放mycat的项目依赖包(jar)|
    logs:存放mycat的日志文件

- 概念介绍
    ![image-20250927111920696](images/image-20250927111920696.png)

#### Mycat入门

- 需求
    ![image-20250927112044009](images/image-20250927112044009.png)
    
- 环境变量
    ![image-20250927112839916](images/image-20250927112839916.png)
    
- 分片配置(schema.xml)
    ![image-20250927113332963](images/image-20250927113332963.png)
    
- 分片配置(server.xml)
    配置mycat用户及用户的权限信息
    ![image-20250927114125681](images/image-20250927114125681.png)
    
- 启动服务
    切换到Mycat的安装目录，执行如下命令，启动mycat

    ```shell
    #启动
    bin/mycat start
    #停止
    bin/mycat stop
    ```

    Mycat启动之后，占用端口号8066
    启动完毕之后，可以查看logs目录下的启动日志，查看Mycat是否启动完成

- 分片测试
    通过mysql连接命令

#### Mycat配置

- schema.xml
    schema.xml作为Mycat中最重要的配置文件之一，涵盖了Mycat逻辑库、逻辑表、分片规则、分片节点及数据源的配置
    主要包括以下三组标签：

    - schema标签
        schema标签用于定义Mycat实例中的逻辑库一个Mycat实例中，可以有多个逻辑库，可以通过schema标签来划分不同的逻辑库。Mycat逻辑库的概念，等同于MySQL中的database概念，需要操作某个逻辑库下的表时，也需要更换逻辑库(use xxx)

        ```
        核心属性：
        name：指定自定义逻辑库名
        checkSQLschema：在SQL语句操作时指定了数据库名称，执行时，是否自动去除，true自动去除，false：不自动去除
        sqlMaxLimit：如果未指定limit进行查询，列表查询模式查询多少条记录
        ```

        table标签定义了Mycat逻辑库schema下的逻辑表，所有需要拆分的表都需要在table标签中定义

        ```
        name：定义逻辑数据库名，在该逻辑库下唯一
        dateNote：定义逻辑表所属的dateNode，该属性需要与DareNode标签中的那么对应，多个dateNode逗号分隔
        rule：分片规则的名字，分片规则是在rule.xml中定义的
        primaryKey：逻辑表对应真实表的主键
        type:逻辑表的类型，目前逻辑表重要全局表和普通表，如果未配置，就是普通表；全局表，配置为global
        ```

    - datanode标签
        定义了mycat
        中的数据节点，也就是我们常说的数据分片，一个dataNode标签是一个独立的数据分片

        ```
        核心属性
        name：定义数据节点名称
        datahost：数据库实例主机名称，引用自datanode标签中的name属性
        database：定义分片所属数据库
        ```

    - datahost标签
        该标签在Mycat逻辑数据库作为底层标签存在，直接定义了具体的数据库实例、读写分离、心跳语句

        ```
        核心属性
        name：唯一属性，共上层标签使用
        maxCon/minCon：最大连接数/最小连接数
        balance：负载均衡策略，取值0，1，2，3
        writeType：写操作分法方式(0：写操作转发到第一个WriteHsot,第一个挂了，切换到第二个；1：写操作随机分法到配置到writeHosr)
        dbDriver：数据库驱动，支持native，jdbc
        ```

- rule.xml
    rule.xml定义所有拆分表的规则，在使用过程中，可以灵活的使用分片算法，或者对同一个分片算法使用不同的参数，他让分片过程可配置化。主要包含两类标签：tableRule、Function

- server.xml
    server.xml配置文件包含了MyCat的系统配置信息，主要有两个主要的标签：system、user

    - server标签
        对应的系统配置相关及其含义、参考资料

    - user标签

        ![image-20250929213918658](images/image-20250929213918658.png)

        

#### Mycat分片

- 垂直拆分

    垂置分库

- 水平分表

- 分表规则-范围
    根据指定字段及其欧培兹的范围与数据节点的对应情况，来决定该数据属于那个分片![image-20250930214256373](images/image-20250930214256373.png)

- 分片规则-取模
    根据指定的字段值与节点数量进行求模运算，根据运算结果，来决定该数据属于哪一个分片
    ![image-20250930214549864](images/image-20250930214549864.png)

- 分片规则-一致性hash

    ![image-20250930214642874](images/image-20250930214642874.png)

    ![image-20250930214732646](images/image-20250930214732646.png)

- 分片规则-枚举
    通过在配置文件中配置可能的枚举值，指定数据分布到不同的数据节点上

    ![image-20250930214951021](images/image-20250930214951021-17592401919711.png)
    ![image-20250930215025097](images/image-20250930215025097.png)

- 分片规则-应用指定
    运行阶段由应用直接决定路由到那个分片，直接根据字符串子串(必须是数字)计算分片号
    ![image-20250930215546748](images/image-20250930215546748.png)

- 分片规则-固定分片哈希算法
    该算法类似于十进制的求模运算，但是为了二进制的操作
    ![image-20250930220059155](images/image-20250930220059155.png)
    特点：

    - 如果是求模，连续的值，分别分配到不同的分片，但是此算法会将连续值可能分配到可能分配到相同的分片，降低事务的处理难度
    - 可以均匀分配，也可以非均匀分配
    - 分片字段必须为数字类型

    ![image-20250930220516835](images/image-20250930220516835.png)

- 分片规则-字符串的hash解析
    截取指定指定位置的子字符串，进行hash算法，算出分片
    ![image-20251001082259877](images/image-20251001082259877.png)

    ​	![image-20251001082316595](images/image-20251001082316595.png)

    

- 分片规则-按(天)日期分片
    ![image-20251001082826789](images/image-20251001082826789.png)
    ![image-20251001082912743](images/image-20251001082912743.png)

-  分片规则-自然月
    使用场景为按照月份来分片，每个自然月为一个分片
    ![image-20251001084017139](images/image-20251001084017139.png)
    ![image-20251001084047648](images/image-20251001084047648.png)

#### Mycat管理及监控

![image-20251001085054837](images/image-20251001085054837.png)

- mycat管理工具

    Mycat默认开通2个端口，可以在server.xml中进行修改

    - 8066数据库访问端口，即进行DML和DDL操作
    - 9066数据库管理端口，即mycat服务管理功能，用于管理mycat的整个集群状态

    | 命令              | 含义                        |
    | ----------------- | --------------------------- |
    | show @@help       | 查看Mycat管理工具帮助文档   |
    | show @@version    | 查看Mycat版本               |
    | reload @@config   | 重新加载Mycat的配置文件     |
    | show @@datasource | 查看Mycat数据源信息         |
    | show @@datanode   | 查看Mycat现有的分片节点信息 |
    | show @@threadpool | 查看Mycat的线程池信息       |
    | show @@sql        | 查看执行的sql               |
    | show @@sql.sum    | 查看执行SQL的统计           |

- Mycat-eye

    - 介绍
        Mycat-web(Mycat-eye)是对mycat-server提供监控服务，功能不局限于对mycat使用。它通过JDBC连接对Mycat，myaql监控远程服务器(linux)的cpu、内存、网络磁盘
        Mycat-eye运行过程中需要zookeeper，

### 读写分离

#### 介绍

简单来说就是把对数据库的读和写分开，以对应不同的数据服务器，主数据库提供写操作，从数据库提供读操作
mycat可以实现上述功能
![image-20251001100347841](images/image-20251001100347841.png)

#### 一主一从

- 原理
    MySQL的主从复制，是基于二进制日志(binlog)开始的
    ![image-20251001100509645](images/image-20251001100509645.png)

    

#### 一主一从读写分离

- 配置
    Mycet控制后台的数据库的读写分离和负载均衡由schema.xml文件datahost标签的banlance属性控制
    ![image-20251001101102213](images/image-20251001101102213.png)

    ![image-20251001101237201](images/image-20251001101237201.png)

    | 参数 | 含义                                                         |
    | ---- | ------------------------------------------------------------ |
    | 0    | 不开启读写分离机制，所欲读操作都发送到当前可用的writehost上  |
    | 1    | 全部的readhost与备用的writehost都参与select语句的负载均衡(主要针对双主从模式) |
    | 2    | 所有的读写操作都随机在writehost，readhost分发                |
    | 3    | 所有的读请求随机分发到writehost回应的readhost不负担读压力    |

#### 双主双从

一个主句Master1用于处理所有写请求它和从机Slave1和另一台主机Master2还有它的从机Slave负责所欲读请求，当Master1主机宕机后，Master2主机负责写请求，Master1和Master2互为备,增强mysql的可用性
![image-20251001103249036](images/image-20251001103249036.png)

关闭所有防火墙

- 搭建

    - 主库配置master01

        1. 修改配置文件/etc/my.cnf

            ```sql
            #mysql服务ID，保证整个集群环境中唯一，取值范围:1-2**32-1，默认为1
            server-id=1
            #忽略的数据，只不需要同步的数据库
            #binlog-ignore-db=mysql
            #指定同步数据库
            binlog-do-db=db01
            binlog-do-db=db02
            binlog-do-db=db03
            #在作为从数据库的时候，有写入操作也要写入二进制文件
            log-slave-updates
            ```
		    
        2. 重启MySQL服务器
	    
    - 搭建两台主库常见账户并授权
    
        ```sql
        #创建用户，设定密码，该用户在任意主机上连接mysql服务
        CREATE USER 'itcast'@'%' IDENTIFIED WITH mysql_native_password BY 'Root@';
        #配置主从复制权限
        GRANT REPLICATION SLAVE ON *.* TO 'itcast'@'%';
        ```
    
        查看两台主库的二进制坐标日志
    
        ```sql
        show master status;
        ```
    
    - 从库配置
		1. 修改配置文件/etc/my.cnf

            ```sql
            #mysql服务ID，保证整个集群环境中唯一，取值范围:1-2**32-1，默认为1
            server-id=2
            ```
            
        2. 重启MySQL服务器
      
    - 两台从库配置关联的主库
    
      ```sql
      CHANGE MASTER TO MASTER_HOST='xxx.xxx',MASTER_USER='xxx',MASTER_PASSWORD='xxx',MASTER_LOG_FILE='xxx',MASTER_LOG_POS=xxx;
      ```
	
      需要注意slave1对应的是master1，slave2对应的是master2
    
      启动两台从库的主从复制，查看从库状态
    
      ```shell
      start slave;
      show slave status \G;
      ```
    

#### 双主双从读写分离

配置

Mycat控制后台数据库的读写分离和负载均衡由schema.xml文件datahost标签的banlance属性控制，通过writeType及switchType来完成失败自动切换的

![image-20251001110738559](images/image-20251001110738559.png)

```
balabce='1'
代表全部的readHost与stand by writeHost参与 select语句的负载均衡，简单的说，当双主从模式(M1->S1,M2->S2,并且M1和M2互为主备)正常情况下，M2，S1，S2都参与select语句的负载均衡
```

```
writeType
	0：写操作都转发到第一台writehost，writehost1挂了。会转移到writehost2上
	1：所有写操作都随机地发送到配置的writehost上
```

```
switchtype
	-1：不自动切换
	1：自动切换
```

