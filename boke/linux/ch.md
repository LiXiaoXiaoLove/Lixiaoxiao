* chmod命令：修改用户对文件操作的权限
```
  格式：
	chmod [ugoa][+-=][rwx] filepath
	chmod nnn filepath
  参数：
	u：属主（文件的创建者）
	g：属组（文件所属组的成员）
	o：其他用户（除所属组的其他成员）
	a：所有的用户（不属于该组的成员）
	
	+：添加权限
	-：删除权限
	=：赋值权限
	nnn：三位八进制的赋值权限
  选项：
	-R：递归修改指定目录下的所有文件与文件夹
```

* Eg
```
	L1:chmod u+x a.txt
	L2:chmod 750 a.txt
	L3:chmod -R 777 aaa(文件夹)
```






* chown命令：修改文件本身的权限
```
  格式：
	chown 属主 filepath
	chown :属组 filepath
	chown 属主:属组 filepath
  选项：
	-R:递归修改指定目录下的所有文件，子目录的归属
```

* Eg
```
	L1:chown java2 aa.txt(用户java1)
	L2:
	
	
```

* yum命令
