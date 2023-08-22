# MySQL

## 基础

### SQL通用语法

1.SQL语句可以单行或多行书写，以分号结尾。

2.SQL语句可以使用空格/缩进来增强语句的可读性。

3.MySQL数据库的SQL语句不区分大小写，关键字建议使用大写。

4.注释：

单行注释：-注释内容或#注释内容（MySQL特有）

多行注释：

```
/*注释内容*/
```

### SQL分类

| 分类 |            全称            |     说明     |
| :--: | :------------------------: | :----------: |
| DDL  |  Data Definition Language  | 数据定义语言 |
| DML  | Data Manipulation Language | 数据操作语言 |
| DQL  |    Data Query Language     | 数据查询语言 |
| DCL  |   Data Control Language    | 数据控制语言 |

### DDL

#### DDL-数据库-操作

##### 查询

查询所有数据库：

```mysql
SHOW DATABASES;
```

查询当前数据库：

```mysql
SELECT DATABASE();
```

##### 创建

```mysql
CREATE DATABASE [IF NOT EXISTS] 数据库名 [DEFAULT CHARSET 字符集] [COLLATE 排序规则];
```

##### 删除

```mysql
DROP DATABASE [IF EXISTS]数据库名;
```

##### 使用

```mysql
USE 数据库名;
```

#### DDL-表操作-查询

##### 查询当前数据库所有表

```mysql
SHOW TABLES;
```

##### 查询表结构

```mysql
DESC 表名;
```

##### 查询指定表的建表语句

```mysql
SHOW CREATE TABLE 表名;
```

#### DDL-表操作-创建

```mysql
CREATE TABLE 表名(
    字段1 字段1类型[COMMENT 字段1注释]
    字段2 字段2类型[COMMENT 字段2注释]
    ...
    字段n 字段n类型[COMMENT 字段n注释]
)[COMMENT 表注释];
```

#### DDL数据类型及案例

时间类型

| 分类       | 类型       | 大小               | 描述                         |                                                       |
| ---------- | ---------- | ------------------ | ---------------------------- | ----------------------------------------------------- |
|            | CHAR       | 0-255 bytes        | 定长字符串（性能好）         | 性别 gender char(10)                                  |
|            | VARCHAR    | 0-65535 bytes      | 变长字符串（性能较差）       | 原因：需要根据内容去计算使用的空间 username (varchar) |
|            | TINYBLOB   | 0-255 bytes        | 不超过255个字符的二进制数据  |                                                       |
| 字符串类型 | TINYTEXT   | 0-255 bytes        | 短文本字符串                 |                                                       |
|            | BLOB       | 0-65535 bytes      | 二进制形式的长文本数据       |                                                       |
|            | TEXT       | 0-65535 bytes      | 长文本数据                   |                                                       |
|            | MEDIUMBLOB | 0-16777215 bytes   | 二进制形式的中等长度文本数据 |                                                       |
|            | MEDIUMBLOB | 0-16777215 bytes   | 中等长度文本数据             |                                                       |
|            | LONGBLOB   | 0-4294967295 bytes | 二进制形式的极大文本数据     |                                                       |
|            | LONGTEXT   | 0-4294967295 bytes | 极大文本数据                 |                                                       |

日期类型

| 分类     | 类型      | 大小 | 范围                                       | 形式                | 描述             |
| -------- | --------- | ---- | ------------------------------------------ | ------------------- | ---------------- |
|          | DATE      | 3    | 1000-01-01 至 9999-12-31                   | YYYY-MM-DD          | 日期值           |
|          | TIME      | 3    | -838:59:59 至 838:59:59                    | HH:MM:SS            | 时间值或持续时间 |
| 日期类型 | YEAR      | 1    | 1901至2155                                 | YYYY                | 年份值           |
|          | DATETIME  | 8    | 1000-01-01 00:00:00至 9999-12-31 23:59:59  | YYYY-MM-DD HH:MM:SS | 混合日期和时间值 |
|          | TIMESTAMP | 4    | 1970-01-01 00:00:01 至 2038-01-19 03:14:07 | YYYY-MM-DD HH:MM:SS | 混合日期和时间值 |

####  DDL-表操作-修改

##### 添加字段

```mysql
ALTER TABLE 表名 ADD 字段名 类型（长度） [COMMENT 注释][约束];
```

##### 修改数据类型

```mysql
ALTER TABLE 表名 MODIFY 字段名 新数据类型（长度）;
```

##### 修改字段名和字段类型

```mysql
ALTER TABLE 表名 CHANGE 旧字段名 新字段名 类型(长度) [COMMENT 注释][约束]
```

##### 删除字段

```mysql
ALTER TABLE 表名 DROP 字段名;
```

##### 修改表名

```mysql
ALTER TABLE 表名 RENAME TO 新表名;
```

#### DDL-表操作-删除

##### 删除表

```mysql
DROP TABLE [IF EXISTS] 表名;
```

##### 删除指定表，并重新创建该表

```mysql
TRUNCATE TABLE 表名;
```

在删除表时，表中的全部数据也会被删除

### DML

增删改

添加数据(INSERT)

修改数据(UPDATE)

删除数据(DELETE)

#### DML-添加数据

给指定字段添加数据

```mysql
INSERT INTO 表名 (字段名1，字段名2,...) VALUES (值1，值2，...);
```

给全部字段添加数据

```mysql
INSERT INTO 表名 VALUES(值1,值2,...);
```

批量添加数据

```mysql
INSERT INTO 表名 (字段名1,字段名2,...) VALUES(值1，值2,...)，(值1,值2,...);
```

```mysql
INSERT INTO 表名 VALUES (值1，值2,...),(值1,值2,...);
```

**注意**

1.插入数据时，指定的字段顺序需要与值的顺序是一一对应的。

2.字符串和日期型数据应该包含在引号中。

3.插入的数据大小，应该在字段的规定范围内。

#### DML-修改数据

```mysql
UPDATE 表名 SET 字段名1=值1，字段名2=值2，...[WHERE 条件];
```

注意：修改语句的条件可以有，也可以没有，如果没有条件，则会修改整张表所有数据。

#### DML-删除数据

```mysql
DELETE FROM 表名 [WHERE 条件]
```

DELETE语句条件可有可无，若没有条件，则会删除整张表所有数据

DELETE语句不能删除某一个字段的值（可以使用UPDATE）

### DQL

```mysql
SELECT
字段列表
FROM                    基本查询
表名列表
WHERE                   条件查询(WHERE)
条件列表
GROUP BY                分组查询(GROUP BY) 聚合函数(max、min、count、avg、sum等)
分组字段列表
HAVING
分组后条件列表
ORDER BY                排序查询(ORDER BY)
排序字段列表
LIMIT                   分页查询(LIMIT)
分页参数
```

#### DQL-基本查询

##### 查询多个字段

```mysql
SELECT 字段1,字段2,字段3,... FROM 表名;
```

```mysql
SELECT * FROM 表名;
```

##### 设置别名

```mysql
SELECT 字段1 [AS 别名1]，字段2 [AS 别名2]... FROM 表名
```

##### 去除重复记录

```mysql
SELECT DISTINCT 字段列表 FROM 表名;
```

#### DQL-条件查询

##### 语法

```mysql
SELECT 字段列表 FROM 表名 WHERE 条件列表;
```

##### 条件

| 比较运算符         | 功能                                     |
| ------------------ | ---------------------------------------- |
| >                  |                                          |
| >=                 |                                          |
| <                  |                                          |
| <=                 |                                          |
| =                  |                                          |
| <>或!=             |                                          |
| BETWEEN ... AND... | 在某个范围内（含最小最大）               |
| IN(...)            | 在in之后的列表中的值，多选一             |
| LIKE占位符         | 模糊匹配(_匹配单个字符，%匹配任意个字符) |
| IS NULL            | 是NULL                                   |

| 逻辑运算符 | 功能     |
| ---------- | -------- |
| AND 或 &&  | 并且     |
| OR 或 \|\| | 或者     |
| NOT 或 !   | 非，不是 |

#### DQL-聚合函数

##### 介绍

将一列数据作为一个整体，进行纵向计算。

##### 常见聚合函数

| 函数  | 功能     |
| ----- | -------- |
| count | 统计数量 |
| max   | 最大值   |
| min   | 最小值   |
| avg   | 平均值   |
| sum   | 求和     |

##### 语法

```mysql
SELECT 聚合函数(字段列表) FROM 表名;
```

注意:null值不参与所有聚合函数运算。

#### DQL-分组查询

##### 语法

```mysql
SELECT 字段列表 FROM 表名 [WHERE 条件] GROUP BY 分组字段名[HAVING 分组后过滤条件];
```

#####  where和having的区别

执行时机不同:where是分组之前进行过滤，不满足where条件，不参与分组;而having是分组之后对结果进行过滤

判断条件不同:where不能对聚合函数进行判断，而having可以。

![image-20230802235604989](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230802235604989.png)

注意：

执行顺序:where>聚合函数>having

分组之后，查询的字段一般为聚合函数和分组字段，查询其他字段无任何意义。

#### DQL-排序查询

##### 语法

```mysql
SELECT 字段列表 FROM 表名 ORDER BY 字段1 排序方式1，字段2，排序方式2;
```

##### 排序方式

ASC：升序（默认值）

DESC：降序

注意：如果是多字段排序，当第一个字段值相同时，才会根据第二个字段进行排序。

#### DQL-分页查询

##### 语法

```mysql
SELECT 字段列表 FROM 表名 LIMIT 起始索引，查询记录数;
```

注意

1.起始索引从0开始，起始索引=（查询页码-1）*每页显示记录数

2.分页查询是数据库的方言，不同的数据库有不同的实现，Mysql中是LIMIT

3.如果查询的是第一页数据，起始索引可以省略，直接简写为limit10.

例子：

查询第一页

```mysql
select *from emp limit 0,10;
```

查询第二页

```mysql
select *from emp limit 10,10;
```

 

#### DQL-执行顺序

```mysql
SELECT                4   
字段列表
FROM                  1    基本查询
表名列表
WHERE                 2  条件查询(WHERE)
条件列表
GROUP BY              3  分组查询(GROUP BY) 聚合函数(max、min、count、avg、sum等)
分组字段列表
HAVING
分组后条件列表
ORDER BY               5 排序查询(ORDER BY)
排序字段列表
LIMIT                  6 分页查询(LIMIT)
分页参数
```

### DCL

主要管理数据库用户、控制数据库的访问权限。

#### DCL-用户管理

##### 查询用户

```mysql
USE mysql;
SELECT *FROM user;
```

##### 创建用户

```
CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';
```

##### 修改用户密码

```
ALTER USER '用户名'@'主机名' IDENTIFIED WITH mysql_native_password BY '新密码';
```

##### 删除用户

```
DROP USER '用户名'@'主机名'
```

这里一个例子值得记录

```mysql
#创建用户splash，可以在任意主机访问该数据库，密码为123456
create user 'splash'@'%' identified by '123456';
```

#### DCL-权限控制

|  权限  |        说明        |
| :----: | :----------------: |
|  ALL   |      所有权限      |
| SELECT |      查询数据      |
| INSERT |      插入数据      |
| UPDATE |      修改数据      |
| DELETE |      删除数据      |
| ALTER  |       修改表       |
|  DROP  | 删除数据库/表/视图 |
| CREATE |   创建数据库/表    |

##### 查询权限

```mysql
SHOW GRANTS FOR '用户名'@'主机名';
```

##### 授予权限

```mysql
GRANT 权限列表 ON 数据库名.表名 TO '用户名'@'主机名';
```

##### 撤销权限

```mysql
REVOKE 权限列表 ON 数据库名.表名 FROM '用户名'@'主机名';
```

### 函数

```mysql
SELECT 函数(参数);
```



#### 字符串函数

|           函数           |                           功能                            |
| :----------------------: | :-------------------------------------------------------: |
|   CONCAT(S1,S2,...Sn)    |         字符串拼接，将S1,S2,...Sn拼接成一个字符串         |
|        LOWER(str)        |                  将字符串str全部转为小写                  |
|        UPPER(str)        |                         转为大写                          |
|     LPAD(str,n,pad)      | 左填充，用字符串pad对str的左边进行填充，达到n个字符串长度 |
|     RPAD(str,n,pad)      | 右填充，用字符串pad对str的右边进行填充，达到n个字符串长度 |
|        TRIM(str)         |                去掉字符串头部和尾部的空格                 |
| SUBSTRING(str,start,len) |      返回从字符串str从start位置起的len个长度的字符串      |

```mysql
select upper('Hello');
```

```mysql
update enp set workno = lpad(workno,5,'0');
```

### 约束

#### 概念

约束是作用于表中字段上的规则，用于限制存储在表中的数据。

#### 目的

保证数据库中数据的正确、有效性和完整性。

#### 分类

|   约束   |                          概述                          |   关键字    |
| :------: | :----------------------------------------------------: | :---------: |
| 非空约束 |               限制该字段的数据不能为null               |  NOT NULL   |
| 唯一约束 |          保证该字段的所有数据都是唯一，不重复          |   UNIQUE    |
| 主键约束 |        主键是一行数据的唯一标识，要求非空且唯一        | PRIMARY KEY |
| 默认约束 |     保存数据时，如果未指定该字段的值，则采用默认值     |   DEFAULT   |
| 检查约束 |                保证字段值满足某一个条件                |    CHECK    |
| 外键约束 | 用来两张表的数据之间建立连接，保证数据的一致性和完整性 | FOREIGN KEY |

#### 外键约束

##### 概念

外键用来让两张表的数据之间建立连接，从而保证数据的一致性和完整性。

![image-20230809203353244](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230809203353244.png)

没有建立外键关联，无法保证数据的一致性和完整性

##### 语法

添加外键

```mysql
CREATE TABLE 表名(
    字段名 数据类型
    ...
    [CONSTRAINT] [外键名称] FOREIGN KEY(外键字段名) REFERENCES 主表(主表列名)
);
```

```mysql
ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段名) REFERENCES 主表(主表列名);
```

删除外键

```mysql
ALTER TABLE 表名 ADD CONSTRAINT 外键名称
```

##### 删除/更新行为

|    行为     |                             说明                             |
| :---------: | :----------------------------------------------------------: |
|  NO ACTION  | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不允许删除/更新。（与RESTRICT一致) |
|  RESTRICT   | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不允许删除/更新。（与NO ACTION一致) |
|   CASCADE   | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有，则也删除/更新外键在子表中的记录。 |
|  SET NULL   | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则设置子表中该外键值为null |
| SET DEFAULT |  父表有变更时，子表将外键列设置成一个默认的值(Innodb不支持)  |

```mysql
ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段名) REFERENCES 主表(主表列名) ON UPDATE CASCADE ON DELETE CASCADE;
```

### 多表关系

#### 概述

在项目开发中，在进行数据库表结构设计时，会根据业务需求和业务模块之间的关系，分析并设计表结构，由于业务之间相互关联，所以各个表结构之间也存在着各种联系，分为三种：

1.一对多

2.多对多

3.一对一

#### 一对多

案例：部门与员工的关系

关系：一个部门对应多个员工，一个员工对应一个部门

实现：在多的一方建立外键，指向少的一方的主键

![image-20230809214916885](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230809214916885.png)

#### 多对多

案例：学生与课程的关系

关系：一个学生可以选修多门课程，一门课程也可以供多个学生选择

实现：建立第三张中间表，中间表至少包含两个外键，分别关联两方主键。

![image-20230809215951140](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230809215951140.png)

#### 一对一

案例：用户与用户详情的关系

关系：一对一关系，多用于单表拆分，将一张表的基础字段放在一张表中，其他详情字段放在另一张表中

实现：在任意一方加入外键，关联另外一方的主键，并且设置外键为唯一的（UNIQUE）

![image-20230813161645215](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230813161645215.png)

### 多表查询概述

#### 概述

指从多张表中查询数据

```mysql
#多表查询  #笛卡尔积
select * from emp ,dept;
```

#### 笛卡尔积

笛卡尔乘积指数学中，两个集合A集合和B集合的所有组合情况**（在多表查询时，需要消除无效的笛卡尔积）**

![image-20230813162418896](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230813162418896.png)

消除笛卡尔积：

**WHERE**

![image-20230813162622002](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230813162622002.png)

### 多表查询分类

#### 连接查询

##### 内连接

相当于查询A、B交集部分数据

###### 内连接查询语法

隐式内连接

```mysql
SELECT 字段列表 FROM 表1，表2 WHERE 条件...;
```

显式内连接

```mysql
SELECT 字段列表 FROM 表1 [INNER] JOIN 表2 ON 连接条件...;
```



##### 外连接

###### 左外连接

查询左表（表1）所有数据，以及两张表交集部分数据（可以省略outer）

```mysql
SELECT 字段列表 FROM 表1 LEFT [OUTER] JOIN 表2 ON 条件...;
```

![image-20230813210426204](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230813210426204.png)

###### 右外连接

查询右表（表2）所有数据，以及两张表交集部分数据

```mysql
SELECT 字段列表 FROM 表1 RIGHT [OUTER] JOIN 表2 ON 条件...;
```



##### 自连接

当前表与自身的连接查询，自连接必须使用表别名

自连接查询语法：

```mysql
SELECT 字段列表 FROM 表A 别名A JOIN 表A 别名B ON 条件...;
```

自连接查询，可以是内连接查询，也可以是外连接查询

#### 联合查询-union,union all

就是把多次查询的结果合并起来，形成一个新的查询结果集

```mysql
SELECT 字段列表 FROM 表A...;
UNION [ALL]  #去掉ALL的话是对结果去重
SELECT 字段列表 FROM 表B...;
##联合查询的列数和字段类型需要保持一致
```

对于联合查询的多张表的列数必须保持一致，字段类型也需要保持一致。

union all会将全部的数据直接合并在一起

union会对合并之后的数据去重

### 子查询

#### 概念

SQL语句中嵌套SELECT语句，称为嵌套查询，又称子查询。

```mysql
SELECT *FROM t1 WHERE column1 = (SELECT column1 FROM t2);
```

子查询外部的语句可以是INSERT/UPDATE/DELETE/SELECT中的任意一个

#### 子查询分类

根据子查询结果不同，分为：

1.标量子查询（子查询结果为单个值）

2.列子查询（子查询结果为一列）

3.行子查询（子查询结果为一行）

4.表子查询（子查询结果为多行多列）

#### 标量子查询

标量子查询返回的结果是单个值（数字、字符串、日期等），最简单的形式。

常用的操作符：= <> > >= < <=

![image-20230813232735951](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230813232735951.png)

#### 列子查询

子查询返回的结果是一列（可以是多行），这种子查询称为列子查询

常用的操作符：IN、NOT IN、ANY、SOME、ALL

| 操作符 |                  描述                  |
| :----: | :------------------------------------: |
|   IN   |      在指定的集合范围之内，多选一      |
| NOT IN |         不在指定的集合范围之内         |
|  ANY   |  子查询返回列表中，有任意一个满足即可  |
|  SOME  | 与ANY等同，使用SOME的地方都可以使用ANY |
|  ALL   |    子查询返回列表的所有值都必须满足    |

![image-20230813233312189](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230813233312189.png)

#### 行子查询

子查询返回的结果是一行（可以是多列）

常用的操作符：=、<>、IN、NOT IN

![image-20230814140214421](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230814140214421.png)

### 事务

#### 简介

事务是一组操作的集合，它是一个不可分割的工作单位，事务会把所有的操作作为一个整体一起向系统提交或撤销操作请求

即这些操作要么同时成功，要么同时失败

![image-20230816112318106](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230816112318106.png)

默认MySQL的事务是自动提交的，也就是说，当执行一条DML语句，MySQL会立即隐式的提交事务

#### 操作

##### 查看/设置事务提交方式

```mysql
SELECT @@autocommit;
SET @@autocommit=0;
```

##### 提交事务

```mysql
COMMIT;
```

##### 回滚事务

```mysql
ROLLBACK;
```

##### 开启事务

```mysql
START TRANSACTION 或 BEGIN
```

##### 提交事务

```mysql
COMMIT;
```

回滚事务

```mysql
ROLLBACK;
```

#### 事务四大特性-ACID

原子性(Atomicity):事务是不可分割的最小操作单元，要么全部成功，要么全部失败

一致性(Consistency):事务完成时，必须使所有的数据都保持一致状态

隔离性(Isolation):数据库系统提供的隔离机制，保证事务在不受外部并发操作影响的独立环境下运行

持久性(Durability):事务一旦提交或回滚，它对数据库中的数据的改变是永久的

#### 并发事务问题

|    问题    |                             描述                             |
| :--------: | :----------------------------------------------------------: |
|    脏读    |          一个事务读取到另外一个事务还没有提交的数据          |
| 不可重复读 |       一个事务先后读取同一条记录，但两次读取的数据不同       |
|    幻读    | 一个事务按照条件查询数据时，没有对应的数据行，但是在插入数据时，又发现这行数据已经存在，像出现了"幻影" |

![image-20230816120944913](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230816120944913.png)

![image-20230818153856646](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230818153856646.png)

![image-20230818154303765](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230818154303765.png)

#### 事务隔离级别

|       隔离级别        | 脏读 | 不可重复读 | 幻读 |
| :-------------------: | :--: | :--------: | :--: |
|    Read uncommited    |  1   |     1      |  1   |
|     Read commited     |  0   |     1      |  1   |
| Repeatable Read(默认) |  0   |     0      |  1   |
| Serializable(串行化)  |  0   |     0      |  0   |

```mysql
##查看事务隔离级别
SELECT @@TRANSACTION_ISOLATION;

##设置事务隔离级别
SET [SESSION|GLOBAL] TRANSACTION ISOLATION LEVEL[READ UNCOMMITTED | READ COMMITTED | REPEATABLE READ | SERIALIZABLE]
```

## 进阶

### 存储引擎

#### MySQL体系结构

![image-20230818235159487](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230818235159487.png)

连接层：

最上层是一些客户端和链接服务，主要完成一些类似于连接处理、授权认证及相关的安全方案。服务器也会为安全接入的每个客户端验证它所具有的权限。

服务层：

第二层架构主要完成大多数的核心服务功能，如SQL接口，并完成缓存的查询，SQL的分析和优化，部分内置函数的执行。所有存储引擎的功能也在这一层实现，如过程、函数等。

引擎层：

存储引擎真正的负责了MySQL中数据的存储和提取，服务器通过API和存储引擎进行通信。不同存储引擎具有不同的功能。这样我们可以根据自己的需要，来选取合适的存储引擎。

存储层：

主要是将数据存储在文件系统之上，并完成与存储引擎的交互。

#### 存储引擎简介

存储引擎就是存储数据、建立索引、更新/查询数据等技术的实现方式

存储引擎是基于表的，而非库，所以存储引擎也被称为表类型

在创建表时，指定存储引擎

```mysql
CREATE TABLE 表名(
    字段1 字段1类型[COMMENT 字段1注释],
    ...
    字段n 字段n类型[COMMENT 字段n注释]
)ENGINE = INNODB [COMMENT 表注释];
```

查看当前数据库支持的存储引擎

```mysql
SHOW ENGINES;
```

#### 存储引擎特点

##### InnoDB

InnoDB是一种兼顾高可靠性和高性能的通用存储引擎，在MySQL5.5之后，InnoDB是默认的mysql存储引擎

**特点**

1.DML操作遵循ACID模型，支持**事务**

2.**行级锁**，提高并发访问性能

3.支持**外键**FOREIGN KEY约束，保证数据的完整性和正确性

**文件**

xxx.ibd:xxx表示表名，InnoDB引擎的每张表都会对应这样一个表空间文件，存储该表的表结构(frm、sdi)、数据和索引。

参数:innodb_file_per_table

```mysql
show variables like 'innodb_file_per_table'
```

逻辑存储结构

![image-20230819231209204](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230819231209204.png)

##### MyISAM

**介绍**

MySQL早期的默认存储引擎

**特点**

不支持事务，不支持外键

支持表锁，不支持行锁

访问速度快

**文件**

xxx.sdi:存储表结构信息

xxx.MYD:存储数据

xxx.MYI:存储索引

##### Memory

**介绍**

Memory引擎的表数据存储在内存中，由于受到硬件问题、或断电问题的影响，只能将这些表作为临时表或缓存值

**特点**

内存存放

hash索引(默认)

**文件**

xxx.sdi:存储表结构信息

![image-20230819231855403](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230819231855403.png)

![image-20230819234325678](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230819234325678.png)

MyISAM(已经有NoSQL代替)

MEMORY(已经有redis代替)

### 索引

#### 介绍

索引(index)是帮助Mysql高效获取数据的数据结构(有序)。在数据之外，数据库系统还维护着满足特定查找算法的数据结构，这些数据结构以某种方式引用(指向)数据，这样就可以在这些数据结构上实现高级查找算法，这张数据结构就是索引。

![image-20230820150858849](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230820150858849.png)

|                            优势                             |                             劣势                             |
| :---------------------------------------------------------: | :----------------------------------------------------------: |
|           提高数据检索的效率，降低数据库的IO成本            |                    索引列也是要占用空间的                    |
| 通过索引列对数据进行排序，降低数据排序的成本，降低CPU的消耗 | 索引大大提高了查询效率，但同时也降低更新表的速度，如对表进行INSERT、UPDATE、DELETE时，效率更低 |

#### 索引结构

![image-20230820151323310](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230820151323310.png)

MySQL的索引是在存储引擎层实现的，不同的存储引擎有不同的结构：

|      索引结构       |                             描述                             |
| :-----------------: | :----------------------------------------------------------: |
|     B+Tree索引      |          最常见的索引类型，大部分引擎都支持B+树索引          |
|      Hash索引       | 底层数据结构是用哈希表实现，只有精确匹配索引列的查询才有效，不支持范围查询 |
|  R-tree(空间索引)   | 空间索引是MyISAM引擎的一个特殊索引类型，主要用于地理空间数据类型 |
| Full-text(全文索引) |          是一种通过建立倒排索引，快速匹配文档的方式          |

![image-20230820151726882](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230820151726882.png)

#### 分类

|   分类   |                         含义                         |           特点           |  关键字  |
| :------: | :--------------------------------------------------: | :----------------------: | :------: |
| 主键索引 |                针对表中主键创建的索引                | 默认自动创建，只能有一个 | PRIMARY  |
| 唯一索引 |           避免同一个表中某数据列中的值重复           |        可以有多个        |  UNIQUE  |
| 常规索引 |                   快速定位特定数据                   |        可以有多个        |          |
| 全文索引 | 全文索引查找的是文本中的关键词，而不是比较索引中的值 |        可以有多个        | FULLTEXT |

在InnoDB存储引擎里，根据索引的存储方式，又可以分为以下两种：

|           分类            |                            含义                            |         特点         |
| :-----------------------: | :--------------------------------------------------------: | :------------------: |
| 聚集索引(Clustered Index) | 将数据存储与索引放到了一块，索引结构的叶子节点保存了行数据 | 必须有，而且只有一个 |
| 二级索引(Secondary Index) | 将数据与索引分开存储，索引结构的叶子节点关联的是对应的主键 |     可以存在多个     |

聚集索引选取规则：

1.如果存在主键，主键索引就是聚集索引

2.如果不存在主键，将使用第一个唯一(UNIQUE)索引作为聚集索引

3.如果表没有主键，或没有合适的唯一索引，则InnoDB会自动生成一个rowid作为隐藏的聚集索引

#### 语法

创建索引

```mysql
CREATE [UNIQUE|FULLTEXT] INDEX index_name ON table_name(index_col_name,...);
```

查看索引

```mysql
SHOW INDEX FROM table_name;
```

删除索引

```mysql
DROP INDEX index_name ON table_name;
```

#### SQL性能分析

##### SQL执行频率

MySQL客户端连接成功后，通过show [session|global] status命令可以提供服务器状态信息。

通过如下指令，可以查看当前数据库INSERT、UPDATE、DELETE、SELECT访问频次：

```mysql
SHOW GLOBAL STATUS LIKE 'Com______' #一个下划线等于一个字符一般七个
```

##### 慢查询日志

慢查询日志记录了所有执行时间超过指定参数(long_query_time，单位：秒，默认10秒)的所有SQL语句的日志。

查看慢查询开关

```mysql
show variables like 'slow_query_log';
```

MySQL的慢查询日志默认没有开启，需要在MySQL的配置文件(/etc/my.cnf)中配置如下信息：

```
#开启MySQL慢日志查询开关
slow_query_log = 1
#设置慢日志的时间为2秒，SQL语句执行时间超过2秒，就会视为慢查询，记录慢查询日志
long_query_time = 2
```

查看慢日志文件中记录的信息/var/lib/mysql/localhost-slow.log

修改完后然后重启

```shell
systemctl restart mysqld
```

##### profile详情

show profiles能够在做SQL优化时帮助我们了解时间都耗费到哪里去了。

通过have_profiling参数，能够看到当前MySQL是否支持profile操作：

```mysql
SELECT @@have_profiling;
```

默认profiling是关闭的，可以通过set语句在session/global级别开启profiling:

```mysql
SET profiling = 1;
```

执行一系列的业务SQL的操作，然后通过以下指令查看指令的执行耗时

```mysql
##查看每一条SQL的耗时基本情况
show profiles;

##查看指定query_id的SQL语句各个阶段的耗时情况
show profile for query query_id;

##查看指定query_id的SQL语句CPU的使用情况
show profile cpu for query query_id;
```

##### *explain执行计划

EXPLAIN或者DESC命令获取MySQL如何执行SELECT语句的信息，包括在SELECT语句执行过程中表如何连接和连接的顺序

###### 语法

```mysql
##直接在select 语句之前加上关键字explain/desc
EXPLAIN SELECT 字段列表 FROM 表名 WHERE 条件;
```

![image-20230820233646330](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230820233646330.png)

EXPLAIN执行计划各字段含义：

id：select查询的序列号，表示查询中执行select子句或者是操作表的顺序（id相同，执行顺序从上到下;id不同值越大越先执行)

select_type：表示SELECT类型，常见取值有SIMPLE（简单表，即不使用表连接或者子查询）、PRIMARY（主查询，即外层的查询）、UNION（UNION中的第二个或者后面的查询语句）、SUBQUERY（SELECT/WHERE之后包含了子查询）等

type：表示连接类型，性能由好到差的连接类型为NULL、system、const(主键、唯一索引）、eq_ref、ref（非唯一性索引）、range、index、all

possible_key:显示可能应用在这张表上的索引，一个或多个

key：实际使用的索引，如果为NULL，则没有使用索引

Key_len:表示索引中使用的字节数，该值为索引字段最大可能长度，并非实际使用长度，在不损失精确性的前提下，长度越短越好

rows：MySQL认为必须要执行查询的行数，在InnoDB引擎的表中，是一个估计值，可能并不总是准确

filtered：表示返回结果的行数占需读取行数的百分比，filtered的值越大越好

#### 使用规则

##### 验证索引效率

在未建立索引之前，执行如下SQL语句，查看SQL耗时

```mysql
SELECT *FROM tb_sku WHERE sn = '1000000003145001';
```

针对字段创建索引

```mysql
create index idx_sku_sn on tb_sku(sn);
```

然后再次执行相同的SQL语句，再次查看SQL的耗时

```mysql
SELECT * FROM tb_sku WHERE sn = '1000000003145001';
```

##### 最左前缀法则

如果索引了多列（联合索引），要遵守最左前缀法则

最左前缀法则指的是查询从索引的最左列开始，并且不跳过索引中的列

如果跳过某一列，索引将部分失效（后面的字段索引失效）

##### 范围查询

联合索引中，出现范围查询(>,<)，范围查询右侧的列索引失效。（尽量使用例如>=这种运算符

##### 索引列运算

不要在索引列上进行运算操作，索引将失效

##### 模糊查询

如果仅仅是尾部模糊匹配，索引不会失效。如果是头部模糊匹配，索引失效

##### or连接的条件

用or分割开的条件，如果or前的条件中的列有索引，而后面的列中没有索引，那么涉及的索引都不会被用到

##### 数据分布影响

如果MySQL评估使用索引比全表更慢，则不会使用索引

##### SQL提示

是优化数据库的一个重要手段，简单来说，就是在SQL语句中加入一些人为的提示来达到优化操作的目的

use index:

```mysql
explain select * from tb_user use index(idx_user_pro) where profession = '软件工程';
```

ignore index:

```mysql
explain select * from tb_user ignore index(idx_user_pro) where profession = '软件工程';
```

force index:

```mysql
explain select * from tb_user force index(idx_user_pro) where profession = '软件工程';
```

##### 覆盖索引

尽量使用覆盖索引（查询使用了索引，并且需要返回的列，在该索引中已经全部能够找到），减少使用select *

![image-20230821113039567](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230821113039567.png)

using index condition：查找使用了索引，但是需要回表查询数据

using where;using index：查找使用了索引，但是需要的数据都在索引列中能找到，所以不需要回表查询数据

![image-20230821113835945](https://github.com/Pumnn1ayLee/MySQL_NOTE/blob/main/images/image-20230821113835945.png)

最优方案：为username,password建立联合索引

##### 前缀索引

当字段类型为字符串(varchar,text等)时，有时候需要索引很长的字符串，这会让索引变得很大，查询时，浪费大量的磁盘IO，影响查询效率。此时可以只将字符串的一部分前缀，建立索引，这样可以大大节约索引空间，从而提高索引效率。

语法

```mysql
create index idx_xxxx on table_name(column(n));
```

前缀长度

可以根据索引的选择性来决定，选择性是指不重复的索引值（基数）和数据表的记录总数的比值，索引选择性越高查询效率越高

### SQL优化 

##### insert优化

###### 批量插入

```mysql
insert into tb_test values(1,'Tom'),(2,'Cat'),(3,'jerry');
```

###### 手动提交事务

```mysql
begin;
insert into tb_test values(1,'Tom'),(2,'Cat'),(3,'jerry');
insert into tb_test values(4,'Tom'),(5,'Cat'),(6,'jerry');
insert into tb_test values(7,'Tom'),(8,'Cat'),(9,'jerry');
commit;
```

###### 主键顺序插入

```mysql
主键乱序插入： 8 1 9 21 88
主键顺序插入： 1 2 3 4 5
```

###### 大批量插入数据-load

如果一次需要插入大批量数据，使用insert语句插入性能较低，此时可以使用load

```mysql
##客户端连接服务端时，加上参数--local-infile
mysql --local-infile -u root -p
##设置全局参数local_infile为1，开启从本地加载文件导入数据开关
set global local_infile = 1
##执行load指令将准备好的数据，加载到表机构中
load data local infile "/root/sql1.log" into table 'tb_user' fields terminated by ',' lines terminated by '\n';
```

##### 主键优化

尽量使用主键顺序插入

主键设计原则：

1.满足业务需求的情况下，尽量降低主键的长度。

2.插入数据时，尽量选择顺序插入，选择使用AUTO_INCREMENT自增主键

3.尽量不要使用UUID做主键或者是其他自然主键，如身份证号。

4.业务操作时，避免对主键的修改。

##### order by优化

```mysql
#根据age,phone进行降序一个升序一个降序
explain select id,age,phone from tb_user order by age asc,phone desc;
#创建索引
create index idx_user_age_phone_ad on tb_user(age asc,phone desc);
#根据age,phone进行降序一个升序一个降序
explain select id,age,phone from tb_user order by age asc,phone desc;
```

##### group by优化

在分组操作时，可以通过索引来提高效率

分组操作时，索引的使用也是满足最左前缀法则的。

##### limit优化

优化思路：

一般分页查询时，通过创建覆盖索引能够比较好的提高性能，可以通过覆盖索引加子查询形式进行优化

```mysql
explain select * from tb_sku t ,(select id from tb_sku order by id limit 20000,10) a where t.id = a.id;
```

