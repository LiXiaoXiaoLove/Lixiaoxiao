## 今天学的命令

```

1. 查询表
   select * from exlxx; 
2. 清空表
   truncate table exlxx;
3. 删除表
   drop table exlxx;
4. 创建外部表
   create external table exlxx(id int,name string)
   row format delimited fields terminated by '\t'                
   location '/dbdata/women.log';
5. 创建内部分区表
   create table lxxtime(id int,name string)
   partitioned by(year string,month string)
   row format delimited fields terminated by '\t';
6. 查看一个表的分区
   show partitions lxxpart;
7. 查看表的结构
   desc lxxtime
8. 查看数据库的所有表
   show tables;
9. 查看当前所使用的数据库
   select current_database();
10.给表添加一列
   alter table users add columns(sex string);
11.修改列名
   alter table users change sex gerder string;
12.把表替换成 
   alter table users replace columns(name string);
13.添加分区+
   alter table lxxtime add partition(year='2018',month='10');
15.删除year=2018的所有分区
   alter table lxxtime drop partition(year='2018');
16.插入数据
   insert into table innerlxx values(1,'lxx');
17. 查看所有的数据库
   show databases;
18. 把一张表拷贝到别一张表中
    insert into woman
    select * from man;
19.  新建一份表women ，并把women里的name的那一列改名为username拷贝到women表中
     create women as
     select name as username from woman;
20. 从本地往数据库传数据（本地文件不消失）
    load data local inpath '/home/lxx/men.log' into table man;
21. 把hdfs上的文件传到数据库上（hdfs上的文件消失）
    load data inpath 'hdfs://namenode1:9000/uu.log' into table man;
22. 把hdfs上的文件传到数据库上（hdfs上的文件消失）
    load data inpath 'hdfs://192.168.107.143/uu.log' into table mans;

```