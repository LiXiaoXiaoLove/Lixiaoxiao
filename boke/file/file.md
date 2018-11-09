## file类

* file类的作用

```

1. 表示文件

2. 表示文件夹

3. 表示路径

```

* 获取文件的三种方法

```
  
1. 常见方法
   File file = new File("E:\\hdfs\\imput\\test.txt")
2. 路径与文件名分离
   File file = new File("E:\\hdfs\\imput","test.txt")
3. 路径是一个对象
   File parent = new File("E:\\hdfs\\input");
   File file = new File(parent,"test.txt");
	  
```

* 判断语句

```
1. 判断一条路径是否存在
   boolean b = file.existst();
   
2. 判断一条路径是否是文件
   boolean b = file.isFile();
   
3. 判断一条路径是否是文件夹
   boolean b = file.isDirrectory();

```

* 获取路径

```

1. 获取绝对路径
   String path = file.getAbsolutePath();
 
2. 获取传入路径
   String path = file.getPath();

```

* 创建文件

```

1. 创建文件前先查看该文件是否以存在，
   若存在，返回false
   若不存在并创建成功就返回true
   boolean newFile = new File("E:\\hdfs\\input\\li.txt").createNewFile();

```

* 创建文件夹

```

1. 创建单个文件夹
   File file = new File("E:\\hsdf\\input\\li");
   boolean b = file.mkdir();
   
2. 创建多层的文件夹
   File file = new File("E:\\hsdf\\input\\b\\a");
   boolean b = file.mkdirs();
   
```

* 删除

```

1. 删除文件 
   boolean b = file.delete();
2. 删除空文件夹
   boolean b = mkdir.delete();
```