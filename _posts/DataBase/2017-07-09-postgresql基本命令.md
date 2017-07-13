---
layout: life
title: postgresql基本命令
category: DataBase
duoshuo: true
date: 2017-07-09
---

******

	作者: minus
	版本: V 0.0.1
	日期: 2017年7月9日

<!-- more -->

*******

### Postgresql 常用链接
```
1. 官方中文文档: http://postgres.cn/docs9.6/ [9.5 9.4]
2. pg资料大全: https://github.com/ty4z2008/Qix/blob/master/pg.md
1. 视图[http://postgres.cn/docs/9.6/tutorial-views.html]
2. 事务[http://postgres.cn/docs/9.6/tutorial-transactions.html]
3. 窗口函数[http://postgres.cn/docs/9.6/tutorial-window.html]
    * over
    * partition by
4. 继承[http://postgres.cn/docs/9.6/tutorial-inheritance.html]
5. SQL全集[http://postgres.cn/docs/9.6/sql-commands.html]
6. json数据类型: 12个Json相关函数: to_json/ row_to_json/ array_to_json  [http://www.zhangxiaojian.name/postgrsql-%e4%b8%ad%e7%9a%84-json-%e4%bb%8e%e4%bd%bf%e7%94%a8%e5%88%b0%e6%ba%90%e7%a0%81/]
7. 数组类型: 
8. MVCC(多版本并发控制)的原理：[http://www.jb51.net/article/52020.htm]
```

### Postgresql基本命令
0. 查看当前版本号 和 查看当前数据库 查看当前用户
	```
	select version();
	select current_database();
	select current_user;
	\c    -- 可以直接查看当前用户连接了哪个数据库
	```

0. 创建用户及数据库
	```
	CREATE USER postgres_user WITH PASSWORD 'password';
	CREATE DATABASE my_postgres_db OWNER postgres_user;
	```

1. 关闭指定数据库
	```
	select datname, pid from pg_stat_activity;  - 查看各数据库链接情况
	select pg_terminate_backend(11480);  -- 关闭数据库连接
	```
	
2. 查看表空间
	```
	\db   or  \db tablespace_name
	SELECT spcname FROM pg_tablespace; // 或者
	```
	
3. 查看数据库列表
	```
	\l
	SELECT datname from pg_database;  // 或者
	```
	
4. 查看数据库表: 只能查看当前 search_path　这个schema中的表（默认是public）,若要看其他schema下的表则需要修改search_path
	```
	\dt
	```
	
5. 给数据库设置参数
	```
	ALTER DATABASE mydb SET geqo TO off;
	```
	
6. 删除数据库
	```
	drop database dbname;
	```
	
7. 创建指定路劲的表空间
	```
	create tablespace fastspace location '/mnt/sda1/postgresl/data';  //注意该路径必须在集群每台机器上都要事先创建好（空目录且属于postgresql系统用户），不然会报错 
	show default_tablespace;  // 显示默认表空间
	\db; \db ts_name          // 显示所有表空间信息
	```
	
8. 删除表空间
	```
	drop tablespace xxx;
	```
	
9. 创建表
	```
	create table foo (i int) tablespace space1;  // 将一个表创建在一个具体的表空间里面
	alter table foo owner xxx;
	CREATE TABLE EMPLOYEE (EMPID INT, NAME TEXT) DISTRIBUTE BY HASH (EMPID) TO datanode1, datanode2; // 设定分片键并指定数据保持的节点
	```
	
10. 设置缺省／默认的表空间
	```
	数据库集群初始化自动创建两个表空间
        pg_global　表空间用于共享的系统表
        pg_default 是template1和template0 数据库的缺省表空间
        为 'create table' | 'create index' | 'create database' 提供一个隐含的表空间
	> set default_tablespace = space1;
	> create table foo(i int);    // 该表就创建在space1　这个表空间里
	```
	
11. [创建/删除角色](http://files.postgres-xl.org/documentation/user-manag.html)
	```
	> create role name;
	> create role name LOGIN;
	> drop role name;
	```
	
12. 查看用户
	```
	> \du
	> SELECT rolname FROM pg_roles;
	```
	
13. 查看表结构
	```
	\d table_name;
	\d+ table_name;
	```
	
14. 表中添加字段
	```
	> alter table [表名] add column [字段名] [类型]; 
	> alter table [表名] drop column [字段名]; 
	> alter table [表名] rename column [字段名A] to [字段名B]; 
	> ALTER TABLE journal ALTER keyword TYPE character(350)
	```
	
15. 表重命名
	```
	> alter table [表名A] rename to [表名B]
	```
	
16. 查看当前以什么用户登陆什么数据库
	```
	> \c
	> \c another-database username　: 连接到另一个数据库
	> \c database1 user1 : 以user1用户登陆数据库database1
	```
	
17. 查看全部schemas　
	```
	http://www.freeoa.net/osuport/db/postgres-db-schema-table-space-user-refer_3073.html
	schemas包含数据库对象（表／视图／索引／包／过程／函数／queues/triggers/types/sequences/等等）的集合，
	schemas　属于逻辑概念,可在不同模式下创建相同的表名
	> \dn
	```
	
18. 查看当前所处的schema
	```
	select current_schema();
	show search_path;
	```
	
19. 修改数据库属性(schema)
	```
	ALTER DATABASE mydatabase SET search_path TO myschema, public, pg_catalog;
	```
	
20. [创建用户](https://support.rackspace.com/how-to/postgresql-creating-and-dropping-roles/)
	```
	CREATE ROLE minus CREATEROLE CREATEDB SUPERUSER LOGIN ;　-　用户设置权限
	grant all on database gpadmin to minus;              -　用户授权数据库
	alter ROLE gpadmin with password 'minus';            - 用户设置密码
	```
	
21. 创建/删除 schema : schema 是跟 数据库走，而不是用户走 
	```
	CREATE SCHEMA myschema;   // 归属者默认为当前登陆的用户
	CREATE SCHEMA schemaname AUTHORIZATION username;   // 指定schema的归属者
	DROP SCHEMA myschema;
	DROP SCHEMA myschema CASCADE; - 删除 schema　下的所有表／数据／函数等等
	```
	
22. 查看一个数据库在哪个表空间上
	```
	select datname, dattablespace from pg_database where datname ='chaoqian';
	select oid,spcname from pg_tablespace where oid=16396;
	```
	
23. 查看schema的默认路径和重新设置
	```
	show search_path;                             -- show the current search_path
	create schema my_schema ;grant all on schema xxx to user;  -- create another schema    
	set search_path to my_schema;                 -- change search_path on a connection-level 临时改变
	alter database xxx set search to my_schema;   -- change search_path on a database-level 　一直改变
	```
	
24. 设置默认表空间
	```
	set default_tablespace=tablespacename
	```
	
25. [copy csv to pg_table](http://www.postgresguide.com/utilities/copy.html)
	```
	\copy address (id, name, parentid, level, checkid, flag) from '/home/minus/Seafile/Seafile/yuqing_bgdev/personal/minus/pg_cp/address.csv' with csv header;
	\copy address (id, name, parentid, level, checkid, flag) from '/home/minus/Seafile/Seafile/yuqing_bgdev/personal/minus/pg_cp/address.csv' delimiter ','  csv header;
	\copy my_table to 'filename' csv header    -  导出1
	\COPY (select id,name from tablename) TO 'filepath/aa.csv' DELIMITER ',' CSV HEADER;  - 导出2
	```
	
26. pg命令行中执行 linux命令
	```
	\cd path
	\! ls 
	\! pwd
	```
	
27. pg命令行中开启时间计时器
	```
	\timing
	```
	
28. pg命令中开启一个linux的shell
	```
	\!　　　　-  进入shell
	exit 　　－　表示退出
	```
	
29. 查询缓存
	```
	\p             显示查询缓存区的内容 
	\r             重置(清除)查询缓存区 
	```
	
30. 命令行中执行sql文件
	```
	\i basics.sql
	```
	
31. 查看安装的插件
	```
	\dx
	```
	
32. 查询本地外部表
	```
	\dE
	select * from pg_foreign_table
	```
	
33. 查看自定义函数
	```
	\df
	```
	
34. [执行计划解释](https://www.postgresql.org/docs/9.5/static/using-explain.html)
	```
	explain(select count(1) from com_patientinfo);
	explain analyze(select count(1) from com_patientinfo);  - 可以查看 执行计划时间和　执行时间
	```
	
35. 创建索引
	```
	CREATE INDEX test1_id_index ON test1 (id);           - B-Tree索引
	CREATE INDEX name ON table USING hash (column);      - Hash索引
                                                             - GIST索引
                                                             - GIN索引  
	CREATE UNIQUE INDEX name ON table (column [, ...]);　- 唯一索引：只有B-Tree索引可以被声明为唯一索引
	```
	
36. psql命令修改默认状态
	```
	在~/.psqlrc中写入一下信息,　如：
	\timing  : psql进入自动带有时间计算功能
	```
	
37. 查看enum 的所有类型取值情况
	```
	select t.typname, e.enumlabel from pg_type t, pg_enum e where t.oid=e.enumtypid;
	```
	
38. 删除enum类型
	```
	drop type rw_value
	```
	
39. 修改　数据库　管理员　密码 (远程登陆需要)
	```
	alter ROLE gpadmin with password 'minus';
	```
	
40. 查找某个表的相对路径
	```
	select pg_relation_filepath('item');
	```
	
41. 查看数据库/表/表空间/索引大小等[pg大小默认是Byte, 得到MB 得需要除以 1024*1024]
	```
	select pg_database_size(current_database());    -- 查看当前库大小
	select sum(pg_database_size(datname)) from pg_database;   -- 查询所有库大小之和
	select pg_size_pretty(pg_relation_size('indexnamt'));            -- 查询一个索引大小
	select pg_size_pretty(pg_total_relation_size('test5'));    -- pg_size_pretty函数直接得到 MB
	select pg_total_relation_size('accounts');      -- 查询包含表和表索引其他总大小
	select pg_tablespace_size('tbs_index')/1024/1024 as 'size m';   -- 查看表空间大小
	select indexrelname,pg_size_pretty( pg_relation_size(relid)) from pg_stat_user_indexes where schemaname = 'schemaname' order by pg_relation_size(relid) desc; --查看所有 schema里面索引大小，大到小的顺序排列：
	select relname, pg_size_pretty(pg_relation_size(relid)) from pg_stat_user_tables where schemaname = 'schemaname' order by pg_relation_size(relid) desc;   --查看所有 schema里面表的大小，从大到小顺序排列：
	select pg_database.datname,pg_size_pretty(pg_database_size(pg_database.datname)) AS size from pg_database;  --查看数据库大小：
	>
	select date_trunc('second', current_timestamp - pg_postmaster_start_time()) as uptime;  -- 查看数据库开启多久
	select pg_postmaster_start_time();    -- 什么时候开启的
	```
	
42. [数据类型转化](http://www.postgresqltutorial.com/postgresql-cast/)
	```
	CAST ( expression AS type );
	'xxx'::type    ->  SELECT CAST ('100' AS INTEGER);
	```
	
43. Vacuum
	```
	-vacuum 就是进行扫除，找到那些旧的“死”数据，把它们所知的行标记为可用状态。但是它不进行空间合并。
 	-vacuum full，就是除了 vacuum，还进行空间合并，因此它需要lock table。
	-而 autovacuum，可以理解为 定时自动进行  vacuum 。
 	-对于有大量update 的表(被频繁操作)，vacuum full是没有必要的，因为它的空间还会再次增长，所以vacuum就足够了。
	- vacuum full requires exclusive lock on the table it is working on
	- 当一个表存在大量的死行数据的话，你需要使用vacuum full
	```
	
### [系统表](http://files.postgres-xl.org/documentation/catalogs.html)
1. pg_database　: 查看各个数据库情况
    	```
	select * from pg_database;
    	```

2. pg_authid : 查看系统用户及其权限
    	```
	select * from pg_authid;
    	```
    
3. pg_tablespace : 查看系统表空间
	```
	select * from pg_tablespace;
	```
    
4. pg_class : 包含所有数据对象:table, index, view
	```
	select * from pg_class;
	```
    
5. pg_roles - pg_user : 包含数据库用户信息
	```
	select * from pg_roles / pg_user;
	```
    
6. pg_views : 视图查看
	```
	select * from pg_views;
	```
    
7. pg_tables : 数据表查看
	```
	select * from pg_tables;
	```
    
8. pgxc_node : 数据库节点情况
	```
	select * from pgxc_node;
	```
    
9. 创建 plpython
    ```
    安装plpython插件： sudo apt-get install postgresql-contrib postgresql-plpython
    进入psql:　create extension plpythonu;
    ---创建函数---
    CREATE FUNCTION pymax (a integer, b integer)
      RETURNS integer
    AS $$
      if a > b:
        return a
      return b
    $$ LANGUAGE plpythonu;
    ---使用函数---
    select pymax(6,2);
    ```

10. 查看数据表块数/记录数
	```
	select relpages,reltuples from pg_class where relname = 'test2';
	```
    
### 特殊语法
1. 聚合组件：grouping set | cube | rollup
	```
	select brand, size, sum(sales) from items_sold group by grouping sets ((brand),(size),())
	```
2. IS DISTINCT FROM | IS NOT DISTINCT FROM
	```
	对于非空输入，IS DISTINCT FROM与<>操作符相同。但是，假如两个输入都是空，那么它将返回假，而如果只有一个输入是空，那么它将返回真。相似地，对于非空输入IS NOT DISTINCT FROM和=是一样的，但是它在两个输入为空时返回真，只有一个输入为空是返回假。所以，这些结构实际上表现得似乎空值是一个普通数据值，而不是"未知"。
	```
3. [pg常用的字符串操作符函数](http://postgres.cn/docs/9.5/functions-string.html)
	```
	SQL字符串函数
	如: trim() lower() substring() chr()
	```
	```
	[数据类型格式化函数](http://postgres.cn/docs/9.5/functions-formatting.html)
	如: to_char  to_date to_number
	```
	```	
	[时间类函数](http://postgres.cn/docs/9.5/functions-datetime.html)
	PostgreSQL提供了许多返回当前日期和时间的函数:
	CURRENT_DATE
	CURRENT_TIME
	CURRENT_TIMESTAMP
	CURRENT_TIME(precision)
	CURRENT_TIMESTAMP(precision)
	LOCALTIME
	LOCALTIMESTAMP
	LOCALTIME(precision)
	LOCALTIMESTAMP(precision)
    ```
4. [pg模式匹配](http://postgres.cn/docs/9.5/functions-matching.html)
    * like 
        ```
        'abc' LIKE 'abc'    true
        'abc' LIKE 'a%'     true
        'abc' LIKE '_b_'    true
        'abc' LIKE 'c'      false
        ```
    * similar
        ```
        string SIMILAR TO pattern [ESCAPE escape-character]
        string NOT SIMILAR TO pattern [ESCAPE escape-character]
        ```
    * POSIX正则表达式
        ```
        regexp_matches
        ```

### postgresql 文件路径
1. 配置文件
	```
	/etc/postgresql/9.5/main
	```
	
2. 插件位置
	```
	/usr/share/postgresql/9.5/extension
	```
	
3. 可执行文件路径
	```
	/usr/lib/postgresql/9.5/bin
	```

### postgresql 如何实现远程登陆
1. 修改 /etc/postgresql/9.5/main/pg_hba.conf
	```
	添加如下(0.0.0.0对任何网段均可访问，md5表示密码登陆)：
	type  database user   address     method
	host  all      all    0.0.0.0/0   md5
	```

2. 修改 /etc/postgresql/9.5/main/postgresql.conf
	```
	listen_addresses = '*'
	```

3. 重启pg
	```
	sudo service postgresql restart
	```
