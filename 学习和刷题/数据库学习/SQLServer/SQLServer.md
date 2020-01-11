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

