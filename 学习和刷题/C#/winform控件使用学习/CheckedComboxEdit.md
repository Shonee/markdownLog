[TOC]

###### 1、20190927 `ChexkedComboxEdit`组件属性绑定

```c#
//绑定数据源，并设置 显示-存储 值
CheckedCombox.Properties.DataSource = dt;
CheckedCombox.Properties.DisplayMember = "NAME";
CheckedCombox.Properties.ValueMember = "ID";
//设置多选时，值根据什么区分，同时显示内容时根据设定字符自动分割
cmb_check_CKID.Properties.SeparatorChar = ',';
//反绑定！！
//查询界面默认选中全部，多选内容直接赋值即可，提前设置好分割符
this.chkCustomerTypeQuery.EditValue = "全部";
//赋值后，一定要调用下面方法，才能正确显示内容
this.chkCustomerTypeQuery.RefreshEditValue();
```

