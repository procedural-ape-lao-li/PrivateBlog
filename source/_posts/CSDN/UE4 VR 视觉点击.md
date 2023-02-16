1. 创建一个类，添加一个Camera摄像机组件，再添加一个 WidgetInteractionCompent 组件，同时设置组件的相关参数。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200817144058492.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70#pic_center)
2. 设置按钮延迟 2.0 秒回触发事件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200817145216634.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70#pic_center)
扩展：
视觉点击和 UI 发生交互的碰撞点，如果不进行设置碰撞点显示的是一个点，如果要自定义设置一个图标，会把图标设置在最上层不被其他组件给遮挡，当点击UI的时候会发现这个图标会阻挡视觉点击和UI发生交互事件，其实设置的方法特别简单，如下图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200817144905471.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70#pic_center)


