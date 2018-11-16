## 今天学的命令

### 基础命令

```

8. 查看数据库中现有的表
   show tables;
9. 查看当前所使用的数据库
   select current_database();
17. 查看现有的数据库
   show databases;
3. 删除表
   drop table exlxx;   
2. 清空表
   truncate table exlxx;
6. 查看表分区
   show partitions lxxpart;
7. 查看表的结构
   desc lxxtime
8. 查看系统的函数
   show functions;

```

### 修改表

```
9. 重命名表
   alter table users rename to goodsname;
10.给表添加一列
   alter table users add columns(sex string);
11.修改列名
   alter table users change sex gerder string;
12.把表替换成 
   alter table users replace columns(name string);
13.添加分区
   alter table lxxtime add partition(year='2018',month='10');
15.删除year=2018的所有分区
   alter table lxxtime drop partition(year='2018');
   
```

### 导入数据

```
19. 插入数据(单条插入)
    insert into table innerlxx values(1,'lxx');   
20. 把hdfs上的文件传到数据库上（hdfs上的文件消失）
    load data inpath '/men.log' into table man;
21. 把hdfs上的文件传到数据库上（hdfs上的文件消失）
    load data inpath 'hdfs://namenode1:9000/men.log' into table man;
22. 把hdfs上的文件传到数据库上（hdfs上的文件消失）
    load data inpath 'hdfs://192.168.107.143/men.log' into table mans;   
20. 从本地往数据库传数据（本地文件不消失）
    load data local inpath '/home/lxx/men.log' into table man;

```

### CTAS

* 将 Hive的查询结果直接存在一个新的表，这种情况被称为CTAS

```

18. 把一张表拷贝到别一张表中
    insert into woman
    select * from man;
19.  新建一份表women ，并把women里的name的那一列改名为username拷贝到women表中
     create table women as
     select name as username from woman;
	 
```

### 创建不同类型的表

```

4. 创建外部表
   create external table exlxx(id int,name string)
   row format delimited fields terminated by '\t'                
   location '/dbdata/women.log';
5. 创建内部分区表
   create table lxxtime(id int,name string)
   partitioned by(year string,month string)
   row format delimited fields terminated by '\t';

6. 创建桶表
    create table goodsbucket(goodsid int,name string)
    clustered by(goodsid) into 3 buckets
    row format delimited fields terminated by '\t';
	 
```

### 查询表

```

1. 查询表
   select * from exlxx;
2. 获取倒数三名学生的信息
   select * from company_emp
   order by money limit 3;
3. 查看各部门的平均工资
   select dep,avg(money)
   from company_emp
   group by dep;

```

### 关联查询

```

1. 连接
   select o.*,g.*
   from orders o
   join
   goods g
   on o.goodsid=g.goodsid;

2. 内连接
   select o.*,g.*
   from orders o
   inner join
   goods g
   on o.goodsid=g.goodsid;
   
3. 全连接
   select o.*,g.*
   from orders o
   full join
   goods g
   on o.goodsid=g.goodsid;
   
4. 左半连接
   select o.*
   from orders o
   left semi join
   goods g
   on o.goodsid=g.goodsid;

```

### in

```

1. select * from orders o
   where o.goodsid in(
                  select g.goodsid
                  from goods g
   );

```

### 使用数组

* 元数据arrays.log

```

战狼2,吴京:吴刚:余男,2017-08-16
三生三世十里桃花,刘亦菲:痒痒,2017-08-20
羞羞的铁拳,沈腾:玛丽:艾伦,2017-12-20

```

```

1. create table movies(name string,actors array<string>,times date )
   row format 
   delimited fields terminated by ','
   collection items terminated by ':'; 
   
2. load data inpath '/dbdata/arrays.log' into table movies;

3. select * from movies;

4. select name,actors[0] from movies;

```

![数组](https://upload-images.jianshu.io/upload_images/14863832-ffc33ecbf1561908.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![selectArray](https://upload-images.jianshu.io/upload_images/14863832-ccb0af0f41dc2f56.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 使用map

* 原数据表maps.log

```

1,zhangsan,father:xiaoming#mother:xiaohuang#brother:xiaoxu,28
2,lisi,father:mayun#mother:huangyi#brother:guanyu,22
3,wangwu,father:wangjianlin#mother:ruhua#sister:jingtian,29
4,mayun,father:mayongzhen#mother:angelababy,26

```

* 步骤

```

1. create table maps(id int,name string,family map<string,string>,age int)
   row format
   delimited fields terminated by ','
   collection items terminated by '#'
   map keys terminated by ':';
   
2. load data inpath '/dbdata/maps.log' into table maps;

3. select * from maps;

4. select name,family['father'] from maps;

```

![map](https://upload-images.jianshu.io/upload_images/14863832-e251fbd120fd4ef0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![selectMap](https://upload-images.jianshu.io/upload_images/14863832-8cc83d72eea9ae5a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 使用结构体

结构体

* 新建数据structs.log

```

1,zhangsan,18:male:beijing
2,lisi,28:female:shanghai

```

* 步骤

```

1. 新建表
   create table structs(id int,name string,info struct<age:int,gender:string,addr:string>)
   row format
   delimited fields terminated by ','
   collection items terminated by ':';

2.导入数据
  load data inpath '/dbdata/structs.log' into table structs;

3.查看结构体
  select id,name,info.age from structs;

```

![结构体](https://upload-images.jianshu.io/upload_images/14863832-62ef5f7a2839a9d4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 作业1

* 元数据access.log

```

访客	月份	访问次数
A	2015-01	5
A	2015-01	15
B	2015-01	5
A	2015-01	8
B	2015-01	25
A	2015-01	5
A	2015-02	4
A	2015-02	6
B	2015-02	10
B	2015-02	5

```

* 步骤

```

1. select *
   from 
  (select ke,month,sum(accesssum) from access group by ke,month) a1
  join
  (select ke,month,sum(accesssum) from access group by ke,month) b1
  on a1.ke=b1.ke;

```

![image.png](https://upload-images.jianshu.io/upload_images/14863832-868df3b6e67e821c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```

2. select a1.*,sum(cnt)
   from 
   (select ke,month,sum(accesssum) as sum from access group by ke,month) a1
   join
   (select ke,month,sum(accesssum) as cnt from access group by ke,month) b1
   on a1.ke=b1.ke
   group by a1.ke,a1.month,a1.sum;

```

![image.png](https://upload-images.jianshu.io/upload_images/14863832-03d8e98b9cc00ddd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
 
3. select *
   from 
   (select ke,month,sum(accesssum) from access group by ke,month) a1
   join
   (select ke,month,sum(accesssum) from access group by ke,month) b1
   on a1.ke=b1.ke
   where a1.month >= b1.month;

```

![image.png](https://upload-images.jianshu.io/upload_images/14863832-df33ca2f542d6f8a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
 
4. select a1.*,sum(cnt)
   from 
   (select ke,month,sum(accesssum) as sum from access group by ke,month) a1
   join
   (select ke,month,sum(accesssum) as cnt from access group by ke,month) b1
   on a1.ke=b1.ke
   where a1.month >= b1.month
   group by a1.ke,a1.month,a1.sum;

```

![image.png](https://upload-images.jianshu.io/upload_images/14863832-293af08e4a771f4c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

