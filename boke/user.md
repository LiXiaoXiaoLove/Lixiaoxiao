* 查看用户的相关信息
	* vim /etc/passwd
* 查看用户密码的相关信息
	* 注意权限问题，若无权限，使用su命令切换成root用户在操作
	* vim /etc/shadow
* 添加用户 
	* 命令 useradd [] 用户名
	* 选项
		* -u 指定组ID（uid）
			* eg
			* 运行结果
			* uid不手动添加，系统会自动添加
		* -g 指定所属的组名（gid）
			* 指定的gid一定是已经存在的组id，若不存在，会出错
			* 运行结果
		* -G 指定多个组，用逗号“，”分开（Groups）
		* -c 用户描述（comment）
		* -e 失效时间（expire date）
* 修改用户属性
	* 命令 usermod [] 修改后的用户名 被修改的用户名
	* 选项
		* -l 修改用户名 
			* usermod *l a b            b改为a
			* 结果
		* -g 添加组 
			* usermod *g sys tom        tom用户添加到sys组
			* 结果
		* -G 添加多个组 
			* usermod *G sys,root tom   tom用户添加到sys与root组中
			* 结果，要到 /etc/group中查看结果
		* –L 锁定用户账号密码
		* –U 解锁用户账号
* 删除用户命令
	* 命令 userdel [] 文件名或路径
	* 选项
		* -r 删除账号时同时删除目录
		* 结果
		* 注意
