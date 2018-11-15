## hive HQL

```

hive 是基于hadoop的一个数据仓库
     并提供了sql的查询功能
	 hive将sql语句转换成了MapReduce任务来运行

```

## hive特点

```

1. 可扩展性：hive可以自由的扩展集群的规模，一般情况下不需要重启

2. 延展性：hive支持自定义的函数

3. 容错性

```

## hive使用

```

1 cli（shell终端命令行）
1.1 先使用hive命令进入hive环境
1.2 在进行select等操作
2. jdbc：是hive的基于jdbc操作提供的客户端，
   用户通过jdbc连接至hive server，通过浏览器访问hive
2.1 先用shell打开有hive环境与mysql环境的namenode或datanode
    运行 hiveserver2 脚本
2.2 在开一个该ip的会话，运行 beeline ，进入该环境
2.3 用 !connect jdbc:hive2://localhost:10000 进行连接，
    按指令输入用户名与密码（若没密码敲回车）
2.4 进行select等操作

```

## hive中为什么要有元数据库（mysql）？

```

因为hive表所对应的数据是存储在hdfs上的，所以真正的数据是存在datanode上的，
而要找到datanode上的数据，我们就需要把这个关联进行记录

```

## hive与hadoop放入关系

```

hive依赖于HDFS来存储数据，hive将HQL转换成MapReduce来执行
所以说，hive是基于hadoop的一个数据仓库工具
实质上就是一款基于HDFS的MapReduce的计算框架

```

## hive与RDBMS的对比

![](https://upload-images.jianshu.io/upload_images/14863832-8d89564dd2ce0011.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## hive的数据存储

```

1. hive中的数据全存储在HDFS中，无专门的数据存储格式

2. 只需要在创建表的时候告诉hive数据中的列分隔符与行分隔符
    hive就是解析数据
	
3. hive中的数据模型
   
   I db：在hdfs中表现为${hive.metastore.warehouse.dir}目录下一个文件夹
   
   II table：在hdfs中表现所属db目录下一个文件夹
   
   III external table：与table类似，不过其数据存放位置可以在任意指定路径
   
   IV partition：在hdfs中表现为table目录下的子目录
   
   V bucket：在hdfs中表现为同一个表目录下根据hash散列之后的多个文件桶

```

## 内部表与外部表的区别：

```

1.1 创建内部表
    create table innerlxx(id int,name string) 
    row format delimited fields terminated by '\t';
1.2 创建外部表
    create external table exlxx(id int,name string) 
    row format delimited fields terminated by '\t' 
    location '/dbdata/';
1.3 通过关键字 external 来进行区分
1.4 因为外部表更多的是用于引用外部的数据，并且不希望对原始数据进行破坏，
    所以要配合location 来指定外部表要读取数据的色位置
1.5 当删除或清空数据时，内部表是把所有的数据都进行删除
    而外部表就是把表的关联信息进行删除，元数据不回丢失
1.6 load data inpath '/dbdata/women.log' into table exlxx;
   从hdfs上进行数据导入就是将hdfs上的数据移动到table所使用的目录下，（即元数据消失）

```

## 分区表

* 相当于在表中又分了小表
* 作用是可以减少我们有一定条件时的查询的数据量，提升我们的查询效率
* 分区不是只有一层，我们可以创建多层的形形式，即小表中又有小表

```

1.1 create table lxxpart(id int,name string)
    partitioned by(year string,month string) 
    row format delimited fields terminated by '\t';
1.2 创建好分区后要进行数据的导入，要这里需要指定好将数据导入到哪个分区，
    否则系统不知道将数据放入哪个分区，例如：
    load data inpath '/dbdata/user.log' into table lxxtime partition(yaer='2017',month='01');
1.3 若分区太多，建议用动态分区
1.4 查看分区表的信息
    show partitions lxxpart;
    show partitions 表名;

```

## 动态分区

* 使用场景
   当我们想要对数据进行分区的时候，你能拿到的数据不一定是已经分好区的文件，
   所以就不能直接load进来就使用，这时候就要用动态分区。

```

user.log
1	tangceng	02	man
2	wukong		03	man
3	xioabailong	06	man
4	nvshen		08	woman
5	xioameinv	11	woman

给你如上文件，让你按月份进行分区：

1.1 将混乱的数据传入一个表中
    load data inpath '/dbdata/user.log' into table users;
1.2 创建对应的分区表
    create table birthdays(id int,name string,month string,sex string)
    partitioned by(month string) 
    row format delimited fields terminated by '\t';
1.3 向分区表动态分区的出入数据
    insert into birthdays partition(month)
    select id,name,month from users;
1.4 若要进行动态分区就不要在 partition(month) 中给分区设置固定值
1.5 默认使用的是严格模式，是不允许动态分区的，所以我们需要在命令行执行
    set hive.exec.dynamic.partition.mode=nonstrict
1.6 使用动态分区会将结果集的最后一个作为分区条件，所以查询时要注意

```

## 分桶表

```

1.1  create table goods(goodsid int,name string)
     row format delimited fields terminated by '\t';
1.2 load data inpath '/dbdata/shangpin.log' into table goods;

1.3 create table goodsbucket(goodsid int,name string)
    clustered by(goodsid) into 3 buckets
    row format delimited fields terminated by '\t';

1.4 insert into goodsbucket
    select * from goods;

```

## 排序

```

1. set mapreduce.job.reduces=3;

2. select * from goods sort by goodsid;
3. select * from goods order by goodsid;
4. select * from goods distribute by goodsid;
5. select * from goods cluster by goodsid;

```

![sort](https://upload-images.jianshu.io/upload_images/14863832-ef564eb3492b9719.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![order](https://upload-images.jianshu.io/upload_images/14863832-0048f3acf274fd8a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![distribute](https://upload-images.jianshu.io/upload_images/14863832-7327eab6735bce43.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![cluster](https://upload-images.jianshu.io/upload_images/14863832-062970bda1e542c7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## sql

```

1. select dep,avg(money) as avg from company_emp group by dep having avg > 4000;
1.1 使用分组就不在是逐行执行模式，而是根据我们分组的key以分组模式执行
    所以我们的数据都是一组一组的，无法调用除了分组key和聚合函数(属性)之外的单独属性
1.2 使用聚合函数得到的结果集默认的字段名不好使，
    我们要进行调用可以给它取个别名，就可以在having条件中使用了或者使用子查询
    同一层给having使用，作为子查询就可以给外层的where使用
1.3 where执行时间是在聚合之前进行数据筛选，而having是在聚合结束之后才进行条件处理

```

