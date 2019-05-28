### 1、二维数组中的查找

在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

##### 分析：

​	二维数组(i*j)，每一行从左到右递增，每一列从上到下递增，

​	判给定数是否存在数组中，则只需要与数组中的**最左(右)边**一列数进行判断，

​	最左(右)列的数有一个特点，**就是其右下方(左上方)的数值一定比其自身大(小)**。

###### 	本次使用左边第一列数字进行筛选：

​	a(0,0)，a(1,0)，a(2,0)，a(3,0)，... ，a(n,0)

​	可知，a(0,0)是所有数中最小的，因为左侧只能精确比其大的数，

​	故只要目标数字k大于a(i,0)，则将k与a(i+1,0)进行比较，

​	否则定位k在a(i-1,0)--a(i,0)之间，搜索不到则不存在。

#### **修正：**s单使用行或者列，能够减少比较次数，但是同时使用行列，则只需要比较一行或者一列即可，最糟糕的情况就是一行+一列

​	<u>从左下角开始比较，target小则减小行比较，target大则增加列比较</u>

```java
public class Solution {
    public boolean Find(int target, int [][] array) {
        int row = array.length - 1;
        int cell = 0;		//定位到左下角开始比较，行列同时使用
        while(row >= 0 && cell < array[0].length){
            if(array[row][cell] > target){
                row--;		//
            }else if(array[row][cell] < target){
                cell++;		//
            }else{
                return true;
            }
        }
        return false;		//循环结束没有跳出说明没有找到
    }
}
```

### 2、替换空格

请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为`We Are Happy`.则经过替换之后的字符串为`We%20Are%20Happy`。

##### `java`中自带的替换方法(String类)：

```java
str.replace('.','#');	//replace方法，将str中的.替换为#,返回新字符串,要有接收
str.replaceAll('.','#')	
//replaceAll方法，将所有字符替换为#，前一个为正则，也可以使用转义字符转义成具体字符
str.replaceFirst('.','#')//replaceFirst方法，将第一个字符替换为#，同样使用了正则
```

##### 具体代码实现分析：

```java
public class Solution {
    public String replaceSpace(StringBuffer str) {
        if(str == null){
            return null;
        }
        //StringBuilder对象字符串，创建时使用 new
        StringBuilder newstr = new StringBuilder();
        for(int i = 0;i < str.length();i++){
            //如果是空格，则在当前位置分别添加 % 2 0 三个字符
            if(str.charAt(i) == ' '){
                newstr.append('%');
                newstr.append('2');
                newstr.append('0');
            }else{
                //如果不是空格，则将字符添加到新字符串中
                newstr.append(str.charAt(i));
            }
        }
        return newstr.toString();
    }
}
//str.charAt(i)方法是获取字符串str在i位置的字符
//str.append('%')方法是在str的最后位置处添加 % 字符
```

##### `StringBuffer`和`StringBuilder`**类**

①两者皆是类，则创建该两种字符串时需要使用对象的创建方式，使用 *new* 关键字

②字符串进行修改的时候需要使用该两类，因两种字符串对象能够被多次修改而不产生新的对象

③`StringBuilder`方法不是线程安全的，但是相比`StringBuffer`速度更快

④多数情况下建议使用`StringBuilder`，在应用程序要求线程安全时，使用`StringBuffer`

##### `StringBuffer`类支持方法：

```java
StringBuffer strBuffer = new StringBuffer();
strBuffer.append(String s);			//追加字符串str
strBuffer.reverse();				//反转字符串
strBuffer.delete(int start,int end);//删除指定序列
strBuffer.replace(int start,int end,String str);//使用字符串str替换指定序列
```







