### wimdows的hadoop环境搭建

* 需要的安装包

```
[Linux系统下的hadoop安装包](https://lixiaoxiaolove.github.io/Lixiaoxiao/bao/hadoop-2.7.3.tar.gz)
[windows系统下hadoop安装包的协助包](https://lixiaoxiaolove.github.io/Lixiaoxiao/bao/hadooponwindows-master.zip)
```

* 伪分布式

```

1. 找好位置把压缩包解压
2. 我们从网上直接下载的hadoop包一般都是Linux系统下用的
   所以要在下载windows系统下的协助包，把协助包里的bin与
   etc拷贝到Linux系统下的hadoop安装包里
3. 把hadoop包里的bin下的hadoop.dll与winutils拷贝到C:\Windows\System32下
   有时候需要重启电脑才有作用
4. 配hadoop环境
   右击电脑 --> 点击属性 --> 点击高级系统设置 --> 点击环境变量 --> 
   新建系统变量(即下面的) --> 变量名为HADOOP_HOME,变量值为hadoop的存放路径
   --> 保存该系统变量 --> 找到Path系统变量 --> 新建路径,%HADOOP_HOME%\bin与
   %HADOOP_HOME%\sbin两个路径 --> 保存
   
```

![image.png](https://upload-images.jianshu.io/upload_images/14466013-28ac1a1e5c429f8e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)version测试hadoop

 ![image.png](https://upload-images.jianshu.io/upload_images/14466013-327d86170d95f92c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
 
```

5. 用cmd窗口输入hadoopA或hadoop version测试hadoop
   环境是否配置成功测试hadoop环境是否配置成功
   若如下图，表示成功，否则，查看以上步骤可有出错
   或重启电脑
 
```

![](https://upload-images.jianshu.io/upload_images/14466013-c45c160e5aa3db87.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
6. 若为找不到JAVA_HOME(如下图1)，就修改配置文件
   在hadoop解压包下的etc下的hadoop下的hadoop-env.cmd(如下图2,3)
   
   *** 一定要是以.cmd为扩展名的那个文件
   
   在配置hadoop-hdfs.xml(如下图4)
   把里面namenode与datanode存放的路径修改成本电脑的实际路径
   
```

![](https://upload-images.jianshu.io/upload_images/14466013-8e5d796338740825.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-c27377fdfc2e5ed1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)![image.png](https://upload-images.jianshu.io/upload_images/14466013-c27377fdfc2e5ed1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-60ed6983a30c29fa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-922d22c15cd7ddee.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
7. 在cmd窗口初始化hadoop的namenode
   hadoop namenode -format
   
8. 启动hadoop
   start-all.cmd
   
9. 用jps命令查看是否以启动
   或登录网站查看（namenode的IP:50070）
   
```

![image.png](https://upload-images.jianshu.io/upload_images/14466013-cf586f17dfa2b12f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

























