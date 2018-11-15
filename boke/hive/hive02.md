## hive配置步骤：

1. 上传hive压缩包到服务器 
1.1 用可视化界面把hive压缩包上传到/home/lxx目录下
2. 解压缩
2.1 tar -zxf apache-hive-1.2.1-bin.tar.gz
2.2 mv apache-hive-1.2.1-bin hive(改名)
3. 在/etc/profiles中配置hive到path中 
3.1 先进入hive，得到hive的根目录
    cd hive/
    pwd
3.2 sudo vim /etc/profile
3.3 添加路径
    export HIVE_HOME=/home/lxx/hive
    PATH=$PATH:$JAVA_HOME/bin:$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$HIVE_HOME/bin
4. 执行 . /etc/profiles 该文件，让其立即生效
5. hive启动测试 （hive命令）
6. 安装mysql 
6.1 先从网上下载依赖关系
    wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
    若wget不是命令，就先安装wget
    sudo yum -y install wget
6.2 用rpm格式把刚下载的依赖关系安装（rpm格式可以把你需要的环境自动帮你配好）
    sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm
6.3 安装mysql-server
    sudo yum -y install mysql-server
6.4 安装mysql（实际上安装上mysql-server后，mysql就已经安装完了）
    sudo yum -y install mysql
6.5 启动mysql
    systemctl start mysqld
6.6 查看mysql的状态
    systemctl status mysqld
7. 使用root登录mysql,给root修改密码
7.1 没密码的时候就直接敲回车
    mysql -u root -p 
7.2 登录后在进行（5.7版本后用的）
    UPDATE mysql.user SET authentication_string=PASSWORD('新密码') where USER='root';
    5.7版本前用的
    UPDATE mysql.user SET Password=PASSWORD('新密码') where USER='root’;
7.2 刷新立即生效
    flush privileges;
7.3 退出重新用密码登录
    exit；
7.4 若忘记密码，就修改配置文件/etc/my.cnf，在里面家一句话
    vim /etc/my.cnf
    skip-grant-tables（跳过输出密码这一步，就可以免密登录数据库）
8. 设置mysql能够远程访问 
   GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '123456' WITH GRANT OPTION;
9. 在hive/conf目录下创建hive-site.xml，并加入连接mysql数据库的配置（jar包）
9.1 先进入该目录下，新建hive-site.xml文件
    cd /home/lxx/hive/conf
    touch hive-site.xml
    sudo vim hive-site.xml
9.2 把如下代码粘进新建hive-site.xml文件，ip地址与密码修改成自己的
     
```
<configuration>
	<property>
		<name>javax.jdo.option.ConnectionURL</name>
		<value>jdbc:mysql://192.168.107.144:3306/hivedb?createDatabaseIfNotExist=true</value>
	</property>
	<property>
		<name>javax.jdo.option.ConnectionDriverName</name>
		<value>com.mysql.jdbc.Driver</value>
	</property>
	<property>
		<name>javax.jdo.option.ConnectionUserName</name>
		<value>root</value>
	</property>
	<property>
		<name>javax.jdo.option.ConnectionPassword</name>
		<value>123456</value>
	</property>
</configuration>

```

9.3 把mysql-connector-java-5.1.34.jar的jar包加入到/home/lxx/hive/bin目录下
10. 启动hive看是否正常（hive命令）
11. 用可视化页面登录数据库，若出现hivedb数据库就说明成功了