[TOC]

### DevExpress SplitContainerControl的使用

###### 1、默认横向分割修改成纵向分割

​	属性 Horizontal = false; 

​	即可将横向分割修改成纵向分割

###### 2、将伸缩标志修改成箭头，并实现点击折叠和弹出

```c#
splitContainerControl.Collapsed = true;	//默认是折叠的
splitContainerControl.CollapsePanel = Panel2;//折叠Panel2
```

###### 3、固定某个PANEL的大小

​	设置SplitContainerControl的属性 FixedPanel为 Panel2即可设置Panel2按比例变化

​	如果固定在设定值不变，则需要增加设置Panel2的属性 MinSize为具体值即可 

###### 4、`splitContainer`默认折叠panel

```c#
splitContainer1.Panel2Collapsed = true;//折叠panel2

```
