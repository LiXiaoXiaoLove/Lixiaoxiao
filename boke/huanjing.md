## 安装环境


* 安装 VMware Workstation

* [详情](https://lixiaoxiaolove.github.io/Lixiaoxiao/boke/hadoop/hadoop)

```

注意：选3项
	安装位置（点完成就好）
	软件选择（已选环境的附加选项全勾上，点完成）
	网络和主机名（打开网络，点完成）
	
```

* 环境准备

```

1. 新建一个用户lxx
   useradd lxx
   passwd lxx
   
2. 在/home/lxx下放上jdk.gz,hadoop.gz，hive.gz

3. yum install -y vim

4. yum install -y wget

5. yum install -y net-tools

6. 关闭防火墙

7. 设置sudo
   yum install -y sudo
   visudo进入配置文件在root下面加一句话，把普通用户的名字加上

```

* 单点配置

* [详情](https://lixiaoxiaolove.github.io/Lixiaoxiao/boke/hadoop/hadoop2)

```

1. 把三个压缩包解压
   
2. 设置/etc/profile
   
3. 修改完运行该文件

```

![/etc/profile](https://upload-images.jianshu.io/upload_images/14863832-5f3fba19223ed389.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 伪分布式

* [详情](https://lixiaoxiaolove.github.io/Lixiaoxiao/boke/hadoop/hadoop2)

```

1. 先进入 ~/hadoop-2.7.3/etc/hadoop/下

```

```

2. 在修改配置文件

```

```
   vim hadoop-env.sh
```

![image.png](https://upload-images.jianshu.io/upload_images/14863832-d33eb207a9ceb797.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
   vim core-site.xml
```

![image.png](https://upload-images.jianshu.io/upload_images/14863832-ddcd846703b2b018.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
   vim hdfs-site.xml
```

![image.png](https://upload-images.jianshu.io/upload_images/14863832-fdc8990212ea31bc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
   vim yarn-site.xml
```

![image.png](https://upload-images.jianshu.io/upload_images/14863832-00d1583817199f3c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
   vim mapred-site.xml（该文件使用vim mapred-site.xml.template拷贝过来的）
```

![image.png](https://upload-images.jianshu.io/upload_images/14863832-4fe4c73353eaa2e1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```

3. namenode进行格式化
   hadoop namenode -format
   
```

* 全分布式

* * [详情](https://lixiaoxiaolove.github.io/Lixiaoxiao/boke/hadoop/hadoop3)

```

1. 到这里就用快照克隆出三个datanode

2. 把这四个的主机名都进行修改
   sodu vim /etc/hostname(修改完要进行虚拟机重启，若不想重启，就用命令临时设置一下)
   sudo hostname 主机名
```

```
   
3. 把这四个的ip与主机名的映射全部放入四个的/etc/hosts中

```

![image.png](https://upload-images.jianshu.io/upload_images/14863832-c4920d4a2f6c6fc9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```

4. 把datanode的主机名放入namenode的 /etc/slaves 下

```

![image.png](https://upload-images.jianshu.io/upload_images/14863832-aaa13fcc061d5e51.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```

5. 免密工作
   ssh-keygen                 用来生成密钥（需要敲三次回车）
   ssh-copy-id 用户名@主机IP  逐个设置免密工作
   
```

![image.png](https://upload-images.jianshu.io/upload_images/14863832-a77837af42413e0d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
   
6. 端口占用问题
   netstat -tunlp | grep 端口号(或java)  查看被占用的端口
   kill -9 进程号(pid)                   杀死被占用的端口
   
7. 安全模式
   hdfs dfsadmin -safemode leave         离开安全模式

```

* namenode与datanode的clusterID不统一问题

```   
原因：
   多次对namenode进行格式化，datanode上保存的却是第一次格式化的结果
   因此出现了不统一的现象
```

```
解决思路：
   查看datanode的日志
   cd hadoop-2.7.3/logs/
   cat hadoop-lxx-datanode-datanode11.log   
```

![image.png](https://upload-images.jianshu.io/upload_images/14863832-44d84d19c7ec3c29.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```   
解决方案：
   cd /home/lxx/dfs/data/current
   vim VERSION
   把里面的clusterID修改成现在的namenode的clusterID（可以从网站是哪个获取）

```


* hive

* [详情](https://lixiaoxiaolove.github.io/Lixiaoxiao/boke/hive/hive02)



























