

###### 20190920 spreadsheet内容

spreadsheet中单元格合并：

```c#
string range = "A"+ row +":D" + row;	//选择要合并的范围
worksheet.Range[range].Merge(); 		//合并
```

spreadsheet中单元格添加实线边框：

```c#
string range = "A3:F" + row;		//选择要合并的范围
worksheet.Range[range].Borders.SetAllBorders(Color.Black, BorderLineStyle.Thin);			//添加边框	
```

worksheet中屏幕定位到某行某列：

```c#
//定位到第 row+1 行 / column+1 列
worksheet.ScrollToRow(row);
worksheet.ScrollToColumn(column);
```

注意：worksheet中Cells只能选择有数据的内容行列范围内，超出会报错，可以使用Rows()