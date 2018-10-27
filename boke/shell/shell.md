## shell基础

* shell简介

```
Shell是一个功能强大的编程语言，易编写，易调试，灵活性较强
Shell是解释执行的脚本，在shell中可以直接调用Linux系统命令
```
* shell分类

```
Bourne Shell：从1979年起，Unix就是用Bourne Shell，BourneShell的主文件名为 sh
C      Shell：C Shell主要在BSD版的Unix系统中使用
```

* 注意

```
1. 以上两种语法互不兼容，
	Bourne 家族主要包括sh，ksh，bash，psh，zsh；  
	C家族主要包括：csh，tcsh
2.一个系统可以存在多个shell，
	可以通过cat /etc/shells命令查看系统中安装的shell，
	不同的shell可能支持的命令语法是不相同的
```

* 基本格式

```
1. 以.sh结尾
2. 第一行：#！/bin/bash（指明解析器,是固定的格式）
3. 执行方式：
	source方式：可以用"."来代替，是bash的内部命令
	   source helloworld.sh
	   . helloworld.sh
```

## Bash

1. Bash基本功能

```
是GNU计划的一个组件，与Unix上的Bourne Shell完全兼容，是其增强版本
支持命令行输入、操作历史、快捷键、输入输出重定向、管道、变量等功能
```

2. 历史命令 history

```
在Bash中输入history指令可以查询用户的过往操作
历史命令会默认保存1000条，可以在环境变量配置文件中/etc/profile进行修改
History表存储在内存中，在用户logout时会记录入用户家目录的.bash_history文件中，在下次login时载入
```

3. 命令的别名

```
1. alias 添加
	alias la=”ls -a --color=auto”
	
2. unalias 删除
	unalias la
```

4. 管道符 `|`

```
将左侧的命令输出结果，作为右侧命令的处理对象
```

5. 通配符

```
*      代表 0 个到无穷多个任意字符

？     代表一定有一个任意字符

[]     代表一定有一个在括号内的字符
	   例如 [abcd] 代表一定有一个字符， 
	   可能是 a, b, c, d 这四个任何一个
	   
[ - ]  若有减号在中括号内时，代表在编码顺序内的所有字符
	   例如 [0-9] 代表 0 到 9 之间的所有数字
	   
[^]    若中括号内的第一个字符为指数符号 (^) ，那表示反向选择 
	   例如 [^abc] 代表 一定有一个字符，
	   只要是非 a, b, c 的其他字符就接受的意思
```

6. 常用的热键

```
	* Ctrl + d  输入已结束
	* Ctrl + c   键盘中断请求
	* Ctrl + s  暂停屏幕输出
	* Ctrl + q  恢复屏幕输出
	* Ctrl + l  清屏，相当于clear
	* Tab     自动补完命令行与文件名
	* Ctrl + u  删除当前光标前的所有字符
	* Ctrl + k  删除当前光标后的所有字符
```

7. 命令

```

$   调用变量

''  任何特殊字符都没意义

""  有的特殊字符有意义（$）

cut	截取命令 

```

8. /etc/profile 每个用户都会用到的shell文件
	* 正常登陆（会执行 /erc/profile文件）
	* su 登陆 （不会执行）

	











		