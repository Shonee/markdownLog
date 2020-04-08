[TOC]

###### 1、使用Linq对集合（数组）中元素进行合并、去重等操作

```c#
//处理目标->将"编号(ProductNo)"相同的产品记录，"库存量(StockNum)"合并，"附属标签(Tag)"合并//合并处理
listProduct.ForEach(c => {        
    var group = listProduct.Where(a => a.ProductNo == c.ProductNo); 
    c.StockNum = group.Sum(x => x.StockNum);        
    c.Tag = group.Select(t => t.Tag).ToList().Join();     	});

//去重复(默认是保留出现相同元素的第一个元素)
listProduct = listProduct.Distinct(new ProductNoComparer()).ToList();

/// <summary>
/// 去"重复"时候的比较器(只要ProductNo相同，即认为是相同记录)
/// </summary>
class ProductNoComparer : IEqualityComparer<Product>
{
    public bool Equals(Product p1, Product p2)
    {
        if (p1 == null)
            return p2 == null;
        return p1.ProductNo == p2.ProductNo;
    }

    public int GetHashCode(Product p)
    {
        if (p == null)
            return 0;
        return p.ProductNo.GetHashCode();
    }
}
```



###### 2、查找一个集合中有但另一个集合没有的元素（使用Linq查询两个集合的共同元素）

```c#
//List1中有 List2中没有 的元素
//方案一、Where()
var result = List1.Where( 
    p1 => !List2.Any(p2 => p2.ID == p1.ID));
//方案二、Except()
var result = List1.Except(List1);
//方案三、Linq Query
var result = from item2 in List2 Where !(
    from item1 in List1 select item1.ID
	).Contains(item2.ID) 
    select item2
//方案四、
var result = List2.Where(
    p1 => List1.All(p2 => p2.ID != p1.ID));
//方案五、
var result = from item in List1 Where
    List2.Contains(item) == false select item;
```

###### 	3、根据一个 `PID` 迭代遍历所有下级内容

```c#
//使用Linq
public List<Tim_LinqTable> GetAllSonID(int p_id)
{
	var query = from c in this.Tim_LinqTables
		   where c.Parent  == p_id
		   select c;
	return query.ToList().Concat(query.ToList().SelectMany(t => GetSonID(t.Id))).ToList();              
}
```



