[TOC]

###### 20190826友雅始

###### 	合同订单中调用工作流api接口

```c#
///注释的地方暂时可以不用，可以用来获取调用接口时返回的结果数据
/// <summary>
/// Get请求
/// </summary>
public void GetHttp()
{
   string userId = "66";//Portal.gc.LoginInfo.ID.ToString();
   HttpWebRequest request = 	HttpWebRequest.Create("http://192.168.1.112:8081/contracts/contractsadd?id=" + userId) as HttpWebRequest;
   request.Method = "GET";
   WebResponse response = request.GetResponse();
   Stream stream = response.GetResponseStream();
   byte[] buf = new byte[1024];
   int len = stream.Read(buf, 0, 1024);
   //string str = Encoding.ASCII.GetString(buf, 0, len);
   string str = System.Text.Encoding.GetEncoding("gb2312").GetString(buf);
   DataSet ds = new System.Data.DataSet();
   //ds.ReadXml(new StringReader(str), System.Data.XmlReadMode.Auto);
   //dataGrid1.DataSource = ds.Tables[0].DefaultView;
        }
```



###### 20190909服良K3续

###### 	想办法将Item的内容做成一个方法，省去每次数据同步时都要重写

```c#
FItemID	-->	自动生成，按顺序递增
FItemClassID	-->	根据类型编码不同，物料是4
FName	-->	名称
FShortNumber	-->	短代码，只当前物料代码，不包括其上级

FParentID	-->	上级内码，即父级的FItemID，(父级自动生成)
FLevel	-->	固定，父级FLevel+1
FNumber	-->	物料代码，即全路径编码，01.001.0001
FFullNumber	-->	长编码，等同与物料代码FNumber
FFullName	-->	全名称，名称全路径，A_B_C

UUID	-->	本不用，此处用来存放当前同步物料信息的ID(唯一标识)	

```



###### 20190917服良

###### 	根据一个`PID`，迭代遍历所有下级内容，子、子子。。。

```c#
//使用Linq
public List<Tim_LinqTable> GetAllSonID(int p_id)
{
	var query = from c in this.Tim_LinqTables
		   where c.Parent  == p_id
		   select c;
		 
	return  query.ToList().Concat(query.ToList().SelectMany(t => GetSonID(t.Id))).ToList();              
}
```



###### 20190919  数据库字段问题

​	数据库更新时，碰到唯一键，提示重复插入错误，需要单独添加几列

​	使用实体进行数据库查找时，如果是刚更新的，则查找时找不到？？



###### 20190919服良项目需要修改问题

- [ ] 原材料合同导入时，
  - 数据是同一品番的物料归类信息，不需要做检查，直接导入即可
  - 品名根据中英文对照表
- [ ] 装箱单导入时，
  - 根据品番到原材料数据中获取单价，
  - 然后是品番+色号匹配物料基本信息
  - 品名根据中英文对照表
- [ ] 物料信息模块，
  - 数据多了，有点卡，如何优化？？



###### 20190920 spreadsheet内容

​	spreadsheet中单元格合并：

```c#
string range = "A"+ row +":D" + row;	//选择要合并的范围
worksheet.Range[range].Merge(); 		//合并
```

​	spreadsheet中单元格添加实线边框：

```c#
string range = "A3:F" + row;		//选择要合并的范围
worksheet.Range[range].Borders.SetAllBorders(Color.Black, BorderLineStyle.Thin);			//添加边框	
```

