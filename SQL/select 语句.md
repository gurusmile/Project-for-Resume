# SQL

SQL Notes from w3school（https://www.w3school.com.cn/sql/index.asp）
## 简介
#### 关系型数据库管理系统（RDBMS）vs. 非关系型数据库管理系统
#####  关系型数据库
关系模型指的就是**二维表格模型**，而一个关系型数据库就是由二维表及其之间的联系所组成的一个数据组织。
#####  非关系型数据库
非关系型数据库不像关系型数据库，有几种数据库能够一统江山，非关系型数据库非常多，并且大部分都是开源的。

* 面向**高性能并发读写的key-value数据库**：key-value数据库的主要特点即使具有极高的并发读写性能，Redis,Tokyo Cabinet,Flare就是这类的代表
* 面向**海量数据访问的面向文档数据库**：这类数据库的特点是，可以在海量的数据中快速的查询数据，典型代表为MongoDB以及CouchDB
* 面向**可扩展性的分布式数据库**：这类数据库想解决的问题就是传统数据库存在可扩展性上的缺陷，这类数据库可以适应数据量的增加以及数据结构的变化

## 语法
一定要记住，SQL 对大小写不敏感！
##### 语法技能list

-DML: 表内活动
-DDL: 整表，表间，数据库活动

查询和更新指令构成了 SQL 的数据操作语言（DML）部分：
* SELECT - 从数据库表中获取数据
* UPDATE - 更新数据库表中的数据
* DELETE - 从数据库表中删除数据
* INSERT INTO - 向数据库表中插入数据


SQL 的数据定义语言 (DDL) 部分使我们有能力**创建或删除表格**。我们也可以**定义索引（键），规定表之间的链接，以及施加表间的约束**。
SQL 中最重要的 DDL 语句:
* CREATE DATABASE - 创建新数据库
* ALTER DATABASE - 修改数据库
* CREATE TABLE - 创建新表
* ALTER TABLE - 变更（改变）数据库表
* DROP TABLE - 删除表
* CREATE INDEX - 创建索引（搜索键）
* DROP INDEX - 删除索引

## 基础教程
低级选择数据
```sql
Select 列1，列2,
From tablename
```
```sql
Select *               -- 所有列
From tablename
````
```sql
select distinct row    -- 删除列中重复值，保持唯一性
from tablename
```
```sql
select row
from tablename
where row = 0       -- 对选择的表格进行限制
and (row1=1          -- 且条件
or row2='SQL'  )     -- 或条件
order by row desc, row1 asc  -- desc降序排列，asc升序排列，缺失为升序
```
插入一行
```sql
insert into tablename 
values (1,2,'Apple')
```
```sql
insert into tablename (row, row2)
values (1, 'Apple')
```
修改数据
```sql
update tablename
set row = 2
where row = 1
```
删除一行
```sql
delete 
from tablename
where row2='SQL'
```
删除所有行，但为删除表
```sql
Delete 
from tablename

Delete *
from tablename
```

## 高级教程

##### TOP
选择前x条/前x%的数据
```sql
select top x *
- select x%  row1 
from tablename
```

##### LIKE
选择文本满足条件的数据
(实例：row2中包含QL的数据。单引号是文本标配，%是通配符)
```sql
select row2
from tablename
where row2 like '%QL%'
```
##### 通配符

SQL 通配符可以**替代**一个或多个字符。
SQL 通配符必须与 **LIKE** 运算符一起使用。

| 通配符 |  描述 |
| --- | --- |
| % | 替代一个或多个字符 |
|\_(下划线) | 仅替代一个字符|
|  [charlist] | 字符列中的任何单一字符 |
| [^charlist]或者[!charlist] | 不在字符列中的任何单一字符 |

例3，以A或S开头的row2，例四，不以A且不以S开头的row2

```sql
select row2
from tablename
where row2 like 'a%'
where row2 like '_p_le'
where row2 like '[AS]%'
where row2 like '[!AS]%'
```
##### IN
IN 操作符允许我们在 WHERE 子句中规定多个值。
```sql
select row2, row1
from tablename
where row2 in ('Apple','SQL')
where row1 in (0,1)
```
##### BETWEEN
BETWEEN 操作符在 WHERE 子句中使用，作用是选取介于两个值之间的数据范围。
操作符 BETWEEN ... AND 会选取介于两个值之间的数据范围。这些值可以是**数值、文本或者日期**。

**重要事项**：不同的数据库对 BETWEEN...AND 操作符的处理方式是有差异的。某些数据库会列出介于 "Adams" 和 "Carter" 之间的人，但不包括 "Adams" 和 "Carter" ；某些数据库会列出介于 "Adams" 和 "Carter" 之间并包括 "Adams" 和 "Carter" 的人；而另一些数据库会列出介于 "Adams" 和 "Carter" 之间的人，包括 "Adams" ，但不包括 "Carter" 。

```sql
select row1, row2
from tablename
where row1 between 0 and 1
where row2 between 'Apple' and 'Sql'  --按字母排序
```

##### AS
通过使用 SQL，可以为**列名称**和**表名称**指定别名（Alias）。
```sql
select row2 as company
from tablename as T1
```

##### 重要系列 join
**SQL join** 用于根据两个或多个表中的列之间的关系，从这些表中查询数据。
**Key**：具有唯一性的某一列

```sql
select t1.row1, t1.row2, t2.row1, t2.row2
from t1 inner join t2
on t1.key = t2.key
```
**Join的类型**
* JOIN =INNER JOIN: 如果表中有至少一个匹配，则返回行
* LEFT JOIN: 即使右表中没有匹配，也从左表返回所有的行
* RIGHT JOIN: 即使左表中没有匹配，也从右表返回所有的行
* FULL JOIN: 只要其中一个表中存在匹配，就返回行

Table 1

| Key_1  | Score |
| --- | --- |
| 1 | A |
| 2 | B |
| 3 | C |
| 4 | D |

Table 2

| Key_2  | Name | Key_1  |
| --- | --- | --- |
| 1 | 11 | 1 |
| 2 | 22 | 1 |
| 3 | 33 | 2 |
| 4 | 44 | 2 |
| 5 | 55 | 4 |
| 6 | 66 | 5 |

```sql
select table1.key_1,key_2,name,score
from table1 join table2
on table1.key_1=table2.key1
```
Join的结果

| Key_1 |  Key_2 | Name  |  Score |
| --- | --- | --- | --- |
| 1 | 1 | 11 | A |
| 1 | 2 | 22 | A |
| 2 | 3 | 33 | B |
| 2 | 4 | 44 | B |
| 4 | 5 | 55 | D |

```sql
select  table1.key_1,key_2,name,score
from table1 left join table2
on table1.key_1=table2.key1
```

Left Join的结果

| Key_1 |  Key_2 | Name  |  Score |
| --- | --- | --- | --- |
| 1 | 1 | 11 | A |
| 1 | 2 | 22 | A |
| 2 | 3 | 33 | B |
| 2 | 4 | 44 | B |
| 3 |   |      | C |
| 4 | 5 | 55 | D |

```sql
select  table1.key_1,key_2,name,score
from table1 right join table2
on table1.key_1=table2.key1
```

Right Join的结果

| Key_1 |  Key_2 | Name  |  Score |
| --- | --- | --- | --- |
| 1 | 1 | 11 | A |
| 1 | 2 | 22 | A |
| 2 | 3 | 33 | B |
| 2 | 4 | 44 | B |
| 4 | 5 | 55 | D |
|   | 6 |  66  |  |

```sql
select  table1.key_1,key_2,name,score
from table1 full join table2
on table1.key_1=table2.key1
```

Full Join的结果

| Key_1 |  Key_2 | Name  |  Score |
| --- | --- | --- | --- |
| 1 | 1 | 11 | A |
| 1 | 2 | 22 | A |
| 2 | 3 | 33 | B |
| 2 | 4 | 44 | B |
| 3 |   |      | C |
| 4 | 5 | 55 | D |
|   | 6 |  66  |  |

##### UNION
Union 将一张表贴在另一张表的后面
* SELECT 语句必须拥有相同数量的列
* 列也必须拥有相似的数据类型
* 每条 SELECT 语句中的列的顺序必须相同
* 列名不需要一致，最后结果以第一条select的列名呈现

* Union - 会删除Table1 & 2的重复值
* Union all - 保留Tbale1 & 2的全部信息

```sql
select ID, name_p, score
from table1
union (all)
select ID_p, student_name, tier
from table2
```

##### SELECT INTO
select into
SELECT INTO 语句从一个表中选取数据，然后把数据插入另一个表中。
SELECT INTO 语句常用于创建表的**备份复件**或者用于**对记录进行存档**。

```sql
SELECT *
INTO table1_backup IN 'Backup.mdb'  --备份另一个数据库
FROM table1
```
##### CREATE
创建数据库和表格
```sql
create database my_db
create table table3
( ID int,
Name_p varchar(255)       --数据类型是 varchar，最大长度为 255 个字符
)
insert into table3 (ID,Name_p)
values (1, 'Apple')
```

##### 数据类型

| 数据类型  | 描述  |
| --- | --- |
| integer(size) int(size) smallint(size) tinyint(size) | 仅容纳整数。在括号内规定数字的最大位数。size规定数字的最大位数。 |
|decimal(size,d) numeric(size,d)  |  容纳带有小数的数字。size规定数字的最大位数。d规定小数点右侧的最大位数。|
| char(size) | 容纳固定长度的字符串（可容纳字母、数字以及特殊字符）。在括号中规定字符串的长度。 |
|  varchar(size)| 容纳可变长度的字符串（可容纳字母、数字以及特殊的字符）。在括号中规定字符串的最大长度。 |
| date(yyyymmdd) | 容纳日期。 |

##### Constraints
约束用于限制加入表的数据的类型。

* NOT NULL      - 如果不向字段添加值，就无法插入新记录或者更新记录。
* UNIQUE         - 数据唯一性，可以对多列进行设置
* PRIMARY KEY  - 数据唯一性，只能设置一个（可以联合多列进行设置）
* FOREIGN KEY  - 本表中存在的其他表的key
* CHECK           - 撤销primary key 
* DEFAULT        - 用于向列中插入默认值


```sql
create table table3
( ID int not null primary key check(ID>0),                  --直接加
Name_p varchar(255) not null unique,   
key_t1 int foreign key references table1(Key_1),
City varchar(255) default 'Shanghai'
)   
--mysql: 
--(ID int, Name_p int, 
--unique(Name_p)，
--primary key(ID)
--foreign key (key_t1) references table1(Key_1)
--check(ID>0)
--)
```

```sql
create table table3
...
constraint idname unique ( ID, Name_p)  --对多列唯一值设置新名称idname
constraint idname primary key ( ID, Name_p) 
constraint id_t1 foreign key (key_t1) references table1(Key_1)
constraint idname check (ID>0 and name_p <>'Julia')
```

```sql
alter table table3                               -- 更改已存在表格
add unique (ID)               
add primary key (ID)                           -- ID 必须 Not Null
add foreign key (key_t1) references table1(Key_1)
add check(ID>0)
add constraint idname unique (ID, Name_p)
add constraint idname primary key ( ID, Name_p)  -- ID，Name_p 必须 Not Null
add constraint id_t1 foreign key (key_t1) references table1(Key_1)
add constraint idname check (ID>0 and name_p <>'Julia')
```
```sql
drop constraint idname                      -- 撤销unique /primary key /check
--mysql drop index idname                   -- 撤销unique
--mysql drop primary key
--mysql drop foreign key id_t1
--mysql drop check idname
```

