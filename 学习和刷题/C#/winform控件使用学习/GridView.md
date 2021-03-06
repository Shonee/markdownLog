[TOC]

(Data) Gird View(数据表格视图)Included Components(包含组件)：

​	1、GridControl：标准的表格形式

​	2、GridLookUpEdit：带有查找功能的数据表格

​	3、GridSplitContainer：区域可以进行拆分的GridControl

​	4、SearchLookUpEdit：带有内置查找面板，更迅速的进行查找

<details>
    <summary>点击查看代码</summary>
    <pre>
    <code>
    	//隐藏
    	print("Hello");
    	//隐藏
    </code>
    </pre>
</details>



###### 1、20191009：gridView中使用下拉列表，出现报错：对象必须实现IConvertible：(已解决)

```c#
//1、绑定转换格式的委托，
lookUpEdit.ParseEditValue += new DevExpress.XtraEditors.Controls.ConvertEditValueEventHandler(lookUpEdit_ParseEditValue);
//2、实现委托中的方法
void lookUpEdit_ParseEditValue(object sender, DevExpress.XtraEditors.Controls.ConvertEditValueEventArgs e)
{
    e.Value = e.Value.ToString(); 
    e.Handled = true;
}
//3、20191017追加，如果仍然报错，说明使用值和传入参数值类型不一致，转换成一致即可
```

###### 2、20191017：GridView页面显示行号

```c#
//设置显示列的宽度，以便数字能够全部显示
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

###### 3、20191018：GridView编辑后消失问题的解决

使用GridView开启编辑后，可以对cell进行编辑操作有时会出现编辑后，点击别处，编辑内容消失的问题。此时就要考虑GridView绑定数据源的方式：

1、如果使用实体List绑定，则保证要编辑的列对应实体对象的属性才行

2、如果是DataTable绑定，根据指定字符串创建列则不会出现这种问题

3、这种问题常出现在使用GridView设计模式，显示列没有对应的数据列支撑、在实体（Entity）中绑定一个虚拟列即可进行编辑操作

###### 4、20191109：设置列宽根据内容适应

```c#
//1、总宽度适应屏幕
this.gridView1.OptionsView.ColumnAutoWidth = false;
//2、根据所有内容适应宽度
this.gridView1.BestFitColumns();
//3、具体设置每一列的宽度
foreach (DevExpress.XtraGrid.Columns.GridColumn column in this.winGridViewPager1.gridView1.Columns)
	{
     	column.Width = 100;	//列宽设置固定值
        column.BestFit();	//列宽设置随内容适应
   	} 
```

###### 5、20191204：实现GridView显示数据的编辑，按钮，下拉列表等功能

[实现编辑](https://www.cnblogs.com/wuhuacong/p/6220826.html)

[实现按钮、下拉列表](https://www.cnblogs.com/wuhuacong/p/6240114.html)

```c#
//1、关闭只读，开启可编辑
this.winGridViewPager1.gridView1.OptionsBehavior.ReadOnly = false;   this.winGridViewPager1.gridView1.OptionsBehavior.Editable = true;
//2、如果只编辑部分列，则要开启全部，然后将其余列的编辑关闭 只有在关闭已读、开启编辑状态下，才能实现下拉列表等功能
this.winGridViewPager1.GridView1.Columns.ColumnByFieldName("DeliveryNum").OptionsColumn.AllowEdit = false;
//3、开启底部新增行
this.winGridViewPager1.gridView1.OptionsView.NewItemRowPosition = DevExpress.XtraGrid.Views.Grid.NewItemRowPosition.Bottom;
//4、编辑后关闭更新（没用过呢，一般不用关闭）
//this.gridView1.OptionsBehavior.Editable = false;
//this.gridView1.CloseEditor();
//this.gridView1.UpdateCurrentRow();
```

###### 6、实现gridView自定义显示内容功能（使用DataTable数据源）

```c#
//1、定义字符串，使用|来指定当前列数据类型
string columns = "id|int,MatInNO,InMemo,create_date,create_name";
//2、使用字符串自定义datable的包含列
DataTable dt = DataTableHelper.CreateTable(columns);
    foreach (MT_MatInInfo info in list) 
    {
        DataRow row = dt.NewRow();
        row["id"] = info.Id;
        row["MatInNO"] = info.MatInNO;
		...
        dt.Rows.Add(row);   
    }
//3、绑定数据源
this.winGridViewPager1.DataSource = dt.DefaultView;
```

###### 7.1、实现gridView选中多行数据功能（按住Ctrl点击）

设置属性：Multiselect = true; 即可

###### 7.2、实现gridView选中多行数据功能（显示勾选框）

```c#
//开启显示复选框
gridView.OptionSection.MultiSelect = true;

gridview.OptionsSelection.MultiSelectMode = DevExpress.XtraGrid.Views.Grid.GridMultiSelectMode.CheckBoxRowSelect;

gridview.OptionsSelection.ShowCheckBoxSelectorInColumnHeader = DevExpress.Utils.DefaultBoolean.True;
//修改样式
this.repositoryItemCheckEdit1.NullStyle = DevExpress.XtraEditors.Controls.StyleIndeterminate.Unchecked;  

//获取选中值
for (int i = 0; i < this.gridView1.RowCount; i++)
{
    if (this.gridView1.IsRowSelected(i))
    {
        
    }
}
```



###### 8、`gridView`显示页脚信息：

```c#
gridView1.OptionsView.GroupFooterShowMode = DevExpress.XtraGrid.Views.Grid.GroupFooterShowMode.VisibleAlways;
gridView1.OptionsView.ShowFooter = true;
```

###### 9、去除 GridView 头上的 "Drag a column header here to group by that column"

找到：OptionView -> 将 ShowGroupPanel ： 设置为 false ;

###### 10、gridView转义显示内容和实际内容：

目前三种方法：

（1）：实体Info添加虚拟字段，获取到数据集合、赋值数据源之前对当前集合中所有的ID，转换成实现显示内容赋值给增加的虚拟字段，用来显示，不再显示ID字段。

​	①遍历数据源集合

​	②针对每一个要转义的字段，使用linq遍历查询转义结果

（2）：使用linq配合CustomColumnDisplayText方法，显示gridView页面时，触发方法，针对ID列，使用linq在已有集合中查询转义结果，并对ID显示转义结果。
	①每一列都触发方法

​	②触发方法后，使用linq转义

（3）：使用Dictionary字典配合CustomColumnDisplayText方法，在获取数据源后，对数据源集合中每个要转义的字段，去字典中查询，如果没有转义结果，则查询对应转义结果，放入集合，已有则不查询，最后gridView显示时触发方法，使用字典进行转义。

​	①：遍历数据源集合，不会重复查询，每个ID只查询一次

​	②：触发方法后，使用字典转义（数量小，针对性强）

###### 11、GridView数据行实体与DataTable之间的转换

① 强类型实体转换成弱DataTable类

> 不能进行强制转换，而是使用DataTable的辅助类进行转换
>
> DataTable dt = DataTableHelper.ToDataTable(SizeDetailList);

② 弱DataTable（DataRow）转换成强实体Info（使用反射）

```c#
static void DataBind(object entity, DataRow row)
{
    //获取实体类类型
    Type type = entity.GetType();
    //获取实体类所有公共属性
    PropertyInfo[] infors = type.GetProperties();
    for (int i = 0; i < infors.Length; i++)
    {
        //如果DataRow列名包含此属性
        if (row.Table.Columns.Contains(infors[i].Name))
        {
            //获取值
            object value = Convert.ChangeType(row[infors[i].Name], infors[i].PropertyType);
            infors[i].SetValue(entity, value, null);
        }
    }
}

    
public static T D2E<T>(DataRow r)
{ 
    T t = default(T);
    t = Activator.CreateInstance<T>();//获取类型
    PropertyInfo[] ps = t.GetType().GetProperties();//获取类所有属性
    foreach(var item in ps)	//遍历所有属性，有则赋值
    {
        if (r.Table.Columns.Contains(item.Name)) 
        { 
            object v = r[item.Name];
            if (v.GetType() == typeof(System.DBNull))
                v = null;
            item.SetValue(t,v,null);
        }
    }
    return t;
}

```

###### 12、gridView中点击列标题时获取当前列的fieldName属性值

> 使用gridView的鼠标响应事件 + 点击位置获取 + 获取gridView列标题 + 获取鼠标状态 

```c#
this.winGridViewPager1.gridView1.MouseDown += new MouseEventHandler(gridView1_MouseDown);

void gridView1_MouseDown(object sender, MouseEventArgs e)
{
    if (e.Button == System.Windows.Forms.MouseButtons.Left) 
    {
        //获取鼠标点击位置
        DevExpress.XtraGrid.Views.Grid.ViewInfo.GridHitInfo gridHitInfo = this.winGridViewPager1.gridView1.CalcHitInfo(e.X, e.Y);

        ////获取该列右边线的x坐标
        //DevExpress.XtraGrid.Views.Grid.ViewInfo.GridViewInfo gridViewInfo = (DevExpress.XtraGrid.Views.Grid.ViewInfo.GridViewInfo)this.winGridViewPager1.gridView1.GetViewInfo();
        //int x = gridViewInfo.GetColumnLeftCoord(gridHitInfo.Column) + gridHitInfo.Column.Width;
        ////右边线向左移动3个像素位置不弹出对话框（实验证明3个像素是正好的）
        //if (e.X < x - 3)
        //{
        //    DevExpress.XtraEditors.XtraMessageBox.Show("点击Name列标题！");
        //}

        //this.winGridViewPager1.Cursor == Cursors.Default  鼠标在边界线上点击可以更改宽度，此时鼠标形状不是默认状态，要排除
        if (Cursor.Current == Cursors.Default && gridHitInfo.InColumnPanel) // && info.Column.FieldName.Equals("MatName")
        {
            DevExpress.XtraEditors.XtraMessageBox.Show("点击" + gridHitInfo.Column.FieldName + "列标题！");
        }
    }
}
```

