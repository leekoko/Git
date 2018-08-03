# Kettle   

下载地址：http://mirror.bit.edu.cn/pentaho/Data%20Integration/

（JDK1.8才可支持Kettle7.0以后的版本）  

### 配置环境变量，启动程序    

![](../imgs/kettleA01.png)  

(变量值根据文件目录而定)   

运行Spoon.bat启动程序   

### 单表数据迁移   

1. 进入主界面，左上角点击**文件-新建-转换**保存为demo.ktr

2. 左侧选择**核心对象**面板。”在**输入**文件夹下选择**表输入**并把它拖动到右侧编辑区。    

   ![](../imgs/kettleA02.png)  

3. 双击编辑区的**表输入**图标，编辑数据输入来源。点击**数据库连接**右侧的**新建**按钮，按demo背景中的要求，配置数据库参数。配置后点击**测试**   

   ![](../imgs/kettleA03.png)  

   _如果报错找不到驱动包，复制oracle的驱动jar文件到ETL(Kettle)的lib目录下（我这里使用的是jdbc7.jar）_   

4. 点击**获取SQL查询语句**”（等待时间较长），选择要迁移的表，点击**确定**

   ![](../imgs/kettleA04.png)  

   选择**否**

   ![](../imgs/kettleA05.png)  

5. 重复以上步骤2，在**输出**文件夹下选择**表输出**并把它拖动到右侧编辑区。连线**表输入**和**表输出**  

   ![](../imgs/kettleA10.png)  

   ​

6. 双击编辑表输出，填入目标表名    

   ![](../imgs/kettleA06.png)  

   _要迁移的目标表不能已存在于目标数据库中，除非是表结构相同。_   

7. 点击 执行SQL 语句列表，选择**执行SQL**      

   ![](../imgs/kettleA07.png)  

8. 点击 “运行转换”，直接选择启动

   ![](../imgs/kettleA08.png)

   之后就能看到执行结果   

   ![](../imgs/kettleA09.png)   

   _这里仅是对数据进行迁移，主键、外键、关联信息不会迁移过去，需要后期去目标数据库配置。_   

9. 当出现数据中文乱码的时候

   ![](../imgs/kettleA11.png)   

   ![img](file:///D:/github_place/itTools/imgs/kettleA12.png?lastModify=1533261337)尝试去掉允许简易转换，再进行预览

   ![](../imgs/kettleA12.png)   

   查看Oracle数据库的编码格式``select userenv('language') from dual; ``



### 多表数据备份   

1. ​
















