## 目录操作命令

* pwd
	* 用途：查看工作目录
![](https://upload-images.jianshu.io/upload_images/14466013-3fb6f34188630f19.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	* cd
		* 用途：切换工作目录
		* 格式：cd 目录位置(路径)
	* ls
		* 用途：显示目录内容
		* 格式：ls	[选项]... [目录或文件名]
![](https://upload-images.jianshu.io/upload_images/14466013-60a47a53ce5ca1cd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
		* 常用命令选项
			* -l ：详细信息显示（ll 是缩写）
![](https://upload-images.jianshu.io/upload_images/14466013-30ba68181f5dd440.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
			* -a：显示所有子目录和文件的信息，包括隐藏文件
			* -A：类似于“-a”，但不显示“.”和“..”目录的信息
			* -R：递归显示内容
![](https://upload-images.jianshu.io/upload_images/14466013-c4282e3e6e0e2679.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	* mkdir
		* 用途：创建新的目录
		* 格式：mkdir [-p]  [/路径/]目录名		 
![](https://upload-images.jianshu.io/upload_images/14466013-373d9309a5b1fc20.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
		* mkdir -p :多层创建文件
![](https://upload-images.jianshu.io/upload_images/14466013-70371de7d8025af3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
		* ### 在用户根目录上创建文件，权限问题要注意  
![](https://upload-images.jianshu.io/upload_images/14466013-b1b452fd2a89868e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	* du
		* 用途：统计目录及文件的空间占用情况
		* 格式: du [选项]... [目录或文件名]
		* 常用命令选项
			* -a：统计时包括所有的文件，而不仅仅只统计目录
			* -h：以更易读的字节单位（K、M等）显示信息
			* -s：只统计每个参数所占用空间总的大小
