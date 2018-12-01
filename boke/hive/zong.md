1. create table
	1. 内部表
	2. 外部表（location）
	3. 分区表
	4. 分桶表

* 分区后在分桶

```

create table partbucket(orderid int,orderno string,goodsid int,times date)
partitioned by(year string,month string)
clustered by(goodsid) into 3 buckets
row format delimited fields terminated by '\t';

```	
	
2. load
3. insert
4. CTAS
	1. create table aaa as select * from users;
5. type
	1. arr
	2. map
	3. struct
6. function
	1. data
	2. arr
	3. 表生成函数
	4. 窗口函数
	
* 窗口函数
	
```

1. Select *,row_number() over(partition by name order by times) from shops;

2. Select name,times,count,date_sub(times,row_num) from 
   (Select *,row_number() over(partition by name order by times) as row_num from shops) as first;

3. Select name from 
  (Select name,times,count,date_sub(times,row_num) as dif from 
  (Select *,row_number() over(partition by name order by times) as row_num from shops) as first) as two 
   group by dif,name 
   Having count(*) >=3;

```

* 联级函数


## 
	
	
