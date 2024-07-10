# 连接MYSQL
``` shell
mysql [-h 127.0.0.1] [-p 3306] -u root -p
```


# SQL语法分类
| 分类 | 全称 | 说明 |
| ---- | ---- | ---- |
| DDL | Data Definition Language | 定义语言，定义数据库对象(数据库、表、字段) |
| DML | Data Manipulation Language | 操作语言，对表中数据进行增删改 |
| DQL | Data Query Language | 查询语言，查询表中数据 |
| DCL | Data Control Language | 控制语言，创建用户，修改访问权限 |
DML和DQL操作对象只是表中数据，DDL操作对象可以为数据库，表，是容器。


# DDL
## 数据库
###  创建数据库
``` sql
CREATE DATABASE [IF NOT EXISTS] <DATABASE NAME> [DEFAULT CHARSET <字符集>];
```
### 删除数据库
``` sql
DROP DATABASE [IF EXISTS] <DATABASE NAME>;
```
### 查询数据库
``` sql
SHOW DATABASES;    -- 查询所有数据库
SELECT DATABASE();  -- 查询当前数据库，就是看一下当前选中的是哪个数据库
```
### 使用数据库
``` sql
USE <DATABASE_NAME>;
```
## 表
### 创建表
```SQL
CREATE TABLE <TABLE_NAME> (
	Column1 datatype constraits,
	Column2 datatype constraits,
	Column3 datatype constraits,
	...
)
```
Datatype: [Datatype](数据库/link/link.md#Datatype)
Constraits: [Constraints](数据库/link/link.md#Constraints)
### 删除表
```SQL
DROP TABLE <TABLE_NAME>;    -- 直接删除表，不检查是否存在
-- 或
DROP TABLE [IF EXISTS] <TABLE_NAME>;

```
### 查询所有表
```SQL
SHOW TABLES;
```
### 查询表的结构
``` sql
DESC <TABLE_NAME>;
// 列出表的字段，默认值，主键等结构
```
### 查询建表时的语句
``` sql
SHOW CREATE TABLE <TABLE_NAME>;
```


# DML
## 插入数据
```SQL
INSERT INTO <TABLE_NAME> (Column1, Column2, ...)
VALUES(Value1, Value2, ...)
```
字段和值在位置上要一一对应，若选中了所有列，则列集合可以省略，按照表原有的列顺序一次给出其值。

未指定的字段（列）将会采用默认值，若有 `AUTO_IMCREMENT` 约束，则会在其前驱的基础上递增。

若 `DEFAULT` 为 `NULL` 而该字段又受到 `NULL:NO` 的约束，不指定值而采用默认值将会报错。

```SQL
INSERT INTO users
VALUES (NULL,'test', 'test@runoob.com', '1990-01-01', true);
```
这里 `NULL` 值为 `ID` 字段占位，`ID` 受`AUTO_IMCREMENT`约束，所以不会真为 `NULL`，而是递增。

```SQL
INSERT INTO users (username, email, birthdate, is_active)
VALUES
    ('test1', 'test1@runoob.com', '1985-07-10', true),
    ('test2', 'test2@runoob.com', '1988-11-25', false),
    ('test3', 'test3@runoob.com', '1993-05-03', true);
```
一次插入多行数据。


# DQL
## SELECT 查询数据
`SELECT` 语句可以用于查询表中特定数据
```SQL
SELECT <FIELD> FROM <TABLE_NAME>
```

## WHERE 过滤条件
用于条件过滤
```SQL
SELECT <FIELD> FROM <TABLE_NAME> WHERE <CONDITION>
```
### 操作符
| 操作符           | 描述            | 示例                                                                  |
| ------------- | ------------- | ------------------------------------------------------------------- |
| `=`           | 等于            | `WHERE field = value`                                         |
| `<>` 或 `!=`   | 不等于           | `WHERE field <> value` 或 `WHERE field != value`         |
| `>`           | 大于            | `WHERE field > value`                                         |
| `<`           | 小于            | `WHERE field < value`                                         |
| `>=`          | 大于等于          | `WHERE field >= value`                                        |
| `<=`          | 小于等于          | `WHERE field <= value`                                        |
| `BETWEEN`     | 在指定范围内        | `WHERE field BETWEEN value1 AND value2`                       |
| `NOT BETWEEN` | 不在指定范围内       | `WHERE field NOT BETWEEN value1 AND value2, [value1, value2]` |
| `IN`          | 等于指定列表中的某个值   | `WHERE field IN (value1, value2, ...)`                        |
| `NOT IN`      | 不等于指定列表中的任何值  | `WHERE field NOT IN (value1, value2, ...)`                    |
| `LIKE`        | 匹配模式（通常用于字符串） | `WHERE field LIKE 'pattern%'`                                 |
| `NOT LIKE`    | 不匹配模式         | `WHERE field NOT LIKE 'pattern%'`                             |
| `IS NULL`     | 是 NULL 值      | `WHERE field IS NULL`                                         |
| `IS NOT NULL` | 不是 NULL 值     | `WHERE field IS NOT NULL`                                     |
| `AND`         | 逻辑与，同时满足多个条件  | `WHERE condition1 AND condition2`                                   |
| `OR`          | 逻辑或，满足其中一个条件  | `WHERE condition1 OR condition2`                                    |
| `NOT`         | 逻辑非，否定条件      | `WHERE NOT condition`                                               |
| `LIMIT`       | 查询行数          | `WHERE LIMIT 10` 及 `WHERE LIMIT 20,10`                              |


# DCL
