## 案例一
* 写一个shell脚本能够对所有的压缩包进行解压
* toncat jdk hadoop压缩包放在 /home/yyc/tar 下（yyc是一个用户）
	1. 获取用户要解压的路径（该路径用参数传过来，用"$1" 符来获取）
	2. 从对应目录获取所有要进行解压的文件
	3. 对这些文件一个个的进行解压
	
* eg：
```
#在 /home/yyc/bin下新建一个shell文件
touch lxxtar.sh
#进入文件内进行编辑
vim lxxtar.sh

#shells脚本的开头，是固定的
#!/bin/bash

#把压缩包的路径放置在一个文件内
ls $1*.gz > /home/yyc/bin/tar.log
#循环该文件
for file in $(cat /home/yyc/bin/tar.log)
#进行解压操作
do
	tar -zxf $file
	echo "$file已解压完成"
done


#运行该脚步
. lxxtar.sh /home/yyc/tar/

```