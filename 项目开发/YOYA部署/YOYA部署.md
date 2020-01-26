[TOC]

ERP登录用户：ZX

密码：123

远程服务器账户：李瑞

密码：LR@987654321YOUYA

WIFI：88157709



外网：121.207.5.17

数据库服务器：

局域网：192.168.0.250

用户名： exun

密码： YouYa2017,888



更改数据源：

Data Source=

192.168.0.250;Initial Catalog=YoYaOA;User ID=exun;Password=YouYa2017,888

121.207.5.17;Initial Catalog=YoYaOA;User ID=exun;Password=YouYa2017,888

连接本地数据库：Data Source=

(local);Initial Catalog=YOYA_ERP;Integrated Security=SSPI

(local);Initial Catalog=WinFramework;Integrated Security=SSPI

(local);Initial Catalog=YOYA_Text;Integrated Security=SSPI



WinFramework



###### 20191218sqlserver数据库局域网共享设置（测试成功）

[教程](https://blog.csdn.net/zw_2011/article/details/8872129)



友雅数据库连接：

<add name="sqlserver" connectionString="Persist Security Info=True;Data Source=121.207.5.17;Initial Catalog=YoYaOA;User ID=exun;Password=YouYa2017,888"
      providerName="System.Data.SqlClient" />
    <add name="WHC.SHFL.Properties.Settings.SHFLBasicConnectionString"
      connectionString="Data Source=121.207.5.17;Initial Catalog=YoYaOA;User ID=exun;Password=YouYa2017,888"
      providerName="System.Data.SqlClient" />
    <add name="WHC.SHFL.Properties.Settings.SHFLbasisMessage" 
      connectionString="Data Source=121.207.5.17;Initial Catalog=YoYaOA;User ID=exun;Password=YouYa2017,888"
      providerName="System.Data.SqlClient" />
    <add name="FL_DataSet.Properties.Settings.SHFL_TextConnectionString"
      connectionString="Data Source=121.207.5.17;Initial Catalog=YoYaOA;User ID=exun;Password=YouYa2017,888"
      providerName="System.Data.SqlClient" />