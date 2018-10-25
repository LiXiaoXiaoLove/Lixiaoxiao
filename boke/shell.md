## shell基础

* shell简介
	* Shell是一个功能强大的编程语言，易编写，易调试，灵活性较强
	* Shell是解释执行的脚本，在shell中可以直接调用Linux系统命令
* shell分类
	* Bourne Shell：从1979年起，Unix就是用Bourne Shell，BourneShell的主文件名为 sh
	* C Shell：C Shell主要在BSD版的Unix系统中使用
	* 注意
		* 以上两种语法互不兼容，
			* Bourne 家族主要包括sh，ksh，bash，psh，zsh；  
			* C家族主要包括：csh，tcsh
		* 一个系统可以存在多个shell，
			* 可以通过cat /etc/shells命令查看系统中安装的shell，
			* 不同的shell可能支持的命令语法是不相同的
* 基本格式
	* 以.sh结尾
	* 第一行：#！/bin/bash（指明解析器,是固定的格式）
	* 执行方式：
		* sh方式：
			* [root@master ~]# sh helloworld.sh
			*  此方式是直接指定用系统默认的bash shell解释执行
		* source方式：
			* 可以用"."来代替，是bash的内部命令
				* source helloworld.sh
				* . helloworld.sh
## Bash

* Bash基本功能
	* 是GNU计划的一个组件，与Unix上的Bourne Shell完全兼容，是其增强版本
	* 支持命令行输入、操作历史、快捷键、输入输出重定向、管道、变量等功能
* 历史命令
	* history
		* 在Bash中输入history指令可以查询用户的过往操作
		* 历史命令会默认保存1000条，可以在环境变量配置文件中/etc/profile进行修改
		* History表存储在内存中，在用户logout时会记录入用户家目录的.bash_history文件中，在下次login时载入
* 命令的别名
	* alias 添加
		* alias la=”ls -a --color=auto”
	* unalias 删除
		* unalias la
* 管道符
	* |
	* 将左侧的命令输出结果，作为右侧命令的处理对象
* 通配符
	* *      代表 0 个到无穷多个任意字符
	* ？     代表一定有一个任意字符
	* []     代表一定有一个在括号内的字符
		*    例如 [abcd] 代表一定有一个字符， 
		*    可能是 a, b, c, d 这四个任何一个
	* [ - ]  若有减号在中括号内时，代表在编码顺序内的所有字符
		*    例如 [0-9] 代表 0 到 9 之间的所有数字
	* [^]    若中括号内的第一个字符为指数符号 (^) ，那表示反向选择 
		*    例如 [^abc] 代表 一定有一个字符，
		*    只要是非 a, b, c 的其他字符就接受的意思
* 常用的热键
	* Ctrl + d  输入已结束
	* Ctrl + c   键盘中断请求
	* Ctrl + s  暂停屏幕输出
	* Ctrl + q  恢复屏幕输出
	* Ctrl + l  清屏，相当于clear
	* Tab     自动补完命令行与文件名
	* Ctrl + u  删除当前光标前的所有字符
	* Ctrl + k  删除当前光标后的所有字符

* /etc/profile 每个用户都会用到的shell文件
	* 正常登陆（会执行 /erc/profile文件）
	* su 登陆 （不会执行）
* 命令：
	* $：调用变量
	* ''：任何特殊字符都没意义
	* ""：有的特殊字符有意义（$）
	* 截取命令 cut
	
* shell的基本语法
	* 函数：减少代码的冗余
	* set 查看变量（系统，自定义）
	* env 查看环境变量
	* 自定义变量
		* 变量名=变量值
			*规则
				* 变量与变量内容以一个等号来连结
				* 等号两侧不能有空格
				* 变量名以字母或下划线开头，区分大小写，建议全大写
		* 赋值时使用引号
			* ""  允许通过$符号引用其变量值 
			* ''  禁止引用其他变量值，$视为普通字符
			* ``  命令替换，提取命令执行后的输出结果
			* $() 命令替换，提取命令执行后的输出结果
		* 从键盘输入内容变为赋值
			* read  -p  "提示信息"  变量名
	* 特殊变量
		* $#：表示参数的个数，常用于循环
		* $*：参数的内容
		* $$：当前shell进程的pid值
		* $?：前一命令返回的状态值（0为正常）
		* $0 表示当前脚本名称
		* $1 第一个参数
		* $N 第N个参数
	* unset 删除自定义的变量
	* export 变量名  可把变量提升为环境变量
	* $() 提取结果的变量名
* 运算符
	* 格式：expr  变量1   运算符  变量2  [运算符 变量3] ...
	* eg：[root@master~]# expr `expr 2 + 3` \* 4
	* 常用运算符：
		* 加法运算：+
		* 减法运算： -
		* 乘法运算： \*
		* 除法运算： /
		* 求模（取余）运算： % 
* 条件测试
	* 文件测试
		* 格式：[  操作符  文件或目录  ]    
			* 注意condition前后要有空格
		* 常用的测试操作符（返回1表示条件不成立，返回0表示条件成立）
			* -d：测试是否为目录（Directory）
			* -e：测试目录或文件是否存在（Exist）
			* -f：测试是否为文件（File）
	* 文件权限测试
		* 格式 [  操作符  文件或目录  ]
		* eg：[root@master ~]# [ -r /root/install.log ] && echo "yes" || "echo no" yes
		*  常用的测试操作符
			* -r：测试当前用户是否有权限读取（Read）
			* -w：测试当前用户是否有权限写入（Write）
			* -x：测试当前用户是否有权限执行（eXcute）
	* 数值比较
		* 格式：[  整数1  操作符  整数2  ]
		* 常用的测试操作符
			* -eq：等于（Equal）
			* -ne：不等于（Not Equal）
			* -gt：大于（Greater Than）
			* -lt：小于（Lesser Than）
			* -le：小于或等于（Lesser or Equal）
			* -ge：大于或等于（Greater or Equal）
	* 字符串比较
		*  格式
			* [  字符串1  =  字符串2 ]
			* [  字符串1  !=  字符串2 ]
			* [  -z  字符串 ]
		* 常用的测试操作符
			* =：字符串内容相同
			* !=：字符串内容不同，! 号表示相反的意思
			* -z：字符串内容为空
* 控制流程
	* 分支结构
		* if语句
		* case语句
		* for语句
		* while语句
* 自定义函数
	* 语法
		[ function ] funname [()]
			{
				action;
				[return int;]
			}
	* 注意：
		1. shell脚本是逐行运行的
		2. 函数返回值，只能通过$?系统变量获得
		3. 语法中的前后两部分不可以全部省略，只能省略其中的一个


## 案例一
* 写一个shell脚本能够对所有的压缩包进行解压
* toncat jdk hadoop压缩包放在 /home/yyc/tar 下（yyc是一个用户）
	1. 获取用户要解压的路径（该路径用参数传过来，用"$1" 符来获取）
	2. 从对应目录获取所有要进行解压的文件
	3. 对这些文件一个个的进行解压
	
* eg：
```
#在 /home/yyc/bin下新建一个shell文件
touch lxxtar.sh
#进入文件内进行编辑
vim lxxtar.sh

#shells脚本的开头，是固定的
#!/bin/bash

#把压缩包的路径放置在一个文件内
ls $1*.gz > /home/yyc/bin/tar.log
#循环该文件
for file in $(cat /home/yyc/bin/tar.log)
#进行解压操作
do
	tar -zxf $file
	echo "$file已解压完成"
done


#运行该脚步
. lxxtar.sh /home/yyc/tar/

```


## 案例二
* 创建多个用户
```
#在/home/yyc/bin目录下创建一个shell脚本
> createUser.sh
#进入文件进行编辑
vim createUser.sh


#!/bin/bash

#从键盘输入内容
read -p "请输入要创建的用户名的前缀：" userName
#用for循环添加新用户
for (( i=0;i<=30;i=i+1 ))
do
	#创建新用户
	useradd $userName$i
	#输出提示
	echo "用户$userName$i创建完成"
	#给用户添加密码
	echo "123456" | passwd $userName$i --stdin
done

```

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


		