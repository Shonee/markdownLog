[TOC]

###### 20190730:

###### 装箱单的导入操作：

excel表中数据的获取

`countCOL`：代表当前物料色号的种数，字典中色号名为 COL + [0123]等

​					大小也是一样，SIZE + [0123]

###### 正则表达式实现从字符串中提取数字：

```c#
//@代表强转义，跟在其后的所有字符均为字符串内容，不会和内部内部定义字符冲突
//()中的内容会放在返回值的value属性中
int num = Regex.match(strs,@"(\d+)").value;
```

问题：

​	1、物料品番、名称相同，规格、色号不同时，是两种物料？

​	2、物料品番、色号、规格相同，名称不同时(可组成一套的)，也是两种物料？

​	3、尺寸色号一样的，分多条，是分包；尺寸/色号不同的

​	

使用品番、色号、规格来决定一个物料，将名称后()内容最为规格，SIZE为规格

字典中键：

`goodsNO` `PFNO` `name` `GG` `row` `column` `SIZE1`  `COL1`  `WIDTH`  `Memo`

`NETWT` `GROSSWT` `MEASURE` `allNum` `allNumUnit` `detail`



装箱单导入时，只要（品番）、名称、尺寸、色号，详情

没有品番时（少见），直接用名字来做品番

名字后边（）内容，下行，非色号/尺寸 的（）内容都不要

尺寸值和单位之间的空格问题，物料信息中都不要加空格！！

装箱单不做要求



**`18CM`	:单个尺寸的，不要空格**

**`18CM` X `20CM`	：两个尺寸的，X号两边加单空**



使用split操作字符串，使用指定的字符串来分割长字符串

```c#
//1、split的重载方法
string result = 
  Text.Split(new string[] {"COL",":"},StringSplitOptions.None)[1];
//2、使用正则中的split方法
```



字符串大小写转换：

```c#
str = str.ToUpper();	//所有字符转换成大写
str = str.ToLower();	//所有字符转换成小写
```



###### 20190802：

###### 项目打包：

**[VS2010winform项目打包方法](https://www.cnblogs.com/hesijian/archive/2013/09/12/3316549.html)**



form窗体中当前用户属性：

`LoginUserInfo.FullName;`//当前登录用户名

`SecurityHelper.GetFullNameByID(info.Creator);` //根据用户ID获取用户名（即存储的是ID、显示的是名称）

**[人员肖像、事物图片控件的实现](https://www.jianshu.com/p/6df173c6a2d8)**

- [x] 登录人信息的转义
- [x] 更新操作的实现
- [x] 物料图片显示(编辑替换新图片时，要把路径下的图片同时替换掉，或者尝试不使用路径显示)
- [x] 添加保存/读取文件功能
- [x] 权限功能
- [x] 数据增删改记录日志

`TreeList`

```c#
//获取treeList中选中行caption为Id的列值，要有该列才可以
this.matsTreeList.FocusedNode.GetValue("Id");

```

###### `treeList`[使用方法小结](https://blog.csdn.net/qq_22698657/article/details/81626357)



###### 自动更新：

开启后台线程，客户端配置config文件，服务端配置.xml文件+更新压缩包

###### [服务器端配置文件](.\XML\manifests.xml)   [客户端配置文件](.\XML\updateconfiguration.config)

**文件**：客户端xml要放在debug文件夹下(项目根目录)，和初始化UpdateClass文件中定义的文件名称一致，否则报错

客户端xml文件内容和服务器xml文件内容要相符

更改服务器更新文件地址时，只需要将配置文件一同放在最后一次更新的文件中，进行替换即可。

```xml
//重启当前名称的exe程序
<entryPoint file="WHC.WareHouseMis.DxUI.exe" parameters="-S"/>

```

登录页面弹窗是新开启的线程，因此能够切换到主页面，两个操作不影响。

登录后的检查更新是主线程的

- [ ] 关于提示信息，进一步优化一下，主线程更新后，不能自动关闭
- [ ] 多线程更新时，关闭了窗口，不能重新启动



###### 原材料操作流程：

*导入***原材料合同** -> 提示将所有原料进行**自定义合并** -> 合并后*导出***面辅料清单** ，

*导入***装箱单** -> 按装箱单格式录入信息，入库时根据实际数量 ，

*导出*进口原材料**报关发票** -> 根据上面两个导入信息来获取数据，合并同类型，最终导出发票

###### 进口装箱单发票信息导出：（价格来自原材料信息）

格式要求：

头部：

内容：

​	英文名称(2列)	中文名称	(项号)	数量 单位	计价单位 价格	计价单位 总价

​	成分

​	规格(幅宽)

尾部：



浮点数，精度数值，保留指定长度小数位

Math.Round(x,n);  	//x代表要指定的数值，n代表要留的小数位数



###### K3系统信息的同步对接：

物料基本信息

人员基本信息

入库、出库

对应的表要有一个K3表数据的ID项，用于连接，加一项，存放K3表名

K3接口，建立单个工程项目，”K3接口“，，

库房出入库，成品，，，K3有科目信息，，，借贷平衡



###### 权限！！要看：：：

功能管理：

​	添加、删除需要添加权限的功能

角色：

​	角色直接与功能权限相关

​	角色可以添加功能设置，当前角色可以操作哪些功能

​	可以指定部门为一个角色，

​	可以指定单个用户是某个角色

组织机构：

​	组织结构包含一定数量的用户，

用户：



**[字段权限的设置](https://www.cnblogs.com/wuhuacong/p/6427494.html)：**

**设置用户对数据库表具体字段的可视权限**

**数据库表操作日志记录！！**

**[记录用户操作日志的权限](https://www.cnblogs.com/wuhuacong/p/3496260.html)：**

**按钮功能权限设置**



**所有表添加字段**	Company_ID(所属公司ID)、Company(公司单位)

**所有表添加公司ID**

###### 





![1565348286455](C:\Users\shone\AppData\Roaming\Typora\typora-user-images\1565348286455.png)

![1565348310907](C:\Users\shone\AppData\Roaming\Typora\typora-user-images\1565348310907.png)





###### 原材料合同，名称单元格格式：

​	1、HOOK & EYE  4PCS/SET  	//带有组合说明，一套为4件

​	2、DYED TAFFETA INTERLINING(FUSED)	//有附加内容，在括号中

​	3、POLY BAG  SIZE:D4 		//含有物料色号属性

​	4、NYLON SATIN TAPE   NYLON 100% 		//含有物料成分属性

​	5、STRAIGHT TAPE  SIZE:28.5MM		//含有物料尺寸属性

​	6、WOOLEN FABRIC NYLON MIXED  205G/M		//带有克重属性？？

​	7、BIAS TAPE   SIZE:28MM  ABT.60M/ROLL		//多个属性、长度/卷属性

​			ABT60M/ROLL这种要写成	ABT.60M/ROLL 标准格式，，要带ABT

​	8、HAIR CLOTH INTERLINING.(DYED)W150/152CM  //W等多个属性，及点 .

​			W150/152CM这种必须要写成	W:150/152CM	否则会出错

**成分的多种格式：**

​	WOOL  50%						POLYESTER  50%		//同一行，不同格子

​	W90%&N10%			//使用&分隔符

​	HAIR40%,CO31%,VISCOSE21%,PO8%		//使用逗号，分隔符



**Aspose.Cells报错导致导入导出不可用！！！（重新导入一下）**