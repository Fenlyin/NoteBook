### 连接MYSQL
``` shell
mysql [-h 127.0.0.1] [-p 3306] -u root -p
```
### SQL语法分类
| 分类 | 全称 | 说明 |
| ---- | ---- | ---- |
| DDL | Data Definition Language | 定义语言，定义数据库对象(数据库、表、字段) |
| DML | Data Manipulation Language | 操作语言，对表中数据进行增删改 |
| DQL | Data Query Language | 查询语言，查询表中数据 |
| DCL | Data Control Language | 控制语言，创建用户，修改访问权限 |
DML和DQL操作对象只是表中数据，DDL操作对象可以为数据库，表，是容器
### DDL
#### 数据库操作
#####  创建数据库
``` sql
CREATE DATABASE [IF NOT EXISTS] <DATABASE NAME> [DEFAULT CHARSET <字符集>];
```
##### 删除数据库
``` sql
DROP DATABASE [IF EXISTS] <DATABASE NAME>;
```
##### 查询数据库
``` sql
SHOW DATABASES;    // 查询所有数据库
SELECT DATABASE();  // 查询当前数据库，就是看一下当前选中的是哪个数据库
```
##### 使用数据库
``` sql
USE <DATABASE NAME>;
```
#### 表操作
##### 查询所有表
``` sql
SHOW TABLES;
```
##### 查询表的结构
``` sql
DESC <TABLE NAME>;
// 列出表的字段，默认值，主键等结构
```
##### 查询建表时的语句
``` sql
SHOW CREATE TABLE <TABLE NAME>;
```
### DML

### DQL

### DCL


