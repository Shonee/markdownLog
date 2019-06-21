### 项目中用到的内容大纲：

1、`treeView：`

​	基本操作、动态加载节点、绑定点击事件

2、`GridView：`

​	`winGridViewPage.GridView`

​	属性、事件、代码添加事件

3、`DataSetAdapter：`

​	适配器插入(更新表或者行对象)数据

4、

```c#
	//guid的生成方法
    //Guid id =  Guid.NewGuid();
    //MessageBox.Show(id.ToString());
```



5、`treeView`中节点添加图标后，点击闪烁问题		

6、属性Anchor，定义当前控件上下左右绑定到容器的边缘

7、使用`pictureBox`显示图片，怎么实现图片的上传和保存？？

8、`treeView`控件添加右键菜单

​		①窗体添加`ContextMenuStrip`组件，并编辑节点

​		②`treeView`属性``ContextMenuStrip`设置为`ContextMenuStrip`

​		③链接成功后，`treeView`中右键即出现菜单

###### 9、treeView组件属性labelEdit，节点是否可以编辑

###### 10、``splitContainer`折叠panel的功能

```c#
splitContainer1.Panel2Collapsed = true;//折叠panel2
```

###### 11、本地上传图片的操作

```C#
		 /// 选择本地图片文件
        private void btnBrowse_Click(object sender, EventArgs e)
        {
            //原先写好的方法，直接调用
            string file = FileDialogHelper.OpenImage();
            if (!string.IsNullOrEmpty(file))
            {	//显示文件全路径
                this.txtFilePath.Text = file; 
                ViewData();
            }
        }
        /// 在pictureBox中展示已选择图片
        private void ViewData() 
        {
            if (this.txtFilePath.Text == "")
            {
           	 MessageDxUtil.ShowTips("请选择指定的图片文件");
                return;
            }
            try
            {
	this.pictureBox1.Load(this.txtFilePath.Text);
    //调整图片在pictureBox中的显示模式，适应情况
   	this.pictureBox1.SizeMode = PictureBoxSizeMode.Zoom;
            }
            catch (Exception ex)
            {
                LogTextHelper.Error(ex);
                MessageDxUtil.ShowError(ex.Message);
            }
        }
		///以二进制格式保存图片到数据库表中
		private void SavePicture()
        {
         MemoryStream ms = new MemoryStream();
         pictureBox1.Image.Save(ms, System.Drawing.Imaging.ImageFormat.Jpeg);
         byte[] bt = new byte[1];
         //转为字节
         bt = ms.GetBuffer();
         DataRow dr = dt.NewRow();
         //对应字段
         dr["photo"] = bt;
         //执行插入
         dt.Rows.Add(dr);
         adt.Update(dt);
         MessageBox.Show("添加成功", "!提示");
        }
```

###### 12、从数据库表中读取图片文件并显示

```C#
////pictureBox.Image获取图片的三种方式
//1.绝对路径: 
this.pictureBox.Image=Image.FromFile("C:\\test.jpg"); 
//2.相对路径: 
//Application.StartupPath;可以得到程序根目录  
this.pictureBox.Image=Image.FromFile(Application.StartupPath "\\test.jpg");  
//3.获得网络图片的路径 
string url = "http://img.zcool.cn/community/01635d571ed29832f875a3994c7836.png@900w_1l_2o_100sh.jpg";
this.pictureBox.Image = Image.FromStream(System.Net.WebRequest.Create(url).GetResponse().GetResponseStream());

 /// 编辑时根据数据库二进制文件展示图片,获取路径显示图片
 /// 如果没有路径则从数据库中读取到项目路径，判断当前路径是否有文件
        private void ShowImage(MT_MaterielsInfo info) 
        {
           
                //直接读取数据流到ms中
                System.IO.MemoryStream ms = new System.IO.MemoryStream(materielsRow.image);
            	//展示到picture中，读取图片会很慢，添加一个路径列
                //pictureBox1.Image = new Bitmap(ms);
                //pictureBox1.SizeMode = PictureBoxSizeMode.Zoom;
                info.ImagePath = Application.StartupPath + "\\images\\" + info.Id.ToString() + ".jpeg";
                bool succeed = BLLFactory<MT_Materiels>.Instance.Update(info, info.Id);
            	//判读目录是否存在，不存在则创建一个
                if (!DirectoryUtil.IsExistDirectory(Application.StartupPath + "\\images\\")) 
                {
                DirectoryUtil.CreateDirectory(Application.StartupPath + "\\images\\");
                }
                //图片保存到指定路径
                new Bitmap(ms).Save(info.ImagePath);
				//展示图片
                pictureBox1.ImageLocation = info.ImagePath;
                pictureBox1.SizeMode = PictureBoxSizeMode.Zoom;
        }
```

###### 13、tab标签种添加form窗体

```C#
		/// 加载form页面到当前tab-panel页中
        private void Add(System.Windows.Forms.Form form) 
        {
            //去掉form窗体的最高级属性，否则不能作为控件添加
            form.TopLevel = false;
            form.Dock = DockStyle.Fill;
            form.FormBorderStyle = FormBorderStyle.None;
            //添加到具体的page中
            this.tabPage1.Controls.Add(form);
            //可视性设置，必须要有，默认不显示
            form.Visible = true;
        }
```

###### 14、`Devexpress`中的`comboxEdit`设置不可输入只能选择,绑定数据

```c#
//设置txtProvCountry不可输入 
this.txtProvCountry.Properties.TextEditStyle = DevExpress.XtraEditors.Controls.TextEditStyles.DisableTextEditor;
//InitDictItem()中设置下拉框对应的数据字典名称
this.txtProvCountry.BindDictItems("国别");

 /// 对指定的comboxEdit控件绑定指定数据内容
 /// <param name="comboxEdit">下拉列表框</param>
 /// <param name="dataTable">数据表</param>
 /// <param name="str">数据表中的指定属性字段</param>
//获取数据源并绑定
DataTable dt = BLLFactory<MT_Materiels>.Instance.GetAllToDataTable();
bindComboxEdit(txtMatID, dt, );
//清除已有的数据绑定
comboxEdit.Properties.Items.Clear();
foreach(DataRow row in dataTable.Rows){
comboxEdit.Properties.Items.Add(row["MatName"]); }
```

###### 15、父子表联动效果实现(使用加载form窗体，则联动效果不好实现)

(使用form窗体的tag传递数据)

```C#
        /// gridView的点击事件获取点击行的数据
        private void gridView1_RowCellClick(object sender, RowCellClickEventArgs e) 
        {
            //new窗体
            System.Windows.Forms.Form form = new SHFL.UI.FrmPU_ProMat();
            //通过tag传递选中行数据
            form.Tag = this.winGridViewPager1.gridView1.GetFocusedRow();
            addForm(form);
        }
```

###### 16、`SqlServer`中模糊搜索语法

```c#
//%为全模糊，包含即可
SELECT * FROM [user] WHERE u_name LIKE '%三%'
//下划线，表示匹配任意单个字符
SELECT * FROM [user] WHERE u_name LIKE '_三_'
//[]表示匹配其中的任意 一个 字符
SELECT * FROM [user] WHERE u_name LIKE '[张李王]三'
//[^]表示不再其中的字符的任意一个
SELECT * FROM [user] WHERE u_name LIKE '[^张李王]三'
```

17、操作人信息增加

```c#
        //在编辑或保存信息方法中调用该方法即可
		setUserInfo(info);  
        /// 操作人信息添加，*info为当前数据库表对象info
        private void setUserInfo( *Info info)
        {	//创建人信息是必填内容，如果没有说明是新建
            if (string.IsNullOrEmpty(info.Create_name))
            {
        info.Create_name = Portal.gc.LoginInfo.FullName;
        info.Create_by = Portal.gc.LoginInfo.ID;
        info.Create_date = System.DateTime.Now;
            }
       //不是新建则只修改当前更新人信息
       info.Update_name = Portal.gc.LoginInfo.FullName;
       info.Update_date = System.DateTime.Now;
       info.Update_by = Portal.gc.LoginInfo.ID; 
        }
```

18、新增编辑页面绑定下拉列表数据内容方法

```c#
///①对指定的下拉列表框绑定指定数据内容
        /// <param name="comboxEdit">下拉列表框</param>
        /// <param name="dataTable">数据表</param>
        /// <param name="str">数据表中的指定属性字段</param>
private void bindComboxEdit( DevExpress.XtraEditors.ComboBoxEdit comboxEdit, DataTable dataTable,  String str )
        {
            comboxEdit.Properties.Items.Clear();
            foreach (DataRow row in dataTable.Rows)
            {          comboxEdit.Properties.Items.Add(row[str]);
            }
        }
//②绑定供应商名称下拉框, 添加到新建页面时的弹窗中,根据具体表对象改变
private void bindProviders()
        {
            DataTable dt = BLLFactory<PU_Providers>.Instance.GetAllToDataTable();
            bindComboxEdit(this.txtProvID, dt, "ProviderName");
        }
//③在数据显示函数中，为新建时调用方法②
bindProviders();
//④在编辑或者保存状态下取值函数中将name转义成ID存储，为空时索引报错怎么办？？
info.ProvID = BLLFactory<PU_Providers>.Instance.Find(string.Format("ProviderName = '{0}'", txtProvID.Text))[0].Id;
```

19、父子表关系关联时的数据传递

```c#
System.Windows.Forms.Form form1 = 
    new SHFL.UI.FrmPU_BuyItem();
//tag中的对象是选中行的info对象，接收时使用强制转换成对应info
form1.Tag = this.winGridViewPager1.gridView1.GetFocusedRow();
addForm(form1);
```

