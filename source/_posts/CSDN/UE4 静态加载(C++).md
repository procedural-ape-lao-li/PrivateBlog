## 静态加载 `LoadClass<T>()`：

LoadClass<转换类型>(路径)
注释：路径名必须带_C后缀（LoadObject不需要带_C后缀）

***例如：***
蓝图查看路径
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181211165144490.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
C++ 可输入（同路径可以有好几种写法，此处只举一个）：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181211165241781.png)


## 动态加载与静态加载的区别：

`LoadObject<T>()`用来加载非蓝图资源，比如动画、贴图、音效等资源；

`LoadClass<T>()`用来加载蓝图并获取蓝图Class，比如角色蓝图等。
