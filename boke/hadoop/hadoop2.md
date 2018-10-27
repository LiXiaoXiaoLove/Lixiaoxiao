## 伪分布式Hadoop

* 准备工作
```
1. 关闭防火墙
   systemctl stop firewalldcd 
   systemctl disable firewalld
   
2. 单点环境，操作步骤如下
```
[单点配置](https://lixiaoxiaolove.github.io/Lixiaoxiao/boke/hadoop/hadoop)
* 配置5个文件
	* 进入到 cd ~/hadoop-2.7.3/etc/hadoop/下修改配置
	
```
3. 修改hadoop-env.sh
  echo $JAVA_HOME
  vim hadoop-env.sh
  修改如下：
  export JAVA_HOME=/home/lxx/jdk1.8.0_181
```

```  
4. vim core-site.xml

    <property>
        <name>hadoop.tmp.dir</name>
        <value>/home/lxx/tmp</value>
    </property>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://192.168.107.137:9000</value>
    </property>  
	
```

```
5. vim hdfs-site.xml 

    <!-- <property>    
        <name>dfs.replication</name>    
        <value>1</value>    
    </property> -->

    <property>
        <name>dfs.namenode.name.dir</name>
        <value>file:/home/lxx/dfs/name</value>
    </property>
    <property>
        <name>dfs.datanode.data.dir</name>
        <value>file:/home/lxx/dfs/data</value>
    </property>
	
```

```
6. vim yarn-site.xml
 
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>

    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
	
```

```
6. vim mapred-site.xml.template 
   cp mapred-site.xml.template  mapred-site.xml
   vim mapred-site.xml（该文件是复制来的）

     <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
	
```

```
5. 格式化namenode
   hadoop namenode -format
```

* 测试工作
```
6. 启动
   start-all.sh 
7. 查看结果
   jps
8. 关闭
   stop-all.sh
```