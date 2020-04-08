[TOC]

###### 1、字符型数，长度固定时，前边补0的方法：

```c#
//固定字符串长度，如果不够则补0，最终得到0001
number = "1";
newInfo.FNumber = number.ToString().PadLeft(4, '0');
```

