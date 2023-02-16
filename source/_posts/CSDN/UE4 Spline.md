Spline和Spline Mesh的区别：

1、Spline Mesh是有实体表现的，Spline Mesh可以拉伸弯曲实体模型，Spline Mesh是具象。

2、Spline 只有曲线，没有实体模型表现，是抽象的，不是具象，游戏运行时是看不到Spline曲线的。但是可以用Spline来做一些事情，比如：运动轨迹，让一个物体沿着Spline曲线进行运动。

3、Spline Mesh只有2个端点，不能添加额外的端点

4、Spline 默认只有2个端点，但是可以添加额外的端点


作用：

1、协助制作者，在场景中，生成一个轨迹；

2、可以按照轨迹，设置静态网格对象

3、Spline本身不包含网格对象，只是一个轨迹，或者是连续的线段。

一、新建一个名为testSpline继承Actor的蓝图，添加一个Spline组件
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709142953246.png)   ![在这里插入图片描述](https://img-blog.csdnimg.cn/2020070914300485.png)

二、把TestSpline拖放到关卡中。
　![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709143010797.png)

三、为了方便测试，把蓝图中默认白色球的显示大小改成0。
　![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709143045788.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
　　![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709143051116.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)

四、Spline跟Spline Mesh一样，也是可以移动旋转端点、切线端点

五、跟Spline添加新的端点
1. 选中Spline其中一个端点，按住Alt键，移动端点，就可以复制出一个新的端点了。复制端点的切线跟源点切线是完全一样的。这个方法跟在场景中复制模型的操作是一样的，都是按住Alt键。
2. 右键Spline曲线（不包括端点），出现的菜单中选择“Add Sline Point Here”，就可以在右键的曲线位置添加一个新端点。通过该方法添加的端点切线是默认水平的

 六、删除Spline端点：选中端点，按Delete键

七、Get Number Of Spline Points 获取Spline端点数量　

八、Get Location at Spline Point：获取一个端点的位置信息

九、调用“AddSplineMeshComponent”就可以添加物体到指定的Actor。记得设置Static Mesh静态网格模型
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709143105775.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
十、Add Spline Mesh Component.Set Start and End　　
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709143119948.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
十一、Spline.Set Spline Points，如果发现spline没有跟抛物线重合，则设置合适的Coordinate Space就可以了。

　　

 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200709143134197.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
 
