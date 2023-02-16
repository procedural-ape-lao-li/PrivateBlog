比较清晰的在 3D 场景中显示 UI，之前在 3D 场景中一直使用的是 Widget Component 组件，在4.19版本中 UI 显示的还是挺清楚的，后来把项目升级到4.22版本后模糊的什么都显示不出来，发现 Stereo Layer 组件可以解决在 3D 场景中显示不清楚导入问题。

Widget Component 组件在 3D 场景中会受到后期处理的影响，而 Stereo Layer 组件 在3D 场景中不受后期处理的影响。

设置方法：
1.添加 Stereo Layer 组件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200803165044340.png)

2. 设置大小尺寸，设置比较合适的大小。建议设置的和要显示的 UI 一样大。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200803165257251.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)

3. 设置参数（注，还是不太清楚的话可以试试把 Priority 参数设置为 1）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200803165412284.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
4. 设置 Texture
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200803165647829.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
5. 隐藏 Widget Compoent 组件显示的 UI
   1）创建材质
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200803165830161.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70) 
  2）赋值给 UI 
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200803171315740.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)


用这种方式设置的 UI 在 3D 空间中显示的更为清楚一些，不好的地方就是 RC 显示屏看不见显示的 UI，只能在 VR 头戴中看见显示的 UI。

