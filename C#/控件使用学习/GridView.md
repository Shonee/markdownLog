[TOC]

(Data) Gird View(数据表格视图)Included Components(包含组件)：

​	1、GridControl：标准的表格形式

​	2、GridLookUpEdit：带有查找功能的数据表格

​	3、GridSplitContainer：区域可以进行拆分的GridControl

​	4、SearchLookUpEdit：带有内置查找面板，更迅速的进行查找

###### 20191009：

###### gridView中使用下拉列表，出现报错：对象必须实现IConvertible：(解决)

<details>
    <summary>点击查看代码</summary>
    <pre>
    <code>
    	print("Hello");
    </code>
    </pre>
</details>

```c#
//gridView下拉框报错对象必须实现IConvertible
//绑定转换格式的委托，
lookUpEdit.ParseEditValue += new DevExpress.XtraEditors.Controls.ConvertEditValueEventHandler(lookUpEdit_ParseEditValue);
//委托方法
void lookUpEdit_ParseEditValue(object sender, DevExpress.XtraEditors.Controls.ConvertEditValueEventArgs e)
{
    //throw new NotImplementedException();
    e.Value = e.Value.ToString(); 
    e.Handled = true;
}
// 20191017追加，如果仍然报错，就是使用值和传入参数值类型不一致，
// 转换成一致即可
```

###### 20191017：	GridView页面显示行号

```c#
//设置显示列的宽度
GridView.IndicatorWidth = 30;
this.gridView1.CustomDrawRowIndicator += (s, e) =>
{
    if (e.Info.IsRowIndicator && e.RowHandle >= 0)
    {
        e.Info.DisplayText = (e.RowHandle + 1).ToString();
    }
};
```

###### [GridView使用教程](https://blog.csdn.net/qq_23944441/article/details/82415812)

###### [GridView属性集合](https://blog.csdn.net/qq_36248777/article/details/99678493)

###### [GridView合并单元格](https://blog.csdn.net/a609141483/article/details/79952768)

###### 20191018：GridView编辑后消失问题的解决

使用GridView开启编辑后，可以对cell进行编辑操作有时会出现编辑后，点击别处，编辑内容消失的问题。此时就要考虑GridView绑定数据源的方式：

1、如果使用实体List绑定，则保证要编辑的列对应实体对象的属性才行

2、如果是DataTable绑定，根据指定字符串创建列则不会出现这种问题

3、这种问题常出现在使用GridView设计模式，显示列没有对应的数据列支撑

4、绑定一个虚拟列即可进行编辑操作

###### 20191109：设置列宽根据内容适应

```c#
foreach (DevExpress.XtraGrid.Columns.GridColumn column in this.winGridViewPager1.gridView1.Columns)
	{
     	column.Width = 100;	//列宽设置固定值
        column.BestFit();	//列宽设置随内容适应
   	} 
```

