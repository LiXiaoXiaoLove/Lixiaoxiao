### 压缩操作
	* tar
		* 用途：打包、解压文件（之前的文件还存在）
		* tar [cvf] 压缩名 文件名 （压缩文件）
		* tar [xvf] 文件名.tar    （解压文件）
		* 常用命令选项
			*  -c：创建 .tar 格式的包文件
			* -x：解开.tar格式的包文件
			* -v：输出详细信息
			* -f：表示使用归档文件（不归档就不成功）
		* eg
			* 打包文件夹与文件
			   ![](https://upload-images.jianshu.io/upload_images/14466013-9136a7e39f3f020c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
			* 解压文件与文件夹
	          ![](https://upload-images.jianshu.io/upload_images/14466013-047597694f2fbb17.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
			
	* gzip
		* 用途：压缩、解压文件（之前的文件消失）
		* gzip [选项] 压缩（解压缩）的文件名
		* 常用命令选项
			* -d将压缩文件解压
			* -l显示压缩文件的大小，未压缩文件的大小，压缩比
			* -v显示文件名和压缩比（verbose）
			* -num用指定的数字num调整压缩的速度，-1或--fast表示最快压缩方法（低压缩比），-9或--best表示最慢压缩方法（高压缩比）。系统缺省值为6
		* eg
			* 压缩文件
			  ![image.png](https://upload-images.jianshu.io/upload_images/14466013-bf0566c01289d200.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
			* 解压文件
			  ![image.png](https://upload-images.jianshu.io/upload_images/14466013-391c42363e0a5925.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
			* 压缩文件夹（不是我们想要的效果，只是把文件压缩了，文件夹没有压缩）
			  ![image.png](https://upload-images.jianshu.io/upload_images/14466013-1d93e14e798953e8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
		* bzip2
			* 用途：压缩、解压文件（之前的文件消失）
			* bzip2 [-cdz] 文档名
			* 常用命令选项
				* -c将压缩的过程产生的数据输出到屏幕上
				* -d解压缩的参数（decompress）
				* -z压缩的参数（compress）
				* -num 用指定的数字num调整压缩的速度，-1或--fast表示最快压缩方法（低压缩比），-9或--best表示最慢压缩方法（高压缩比）。系统缺省值为6
			* 注意：是否有插件
			![image.png](https://upload-images.jianshu.io/upload_images/14466013-4449d822f664eb05.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
			* 若没有，就加入插件
			![image.png](https://upload-images.jianshu.io/upload_images/14466013-f294962562657e36.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
			* 用yum
			![image.png](https://upload-images.jianshu.io/upload_images/14466013-c1ff3bf2c8599eb8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
		* eg
			* 压缩文件（原文件消失）
			![image.png](https://upload-images.jianshu.io/upload_images/14466013-556ea4455427fc0e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
			* 解压文件（压缩文件会消失）
			![image.png](https://upload-images.jianshu.io/upload_images/14466013-f96c7411301cba22.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
			* 压缩文件夹（不能实现）
			![image.png](https://upload-images.jianshu.io/upload_images/14466013-eadfc53132c480a7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)