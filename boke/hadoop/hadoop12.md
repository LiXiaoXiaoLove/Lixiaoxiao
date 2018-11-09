* mapreduce

* 原理

1. 什么是mapreduce
	1. 是一个分布式运算程序的编程框架，是“基于hadoop数据分析应用”的核心框架
	2. 核心功能：
		* 将用户编写的业务逻辑代码与自带默认组件整合成一个完整的分布式运算程序，
		  并运行在一个hadoop集群上
		  
2. mapreduce出现的原因
	1. 海量的数据在单机上被处理受硬件条件的限制，无法实现
	2. 将单机程序扩展成集群来运行，极大地增加程序的复杂性与开发的难度
	3. mapreduce能使开发人员将大部分工作集中到业务逻辑上，而分布式计算
	   的复杂性可以交给mapreduce框架来完成
	   
3. 框架的基本组成
	1. MRAppMaster：mapreduce  application  master
	2. MapTask
	3. ReduceTask

4. 结构
	1. MRAppMaster：负责整个程序的过程调度与状态协调
					MR是mapreduce的简写
					是这个mapreduce任务的管理者
	2. mapTask：负责map阶段的整个数据处理流程
				map任务
	3. ReducerTask：负责reduce阶段的整个数据处理流程
	                reduce任务
5. 程序运行流程

图片

6. 流程解析
	1. 一个mr程序启动时，最先启动的是MRAppMaster，然后根据job的描述，计算出需要多少个maptask，
	   然后向集群申请启动相应数量的maptask进程
	
	2. maptask进程启动后，在根据给定的数据切片范围进行数据处理，处理过程如下：
		i. 通过客户给定的inputformat来获取RecordReader来读取数据，形成键值对
		
		ii. 将键值对传输给map()方法，做逻辑运算，并将map()方法输出的键值对收集到缓存
		
		iii. 将缓存中的键值对按照键进行分区，排序之后不断溢写到磁盘文件
		
	3. MRAppMaster监控到所有的maptask进程任务完成后(通过maptask的心跳机制)
	   根据客户指定的参数启动相应数量的reducetask进程，并告诉reducetask进程要处理的数据范围(数据分区)
	
	4. 根据MRAppMaster告诉的待处理数据所在的位置，从若干台maptask获取maptask输出文件，
	   并在本地进行重新归并与排序，按照键相同为一组的原则来调用reduce()方法进行逻辑运算，
	   将运算结果按键值对的形式收集起来，然后调用outputformat()方法将结果输出
	   
7. mapTask并行度决定机制

	1. 并行度影响整个job的处理速度
	
	2. 该并行度由客户端在提交job时(切片)决定，操作如下：
		i. 将待处理的数据进行逻辑切片(split)
		ii. 每个split分配一个mapTask并行处理
		
	3. 上面的过程由FileInputFormat类的getSplit()方法完成
	
	图片
	
8. FileInputFormat切片机制

	1. FileInputFormat默认的切片机制
	
		i. 简单的按照文件的内容长度进行切片
		
		ii. 切片大小默认为block的大小(block块的大小)
		
		iii. 切片时不考虑数据整体，而是逐个针对每个block块进行单独切片
	
	2. Eg
	
![image.png](https://upload-images.jianshu.io/upload_images/14863832-221b4d61d2e73c08.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	3. 切片大小的参数配置
		
		i. 由源码得切片大小的逻辑：
		   Math.max(minSize,Math.min(maxSize,blockSize))
		   
9. ReduceTask并行度的决定

	1. reduceTask的并行度影响整个job的执行效率
	
	2. ReduceTask数量的决定可以直接手动设置，默认值为1
	
10. MapReduce程序的运行模式

	1. 本地模式
	
		i. 程序将job提交给LocalJobRunner
		ii. 处理的数据与输出结果可可以在本地或hdfs上
		
		注意：该运行模式需要(windows的hadoop环境)[https://lixiaoxiaolove.github.io/Lixiaoxiao/boke/hadoop/hadoop13]
		
	2. 集群模式
	
		i. 将程序提交到yarn集群resourcemanager上
		
		ii. 处理的数据与输出结果应放在hdfs上
		
		iii. 提交到集群的步骤：
			
			a. 将程序打成jar包，放在linux环境下，用集群上的任意一个节点用hadoop命令运行
			
			b. 在linux的eclipce中运行main方法
			
			c. 若是在windows环境下运行，需要修改YarnRunner类，比较麻烦，不推荐用
		
11. Combiner

	1. combiner是MR程序中Mapper与Reducer之外的一种组件
	
	2. 该组件也需要继承Reducer类
	
	3. combiner是在每一个maptask所在的节点运行
	   而Reducer是接收全局所有的Mapper的输出结果
	   
	4. 作用是对每个maptask的输出进行局部汇总，以减少网络传输量
			
12. shuffle(洗牌)机制

	1. map阶段的输出结果如何传递给reduce阶段这一流程叫做shuffle
	
	2. 核心机制：数据分区  排序  缓存
	
13. shuffle缓存流程

图片

	1. 流程解析
		
		i. 分区 partition
		
		ii. sort 根据key排序
		
		iii. combiner 进行局部value合并
	
图片
	
14. 详细流程

	1. maptask收集
			
			
			
			
			
			
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	