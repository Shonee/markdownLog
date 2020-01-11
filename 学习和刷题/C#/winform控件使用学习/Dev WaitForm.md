[TOC]



###### DevExpress WaitForm使用（做类似进度条）

一、新建一个Dev WaitForm窗体

二、在需要使用的页面拖入splashScreenManager控件，并在属性中加入WaitForm窗体

三、//显示等待控件

```c#
splashScreenManager.ShowWaitForm();
```

四、更新控件描述信息

```c#
// 添加标题
splashScreenManager1.SetWaitFormCaption("请稍后,正在加载中....");　
// 添加描述信息
splashScreenManager1.SetWaitFormDescription("正在初始化.....");　　　　　
```

五、关闭控件显示

```c#
splashScreenManager1.CloseWaitForm();
```

六、注意：此种方法可以不使用线程，但是为了使用更流畅 建议开启线程