## hadoop中hdfs的环境诶配置

```
(在eclipse开发hadoop所需要的插件)[https://lixiaoxiaolove.github.io/Lixiaoxiao/bao/hadoop-eclipse-plugin-2.7.3.jar]
(ecplise安装包)[https://lixiaoxiaolove.github.io/Lixiaoxiao/bao/eclipse-jee-neon-3-win32-x86_64.zip]
```

```

1. 将hdfs的插件放在eclipse下的plugins里(若还不能用，就放在eclipse下的dropins文件里)
    重新打开ecplise就能看到如下图所示
```

![image.png](https://upload-images.jianshu.io/upload_images/14466013-7c643ae0bdbdd04c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```

2. 重新打开ecplise，在打开window下的show view里的other，搜索map,选中Map/Reduce Locations，点OK
   就会在控制台上出现Map/Reduce Locations的一个小窗口，打开该窗口，会看到一个小蓝象，
   同时在控制台的右上角也会有小象，点该小象进行第三步操作

```

![image.png](https://upload-images.jianshu.io/upload_images/14466013-b39283dd6903b166.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-625d6f6e171973a3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)![image.png](https://upload-images.jianshu.io/upload_images/14466013-625d6f6e171973a3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/14466013-bb709368501ef874.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


```

3. 填写信息
     Location name:随意起
   Map/Reduce下的
     Host:写namenode的Ip
     Port:写50020
   DFS Mater下的
     Host:写namenode的Ip
     Port:写9000
   
```

![image.png](https://upload-images.jianshu.io/upload_images/14466013-c79bf91dbf7123c6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


