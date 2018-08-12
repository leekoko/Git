# IDEA（中）

## 分布式项目创建

Z：复杂项目创建步骤，首先创建目录结构   

1. 创建空项目，作为顶级文件夹   

   ![](..\imgs\id40.png)  

2. 创建聚合项目

   ![](..\imgs\id41.png)  

   ![](..\imgs\id42.png)  

   填写项目名，点击完成即可。

3. 往聚合项目中创建Module   

   ![](..\imgs\id42.png)

   ![](..\imgs\id43.png)  

   ![](..\imgs\id44.png)  

   ![](..\imgs\id45.png)  

   创建后目录如下

   ![](..\imgs\id46.png)  

4. 因为以上创建的项目都不用于编译，所以可以把src文件夹删除   

Z：在聚合项目中创建pom工程  

1. 也是使用New - Module，创建父工程，设置Parent为none  

   ![](..\imgs\id47.png)  

   ![](..\imgs\id47.png) 

   往pom.xml中添加package``<packaging>pom</packaging>``    

2. 同理创建继承模块，继承于Parent，其属于basic项目      

   ![](..\imgs\id49.png)   

   获得以下目录结构

   ![](..\imgs\id50.png)  

3. install安装pom工程项目到仓库

   ​

Z：创建war项目   

1. 创建module，继承于Parent

   ![](..\imgs\id51.png)    

2. 修改路径位置  

   ![](..\imgs\id52.png)  







 









http://edu.51cto.com//center/course/lesson/index?id=273234





## 4.热部署



#### 3.热部署模式

M：当修改一些参数，不想重启服务器，应该怎么做？

Z：可以配置tomcat热部署。

![](D:\github_place\itTools\imgs\id18.png)  

修改了内容之后，将焦点挪出编辑框，即执行热部署。

![](D:\github_place\itTools\imgs\id19.png)  

M：但是这种配置对新增新成员（例如参数，方法）是不起效果的。

D：那只能重启服务器，否则就是使用JRebel插件。

M：怎么离线安装JRebel插件呢？

Z：点击设置，选择插件并导入

![](D:\github_place\itTools\imgs\id20.png)  

JRebel下载地址：链接：https://pan.baidu.com/s/10Vlu2NJU-7TS7mpD_Jf65Q 密码：5imr   

这个软件是收费的，激活方式可以参照该[网友](https://blog.csdn.net/qq_27093465/article/details/79148498)写的文章。







​    

Z：在部署旧的的maven项目时，需要注意配置新的tomcat（否者会默认使用旧的），添加项目需要选择war exploded  

![](D:\github_place\itTools\imgs\id22.png)











------

参考资料：

https://ke.qq.com/course/298348

http://edu.51cto.com/course/13866.html?source=so   <

https://ke.qq.com/course/297923

https://www.imooc.com/video/16216一大堆快捷键

https://ke.qq.com/course/320065























