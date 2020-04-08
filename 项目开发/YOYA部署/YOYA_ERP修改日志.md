

> 2020-03-07之后对友雅数据库表结构进行修改的操作记录。

2020-03-07

- 盘点数据库表结构的设计更改
  - 将表 SR_InventoryInfo 更改成 SR_Inventory 并重新设计了表字段。
  - 对表SR_InventoryDetail 重新设计了表字段。
  - 将表 SR_InventoryDetail 更改成 SR_InventoryDetailMat 来存放原材料的盘点明细。
  - 新增表 SR_InventoryDetailProduct 用来存放成品的盘点明细。（是否考虑成品的号型问题） 
- 整理数据库表
  - 删除了MT_MatInAp[plyItem表，此前用于物料占用信息的存放，现今不用，删除。
- 库存调拨（转移）数据库表的设计
  - 新增表 SR_StockTransfer 作为库存调拨的主表。
  - 新增表 SR_StockTransferMat 来存放原材料库存调拨明细。
  - 新增表  SR_StockTransferProduct 来存放成品库存调拨明细。 （是否考虑成品的号型问题） 

2020-03-08

- 库位物料表结构修改
  - 表 SR_PositionMats 增加了字段 ConNO 用来显示库存物料所属的合同编号信息。

2020-03-09

- ​	权限管理-功能模块修改
  - 将库存转移功能模块下的 物料库和半成品库 合并成物料转移，成品库修改成成品转移

2020-03-13

- ​	更新库存
  - 入库表 MT_MatIn 中字段 CheckWorkrtID 修改为CheckWorker 类型int修改为nvarchar

2020-03-14

- ​	之前的数据库修改内容已经同步到云服务器
- ​    备份同步到本地一个 20200314... 的数据库