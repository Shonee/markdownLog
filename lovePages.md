##### Git-Hub资源

- ###### [Chrome插件英雄榜，看看大家都在用什么插件提高效率](https://github.com/zhaoolee/ChromeAppHeroes)

- ###### [爬虫学习项目，到这里来就对了](https://github.com/facert/awesome-spider)

- ###### [爬虫项目练习！](https://github.com/shengqiangzhang/examples-of-web-crawlers?utm_source=gold_browser_extension)

- ###### [JavaGuide](https://github.com/Snailclimb/JavaGuide)

- ###### [CS-Notes](https://github.com/CyC2018/CS-Notes?utm_source=gold_browser_extension)

- ==高亮==   

 <font face="黑体">我是黑体字</font> 

 <font face="微软雅黑">我是微软雅黑</font> 

 <font face="STCAIYUN">我是华文彩云</font> 

 <font color=#0099ff size=12 face="黑体">黑体</font> 

 <font color=#00ffff size=3>null</font> 

<font color="green" size=5>绿色, 啦啦啦啦啦啦啦啦。 </font> 

-   <table><tr><td bgcolor=#FF4500>这里的背景色是：OrangeRed，  十六进制颜色值：#FF4500， rgb(255, 69, 0)</td></tr></table>  

- 

- ###### [最全中文诗歌诗词文集数据库](https://github.com/chinese-poetry/chinese-poetry)

- ###### [结构化算法刷题训练指南，快刷起来](https://github.com/apachecn/awesome-algorithm)

- ###### [从程序员到CTO](https://github.com/0voice/from_coder_to_expert)

- ###### [互联网架构设计](https://github.com/davideuler/architecture.of.internet-product)

- ###### [后端架构师技术图谱](https://github.com/xingshaocheng/architect-awesome)

- ###### [从0到1设计大型系统](https://github.com/donnemartin/system-design-primer/blob/master/README-zh-Hans.md)







###### [幕布，帮助你整理思绪，实现头脑风暴的好地方](https://mubu.com/list)

###### [在线画图，思维导图、流程图，uml等都可以](https://www.processon.com/diagrams)

###### [知乎热榜，微信排行只用这一个就够了](http://guozhivip.com/rank/)

###### [今日热榜，更全面](https://tophub.today/)

###### [可可英语，过六级就靠你了](http://www.kekenet.com/)

###### [牛客网，程序员刷题专业网站，在线编程](https://www.nowcoder.com/activity/oj)

###### [油猴脚本下载网址](https://greasyfork.org/en/scripts)

###### [SpringBoot中文社区](http://springboot.fun/)



###### [之前收藏网站的文本](Pages.txt)

<h5><a href = "www.baidu.com">你好啊,这是我写的html<a><h5>


```java
public static void main(string[] args){

​	System.out.print("");
    int a = 0;

}
```

#### 游戏区

###### [休闲游戏](https://t.cn/E9tsC30)











18日-21日，共四天：

第一天：

打车到青浦新城地铁站，17号线 -> 虹桥火车站，转10号线 -> 交通大学，

转11号线 -> 徐家汇，转9号线 -> 打浦桥，日月光中心，田子坊。

​	**田子坊（日月光、黄浦区泰康路210弄）**

田子坊后，建国中路瑞金二路站，公交车 -> 复兴东路光启路(豫园站)(5站，共约30分钟)

​	**城隍庙—豫园 (豫园旅游商业区)**(16点关门)

豫园出来，河南中路，10号线 -> 南京路步行街

​	**广南京路步行街(下午)、外滩(傍晚)**

轮渡或地铁至对岸，

​	**陆家嘴(东方明珠、中心大厦，上海市浦东新区)**

陆家嘴 2号线 -> 龙阳路，转16号线 -> 罗山路，转11号线 -> 迪士尼。(约50分钟)

**（住）**

第二天：（提前购票！！！）

​	**迪士尼游玩（一整天）**

迪士尼，11号线 -> 交通大学站，转10号线 -> 虹桥火车站。(约1.5小时)

**（住）**

第三天：

​	一早，虹桥站 --->>> 杭州东(50分钟)

​	火车东站，1号线 -> 凤起路

​	杭州西湖风景区，

​	**杭州花圃、西湖游船、灵隐景区、虎跑公园、九溪十八涧、梅家坞、龙井村、**

**浙江大学之江校区、白塔、八卦田遗址公园、观钱塘江**

**（住）**

第四天：

​	上午，休息，再转一下想去的地方

​	下午，回，，--->>> 虹桥 ，17号线 -> 青浦新城，打车到家。

​	

```c#
/// <summary>
        /// 右键添加功能到我的工作区以及从我的工作区删除
        /// </summary>
        private void myWorkSpace_ItemClicked(object sender, ToolStripItemClickedEventArgs e)
        {
            //获取我的工作区下的功能
            List<Function_UserInfo> list = BLLFactory<Function_User>.Instance.GetAll();
            //获取最大ID
            string maxID = list.Count == 0 ? "0" : list.Max(p => p.ID.ToInt32()).ToString();
            //有选中值是才能进行操作
            if (itemname != null)
            {
                //添加到我的工作区功能
                if (myWorkSpace.Items[0].Selected)
                {
                    //我的工作区有内容去判断要添加的是否重复，没有内容的话直接添加
                    if (list.Count > 0)
                    {
                        int hasfunction = list.Where(m => m.Name.Contains(itemname)).ToList().Count;
                        if (hasfunction > 0) { MessageBox.Show("请不要重复添加！"); }
                    }
                    //直接添加
                    else
                    {
                        Function_UserInfo newInfo = new Function_UserInfo();
                        newInfo.ID = (maxID.ToInt32() + 1).ToString();
                        //拿到要添加到我的工作区的功能名称
                        newInfo.Name = itemname;
                        //设置这是属于谁的工作区
                        newInfo.Create_Name = FLsimpleUtils.CreateID;
                        newInfo.Create_FullName = FLsimpleUtils.CreateName;
                        if (BLLFactory<Function_User>.Instance.Insert(newInfo)) { MessageBox.Show("添加成功！"); }
                        //刷新功能列表
                        InitAuthorizedUI();
                    }

​```
            }
            //从我的工作区移除功能
            else if (myWorkSpace.Items[1].Selected)
            {
                //如果我的工作区内容大于零进行判断有要删除的功能，有的话删除，没有提示
                if (list.Count > 0)
                {
                    int hasfunction = list.Where(m => m.Name.Contains(itemname)).ToList().Count;
                    if (hasfunction > 0)
                    {
                        if (BLLFactory<Function_User>.Instance.Delete(list.Where(m => m.Name.Contains(itemname)).ToList()[0].ID)) { MessageBox.Show("删除成功！"); }
                        //刷新功能列表
                        InitAuthorizedUI();
                    }
                    else { MessageBox.Show("未添加此功能到我的工作台!"); }
                }
                else { MessageBox.Show("我的工作台没有内容！"); }
            }
        }
        //当添加我的工作区结束时，将记录的功能栏Item的字符串初始化
        itemname = null;
    }

//树形结构功能菜单 && 联合我的工作台数据表
        private void InitTreeList()
        {
            this.treeList1.Nodes.Clear();
            List<FunctionInfo> memuList = BLLFactory<Function>.Instance.Find("(1=1)", "ORDER BY SortCode ASC");
            List<Function_UserInfo> myFunctionList = BLLFactory<Function_User>.Instance.Find(string.Format("Create_name = '{0}'", Portal.gc.LoginInfo.Name));
            memuList = memuList.Where(p => Portal.gc.HasFunction(p.ControlID) && !p.ControlID.Contains("/")).ToList();
            this.treeList1.DataSource = myFunctionList.Select(p => new { p.ID, p.PID, p.Name }).Union(memuList.Select(a => new { a.ID, a.PID, a.Name })).ToList();
            this.treeList1.ContextMenuStrip = myWorkSpace;
        }




```



