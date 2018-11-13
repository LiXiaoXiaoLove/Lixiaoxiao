## mysql的安装

* 用yum安装wget
* sudo yum -y install wget

* 用wget从网上下载mysql
* wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm

* 
* sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm

* 启动mysql服务
* sudo yum -y install mysql-server

* 安装mysql
* sudo yum -y install mysql

* 启动mysql
* systemctl start mysqld

* 登录mysql
* mysql -u root -p(没密码)
* 没密码的时候直接敲回车就进入了，有密码的时候敲密码

* 查看mysql的状态
* systemctl status mysqld

* 解压安装包
* tar -zxf apache-hive-1.2.1-bin.tar.gz

* 改名
* mv apache-hive-1.2.1-bin hive

* 进入hive
* cd hive/

* 得到当前hive的路径
* pwd

* 配置环境
* sudo vim /etc/profile

* 运行该配置文件，让其生效
* . /etc/profile

* 修改配置文件
* cd /home/lxx/hive/conf

* 修改配置文件（因为不存在）
* touch hive-site.xml

* 进入该配置文件
* sudo vim hive-site.xml

* 把如下代码粘进去
* 就把ip地址改成自己的，密码也改成自己的，若没有密码，就不写，不要流空格

```

<configuration>
        <property>
                <name>javax.jdo.option.ConnectionURL</name>
                <value>jdbc:mysql://127.0.0.1:3306/hivedb?createDatabaseIfNotExist=true</value>
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

* 修改密码（登录进去后修改）

* 7.5版本后的用该句（后面的";"分号不要丢）
* UPDATE mysql.user SET authentication_string=PASSWORD('新密码') where USER='root';

* 7.5版本之前的用这句（后面的";"分号不要丢）
* UPDATE mysql.user SET Password=PASSWORD('新密码') where USER='root’;

* 修改完后刷新一下
*  flush privileges;

* 退出后用新密码重新登录
* exit；

* 用新密码登录
* mysql -u root -p 

* 输出新密码
* 123456

* 登录成功，建立远程连接（不建立远程连接，不能用可视化界面）
* GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '123456' WITH GRANT OPTION;

* 用可视化界面连接
* 用ip号登陆，若有hivedb就说明成功

* 修改密码（忘记密码）
* 修改配置文件
* vim /etc/my.cnf
* 加入一句话
* skip-grant-tables（跳过输出密码这一步）
* 然后就可以免密登录上去后在修改密码，但要记住：修改完密码后要吧配置文件在修改回来



























