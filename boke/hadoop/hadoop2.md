## 伪分布式Hadoop

1. 关闭防火墙

```
   systemctl stop firewalldcd 
   systemctl disable firewalld
```

2. 在单点的基础上，进入到 cd ~/hadoop-2.7.3/etc/hadoop/
3. 修改配置

```
   echo $JAVA_HOME
   vim hadoop-env.sh
   将JAVA_HOME修改为以上结果
```
4. 配置4个文件
   
* vim core-site.xml

```
    <property>
        <name>hadoop.tmp.dir</name>
        <value>/home/yyc/tmp</value>
    </property>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://192.168.107.137:9000</value>
    </property>   
```
* vim hdfs-site.xml 

```
    <!-- <property>    
        <name>dfs.replication</name>    
        <value>1</value>    
    </property> -->

    <property>
        <name>dfs.namenode.name.dir</name>
        <value>file:/home/yyc/dfs/name</value>
    </property>
    <property>
        <name>dfs.datanode.data.dir</name>
        <value>file:/home/yyc/dfs/data</value>
    </property>
```

* vim yarn-site.xml

```   
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>

    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
```
* vim mapred-site.xml.template 
  cp mapred-site.xml.template  mapred-site.xml
  vim mapred-site.xml（该文件是复制来的）
  
```
     <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
```

5. 格式化
   hadoop namenode -format
6. 启动
   start-all.sh 
7. 关闭
   stop-all.sh