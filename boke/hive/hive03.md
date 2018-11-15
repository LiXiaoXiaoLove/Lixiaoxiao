## hive使用

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

## hive中为什么要有元数据库（mysql）？

因为hive表所对应的数据是存储在hdfs上的，所以真正的数据是存在datanode上的，
而要找到datanode上的数据，我们就需要把这个关联进行记录

## 内部表与外部表的区别：

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

## 分区表

相当于在表中又分了小表
作用是可以减少我们有一定条件时的查询的数据量，提升我们的查询效率
分区不是只有一层，我们可以创建多层的形形式，即小表中又有小表
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

## 动态分区

1. 使用场景
   当我们想要对数据进行分区的时候，你能拿到的数据不一定是已经分好区的文件，
   所以就不能直接load进来就使用，这时候就要用动态分区。例如给你如下数据文件：
user.log
1	tangceng	02	man
2	wukong		03	man
3	xioabailong	06	man
4	nvshen		08	woman
5	xioameinv	11	woman

2. 给你如上文件，让你按月份进行分区
2.1 将混乱的数据传入一个表中
    load data inpath '/dbdata/user.log' into table users;
2.2 创建对应的分区表
    create table birthdays(id int,name string,month string,sex string)
    partitioned by(month string) 
    row format delimited fields terminated by '\t';
2.3 向分区表动态分区的出入数据
    insert into birthdays partition(month)
    select id,name,month from users;
2.4 若要进行动态分区就不要在 partition(month) 中给分区设置固定值
2.5 默认使用的是严格模式，是不允许动态分区的，所以我们需要在命令行执行
    set hive.exec.dynamic.partition.mode=nonstrict
2.6 使用动态分区会将结果集的最后一个作为分区条件，所以查询时要注意