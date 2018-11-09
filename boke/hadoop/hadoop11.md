## HDFS的概念与特征

* HDFS：是一个分布式的文件系统，通过目录来定位

* 特征

	* 分块存储：hadoop2.0版本是128M，1.0版本是64M

	* HDFS一次写入，多次读出，不能修改


## HDFS的shell命令

```
* hadoop fs -ls
```
	
![image.png](https://upload-images.jianshu.io/upload_images/14466013-f2e60f2c3b36c31e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
1. hadoop fs -mkdir -p /aaa/bbb/ccc

2. 将本地的文件剪切复制到hdfs
	hadoop fs -moveFromLocal 本地目录/hdfs目录 hdfs目录/本地目录 

3. 将本地目录的内容追加到hdfs目录中
	hadoop fs -appendToFile 本地目录 hdfs的目录	

4. hadoop fs -cat hdfs的目录

5. 从hdfs下载文件，下载到当前目录下
	hadoop fs -get hdfs的目录

6. 上传文件
	hadoop fs -put 本地目录 hdfs的目录

7. 删除文件或文件夹
	hadoop fs -rm -r hdfs的路径
	
```


## hdfs的工作机制

* HDFS:分布式文件系统
	* Namenode:管理元数据
	* Datanode:管理真实的数据块

* 心跳：datanode会定期向namenode汇报所保存的文件的信息，
        而namenode负责保持文件的副本数量

* HDFS的工作机制对客户是透明的，客户通过请求namenode来访问HDFS

* HDFS写数据

```

1. 根namenode通信请求上传文件，namenode检查目标文件是否已存在，
   父目录是否存在
   
2. namenode返回是否可以上传

3. client请求第一个 block该传输到哪些datanode服务器上

4. namenode返回3个datanode服务器ABC(默认备份三个)

5. client请求3台dn中的一台A上传数据（本质上是一个RPC调用，建立pipeline），
   A收到请求会继续调用B，然后B调用C，将这个pipeline建立完成，逐级返回客户端
   
6. client开始往A上传第一个block（先从磁盘读取数据放到一个本地内存缓存），
   以packet为单位，A收到一个packet就会传给B，B传给C；
   A每传一个packet会放入一个应答队列等待应答
   
7. 当一个block传输完成之后，client再次请求namenode上传第二个block的服务器。

```

![HDFS_write](https://upload-images.jianshu.io/upload_images/14466013-eea1875e66b77fb5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 扩展

[RPC](https://baike.baidu.com/item/%E8%BF%9C%E7%A8%8B%E8%BF%87%E7%A8%8B%E8%B0%83%E7%94%A8%E5%8D%8F%E8%AE%AE/6893245?fr=aladdinv)

* HDFS读数据

```
1、跟namenode通信查询元数据，找到文件块所在的datanode服务器
2、挑选一台datanode（就近原则，然后随机）服务器，请求建立socket流
3、datanode开始发送数据（从磁盘里面读取数据放入流，以packet为单位来做校验）
4、客户端以packet为单位接收，现在本地缓存，然后写入目标文件
```

![HDFS_read](https://upload-images.jianshu.io/upload_images/14466013-71c415ba5d4fe15b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* namenode的工作机制

	* 职责
	```
	1. 负责客户端请求与响应
	2. 元数据的管理
	```

	* 元数据管理的三种存储形式
	```
	1. 内存存储元数据
	   内存中保存了一份完整的元数据
	   但是内存中的数据一关机就没有了
	2. 磁盘元数据镜像文件（fsimage）
	3. 数据操作日志文件
	```
	
![](https://upload-images.jianshu.io/upload_images/14466013-54b2197b8ccccfac.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 元数据的cheakpoint	

![image.png](https://upload-images.jianshu.io/upload_images/14466013-405ba279a32b710e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
1. secondary namdnode 每隔一段时间，都会询问namdnode是否需要备份
2. namenode 会将积累的所有的edits和一个最新的fsimage下载到本地
3. 整合后在加载到内容中
```




























