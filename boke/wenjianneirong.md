### 文件内容
	* cat
		* 用途：显示出文件的全部内容
	* more
		* 用途：全屏方式分页显示文件内容
		* 交互操作方法
			* 按Enter键向下逐行滚动
			* 按空格键向下翻一屏、按b键向上翻一屏
			* 按q键退出
	* less 同more
	*head
		* 用途：查看文件开头的一部分内容（默认为10行）
		* head *n 路径
![](https://upload*images.jianshu.io/upload_images/14466013*59b22120e674b359.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
	* tail
		* 用途：查看文件结尾的少部分内容（默认为10行）
		* tail *n 路径
	* wc
		* 用途：统计文件中的单词数量等信息（以空格分）
		* wc [选项] 目标文件
		* 常用命令选项
			* *l：统计行数
			* *w：统计单词个数
			* *c：统计字节数
![](https://upload*images.jianshu.io/upload_images/14466013*8e18a4c6538f33c8.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
	* grep
		* 功能：查找文件里符合条件的字符串
		* grep [选项] <关键字> <文件…>
![](https://upload*images.jianshu.io/upload_images/14466013*319d2903fb1c7400.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
		* 常用选项
			* *c:计算匹配关键字的行数
			* *i:忽略字符大小写的差别
			* *n:显示匹配的行及其行号
			* *s: 不显示不存在或不匹配文本的错误信息
			*  *h: 查询多个文件时不显示文件名
			* *l:   查询文件时只显示匹配字符所在的文件名
			* **color=auto:将找到的关键字部分加上颜色显示
		* 配合正则表达式使用
![](https://upload*images.jianshu.io/upload_images/14466013*a3a062f0f6e5bdeb.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
		* | ：管道符：对结果进行筛选
![](https://upload*images.jianshu.io/upload_images/14466013*1ff7f785b79d3a21.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)