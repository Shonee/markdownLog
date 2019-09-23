



###### 20190921：

###### 	国别地区：

​		字典中类型为 国别

​		国别地区在数据字典中添加，因此在数据字典添加时，同步到K3中

​		数据字典中添加国别分类下的具体数据时，可以进行批量添加

​		批量添加到数据库中时，使用了事务操作，将多条数据一块添加进去

​		单个添加 `FrmEditDictData`

​		批量添加 `FrmBatchAddDictData`

```c#
DbTransaction trans = BLLFactory<DictData>.Instance.CreateTransaction();
InsertDictData(dictData, seq, trans);
trans.Commit();
//trans.Rollback();
```

###### 	省份城市：

###### 	城市港口：

###### 	供应商信息：