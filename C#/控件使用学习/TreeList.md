###### XtraTreeList是一个多功能的数据可视系统，可以把信息显示为树状、网格或者两者的结合——在数据绑定模式或者非绑定模式中

#### TreeList的使用：

##### 	数据库的绑定

```c#
		//使用适配器映射连接获取数据库中数据表
		//SqlConnection方式连接数据库，要先引用命名空间 System.Data,SqlClient
        string constr = "server=.;database=build;integrated security=SSPI";
		//server值表示运行sql的计算机名，同在本地则使用.或者localhost；
		//database表示使用的数据库名称(build)；
		//integrated security=SSPI 则表示使用集成的Windows验证方式
        SqlConnection con = new SqlConnection(constr);
        string sql = "select * from XtraTreeListTest";
        SqlDataAdapter sda = new SqlDataAdapter(sql, con); 	//建立连接，获取数据到适配器中
        DataTable table = new DataTable();                	//声明datatable类型接收数据表
        sda.Fill(table);                                  	//填充数据
```

​		绑定数据源DataSource

```c#
			treeList.DataSource = table; 
```

​		绑定属性KeyFieldName

​		绑定属性ParentFieldName

##### 	TreeList的常用属性

​		列名标题自定义

```c#
			treeList.Columns["NodeName"].Caption = "地区名称";
			//更改NodeName列的显示标题，NodeName是数据表中的列
```

​		数据不可更改属性

```c#
			treeList.OptionsBehavior.Editable = false;	//设置为false则执行后页面数据不可更改
```

​		复选框CheckBox可见

```c#
			treeList.OptionsView.ShowCheckBoxes = true;	//复选框显示
```

​		默认展开层级菜单

```c#
			treeList.ExpandAll();                       //默认展开所有的节点
```

```c#
        //其他属性
		treeList1.LookAndFeel.UseWindowsXPTheme = true;    	//使用XP主题
        treeList1.LookAndFeel.UseDefaultLookAndFeel = false;
        treeList1.OptionsView.ShowColumns = false;       	//隐藏列名
        treeList1.OptionsView.ShowColumns = false;       	//显示展开按钮
        treelist1.OptionView.ShowIndicator = false;    		//隐藏最前面的行指示列
        treeList1.Appearance.FocusedCell.BackColor = Color.LightSteelBlue;    //焦点行颜色渐变
        treeList1.Appearance.FocusedCell.BackColor2 = Color.SteelBlue;
        treeList1.OptionsView.ShowHorzLines = false;     	//隐藏行列边框
        treeList1.OptionsView.ShowVertLines = false;
		treeList1.OptionSelection.InvertSelection = true;	//选中时的颜色
//隐藏焦点行边框   	
treeList1.OptionsView.FocusRectStyle = 	DevExpress.XtraTreeList.DrawFocusRectStyle.None;  
```



##### 	TreeList的常用操作

###### 		节点选中高亮

###### 		使用复选框时父子联动效果

```c#
			//节点checked状态改变时触发事件 
			//定义了命名空间DevExpress.XtraTreeList.NodeEventArgs，可以写成NodeEventArgs e
			private void treeList_AfterCheckNode(object sender, NodeEventArgs e)
        	{
                //调用父选子函数
           		SetCheckedChildNodes(e.Node, e.Node.CheckState);
                //调用子选父函数
            	SetCheckedParentNodes(e.Node, e.Node.CheckState);
        	}
```

###### 			选择父则选择所有子

```c#
			/// <summary>
            /// 对控件操作，选择某一节点时，其子节点全部选中，取消时，其子节点全部取消
            /// </summary>
            /// <param name="node"></param>
            /// <param name="check"></param>
            private void SetCheckedChildNodes(DevExpress.XtraTreeList.Nodes.TreeListNode node, CheckState check)
            {
                for (int i = 0; i < node.Nodes.Count; i++)
                {
                    //其子节点选中状态和其相同
                    node.Nodes[i].CheckState = node.CheckState;   
                    //迭代遍历子节点的子节点
                    SetCheckedChildNodes(node.Nodes[i], check);     
                }
            }
```

###### 			选择所有子时才选择父

```c#
			/// <summary>
            /// 选择全部子节点时，自动选择子节点的父节点，未全部选择则不选择父节点，
            /// 当取消节点的所有子节点时，则取消该节点，
            /// 有了命名空间 using DevExpress.XtraTreeList.Nodes;
            /// 则DevExpress.XtraTreeList.Nodes.TreeListNode node可以直接写成TreeListNode
            /// 只有最后一个带颜色的可以直接写，要么写完，不能写一半，例如：Nodes.TreeListNode node不行
            /// </summary>
            /// <param name="node"></param>
            /// <param name="check"></param>
            private void SetCheckedParentNodes(TreeListNode node, CheckState check)
            {
                if (node.ParentNode != null) 
                {
                    //获取父节点的状态
                    CheckState parentCheckState = node.ParentNode.CheckState;   
                    CheckState nodeCheckState;
                    for(int i = 0;i < node.ParentNode.Nodes.Count;i++)
                    {
                        //获取兄弟节点的状态
                        nodeCheckState = node.ParentNode.Nodes[i].CheckState;   
                        //只要有一个状态不同，即没有全部选择，则父节点不选中
                        if (!check.Equals(nodeCheckState)) 
                        {
                            parentCheckState = CheckState.Unchecked;
                            break;
                        }
                        //全部相同时，则父节点和当前节点状态一致
                        parentCheckState = check;                  
                    }
                    //全部选中后，才能进行到下一步，迭代判断父节点的兄弟节点
                    node.ParentNode.CheckState = parentCheckState;
                    SetCheckedParentNodes(node.ParentNode,parentCheckState);
                }
```

##### 		为每一个节点添加节点图片(选中状态和未选中状态图片切换)

```c#
		//工具栏选择imageList控件拖动到界面，添加图标文件；
		//在treeList控件的属性中找到SelectImageList选择存在的imageList，这样两个控件即连接起来
		//初始默认所有行的图标均为0号图标文件，通过*treeList1_CustomDrawNodeImages()*事件来设置。
		private void treeList1_CustomDrawNodeImages(object sender, DevExpress.XtraTreeList.CustomDrawNodeImagesEventArgs e)
        {	//使用各种条件来为不同的节点添加不同的图标文件
            //有子菜单
            if (e.Node.Nodes.Count > 0)
            {
                if (e.Node.Expanded)
                {   //展开状态
                    e.SelectImageIndex = 2;
                    return;
                }
                    //合并状态
                e.SelectImageIndex = 1;
            }
            else
            {   //无子菜单
                e.SelectImageIndex = 0;
            }
        }
```

​		根据复选框获取选择节点（Checked状态）

​		没有复选框时获取选择节点（Focused = true状态）

​		获取到指定节点后对其数据的操作（注意获取数据时要和数据库中数据类型对应）

​		