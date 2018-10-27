
* 基本概念

```
awk以行为单位逐行处理
 每一行中默认以空格分割字符串
```

* 基本语法

```
awk 选项 'command' filepath
```

* 选项

```
-F 设置分隔符，默认以空格进行分割
```

* command

```
NR     行号

NF     列号

$n     第n列

print  输出

printf 输出

```

* awk的扩展格式

```
awk options选项 'BEGIN{} ~//{} END{}' filepath
```
	
* Eg

```
1. 简单格式：
   awk -F ':' '{print NR}' /etc/passwd
   awk -F ':' '{print NF}' /etc/passwd
   awk -F ':' '{print $1}' /etc/passwd
    
2. 输出格式：
   awk -F ':' '{print "1: "$1,"2: "NR}' /etc/passwd
   awk -F ':' '{printf("Line:%2s col:%s User:%s\n",NR,NF,$1)}' /etc/passwd

3. if
   awk -F ':' '{if($3<100) printf("Line:%2s Col:%s UserId:%4s User:%s\n",NR,Nf,$3,$1)}' /etc/passwd
  
4. 配合正则使用
   awk -F ':' '$1~/^java.*/{printf("Line:%2s Col:%s UserId:%4s User:%s\n",NR,Nf,$3,$1)}' /etc/passwd

5. awk的扩展
   awk -F ':' 'BEGIN{print "Line Col UserId User"} {printf("%3s %s %4s %s\n",NR,Nf,$3,$1)} END{print"---"FILENAME"---"}' /etc/passwd
   
6. for
   ls -l | awk 'BEGIN{size=0} {size+=$5} END{print "FileSize is "size}'
   
7. 正则
   awk -F ':' 'BEGIN{count=0} $1!~/^$/{count++} END{print "peopleCount is "count}' /etc/passwd
  
8. 数组
   awk -F ':' 'BEGIN{cunt=0} {if($3.100) name[count++]=$1} END{for (i=0;i<count;i++) print i,name[i]}' /etc/passwd
 
```