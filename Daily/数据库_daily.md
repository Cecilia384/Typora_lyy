### 9.11

SQL Vs MySQL

SQL是一种语言，而MySQL是基于这种语言的软件之一。实际上，MySQL、SQL Server、Oracle和PostgreSQL都是基于SQL语言的软件。由于它们来自不同的厂商，所以它们的部分语法会有一定的差别，不过大部分语法都是相同的(https://zhuanlan.zhihu.com/p/609117553

MySQL是一个开源的关系型数据库管理系统，它支持多用户、多线程和多表等特性。MySQL可以运行在各种操作系统上，包括Windows、Linux和Mac OS X等](https://blog.csdn.net/weixin_31354669/article/details/113130118)

SQL是一种标准化的语言，用于管理关系型数据库。它可以用来执行各种任务，例如查询数据、插入数据、更新数据和删除数据等](https://zhuanlan.zhihu.com/p/130768469)

因此，可以说MySQL是SQL的一种实现方式。它使用SQL语言来进行操作，并提供了许多其他功能和特性，例如事务处理、存储过程和触发器等](https://blog.csdn.net/weixin_31354669/article/details/113130118



### 10.11

[db-tutorial](https://github.com/dunwu/db-tutorial)



[youtube1_4h_SQL](https://www.youtube.com/watch?v=HXV3zeQKqGY)



- [x] [Learn SQL In 60 Minutes](https://www.youtube.com/watch?v=p3qvj9hO_Bo)

```mysql
create database record_company;
use record_company;
create table bands(
  id int not NULL auto_increment,
  name varchar(255) NOT NULL,
  primary key(id)
);
create table albums(
  id int not NULL auto_increment,
  name varchar(255) not NULL,
  release_year int,
  band_id int not NULL,
  primary key(id),
  foreign key (band_id) references bands(id)
);

insert into bands (name)
values('Iron Maiden');

insert into bands(name)
values ('Deuce'),('Avenge Sevenfold'),('Ankor');

select * from bands;

select * from bands limit 2;

select name from bands;

select id as 'ID',name as 'Band Name' from bands;

rename table bans to bands;

select * from bands order by id desc;

select * from bans order by name asc;

insert into albums(name, release_year, band_id)
values('The Number of the Beasts', 1985, 1),
	  ('Power Slave', 1984, 2),
      ('Nightmare', 2010, 3),
      ('Test Album', NULL, 3);
      
insert into albums(name, release_year, band_id)
values('Nightmare', 2018, 3);
select * from albums;
select distinct name from albums;

update albums
set release_year = 1982 
where id = 1; 

select * from albums
where release_year < 2000;

select * from albums
where name like '%er%' or band_id = 3;

select * from albums
where release_year = 1984 and band_id = 2;

select * from albums
where release_year between 2000 and 2018;

select * from albums
where release_year is NULL;

delete from albums where id = 4;

select * from albums;

update albums
set id = 4 where id = 5;

select * from bands
 left join albums on bands.id = albums.band_id;

select * from albums
join bands on bands.id = albums.band_id;

select avg(release_year) from albums;

select band_id, count(band_id) from albums
group by band_id;

select b.name as band_name,count(a.id) as num_albums
from bands as b
left join albums as a on b.id = a.band_id
where b.name = 'Deuce'
group by b.id
having num_albums = 1;

delete from bands where id = 5;
```



#### CMU_01-RelationalModel

- **DATA MODELS** 

  - Relational 

  - Key/Value 

  - Graph

  -  ==Document / XML / Object== (Leading Alternative)

  - Wide-Column / Column-family 

  - Array / Matrix / ==Vectors==( Current Hotness)

  -  Hierarchical 

  - Network 

  - Multi-Value

- **DOCUMENT DATA MODEL**

  > 文档数据模型 : 包含已命名字段/值对层次结构的记录文档集合。
  >  →字段的值可以是标量类型、值数组或其他文档。
  > →现代实现使用 JSON。旧系统使用 XML 或自定义对象表示法。通过将对象与数据库紧密耦合，避免 "关系对象阻抗失配"。

![img](%E6%95%B0%E6%8D%AE%E5%BA%93_daily.assets/%60F$F%5BFZ3UCLJM9OP@%25ZBQX1.png)

![img](%E6%95%B0%E6%8D%AE%E5%BA%93_daily.assets/P%7BEBTJ66R78R%60KL7LZJ3P8V.png)





**VECTOR DATA MODEL**

> 矢量数据模型
>  用于最近邻搜索（精确或近似）的一维数组。
> →用于对由 ML 训练的转换器模型（如 ChatGPT）生成的嵌入进行语义搜索。
> →与现代 ML 工具和 API（如 LangChain、OpenAI）的原生集成。这些系统的核心是使用专门的索引来快速执行 NN 搜索。

![img](%E6%95%B0%E6%8D%AE%E5%BA%93_daily.assets/8%5DU%60%5B58@G1BSFB6DIH%5B%5B4FJ.png)

 

 



#### 11.2

mysql重置密码

临时密码**root@localhost**: #gOMRS,EL6h-





#### 11.17

##### Concurrency Control

​	`txn:transaction`

**ACID**

![image-20231117222239346](%E6%95%B0%E6%8D%AE%E5%BA%93_daily.assets/image-20231117222239346.png)



#### 11.23

1.MYSQL bench导入txt/csv文件

[csdn](https://blog.csdn.net/qq_55345814/article/details/126646147)



2.#坑 [Error Code 1175. You are using safe update mode and you tried to update a table](https://www.cnblogs.com/jilili/p/14439189.html)

> Solution:
> set sql_safe_updates=off;
>
>  1、SET SQL_SAFE_UPDATES = 0;执行该命令更改mysql数据库模式。
>  2、在where判断条件中跟上主键id  例如：delete from firstmysqldatabase.user where UserName='zhangsan' and ID>=0;



3.**select 1**

在 SQL 查询中，`SELECT 1` 是一个常见的用法，表示在结果集中选择一个常量值 `1`。这种写法通常用于 `EXISTS` 或 `NOT EXISTS` 子查询中，目的是检查是否存在满足特定条件的行，而不需要实际选择或返回实际的数据。

例如，在 `EXISTS` 子查询中，`SELECT 1` 可以简单地检查条件是否为真（即是否存在满足条件的行），而不需要返回实际的数据。如果子查询返回至少一行结果，`EXISTS` 将会返回 `TRUE`，否则返回 `FALSE`。 

```sql
SELECT *
FROM table1 t1
WHERE EXISTS (
    SELECT 1
    FROM table2 t2
    WHERE t1.column = t2.column
);
```

这个查询会检查 `table1` 中是否存在满足条件 `table1.column = table2.column` 的行。在子查询中，`SELECT 1` 表示只需要确定是否存在这样的行，而不需要实际选择任何数据。
