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