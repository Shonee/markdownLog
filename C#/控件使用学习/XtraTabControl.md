[TOC]

###### 1.点击关闭按钮关闭

若要tabpage显示 关闭按钮：

把xtraTabControl的ClosePageButtonShowMode属性设为InAllTabPageHeaders；

若想要首页不显示关闭按钮：

```c#
//首页不显示关闭按钮
xtraTab_index.ShowCloseButton = DevExpress.Utils.DefaultBoolean.False;
```

 添加xtraTabControl的CloseButtonClick事件： 

```c#
//关闭选项卡方法
private void xtraTabControl_CloseButtonClick(object sender, EventArgs e)
{        DevExpress.XtraTab.ViewInfo.ClosePageButtonEventArgs EArg = (DevExpress.XtraTab.ViewInfo.ClosePageButtonEventArgs)e;
    string name = EArg.Page.Text;//得到关闭的选项卡的text
 	//遍历得到和关闭的选项卡一样的Text   
	foreach (XtraTabPage page in xtraTabControl.TabPages)
    {
         if (page.Text == name)
         {
         	xtraTabControl.TabPages.Remove(page);
            page.Dispose();
            return;
         }
    }
}
```

2.双击标签关闭

```c#
//得到你现在鼠标所在的Page
XtraTabPage CurrentPage = new XtraTabPage();
private void xtraTabControl_HotTrackedPageChanged(object sender, DevExpress.XtraTab.TabPageChangedEventArgs e)
        {
            try
            {
                CurrentPage = e.Page;
            }
            catch (System.Exception ex)
            {
                CurrentPage = null;
            }
        }
//双击事件
private void xtraTabControl_MouseDoubleClick(object sender, MouseEventArgs e)
        {
            if (CurrentPage != null)
            {
                xtraTabControl.TabPages.Remove(CurrentPage);
                CurrentPage.Dispose();
            }
        }
```

###### 2.隐藏XtraTabControl的Page

```c#
//将标签隐藏，只显示当前选择页面，不可切换
XtraTabControl.SelectedTabPage = xtraTabPage1;
XtraTabControl.ShowTabHeader = false;
//隐藏指定页面
xtraTabPage2.PageVisible = false;
xtraTabPage5.PageVisible = true;
```

