## outputFormat

学会何如自定义
结果输出到哪，以什么形式输出

1. 在driver中设置job.setOutputFormatClass(）
2. 创建自定义的XXOutputFormat extends FileOutputFormat
3. 实现对应方法getRecordReade()
3.1 需要通过this.getOutputPath(job)拿到我们想要输出的位置
3.2 根据输出目录创建输出流，传给RecordWriter
4. 创建对应的XXRecordWriter extends RecordWriter
5. 实现三个方法
5.1 带参数的构造方法：用来接收输出流，知道要往哪些位置写
5.2 write(Text key, Text value)方法：能够接收到最终要写入的内容
    在这里进行逻辑判断决定往哪个输出流进行写入
5.3 close(TaskAttemptContext context)方法：用来关闭流，也是job的结束

## inputFormat

以什么形式输入，这时候map形参要注意对应

1. driver job.setOutputFormatClass()
2. 创建自定义的XXInputFormat extends FileInputFormat<>
3. 实现对应方法createRecordReader
   除了要创建对应的RecordReader，还需要通过initialize(split,context)来进行赋值
4. 创建对应的XXRecordReader extends RecordReader
5. 实现对应的方法：
5.1 initialize(InputSplit split, TaskAttemptContext context)
    因为我们recordReader是真正要读数据的人，所以需要通过split来读取文件的信息
    从context.getConfiguration()中获取到我们配置的文件系统的位置
5.2 nextKeyValue() 按格式读取文件，并根据读取的结果返回，返回值将决定map是否要执行
5.3 getCurrentKey() map方法传入的key值是从这个方法中获取的
5.4 getCurrentValue() map方法传入的vlaue值是从这个方法中获取的
5.5 getProgress() 获取进度的方法