

###### 20190826友雅始

###### 合同订单中调用工作流api接口

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

