## reduce的控制台

```

	public static void main(String[] args) throws IOException, ClassNotFoundException, InterruptedException, URISyntaxException {
//		配置文件
//		Configuration 配置
		Configuration conf = new Configuration();
		
//		设置文件系统，不设置时默认是本地系统（hdfs:///）
		conf.set("name","hdfs://192.168.107.143:9000");
//		设置要使用的用户名，是键值对（key,value）
		System.setProperty("HADOOP_USER_NAME","lxx");
		
//		获取所有的被使用的文件
//		GenericOptionsParser 泛型选项解析器
//		getRemainingArgs 获取剩余ARG
		String[] otherArgs = new GenericOptionsParser(conf,args).getRemainingArgs();
		
//		otherArgs是所有文件的个数，若小于2，表示没有文件，
//		因为若要进行该操作，至少需要一个输入文件，一个输出文件
		if(otherArgs.length < 2){
//			终止当前运行的Java虚拟机。
//			这个参数用作状态代码；
//			按照惯例，非零状态代码指示异常终止。
			System.exit(2);
		}
		
//		创建一个工作
		Job job = Job.getInstance(conf,"name");
		
//		设置测试的类，打包使用的
		job.setJarByClass(MainTest.class);
		
//		设置map方法的类，用来拆分数据
		job.setMapperClass(WordCountMapper.class);
//		设置map方法输出的key与value的类型
		job.setMapOutputKeyClass(Text.class);
		job.setMapOutputValueClass(IntWritable.class);
		
//		设置每个map方法结束后的排序的方法，重写reduce方法
		job.setCombinerClass(WordCountReducer.class);
		
//		设置reduceTask的个数，若为0
//		表示没有reduce方法可以执行，所以就只执行map方法
//		若没有这句话，即使你不提交setReducerClass()
//		这个方法,默认也是执行reduce方法的
		job.setNumReduceTasks(0);
		
//		添加缓存文件，是map端join算法的时候用
		job.addCacheFile(new URI("hdfs://192.168.107.143:9000/具体文件的路径"));
		
		
//		设置reduce方法的类，用来合并数据
		job.setReducerClass(WordCountReducer.class);
//		设置reduce方法输出的key与value的类型
		job.setOutputKeyClass(Text.class);
		job.setOutputValueClass(IntWritable.class);
		
//		设置getPartition()方法的类，用来把数据分区输出
//		job.setPartitionerClass(MobilePartitioner.class);
//		设置分区就一定要设置reduce的进程数，否则分区不会生效
//		并且这里所设置的数要大于等于你的分区数，否则会出现异常
		job.setNumReduceTasks(4);
		
		
//		获取所有的输入文件（所有的文件中最后一个是输出地址，其他的全是输入文件）
		for (int i = 0; i < otherArgs.length - 1; i++) {
			FileInputFormat.addInputPath(job, new Path(otherArgs[i]));
		}
//		获取输出文件
		FileOutputFormat.setOutputPath(job,new Path(otherArgs[otherArgs.length - 1]));
		
//		把该job提交，并返回提交是否成功
		boolean result = job.waitForCompletion(true);
//		若返回0表示成功，否则就终止当前运行的java虚拟机
		System.exit(result ? 0 : 1);
	}

```

