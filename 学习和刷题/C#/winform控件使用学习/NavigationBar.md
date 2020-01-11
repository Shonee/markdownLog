### Navigation Bar的使用总结

1、Add Groups      在Navigation组件的功能标签中直接创建

2、Add Items         在创建的Groups上右键，即可创建Items

3、Change Caption and Icons     在功能标签中可以对Groups和Items修改标题和图标

4、Add Separators     可以通过Groups上右键为组中的Items添加分隔标记Separator

5、Add External Controls to Groups    

在组标签上右键Change GroupStyle --> ControlContainer 切换到编辑模式，

此模式下可以在导航栏中添加其他组件，文本框，按钮等

6、Items and Item Links

NavigationBar组件的智能标签中选择Run Designer 在弹窗中进行操作，

选择显示所有Items，将存在的Item拖动到另外的组中，即可完成复制关联

标签的关联，同一个标签复制出现在不同的组中，因为是同一个标签Item，一个改变时另一个随之改变

7、Drop-and-Drop Operations 

拖拽属性默认开启，运行后用户可以使用鼠标拖拽将Item移动到其他Group，

或者按住 Ctrl 用鼠标拖拽则可以直接复制产生关联Item

属性：DragDropFlags可以设置NavigationBar或者Group的相关属性，

DragDropFlags的属性值AllowOuterDrop代表可以从一个NavigationBar拖拽到另一个中

##### 运行后组件的点击响应事件：

使用Navigation Frame组件可以产生page，根据点击事件可以切换不同的页面

在页面中可以添加各种组件来丰富页面

8、Item点击事件，事件中可以关联NavigationFrame组件的Page，

NavigationFrame.SelectedPage = navigationPage1;     //可以关联Page1

9、代码实现group/item的创建与加载

