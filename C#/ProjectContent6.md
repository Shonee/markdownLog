[TOC]

###### 20191009：

###### gridView中使用下拉列表，出现报错：对象必须实现IConvertible：(解决)

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
```



###### 20191011 使用异步函数(.NET4.5新增)(没做呢)：



###### 20191015 使用backgroundworker 线程实现进度条：


