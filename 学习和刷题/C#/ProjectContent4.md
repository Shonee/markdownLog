[TOC]

###### 20190814:

###### 框架中一个项目使用多个数据库配置：

​	**[教程](https://www.cnblogs.com/wuhuacong/p/3783294.html)**

###### 20190815：

###### 权限功能全部可以实现：

1. **部门管理：**

   ​	管理用户所在部门分类

2. **角色管理：**

   ​	管理所有用户的对应角色分类，

3. **用户管理：**

   ​	添加用户

4. **功能管理：**

   ​	添加某一块功能，在权限功能管理里中添加，并在角色管理中为角色添加可操作功能，然后再页面中根据当前用户添加操作权限

5. **菜单、按键管理：**

   ​	等同与功能管理，将每一个按钮看作时一个小的功能，在权限管理功能模块中为其添加功能控件ID，根据ID判断当前登录用户是否可以操作该菜单、按钮

   ```c#
   //根据权限管理是否创建委托事件
   if (Portal.gc.HasFunction("MT_Materiels/Edit")) 
               {
                   this.winGridViewPager1.OnEditSelected += new EventHandler(winGridViewPager1_OnEditSelected);
               }
   //初始化时，对按钮的有效性，根据权限来进行管理
   this.barButtonAdd.Enabled = Portal.gc.HasFunction("MT_Materiels/Add");
   ```

6. **登录日志：**

   ​	有，比较全，暂时不用要增加

7. **操作日志(重要)：**

   ​	**[一行代码实现操作日志](https://www.cnblogs.com/wuhuacong/p/3496260.html)**

   ​	权限管理中，操作日志，新增记录表信息，设置该表操作时需要记录

   ​	在`BLL`文件中添加语句：

   ```c#
   baseDal.OnOperationLog += new OperationLogEventHandler(WHC.Security.BLL.OperationLog.OnOperationLog);
   ```

   ​	此时记录的日志无法获取当前登录人信息，因此需要弥补一下

   ​	在增加、修改、删除时，操作info之前，对info的`CurrentLoginUserId`属性赋值

   ```c#
   info.CurrentLoginUserId = Portal.gc.LoginInfo.ID.ToString(); 
   ```

   ​	这样在使用实体操作数据库时，记录操作日志便有了登录人信息。

###### 文件(图片)常用操作：

​	**判断文件夹、文件是否存在**

```c#
//判断文件夹是否存在，不存在则创建
if (!DirectoryUtil.IsExistDirectory(Path))
{ DirectoryUtil.CreateDirectory(Path);}
//判断文件是否存在，存在则删除
if (FileUtil.IsExistFile(Path))
{ FileUtil.DeleteFile(Path);}
```

​	**图片字节流操作**

```c#
//将二进制文件转化成流， byte[1]
System.IO.MemoryStream ms = new System.IO.MemoryStream(image);
//项目根目录下，创建文件绝对路径
string Path = Application.StartupPath + ID.ToString() + ".jpeg";
//在绝对路径下，将流转成图片文件，要有路径才可以，且流是图片二进制文件才行
//路径不存在则报错GUI+错误
//如果转成二进制的不是图片文件，则转换出来报错：参数无效
new Bitmap(ms).Save(Path);
```

​	**自己写数据库连接**

```c#
//数据库连接字符串，为连接数据库的依据，连接方式、库名、账号、密码等
string connectionString = new AppConfig().GetConnectionString("sqlserver");
//建立连接
SqlConnection connection = new SqlConnection(connectionString)
//判断连接是否开启，没有则开启
if(connection.State != ConnectionState.Open){ connection.Open(); }
string sql = "SELECT * FROM ..";
//根据连接和sql进行数据库的操作
SqlCommand cmd = new SqlCommand(sql,connection);
cmd.CommandType = CommandType.Text;	//命令类型
//获取数据返回，使用数据集适配器
System.Data.SqlClient.SqlDataAdapter adapter = new System.Data.SqlClient.SqlDataAdapter();
adapter.SelectCommand = cmd;
DataSet ds = new DataSet(); //数据集
adapter.Fill(ds);
connection.Close();			//关闭连接
DataTable dt = ds.Tables[0];//获取表
DataRow row = dt.Rows[0];	//获取行
```

​	**使用流将数据库中的二进制文件取出来**

```c#
//使用字节流获取二进制数据，cmd接上一步数据库连接
System.Data.SqlClient.SqlDataReader dataRader = cmd.ExecuteReader();
byte[] image = null;
while(dataRader.Read())
{
    image = (byte[])dataRader.GetValue(0);
}
```

###### 

数据库查询条件语句：

```sqlserver
update tb set B=(case when len(A)>0 then C  end) ,D=(case when len(A)<=0 then E end)
//测试
select '操作人' = CASE when update_name is NULL then 111 else update_by end from MT_Materiels
```



 