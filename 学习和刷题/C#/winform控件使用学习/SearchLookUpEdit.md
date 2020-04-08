



```c#
//设置高度（好像没用）
con.AutoHeight = true

//自适应宽度，根据内容（第二句要有，表示按此设置进行适应）
con.Properties.PopupWidthMode = PopupWidthMode.ContentWidth;
con.Properties.BestFitMode = BestFitMode.BestFitResizePopup;
//自适应宽度，根据编辑框宽度
con.Properties.PopupWidthMode=PopupWidthMode.UseEditorWidth;
con.Properties.BestFitMode = BestFitMode.BestFitResizePopup;

//设定最适宽度
con.Properties.BestFitWidth = 500;
//设置弹窗大小
searchEdit.Properties.PopupFormSize = new Size(300, 300);

```



###### searchLookUpEdit 实现复选框

[代码教程](https://blog.csdn.net/u014682870/article/details/73505786?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task)