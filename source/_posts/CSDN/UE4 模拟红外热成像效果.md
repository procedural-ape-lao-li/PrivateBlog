红外热成像效果实现运用的是后期处理材质，可参考官方文档：[后期处理材质](https://docs.unrealengine.com/zh-CN/Engine/Rendering/PostProcessEffects/PostProcessMaterials/index.html)
1. 创建类时添加 PostPricess 蓝图后期处理组件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200519115141962.png)
2.  创建的 PostPricess 细节里，在这里添加后期处理材质
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200519115334731.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
3. 材质的实现，仅供参考
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200519115544381.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20200519115632197.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200519115650229.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)

然后设置要渲染出来的类，打上对勾就可以。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200519120645286.png)
效果图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200519120748803.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)

