[TOC]

###### 使用字典Dictionary存储数据<Guid,string>

```c#
//定义一个字典类型
private Dictionary<Guid, string> dict = new Dictionary<Guid, string>();
//字典中添加数据元素（key,value）
dict.Add(conList[i].Id, conList[i].ConNO);

//根据键获取值
//1、直接通过索引，不过可能字典中不存在当前key，会报错，要先判断（复杂）
//判断+检索两次索引，key不对时会抛异常
if(dict.ContainsKey(key))
{
 	string value = dict[key];   
}
//2、通过TryGetValue的方法
//检索一次，速度更快，key不对时方法返回false
int resValue ;
myDictionary.TryGetValue(key, out resValue);
//根据值获得键
//1、遍历判断，得到对应值的键
//dict元素遍历,每次得到一个键值对
foreach (KeyValuePair<Guid, string> kvp in dict){}
//dict-key遍历，每次得到一个键
foreach (Guid key in dict.Keys){}
//2、使用Linq语句查询  添加命名空间using System.Linq
//get all keys,返回符合条件的所有key
var keys = dic.Where(q => q.Value == "2").Select(q => q.Key); 
//get all keys，返回所有key的list集合
List<string> keyList = 
    (from q in dic where q.Value == "2" select q.Key)
    .ToList<string>(); 
//get first key，返回符合条件的第一个key
var firstKey = dic.FirstOrDefault(q => q.Value == "2").Key;  
```

