### 任务：

1. gridView列宽的自动设置
   
   1. 暂时只能单独设置固定值
   
2. 创建人信息的补充
   
   1. 创建人信息在info类初始化时自动生成，更新人信息则在保存时添加
   
3. 供应商详情的新建编辑内容
   
   1. 下拉列表数据填充
   
4. 供应商内容和详情内容的联动

   1. 使用form窗体tag属性传递数据
   
5. 供应商详情页面的搜索功能实现

   1. 转义搜索
   2. gridView窗体显示内容格式化？？？
      1. 新添加物料名称和供应商名称列，数据库表中为ID，隐藏了
   
7. ##### 采购合同表
   
   - [ ] 新增功能不需要吧？
   - [ ] 新增供应商名称列
   - [x] 实现供应商搜索功能
   - [x] 采购合同信息操作人信息记录
   - [x] 编辑框供应商编辑框实现转义显示和下拉列表内容
     1. 下拉框和数据库表列的绑定函数
     2. 方法传参指定具体下拉框和数据库表
     3. 在新建时调用具体方法
     4. 在保存时使用find方法将name转义成id保存(find返回空时？报错吗？)
     5. 在显示函数中使用findByID将ID转义成name显示
   
7. ##### 合同清单表

   - [ ] 合同清单内容和物料申请清单表内容的关系，有一个关系表
   - [x] 新建窗口自动获取当前合同编号
   - [x] 合同单号、物料名称搜索功能，都是转义搜索
   - [x] 新增编辑页面合同、物料 显示-保存转义，数据字典添加
   - [x] 操作人信息
   - [ ] 父子表关联，不要每次刷新闪动，关联显示相应数据
   - [ ] gridView新增物料名称、合同编号列，单纯显示

8. ##### 送货单表

   - [ ] 适应小宽度，只有两个显示字段
   - [ ] 去掉gridView下方的记录信息
   - [ ] 搜索和编辑转义显示
   - [ ] 获取当前选中合同行信息

9. 送货清单表

   - [ ] 由合同清单生成，但是根据实际送货变化
   - [ ] 一点都没有写呢！！！！

10. 物料信息表添加了新字段

   11. 物料单价

   12. 库存信息

   3. 需要新增字段常备库存(`isStanding`)

14. 入库信息表

    - [x] 仓库名称和入库部门搜索功能添加
    - [x] 入库信息编辑数据字典添加
    - [x] 入库信息编辑关联数据下拉列表
    - [x] 操作人信息添加
    - [ ] 生产归还针对**领料表**中没有可以用来显示的 **列**
    - [x] 逻辑删除功能实现，并针对搜索数据实现删除过滤
    - [ ] gridView显示列中进行ID-Name的转义

15. 物料入库清单表

    - [ ] 部分外键没有设置好，供应商ID，合同ID等
    - [ ] 搜索功能实现
    - [ ] 新增编辑弹框是一个`gridView`编辑界面,通过条件显示编辑保存

16. 出库信息新建编辑表(信息和详情单放在一个页面添加和编辑)

    - [ ] 信息内容显示在编辑框中，保存时存入信息表中
    - [ ] 详情单显示在gridView中，编辑后保存实现存入详单数据库
    - [ ] gridView先手内容的转义
    - [ ] gridView的编辑保存实现
    - [ ] gridView的页脚分页信息去掉

17. 出库信息表

18. 出库清单表

19. 

20. 000

Current Login User Id



string where = GetConditionSql2();
            List<PL_DrawMatPlanItemInfo> list = BLLFactory<PL_DrawMatPlanItem>.Instance.FindWithPager(where, this.winGridViewPager2.PagerInfo);

            string tableColumns = "DrawPlanID,ColorMatchID,MatNum,DrawNum,UnitName,update_name,update_date,create_name,create_date";
            DataTable dt = DataTableHelper.CreateTable(tableColumns);
            DataRow dr = null;
    
            //Guid Mnameandcolor = materialsadapter.ScalarQueryMatnameColornoById(critemdetailcolormatchapter.ScalarQueryMatIDById(drawmatplanitemadapter.ScalarQueryIdByColormatchid()));
    
            foreach (PL_DrawMatPlanItemInfo info in list)
            {
                //Guid g = (Guid)drawmatplanitemadapter.ScalarQueryIdByColormatchid(info.ColorMatchID);
                //根据colormatchid也就是等于colormatch表的id得到Matid
                Guid matid = (Guid)critemdetailcolormatchapter.ScalarQueryMatIDById(info.ColorMatchID);
                //string Mnamecolor = materialsadapter.ScalarQueryMatnameColornoById(matid);
                string Mname = materialsadapter.ScalarQueryMatnameById(matid);
                string Mcolor = materialsadapter.ScalarQueryColorNoById(matid);
                 dr = dt.NewRow();
               //dr["DrawPlanID"] = draw.ScalarConTitleByid(info.ConID);
               dr["DrawPlanID"] = drawmatplanadpter.ScalarDrawNoQuerybyId(info.DrawPlanID);
    
               dr["ColorMatchID"] = Mname + "(" + Mcolor + ")";
                //dr["ColorMatchID"] = info.ColorMatchID;
    
                dr["MatNum"] = info.MatNum;
                dr["DrawNum"] = info.DrawNum;
                dr["UnitName"] = info.UnitName;
                dr["update_name"] = info.Update_name;
                dr["update_date"] = info.Update_date;
                dr["create_name"] = info.Create_name;
                dr["create_date"] = info.Create_date;
    
                dt.Rows.Add(dr);
    
            }
            this.winGridViewPager2.DataSource = dt.DefaultView; 
          //  this.winGri
          

178，503
