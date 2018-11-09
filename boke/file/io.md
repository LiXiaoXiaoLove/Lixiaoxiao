* 流的分类

字节流

输入流：文件---->程序 读文件 outputStream
输出流：程序---->文件 写文件 intputStream

字节输出流：

```
路径正确但文件不存在是，系统会帮你创建出来，
否则会覆盖原文件
File file = new File("路径");
FileOutputStream fos = new FileOutputStream(file);

1. 一个字节一个字节的写入，按ASCII码写入
fos.write(48);

2. 利用字节数组写入,按ASCII码
byte[] b = {66,77,88,99};
fos.write(b);

3. 利用字符串输入
String str = "lixiao";
fos.write(str.getBytes());

4. 按字节数组偏移量写入
b数组中从第二个字节开始，写入2个字节的长度
fos.write(b,1,2);

```

字节输入流

```

路径正确但文件不存在是，系统会帮你创建出来，
否则会覆盖原文件
File file = new File("路径");
FileIntputStream fis = new FileIntputStream(file);

1. 一个字节一个字节的读出，按ASCII码读
int read = fis.read();
System.out.println((char)read);
read = fis.read();
System.out.println((char)read);
//文件读取完毕会返回-1
read = fis.read();
System.out.println((char)read);


2. 循环读取文件
//事先声明一个变量来接收读出来的数据
 int len = 0;
 //循环读取文件
 while((len = fis.read()) != -1){
	System.out.println((char)len);
 }
 
 
3. 利用数组读取文件
byte[] b = new byte[1024];
int read = fis.read(b);
//若没读完，会返回读取的长度
System.out.println(read);
read = fis.read(b);
//若已读完，则返回-1
System.out.println(read);
//查看数组中的内容，数组输出不用循环，就要用该系统函数
System.out.println(Arrays.toString(b));

```

4. 利用数组在循环读取
//byte的长度一般填1024或1024的倍数
byte[] b = new byte[1024];
int len = 0;
//当文件没读完，但数组已满时，先让数组输出，在用数组读取
//当最后文件读完，但数组没用完时，数组中剩下的部分可能有以前的
//数据没被覆盖，所以要有读取的长度来规定写入时的大小
//否则可能会出现得到的文件比读取的文件大的情况
while((len = fis.read(b)) != -1){
//  保证只写入有效的部分
	String str = new String(b,0,len);
}


字符流：主要用于文档的读写

输入流：FileReader
输出流：FileWriter

字符输入流

```

FileWriter fw = new FileWriter("路径");

按字符串写入
//两个字符 "\n" 是一个字符，两个字节（回车 13 换行 10）
//2个字符
fw.write("李\n");

用数组写入
//四个字符
char[] c = {'李','a','b','c'};
fw.write(c);


//写入文件时是看不到换行效果的，但读出时可以看到效果
fw.write("\n离离原上草\n一岁一枯荣\n野火烧不尽\n春风吹又生");

```


字符流输出流：

```

FilrReader fr = new FileReader("路径");

```


转换流：

OutputStreamWriter  字符流向字节流转换的桥梁
1. 将程序中的字符通过创建转换流时给出的编码格式[GBK或UTF-8]，查对应的码表
2. 将查到的字节[两个过三个]，交给创建流时传入的字节流对象
3. 最终是用字节流将文件写入

InputStreamReader   字节流转向字符流的桥梁
1. 先按字节读，读完后，用转换流去查对应的表
2. 最终以字符的形式读到程序中

编码格式：
Mac  默认的编码格式是UTF-8  一个字是3个字节
Win  默认的编码格式是GBK    一个字是2个字节

```

1. 用转换流写UTF-8格式的文件

   FileOutputStream fos = new FileOutputStream("路径");
   OutputStreamWriter osw = new OutputStreamWriter(fos,"UTF-8");
   osw.write("LiXiao");
   osw.close();
   
2. 用转换流写GBK格式的文件
   FileOutputStream fos = new FileOutputStream("路径");
   OutputStreamWriter osw = new OutputStreamWriter(fos,"GBK");
   osw.write("YangYun");
   osw.close();
   
3. 用转换流读取GBK格式的文件
   FileIntputStream fis = new FileIntputStream("路径");
   InputStreamReader isr = new InputStreamReader(fis,"GBK");
   char[] b = new char[1024];
   int len = 0;
   while((len = isr.read(b)) != -1){
		System.out.println(new String(b,0,len));
   }
   isr.close();
   
4. 用转换流读取UTF-8格式的文件
   FileIntputStream fis = new FileIntputStream("路径");
   InputStreamReader isr = new InputStreamReader(fis,"UTF-8");
   char[] b = new char[1024];
   int len = 0;
   while((len = isr.read(b)) != -1){
		System.out.println(new String(b,0,len));
   }
   isr.close();

```

关闭流的规则：

```

1. 多个流嵌套(即流当参数传入)时,只需要关闭最外层的流;
2. 自己创建出来的流,自己关;
3. 从系统中获取的流,不需要自己关闭,系统自动处理.

```


缓冲流：高效流
        默认缓冲区大小：8K
		内部自带一个缓冲数组



BufferedOutputStream   缓冲字节输入流
BufferedInputStream    缓冲字节输出流


缓冲字节流读取

```

FileIntputStream fis = new FileIntputStream("路径");
BufferedInputStream bis = new BufferedInputStream(fis);
byte[] b = new byte[1024];
int len = 0;

1. 
   while((len = bis.read(b)) != -1){
		System.out.println(new String(b,0,i));
   }
   
   
2. 
   BufferedOutputStream bos = new BufferedOutputStream("路径");
   while((len = bis.read(b)) != -1){
		bos.write(b,0,len);
   }



```

缓冲字节流写

```

FileOutputStream fos = new FileOutputStream("路径");
BufferedOutputStream bos = new BufferedOutputStream(fos);
//把字符串转换成字节
bos.write("lixiao".getBytes());
fos.close();

```


缓冲流字符流读

```
day20  04
```


缓冲流字符流写

```

```


总结：

```

源文件.....输入流  InputStream Reader
目标文件....输出流  OutputStream Writer

文本 字符流  
其他 字节流

转换流(按码表读写)
高效流(读写快)
对象流(将对象持续化)
打印流(原样输出)

```







































