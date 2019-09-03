###### 20190716：上海

`checkComboxEdit` 下拉列表选择框

框架中`gridView`的数据显示转义方法



###### 20190717：

```c#
//根据物料/库位来新增盘点详情
        private DataTable matInventory() 
        {
            string columns = "id,InfoID,PID,DeportMatID,MatNum,InvNum,DiffNum,UnitName,TreadForID,IsChecked,DetailMemo";
            DataTable dt = DataTableHelper.CreateTable(columns);
            List<object> listValues = this.txtMatOrPosition.Properties.Items.GetCheckedValues();
            for (int i = 0; i < listValues.Count; i++) 
            {
                DataRow row = dt.NewRow();
                Guid matID = BLLFactory<MT_Materiels>.Instance.FindSingle(string.Format("MatName = '{0}'",listValues[i])).Id;
                SR_DepotMatsInfo depotInfo = BLLFactory<SR_DepotMats>.Instance.FindSingle(string.Format("MatID = '{0}'",matID));
                SR_PostionMatsInfo positionMatsInfo = BLLFactory<SR_PostionMats>.Instance.FindSingle(string.Format("MatID = '{0}'", matID));
                string positionName = BLLFactory<SR_StorePositions>.Instance.FindByID(positionMatsInfo.PID).PosName;
                row["PID"] = positionName;
                row["DeportMatID"] = listValues[i];
                row["MatNum"] = depotInfo.MatNumAll;
                row["InvNum"] = depotInfo.MatNumAll;    //默认相等
                row["DiffNum"] = Convert.ToDecimal(row["MatNum"]) - Convert.ToDecimal(row["InvNum"]);
                row["UnitName"] = depotInfo.UnitName;
                row["IsChecked"] = false;
                dt.Rows.Add(row);
            }
                return dt;
```

###### `gridView`显示内容的转义：

```c#
this.winGridView2.gridView1.CustomColumnDisplayText +=new DevExpress.XtraGrid.Views.Base.CustomColumnDisplayTextEventHandler(gridView2_CustomColumnDisplayText);//定义事件委托

 void gridView2_CustomColumnDisplayText(object sender, DevExpress.XtraGrid.Views.Base.CustomColumnDisplayTextEventArgs e)
        {
            string fieldName = e.Column.FieldName;
            if (e.Column.ColumnType == typeof(Guid)) 
            {
                if (fieldName == "DeportMatID" )
                {
                    //if (e.Value != null)
                    //{
                    //    e.DisplayText = e.Value.ToString().ToDecimal().ToString("C2");
                    //}
                }
            }
            
        }
```



###### `gridView`页脚信息：

```c#
gridView1.OptionsView.GroupFooterShowMode = DevExpress.XtraGrid.Views.Grid.GroupFooterShowMode.VisibleAlways;
gridView1.OptionsView.ShowFooter = true;
```



###### 框架自带添加操作人信息

```c#
//第二个参数代表新增或者编辑，true为新增，不填默认为false为编辑
ExtensionMethod.SetSpecialField(info, true);    //添加操作人信息

```

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

###### 开启关闭`gridControl`的编辑功能：

```c#
this.winGridViewPager1.gridView1.OptionsBehavior.ReadOnly = false;	//关闭只读
            this.winGridViewPager1.gridView1.OptionsBehavior.Editable = true;	//开启编辑
            this.winGridViewPager1.gridView1.OptionsView.NewItemRowPosition = DevExpress.XtraGrid.Views.Grid.NewItemRowPosition.Bottom;
      	//开启新增行      
//this.gridView1.OptionsBehavior.Editable = false;
            //this.gridView1.CloseEditor();
            //this.gridView1.UpdateCurrentRow();
```

###### 20190718：

`gridView`根据内容适应宽度

```c#
this.winGridView2.gridView1.DataSourceChanged += new EventHandler(gridView2_DataSourceChanged);//事件委托
//总宽度适应屏幕
//this.gridView1.OptionsView.ColumnAutoWidth = false;
//根据单个内容适应宽度
//this.gridView1.BestFitColumns();

this.winGridView2.gridView1.CustomColumnDisplayText +=new DevExpress.XtraGrid.Views.Base.CustomColumnDisplayTextEventHandler(gridView2_CustomColumnDisplayText);//显示内容转义，事件委托
```

#### 使用字典Dictionary存储数据<Guid,string>

```c#
//定义一个字典类型
private Dictionary<Guid, string> dict = new Dictionary<Guid, string>();
//字典中添加数据元素（key,value）
dict.Add(conList[i].Id, conList[i].ConNO);

//根据键获取值
//1、直接通过索引，不过可能字典中不存在当前key，会报错，要先判断（复杂）
//判断+检索两次索引，key不对时会抛异常
if(dict.ContainsKey(key))
{
 	string value = dict[key];   
}
//2、通过TryGetValue的方法
//检索一次，速度更快，key不对时方法返回false
int resValue ;
myDictionary.TryGetValue(key, out resValue);
//根据值获得键
//1、遍历判断，得到对应值的键
//dict元素遍历,每次得到一个键值对
foreach (KeyValuePair<Guid, string> kvp in dict){}
//dict-key遍历，每次得到一个键
foreach (Guid key in dict.Keys){}
//2、使用Linq语句查询  添加命名空间using System.Linq
//get all keys,返回符合条件的所有key
var keys = dic.Where(q => q.Value == "2").Select(q => q.Key); 
//get all keys，返回所有key的list集合
List<string> keyList = 
    (from q in dic where q.Value == "2" select q.Key)
    .ToList<string>(); 
//get first key，返回符合条件的第一个key
var firstKey = dic.FirstOrDefault(q => q.Value == "2").Key;  
```



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



```c#
//创建事务，在之后的数据操作中使用事务即可
DbTransaction trans = BLLFactory<DictData>.Instance.CreateTransaction();

```

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