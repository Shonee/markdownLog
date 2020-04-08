[TOC]



###### 1.使用SQL对数据库指定表中指定字段进行批量赋值操作

```sql
//指定单个列
UPDATE TB_DictData SET IsSync = 0 WHERE IsSync is NULL
//指定多个列
UPDATE TB_DictData SET IsSync = 0, SyncReturnValue = "" WHERE IsSync is NULL
```

###### 2.SQL中模糊查询

```sql
SELECT * FROM [user] WHERE u_name LIKE '%三%'
```

###### 3.[SQL2005安装教程](https://mp.weixin.qq.com/s/AudhTJdblnYieusQqfpBVQ)

远程

###### 4.SQL中对varchar字段按照数值大小排序

字段为varchar，

排序：1、10、11、123、1234、2、25、253、3

希望：1、2、3、10、11、25、123、253、1234

①：ORDER BY CAST(字段名 AS DECIMAL)

②：order by 字段名+0

附③：使用MySQL绝对值函数ABS，告诉MySQL使用绝对值来处理处理这个字段：ORDER BY ABS(字段名)

④：直接使用  ORDER BY (字段名)  不加(正序/倒序)，就会按照字符串中数值内容排序，有的字符串带有-a也可排序

⑤：终极办法，sql语句中使用正则匹配排序

```sql
排序：order by to_number(regexp_substr(salary,'[0-9]*[0-9]',1)) desc
regexp_substr 为截取方法，1为起始位置

REGEXP_SUBSTR(String, pattern, position, occurrence, modifier)
__srcstr     ：需要进行正则处理的字符串
__pattern    ：进行匹配的正则表达式
__position   ：起始位置，从第几个字符开始正则表达式匹配（默认为1）
__occurrence ：标识第几个匹配组，默认为1
__modifier   ：模式（'i'不区分大小写进行检索；'c'区分大小写进行检索。默认为'c'。）

```

###### 5.`SQLSERVER2012`中开启远程访问

[教程](https://www.cnblogs.com/Davi123/p/10077756.html)

最后：一定要做好防火墙设置，如果不确定的话，就把所有防火墙都关闭掉！

###### 6.`SQLSERVER`中获取指定时期的数据

```SQL
//查询表中30天内的数据
SELECT DISTINCT ConID FROM MT_MatIn WHERE DATEDIFF(dd,create_date,GETDATE()) <= 30 AND isdeleted = 0 AND InType <> '红冲入库'
```

