## boot

* maven环境的安装
	* 与java相同
* 测试maven是否安装成功
	* 安装完成后在cmd中敲maven -version来验证maven是否安装完成
	* 若没反应就重启电脑

![image.png](https://upload-images.jianshu.io/upload_images/14466013-0b0e4423b1b4e603.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* maven:jar包管理工具
* ide:集成开发环境：包含idea，eclipse
* 在百度中搜maven仓库去下载jar

* 从后端往前端传数据，是用json

```

   //可以是自定义的实体类
   String jsonStr = JSON.toJSONString(users);
   //也可以是map等对象
   String json = JSON.toJSONString(map);
   
```

* 异步请求：ajax：可以实现局部更新

```

把$当对象来看
Function succ(data){
Console.log(data)
}

对象
obj = {
//请求地址：可以是接口，文件，文档
Url:”localhost:8080/list.html”,
//请求方式
Method:”get”,

//data:{从前端往后端传数据,以键值对的形式传},
data:{
  "name":$("#name"),.val(),
  "pwd":$("$pwd").val()
}
//成功时的回调函数，还有失败时的回调函数
Success:succ
}

方法
$.ajax(obj)

```

* tomcat在虚拟机中用的时候也是直接解压就好了
	* 在lib目录下进行手动的启动与关闭
* export 导出War包
	* 把war包传到webapps下，在启动tomcat，然后在浏览器上去查看结果
	
* Springboot --ssm框架搭建

* 在idea中运用maven

![image.png](https://upload-images.jianshu.io/upload_images/14466013-0032812338edddc9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-ddcc42f643e6a0a8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-ae5448cbcd3a8394.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-f7f2b544249120d0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

1. 创建springboot的项目（需要在有网的情况下运用）

![image.png](https://upload-images.jianshu.io/upload_images/14466013-b7845cf2e5267285.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-991b2695daba0ea7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-aa95f06e98680d7b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. 修改pom.xml，引入dependence（依赖）与plugin（插件）

![image.png](https://upload-images.jianshu.io/upload_images/14466013-b182994add54dd79.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-45e988b879a50560.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-b77fd8e1c71c9d81.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-31487168c4f9473d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-a0cffd8177af27e8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 起步依赖：web是我们刚刚创建项目的时候选的

![image.png](https://upload-images.jianshu.io/upload_images/14466013-866e9a1df2d6be32.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```

依赖：
<dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <!--起步依赖-->
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
        </dependency>
        <!--alibaba-start-->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.1.0</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.9</version>
        </dependency>

        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.47</version>
        </dependency>
        <!--alibaba-end-->

        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.41</version>
        </dependency>
        <!--ssm-->
        <!--mybatis-start-->
        <!--mybatis-->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>1.3.1</version>
        </dependency>
        <!--generator-->
        <dependency>
            <groupId>org.mybatis.generator</groupId>
            <artifactId>mybatis-generator-core</artifactId>
            <version>1.3.2</version>
            <scope>compile</scope>
            <optional>true</optional>
        </dependency>
        <!--mapper-->
        <dependency>
            <groupId>tk.mybatis</groupId>
            <artifactId>mapper-spring-boot-starter</artifactId>
            <version>1.2.4</version>
        </dependency>
        <!--pagehelper-->
        <dependency>
            <groupId>com.github.pagehelper</groupId>
            <artifactId>pagehelper-spring-boot-starter</artifactId>
            <version>1.2.3</version>
        </dependency>
        <!--mybatis-end-->
    </dependencies>

插件：

![image.png](https://upload-images.jianshu.io/upload_images/14466013-7f46830fdcc0f3c7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-276f33992b7e0c7e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 <plugin>
                <groupId>org.mybatis.generator</groupId>
                <artifactId>mybatis-generator-maven-plugin</artifactId>
                <version>1.3.2</version>
                <configuration>
                    <verbose>true</verbose>
                    <overwrite>true</overwrite>
                </configuration>
                <dependencies>
                    <dependency>
                        <groupId>mysql</groupId>
                        <artifactId>mysql-connector-java</artifactId>
                        <version>5.1.29</version>
                    </dependency>
                    <dependency>
                        <groupId>tk.mybatis</groupId>
                        <artifactId>mapper</artifactId>
                        <version>4.0.0</version>
                    </dependency>
                </dependencies>
</plugin>

```

3. 逆向工程---告诉他要逆向工程的表有哪些，要生成的实体类放哪里，
* 要生成的dao层接口放哪里，要生成的xml放在哪里
* 是引用的外来文档generatorConfig.xml，里面需要修改一下项目名称等
* 进行到这里，就会在maven里生成mybatis-generator插件，运行该插件，就会逆向生成项目的底层，dao，model，mappers

![image.png](https://upload-images.jianshu.io/upload_images/14466013-6847391d561f78f0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-be46080227f677c7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4. 创建一个util工具包，在里创建一个MyMapper类，继承Mapper<T>,MyMapper<T>接口，才能用出来公共方法

![image.png](https://upload-images.jianshu.io/upload_images/14466013-fbb04febf140339b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-77a32720362044cd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5. Application.yml设置数据库的配置（运用代码提示，不要都手动敲，不然可能有错）

![image.png](https://upload-images.jianshu.io/upload_images/14466013-887ff8ae4c36810d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-1ad96aab2ae092ec.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```

# 连接数据库的配置
spring:
  datasource:
    driver-class-name: com.mysql.jdbc.Driver
    url: jdbc:mysql://192.168.107.155:3306/lxxsql?characterEncoding=utf-8
    username: root
    password: 123456
  profiles:
    active: prod

#mybatis 框架需要进行的设置
mybatis:
  type-aliases-package: com.lanou.firstboot.model
  mapper-locations: classpath:mappers/*.xml

#mapper
#mappers 通用mapper的设置，这样就可以使用很多通用方法了
mapper:
  mappers: com.lanou.firstboot.util.MyMapper
  not-empty: false
  identity: MYSQL

#pagehelper 分页插件的配置
pagehelper:
  helperDialect: mysql
  reasonable: true
  supportMethodsArguments: true
  params: count=countSql

```

6. 在自己boot项目(MybootApplication)的主入口设置

![image.png](https://upload-images.jianshu.io/upload_images/14466013-66ed6615b5b17100.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```

    @MapperScan选择tk包下的(basePackages = “dao层接口所在的包名”)
    @MapperScan(basePackages = “com.lanou.firstboot.dao”)

```

7. 把要使用的dao层接口定义成对应的controller的属性，并且加上@Autowired注解，
* 就可以在请求方法(UserController)中进行使用了

![image.png](https://upload-images.jianshu.io/upload_images/14466013-60d6cc04788801bd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
    @Autowired
    private UserMapper userMapper;
```

8. 请求方法也需要注解

```
    @RequestMapping("/user/finduser")
    public PageInfo findBy(User user, Integer pageNum){}
```

![image.png](https://upload-images.jianshu.io/upload_images/14466013-967beb0ca08876f4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-2188c2180cc28005.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-53a66385460419e7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可以有多张表

![image.png](https://upload-images.jianshu.io/upload_images/14466013-426c00f0740f0c6e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)	

![image.png](https://upload-images.jianshu.io/upload_images/14466013-359b6146522f5b3c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-e7b24effc9de3026.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


* 在eclipce里使用maven

* 在tomcat上运行servlet
* 在eclipce上运行tomcat，Tomcat直接解压就能用

![image.png](https://upload-images.jianshu.io/upload_images/14466013-e743dd0796ca4c41.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-60a6a7b6299fc283.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-03667fbbafec60dc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-cc9c7e9f48247143.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-0a621e9c3b3ef3fc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 修改端口

* 方法一：

![image.png](https://upload-images.jianshu.io/upload_images/14466013-09be1e5b3cdfccf3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-4f00421ee531e9f0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 方法二：

![image.png](https://upload-images.jianshu.io/upload_images/14466013-3140a53dba70aae0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 让server服务器能够运行

* 方法一：

![image.png](https://upload-images.jianshu.io/upload_images/14466013-af09cb9da6901d0e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 方法二：

![image.png](https://upload-images.jianshu.io/upload_images/14466013-346389939948177b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 清理缓存

* 方法一：

![image.png](https://upload-images.jianshu.io/upload_images/14466013-598f4fce4544a191.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-e6f2127260fdf438.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 在Linux环境里设置tomcat环境
* 把tomcat压缩包导入linux里，解压，然后需要自己在bin里启动才能用

![image.png](https://upload-images.jianshu.io/upload_images/14466013-86ea1a92d438d37a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 导出war包后再linux里运行

![image.png](https://upload-images.jianshu.io/upload_images/14466013-41217fbefed30b6b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-0df12bb881611f47.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 把war包上传到linux环境下

![image.png](https://upload-images.jianshu.io/upload_images/14466013-87bce7800d0fd36f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)









