## Linux的运行级别
    * 配置文件
![](https://upload-images.jianshu.io/upload_images/14466013-6f6e17b57b5ce608.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	* 查看运行级别
		* 使用runlevel命令，分别显示：切换前的运行级别、当前的运行级别（n 表示之前未切换过运行级别）
![图1.1](https://upload-images.jianshu.io/upload_images/14466013-63c92e5d0d84206e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)![image.png](https://upload-images.jianshu.io/upload_images/14466013-63c92e5d0d84206e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	* 临时切换运行级别临时切换运行级别
	    *  使用init命令结合0-6运行级别参数
![图1.2](https://upload-images.jianshu.io/upload_images/14466013-79eb308a1b11e70e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	* hostname命令
        * 查看当前主机名
![图1.3](https://upload-images.jianshu.io/upload_images/14466013-e355bae5b59d54c9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
		* 临时修改(一次性修改，重启后变回原来的)
![图1.4](https://upload-images.jianshu.io/upload_images/14466013-bc28ff7bd903755f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
		*  永久修改（修改配置文件）
			*  /etc/hostname文件
			*  用途：保存全局网络设置，主要包括主机名信息
			* 步骤
				* 使用vi命令进入到配置文件
				* 按i 键后进行编辑，之后先按esc 键退出编辑状态，在按:wq进行保存退出
				* 重启后才能看到效果
![图1.4](https://upload-images.jianshu.io/upload_images/14466013-5c94c2d3c1a3e04b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
		* ### 注意权限问题，root才拥有修改主机名的权限
			* 从用户切换到root用户
![图1.5](https://upload-images.jianshu.io/upload_images/14466013-e121d710522d5026.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
			* 修改完在从root用户切回原用户
![图1.6](https://upload-images.jianshu.io/upload_images/14466013-44e5e44f5b0ccd2e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	* ping命令
		* 测试网络连通性
		* 格式：ping [选项] 目标主机
		* ctrl + c 终止测试
![图1.7](https://upload-images.jianshu.io/upload_images/14466013-4b6852e5ef4d6f4a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	* ifconfig
		* 查看所有活动网络接口的信息
![图1.6](https://upload-images.jianshu.io/upload_images/14466013-d9125068b290b4a0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
		* 查看指定网络接口信息
			* 格式：ifconfig IP
		* Ifconfig不能用，使用yum命令
			* yum install net-tools -y
	* 设置防火墙
        * 查看防火墙状态
			* service firewalld status
![](https://upload-images.jianshu.io/upload_images/14466013-ed0a6797af818bf5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
		* 临时关闭防火墙
			* systemctl stop firewalld
![](https://upload-images.jianshu.io/upload_images/14466013-346bddfcb16a8e85.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
 		* 永久关闭防火墙
			* 修改配置文件
	* 本地主机映射文件
		* 用途：保存主机名与IP地址的映射记录
		* 查看
![](https://upload-images.jianshu.io/upload_images/14466013-819b4de6c879e530.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	* 设置网络信息
		* 查看
![](https://upload-images.jianshu.io/upload_images/14466013-2cde392efeb633ba.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	* 设置SELinux
		* 是美国安全局开发的，安全级别很高，不进行设置，有时候下载东西时会不让下载
![](https://upload-images.jianshu.io/upload_images/14466013-70fa95938ac76186.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
		* 查看SElinux，可能返回的结果有三种
			* Enforcing：强制模式，代表记录安全警告且阻止可疑行为
			* Permissive：宽容模式，代表记录安全警告但不阻止可疑行为
			* Disable：关闭
		* 临时修改
![](https://upload-images.jianshu.io/upload_images/14466013-9cb3bced3356402e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
		* 永久修改
![](https://upload-images.jianshu.io/upload_images/14466013-840d2470a673ba95.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
