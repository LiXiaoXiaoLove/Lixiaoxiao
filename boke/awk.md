
* 基本概念
	* awk以行为单位逐行处理
	* 每一行中默认以空格分割字符串
* 基本语法
	* awk 选项 'command' filepath
		* 选项
			* -F 设置分隔符，默认以空格进行分割
		* command
			* NR     行号
			* NF     列号
			* $n     第n列
			* print  输出
			* printf 输出
* awk的扩展格式
	* awk options选项 'BEGIN{} ~//{} END{}' filepath