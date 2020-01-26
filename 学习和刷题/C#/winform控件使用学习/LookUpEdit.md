

###### 绑定数据源：

```c#
//相当于editvalue  
lookupedit.Properties.ValueMember = "实际要用的字段";   
//相当于text  
lookupedit.Properties.DisplayMember = "要显示的字段";    
lookupedit.Properties.DataSource = "数据源"; 
```

###### 常用属性：

```c#
lookupedit.PopupWidth = 100; //下拉框总宽度  
lookupedit.NullText = "";//空时的值  
lookupedit.DropDownRows = 10;//下拉框行数  

//自适应宽度（两个都要有）
mat.Properties.BestFit();
mat.Properties.BestFitMode = DevExpress.XtraEditors.Controls.BestFitMode.BestFitResizePopup; 

//要使用户可以输入，这里须设为Standard  
lookupedit.TextEditStyle = TextEditStyles.Standard;
//可用Ctrl + Delete清空选择內容
lookupedit.AllowNullInput = DevExpress.Utils.DefaultBoolean.True; 

//列格式设置  
lookUpEdit1.Properties.Columns[0].FormatString = "000000";
//选择第一项  
lookUpEdit1.ItemIndex = 0;                
```

###### 获取选择值：

```c#
//设置未选择时显示内容
lookupedit.properties.nulltext=“请您选择。。”; 
//清空未选择时显示内容
lookupedit.properties.nulltext=null;
//是lookUpEdit.Properties.ValueMember的值 
string id = this.lookUpEdit1.EditValue.ToString(); 
//是lookUpEdit.Properties.DisplayMember的值
string name = this.lookUpEdit1.Text.Trim();   

//判断未选择数据
if(this.lookupedit.editvalue==null ||this.lookupedit.editvalue.tostring()=="nulltext")  
{  
	//提示信息,说明未选择下拉框  
}  
```

###### 动态添加列：

```c#
this.lookUpEdit1.Properties.Columns.AddRange(new DevExpress.XtraEditors.Controls.LookUpColumnInfo[] {  
           new DevExpress.XtraEditors.Controls.LookUpColumnInfo("FieldName1", "Caption1"),  
           new DevExpress.XtraEditors.Controls.LookUpColumnInfo("FieldName2", "Caption2")});  
```

###### 允许输入自定义值：

```c#
lookUpEdit1.Properties.TextEditStyle = DevExpress.XtraEditors.Controls.TextEditStyles.Standard;
```

