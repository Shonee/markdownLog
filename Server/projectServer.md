### 记一次服务器罢工导致的项目崩溃

服务器开发项目： ERP系统

使用语言：C# 

编译工具VS2010&SQL2012

版本控制工具：SVN

使用C#中的winform窗体进行开发，在代码生成器Database2Sharp18.0的基础上进行开发，使用C#中dataset来对数据库表进行操作。由于是多人协作，因此对于数据的同步以及版本的控制就显得比较重要。

数据同步：

①、将数据库表置于服务器上，所有人进行远程连接，开发时操作统一个数据库，便于数据实时同步；

②、dataset的同步，由于使用了dataset操作数据库表，要对相应的datasetAdapter添加相应的方法，同样在服务器创建一个dataset，运行后将.dll文件添加到项目的引用中来同步dataset的变化。

版本控制：

使用SVN，每人开发不同的模块，每次开发完毕后先将当前SVN中的最新版本下载，然后将自己的版本上传，其他人可以update至最新版本。



在一次莫名的断电后......服务器罢工了，重启后系统坏了，无限重启

...

...

在经过了漫长(一个星期)的修复操作后,终于将服务器复活(还以为挂了呢)，重新装了服务器系统。

系统是这种：ESXi--VMware-VMvisor-Installer-6.0.0-2494585.x86_64

![1559353468058](D:\markdownLog\Server\assets\1559353468058.png)

使用工具制作光盘映像到U盘来制作U盘启动

![1559353559169](D:\markdownLog\Server\assets\1559353559169.png)

使用方法：![1559354986275](D:\markdownLog\Server\assets\1559354986275.png)

安装时可能会报错：

![img](D:\markdownLog\Server\assets\IMG_20141212_130456.jpg)

Can‘t have a partition outside the disk --> “无法在磁盘外创建分区”

解决方法：

由于要装系统的硬盘使用过或者装过系统，因此此次装系统会有问题

①、使用ESXi-5.5U1进行安装，然后升级到6.0版本

②、将硬盘RAID重新排列，装入系统则不会报错(亲测)。在服务器种设置，进行时 ctrl+R 进行配置，将之前的阵列删除重新生成。

[U盘装系统教程1](https://www.cnblogs.com/fourseas/p/4616943.html)

[U盘装系统教程2](https://www.jb51.net/softs/582923.html)

[ESXI系统设置](https://www.jb51.net/softs/582923.html)

关于Svphere虚拟机安装虚拟机tool：

​	点击安装后，针对每一个虚拟机系统，要进入系统种使用虚拟光驱进行安装。













id:054914da-7e07-49da-8328-1b42d3bbef81

Memo(备注):

supplier(供应商):

create_name:管理员

MixRateEN(混率(英文)):

Unit(标准计量单位):

MatNO(物料编码):12312

unitPrice(采购单价):

MixRateJP(混率(日文)):

UnitName(记账单位):kg

update_date:2019/6/1 星期六 下午 21:25:19

PFNo(品番):

MatNOK3(K3中的物料编码):12132

ColorNO(色号):色号i15

KZ:0

CUnit:

MinProcure(最小采购数量):0

create_by:0

isdeleted:False

create_date:2019/6/1 星期六 下午 21:25:19

update_by:0

update_name:管理员

MatClassID(物料子类):8f6c2892-88f6-4661-af41-a9e924bebe5d

kemu(科目):

constituent(成分):

MatMemo(物料说明):

IsBatch(是否批次管理):False

supplierNo(供应商编码):

MatName(物料名称):涤棉物料123

MT:01

Method(计价方法):

SpeSub(规格型号):

MixRateCH(混率(中文)):

taxRate(税率):0

unitPricePrecision(单价精度):0







update_date:
	 2019/6/1 星期六 下午 21:25:19 -> 2019/6/1 星期六 下午 21:42:45

ColorNO(色号):
	 色号i15 -> 色号1111111

KZ:
	 0.00 -> 0