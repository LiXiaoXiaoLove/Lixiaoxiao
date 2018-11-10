## 求手机的上行流量，下行流量与总流量

* 准备工作

1. 三个源文件，数据如下：

	* flow01.log
	
![](https://upload-images.jianshu.io/upload_images/14863832-8d483de6dd2c27bd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	
	* flow02.log
	
![](https://upload-images.jianshu.io/upload_images/14863832-0e83e1ce5dd46350.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	
	* flow03.log
	
![](https://upload-images.jianshu.io/upload_images/14863832-8d483de6dd2c27bd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. 把文件上传到hdfs上

* 代码

	1. Bean类

```

//自定义方法当value时只需要实现Writable接口就可以，因为不需要进行比较
//但当自定义方法当key使用时，就需要实现WritableComparable<T>接口，
//因为key要进行比较运算进行排序分组
public class JiChuBean implements Writable{
//	bean类的四大要素
//	1. 公共类
//	2. 私有属性
//	3. 私有属性的get与set方法
//	4. 无参构造方法
	
//	上行流量
	private int uploadStranm;
//	下行流量
	private int downloadStream;
//	总流量
	private int sumStream;
//	无参构造
	public JiChuBean() {
		// TODO Auto-generated constructor stub
	}
//	两参构造，因为第三参可以通过前两个得到，并且第三参在文件中不能直接获得，也是通过前两参得到的
	public JiChuBean(int uploadStranm, int downloadStream) {
		this.uploadStranm = uploadStranm;
		this.downloadStream = downloadStream;
	}
//  从文件中得到的是String类型，需要强转类型，在构造方法中强转只需要进行一次，简单
	public JiChuBean(String uploadStranm, String downloadStream) {
		this.uploadStranm = Integer.parseInt(uploadStranm);
		this.downloadStream = Integer.parseInt(downloadStream);
		this.sumStream = this.uploadStranm + this.downloadStream;
	}
//  toString方法，是写入文件中的格式，也是从文件中读取时的格式
	@Override
	public String toString() {
		return "uploadStranm=" + uploadStranm + "\tdownloadStream=" + downloadStream + "\tsumStream="
				+ sumStream;
	}
//  get与set方法
	public int getUploadStranm() {
		return uploadStranm;
	}
	public void setUploadStranm(int uploadStranm) {
		this.uploadStranm = uploadStranm;
	}
	public int getDownloadStream() {
		return downloadStream;
	}
	public void setDownloadStream(int downloadStream) {
		this.downloadStream = downloadStream;
	}
	public int getSumStream() {
		return sumStream;
	}
	public void setSumStream(int sumStream) {
		this.sumStream = sumStream;
	}
//  相当于java中的反序列化，
//	注意：
//	       反序列化的顺序是固定的，
//	      序列化的顺序是什么样子，反序列化的顺序就是什么样子
	@Override
	public void readFields(DataInput in) throws IOException {
		this.uploadStranm = in.readInt();
		this.downloadStream = in.readInt();
		this.sumStream = in.readInt();
	}
//  序列化
//	注意：
//	   写入的格式
	@Override
	public void write(DataOutput out) throws IOException {
		out.writeInt(uploadStranm);
		out.writeInt(downloadStream);
		out.writeInt(sumStream);
	}
}

```

	2. map类

```

public class JiChuMapper extends Mapper<Object,Text,Text, JiChuBean>{
//  节省空间，一共就用一个实例化对象，
//	但要注意一个实例化对象就只有一个地址
//	若用该对象保存数据，就只能保存循环的最后一个，因为会发生覆盖现象
	private Text phoneText = new Text(); 
//	一般从文件中读取数据时输入的key类型就要用个Object
//	因为从文件中读取数据，key表示的是偏移量，会是一个很大的数字
//	hadoop中Test表示Java中的String
//	自定义的类要实现接口
//	map方法结束后的数据会传给combiner
//	若没有该方法，会直接传给reduce
	@Override
	protected void map(Object key, Text value, Mapper<Object, Text, Text, JiChuBean>.Context context)
			throws IOException, InterruptedException {
//		用正则拆分一行数据
//		map方法一次接收文件中的一行数据
		String[] vals = value.toString().split("\\s+");
//		按照拆分结果获取自己需要的信息
		String phone = vals[1];
		String uploadStream = vals[vals.length - 3];
		String downloadStream = vals[vals.length - 2];
//		类型转换
		phoneText.set(phone);
//		实例化对象，把信息传给该对象
		JiChuBean bean = new JiChuBean(uploadStream,downloadStream);
//		把数据先传给pasrtition()方法进行分区，然后写入磁盘文件
		context.write(phoneText,bean);
	}
}

```

	3. partition类

```

public class JiChuPartitioner extends Partitioner<Text, JiChuBean>{
//	静态变量才能在静态方法中运用
	private static Map map;
//	静态代码块，只在刚运行时加载一次
	static{
		map = new HashMap<>();
		map.put("135",0);
		map.put("137",1);
		map.put("139",2);
	}	
//	按手机号来分区
//	135开头的放第一区
//	137开头的放第二区
//	139开头的放第三区
//	其他的放第四区
	@Override
	public int getPartition(Text key, JiChuBean value, int arg2) {
//		获取每个map传过来的数据的key（手机号）的前三位
		String keyPartition = key.toString().substring(0,3);
//		用map的key值得到返回值
		Integer result = (Integer) map.get(keyPartition);
		if(result == null){
			System.out.println("aaa:" + arg2);
			return 3;
		}
		return result;
	}
}

```

	4. combiner类

```

public class JiChuCombiner extends Reducer<Text, JiChuBean, Text, JiChuBean>{
//	该方法也是进行汇总，所有和XXreduce类一样继承reducer类，实现reduce方法
//	只是XXreduce方法是最后汇总，而XXcombiner是在每个map结束后进行一次汇总
//	即有几个map就调用几次XXcombiner方法，而XXreducer方法每一个job调用一次
	@Override
	protected void reduce(Text key, Iterable<JiChuBean> value, Reducer<Text, JiChuBean, Text, JiChuBean>.Context context)
			throws IOException, InterruptedException {
//		按key相同来进行信息的合并
		int uploadsum = 0;
		int downloadsum = 0;
		for (JiChuBean jiChuBean : value) {
			uploadsum += jiChuBean.getUploadStranm();
			downloadsum += jiChuBean.getUploadStranm();
		}
//		新建对象，传数据
		JiChuBean bean = new JiChuBean(uploadsum,downloadsum);
//		把合并的结果再次写入文件中
		context.write(key, bean);
	}
}

```

	5. reduce类

```

public class JiChuReducer extends Reducer<Text,JiChuBean, Text,JiChuBean>{
//	最后进行汇总输出到文件中
	@Override
	protected void reduce(Text key, Iterable<JiChuBean> value, Reducer<Text, JiChuBean, Text, JiChuBean>.Context context)
			throws IOException, InterruptedException {
		int uploadsum = 0;
		int downliadsum = 0;
		for (JiChuBean jiChuBean : value) {
			uploadsum += jiChuBean.getUploadStranm();
			downliadsum += jiChuBean.getDownloadStream();
		}
		JiChuBean bean = new JiChuBean(uploadsum,downliadsum);
		context.write(key, bean);			
	}
}

```

	6. driver类(Test类)

```

public class JiChuTest {
	public static void main(String[] args) throws IOException, ClassNotFoundException, InterruptedException {
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
		job.setJarByClass(JiChuTest.class);
		
//		设置map方法的类，用来拆分数据
		job.setMapperClass(JiChuMapper.class);
//		设置每个map方法结束后的排序的方法，重写reduce方法
		job.setCombinerClass(JiChuCombiner.class);
//		设置reduce方法的类，用来合并数据
		job.setReducerClass(JiChuReducer.class);
//		设置reduce方法输出的key与value的类型
		job.setOutputKeyClass(Text.class);
		job.setOutputValueClass(JiChuBean.class);
		
//		设置getPartition()方法的类，用来把数据分区输出
		job.setPartitionerClass(JiChuPartitioner.class);
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
}

```

* 结果：分四个文件(四个区)

	- 第一个

![](https://upload-images.jianshu.io/upload_images/14863832-1b90a0a93993eb56.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	- 第二个

![](https://upload-images.jianshu.io/upload_images/14863832-b836a698f53dc81e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	- 第三个

![](https://upload-images.jianshu.io/upload_images/14863832-1b2d9dbe42c22f62.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	- 第四个

![](https://upload-images.jianshu.io/upload_images/14863832-0426f4162764a0b9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 用图解析

![](https://upload-images.jianshu.io/upload_images/14863832-6d80210bbe8c0c28.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
