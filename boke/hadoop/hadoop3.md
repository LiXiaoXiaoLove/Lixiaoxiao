### hadoop的完成分布式

* 准备工作

```
1. 虚拟机模板（作为namenode）
   拥有一个普通用户（lxx）
   在/home/lxx/下放上 jdk.gz,hadoop.gz
   yum install -y vim
   yum install -y net-tools
   关闭防火墙
2. 以namenode作为模板，在克隆出三个同样的虚拟机，作为datanode
3. 将namenode的伪分布式hadoop环境配好，配置步骤可查看如下网页
```
[伪分布式](https://lixiaoxiaolove.github.io/Lixiaoxiao/boke/hadoop/hadoop2)

* namenode的配置

```
4. 伪分布式环境配好后，进入如下目录，将datanode写入该文件进行注册
   cd ~/hadoop-2.7.3/etc/hadoop
   vim slaves
```

 ![slaves](https://upload-images.jianshu.io/upload_images/14466013-27dac49ceb1800eb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
5. 进入如下目录，进行编辑，将四个ip都设置上对应的别名
   vim /etc/hosts
```

![hosts](https://upload-images.jianshu.io/upload_images/14466013-7f91595959fca374.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* datanode的配置

```
6. 运用shell的发送消息到所有会话，一下对三个打他弄的进行同步操作
7. 将datanode设置成单点环境，单点hadoop环境设置步骤如下：
```
[单点配置](https://lixiaoxiaolove.github.io/Lixiaoxiao/boke/hadoop/hadoop)
```
8. 伪分布式环境不用自己一个个的配置，将namenode的配置文件传给datanode即可，
   操作如下：（该步骤就进行三次，分别传到三台datanode上）
   scp 要传输的内容 要传到的电脑的用户@要传到电脑电脑的IP:要传到电脑的位置
   scp -r ~/hadoop-2.7.3/etc/hadoop/ lxx@192.168.107.144:~/hadoop-2.7.3/etc
```

* 免密操作

```
9. 用ssh-keygen命令来生成密钥
   用ssh-copy-id 用户名@主机IP来操作主机的免密工作，步骤如下：
   操作完成后要重新启动namenode与datanode
```

![免密操作](https://upload-images.jianshu.io/upload_images/14466013-a0fee5d789110e3b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 测试操作

```
11. 用hadoop-daemon.sh start namenode 来启动namenode
    用hadoop-daemon.sh start datanode 来启动datanode
12. 用namenode的ip:50070来登录网站，验收成果
```

![网站成果](https://upload-images.jianshu.io/upload_images/14466013-77742d93f0512917.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
13. 还可以用hdfs dfsadmin -report命令来验收成果，成果如下：
```

![image.png](https://upload-images.jianshu.io/upload_images/14466013-1684423ea3317a20.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 收尾工作

```
14. 用完后要将namenode与datanode关闭
     hadoop-daemon.sh stop namenode
	 hadoop-daemon.sh stop datanode
```