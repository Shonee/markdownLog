[TOC]



###### 1、新建功能窗体，已存在则不创建，而是聚焦

```c#
//①、每一个窗体对应一个对象 如果窗体过多，会影响使用效果
/// <summary>
/// 点击导航标签，新建窗体，如果已存在，则聚焦到窗体
/// </summary>
RibbonForm1 form1;
private void navBarItem1_LinkClicked(object sender, DevExpress.XtraNavBar.NavBarLinkEventArgs e)
{
    //窗体不存在则新建窗体
    if (form1 == null || form1.IsDisposed)
    {
        form1 = new RibbonForm1();
        form1.Show();
    }
    else 
    {
        form1.Activate();   //激活窗体获取焦点    
    }
}

//②、根据当前应用打开的窗体进行判断，是否有相同类型的窗体。有则聚焦，没有则创建
foreach (Form frm in Application.OpenForms)
 {
    if (frm is youForm)
    {
       youForm.Activate();
       youForm.WindowState = FormWindowState.Normal;
       return;
     }
 }
 Form youForm = new Form();
 youForm.Show();
```

###### 2、将一个窗体作为主窗体，在该窗体中新建窗体作为子窗体（标签式）

```c#
this.MdiParent  =  true;   //设置当前窗体为父窗体
subForm sform = new subForm();  //新建窗体
sform.MdiParent = this;         //设置新窗体作为当前窗体的子窗体
sform.Parent = panel;         //设置子窗体的容器为父窗体中的panel，没有panel时不用写该行
sform.show();         //显示窗体

//当前窗体的容器中显示另一个窗体
sysholiday = new FrmPU_ProMat();
sysholiday.TopLevel = false;
sysholiday.Dock = DockStyle.Fill;
sysholiday.FormBorderStyle = FormBorderStyle.None; splitContainer1.Panel2.Controls.Add(sysholiday);
sysholiday.Visible = true;
```

###### 3、点击关闭按钮，提示是否关闭，确定后退出系统功能实现

```c#
// mainform2_FormClosing事件是点击关闭按钮后、正式关闭窗口前触发
private void mainform2_FormClosing(object sender, FormClosingEventArgs e)
{
    //显示提示框，取消则不关闭
    if (MessageBox.Show("你确定要退出系统吗？", "退出提示", MessageBoxButtons.OKCancel, MessageBoxIcon.Question) == DialogResult.Cancel)
    {
        e.Cancel = true;
    }
    else 
    {
        //确定后关闭系统环境
        System.Environment.Exit(0);
    }
}
```

###### 4、获取当前显示屏幕的大小

```c#
//当前的屏幕除任务栏外的工作域大小
this.Width = System.Windows.Forms.Screen.PrimaryScreen.WorkingArea.Width;
this.Height = System.Windows.Forms.Screen.PrimaryScreen.WorkingArea.Height;
//当前的屏幕包括任务栏的工作域大小
this.Width=System.Windows.Forms.Screen.PrimaryScreen.Bounds.Width;
this.Height=System.Windows.Forms.Screen.PrimaryScreen.Bounds.Height;
```

###### 5、form窗体最小化效果

```c#
//点击最小化按钮后，事件触发
if(this.WindowState == FormWindowState.Minimized)  //判断是否最小化
{
    this.ShowInTaskbar = false;  //不显示在系统任务栏
     notifyIcon.Visible = true;  //托盘图标可见
}
//双击托盘按钮后，DoubleClick事件
if(this.WindowState == FormWindowState.Minimized)
{
    this.ShowInTaskbar = true;  //显示在系统任务栏
    this.WindowState = FormWindowState.Normal;  //还原窗体
     notifyIcon.Visible = false;  //托盘图标隐藏
}
```

###### 6、在一个容器中添加另外一个form

```C#
/// <summary>
/// 加载form页面到splitPanel中
/// </summary>
private void addFromInPanel(SplitterPanel panel, System.Windows.Forms.Form form)
{
    if (panel.Controls.Count != 0)
    {
        panel.Controls.Clear();
    }
    form.TopLevel = false;
    form.Dock = DockStyle.Fill;
    form.FormBorderStyle = FormBorderStyle.None;
    panel.Controls.Add(form);
    form.Visible = true;
}
```

