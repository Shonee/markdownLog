###### 20190716：到上海



###### 数据字典中键值不同时的切换

```c#
//根据数据字典名和值，得到键
BLLFactory<WHC.Dictionary.BLL.DictData>.Instance.GetDictName("盘点模式", info.InvMode.ToString());
//根据键在数据字典中找值
Dictionary<string, string> dict = BLLFactory<WHC.Dictionary.BLL.DictData>.Instance.GetDictByDictType("盘点模式");
info.InvMode = Convert.ToInt32(dict[txtInvMode.Text]);
```

###### 主表列表选择出发子表数据绑定事件

```c#
gridView1_FocusedRowChanged(object sender, DevExpress.XtraGrid.Views.Base.FocusedRowChangedEventArgs e)
```

###### 20190718：

`sql`语句中，多个条件OR连接和分别查询哪个快？

###### 错误：将截断字符串或二进制数据。语句已终止

（已解决）插入的内容超过该类型限定长度或者插入类型错误

###### 20190722：

入库要增加装箱单入库分类，即合同来料入库，没有采购合同，

此时将来料装箱单直接导入到送货单表中，

sendBill表的BuyID外键，可以为null

添加ConID，使其在没有采购合同时可以存放来料对应合同，可以为空

sendItem表的BuyID和BuyItem外键，来存放采购合同和合同订单id，可以为空

添加ConID，ConItem



###### 20190723：

`Guid`类型可为空的实现，

数据库中类型可以为空null，但是C#中`Guid`类型不可为空，当数据库为空，调出数据时会自动填充32位000...

**办法：**

实体定义`Guid`类型变量时，使用`Guid?`来代替`Guid`

DAL实体中从数据库获取类型数据时，使用`GetGuidNullable()`来代替`GetGuid()`

这样变量读取时皆可以为空了

从数据库中取出null值时，在c#中判断类型是需要使用`System.DBNull.Value`来判断是否为空值



###### 20190724：

重新设计裁剪领料业务

###### 20190725：

###### List集合去重方法

```C#
//1、Distinct()去重，只能用于值类型去重，引用类型时，值相同地址不同，不会去重
list_distinct = list_distinct.Distinct().ToList();
//2、使用Linq语句，类似数据库搜索，按照相同值分组，每组取第一个
list_distinct = list_Persons.GroupBy(c => c.name).Select(c => c.First());
```

正则表达式匹配逗号间隔字符串

1、开头和结尾不能是逗号

2、可以只有一个值没有逗号

3、值是数字类型的值

```c#
//指定开头类型(\d+,)，*代表可以重复0次或多次，\d+$代表以此结尾	
	^(\d+,)*\d+$
//使用正则表达式进行字符串判断,返回bool类型
CRegex.IsMatch(str, "^(\\d+,)*\\d+$");
```

###### 使用`Linq`对数据array，集合list中的数值进行求和运算

```c#
//对字符串数组中的可转数值数据求和,引用Linq
string[] batches = {"100","200","200"};
int sum = batches.ToList().Sum(p => p.ToInt32());
//即将其中每个元素转化成32位整型，进行求和

```

###### 使用`Linq`在集合list等中搜索指定元素，及对属性重新赋值

```c#
List.FirstOrDefault(p => p.MatID == "value");
//判根据集合中对象的属性值，判断是否存在对象，不存在返回null，不报异常
info = List.FirstOrDefault(p => p.MatID == "value");
info.key = value;
//根据linq搜获获得的info对象，当对info的属性值改变时，list集合中对应值也会改变
```



###### [1、爬取豆瓣图书信息](E:\CODES\WorkSpace\PyCharm\.idea\book.txt)



###### 20190727：

###### 设置form窗体最大化

`this.WindowState = FormWindowState.Maximized;`

###### 按钮的自点击设置：

`buttonName.PerformClick();`