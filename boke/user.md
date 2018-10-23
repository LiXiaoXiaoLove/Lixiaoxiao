* 查看用户的相关信息
	* vim /etc/passwd
	![yonghu.png](https://upload*images.jianshu.io/upload_images/14466013*e6377a37fa82b2c7.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
	![jianjie.png](https://upload*images.jianshu.io/upload_images/14466013*e6377a37fa82b2c7.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
* 查看用户密码的相关信息
	* 注意权限问题，若无权限，使用su命令切换成root用户在操作
	![image.png](https://upload*images.jianshu.io/upload_images/14466013*78f5f8a7f794351d.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
	* vim /etc/shadow
	![image.png](https://upload*images.jianshu.io/upload_images/14466013*f2b5ac1762b2aed9.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
	![image.png](https://upload*images.jianshu.io/upload_images/14466013*db4601ef4da70cb7.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
* 添加用户 
	* 命令 useradd [] 用户名
	* 选项
		* -u 指定组ID（uid）
			* eg
			![image.png](https://upload*images.jianshu.io/upload_images/14466013*bb23e7ebce7fc321.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
			* 运行结果
			![image.png](https://upload*images.jianshu.io/upload_images/14466013*f0ec08aceea36e19.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
			* uid不手动添加，系统会自动添加
			![image.png](https://upload*images.jianshu.io/upload_images/14466013*5def2cb554d96686.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
		* -g 指定所属的组名（gid）
			* 指定的gid一定是已经存在的组id，若不存在，会出错
			![image.png](https://upload*images.jianshu.io/upload_images/14466013*d5f56674c64da312.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
			* 运行结果
			![image.png](https://upload*images.jianshu.io/upload_images/14466013*3e8305f19b7c8e60.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
		* -G 指定多个组，用逗号“，”分开（Groups）
		* -c 用户描述（comment）
		* -e 失效时间（expire date）
* 修改用户属性
	* 命令 usermod [] 修改后的用户名 被修改的用户名
	* 选项
		* -l 修改用户名 
			* usermod *l a b            b改为a
			* 结果
			![image.png](https://upload*images.jianshu.io/upload_images/14466013*130cabc5f4709f8c.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
			![image.png](https://upload*images.jianshu.io/upload_images/14466013*d45401ce0e2d26ff.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
		* -g 添加组 
			* usermod *g sys tom        tom用户添加到sys组
			* 结果
			![image.png](https://upload*images.jianshu.io/upload_images/14466013*2c9595eaceec534c.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
			![image.png](https://upload*images.jianshu.io/upload_images/14466013*e70d5cb5a17927fe.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
		* -G 添加多个组 
			* usermod *G sys,root tom   tom用户添加到sys与root组中
			* 结果，要到 /etc/group中查看结果
			![image.png](https://upload*images.jianshu.io/upload_images/14466013*a072b9db374aea46.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
		    ![image.png](https://upload*images.jianshu.io/upload_images/14466013*842046408c702a96.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
		* –L 锁定用户账号密码
		* –U 解锁用户账号
* 删除用户命令
	* 命令 userdel [] 文件名或路径
	* 选项
		* -r 删除账号时同时删除目录
		* 结果
		![image.png](https://upload*images.jianshu.io/upload_images/14466013*422b91cbce4f6d80.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
		* 注意
		![image.png](https://upload*images.jianshu.io/upload_images/14466013*22264a8e55c30dae.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)