## 自己创建博客

### 关于Linux
1. pwd 显示当前目录
2. cd 切换当前目录到其他目录
3. cd / 进入根目录
4. cd ~ 进入家目录（管理员身份进入到/root/,普通用户进入到/home/）
5. mkdir 文件名 创建文件夹

### 用git Bash 操作博客
1. cd ~ (因为用此语句，下面的单词可以用tab自动补齐)
2. psw
3. cd Destop/
4. git clone 博客名（来自如下）(直接克隆克隆不到，需要先生成公钥)
    ![图1](https://upload-images.jianshu.io/upload_images/14466013-28f10969a92c739d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
    ![图2](https://upload-images.jianshu.io/upload_images/14466013-4e6886f09dbe9033.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
5. ssh*keygen *t rsa *C "邮箱名" 生成博客的公钥（按三次回车,得到一个文件，把文件里的公钥copy到博客里（点击用户的setting，找到SSH and GPG keys ,找到 New SSH key,copy进去））））））））
    ![图3](https://upload*images.jianshu.io/upload_images/14466013*5820719bdee93fd8.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
6. git clone 博客名（来自如下）
    ![图4](https://upload*images.jianshu.io/upload_images/14466013*ecfaa6d6ac910085.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
7. cd 博客文件夹名 进入博客文件夹中
8. ls 查看当前文件夹里的文件
9. git status 查看状态码
10. touch 文件名.md (创建文件，并编写文件)
11. git add 文件名.md (把内容放进缓冲区)
12. git commit *m "first commit" (防止进行这步操作时系统崩溃，好回到上一步)
    ![图5](https://upload*images.jianshu.io/upload_images/14466013*85782962832436fb.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
13. git config **global user.email "邮箱名"
14. git config **global user.name "博客名"
15. git commit *m "first commit"
    ![图6](https://upload*images.jianshu.io/upload_images/14466013*be3910c6ce2eff67.png?imageMogr2/auto*orient/strip%7CimageView2/2/w/1240)
16. git push *u origin master(把文件上传)

### Markdown语法
* [Markdown帮助教程](https://guides.github.com/features/mastering-markdown/)

