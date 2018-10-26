## 案例三
* java环境的配置

```

#在一个新的环境中，即没有java环境内配置，把目录切到/home/yyc/bin下
#新建一个shell脚本
> javaPath.sh
#进入编辑
vim javaPath.sh

#!/bin/bash
#从网上下载安装包
wget  --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" 
http://download.oracle.com/otn-pub/java/jdk/8u191-b12/2787e4a523244c269598db4e85c51e0c/jdk-8u191-linux-x64.tar.gz
#从当前目录查找安装包
javatar=$(ls | sed -n '/jdk.*gz$/p')
#解压安装包
tar -zxf $javatar
#删除压缩的安装包
rm -rf $javatar
#获取jdk的路径
jdkname=$(ls | grep jdk)
#进入该路径
cd $jdkname
#得到现在的路径
javaname=$(pwd)
#在 /etc/profie里添加环境变量
echo "export JAVA_HOME=$javaname" >> /etc/profile
echo 'export PATH=$PATH:$JAVA_HOME/bin' >> /etc/profile
echo 'export CLASSPATH=$:CLASSPATH:$JAVA_HOME/lib/' >> /etc/profile
#运行该配置文件
. /etc/profile

```