以 4.19 版本为例
插值：给两个数之间补充一些数，过渡变得更自然。

一、CInterp To：颜色（Color）插值。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191126132835678.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
二、FInterp To、FInterp To Constant：浮点数（Float）插值。
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019112613291665.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)

三、RInterp To 、RInterp To Constant：角度（Rotation）插值。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191126133037497.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
四、VInterp To、VInterp To Constant：向量插值
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191126133317247.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
五、Transform To
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019112613352089.png)

以上函数一般在“Tick”事件中使用：

Current：当前值

Target：期望的目标值

Delta Time：时间变化值。

Interp Speed：插值速度

返回值：从“当前值”过渡到“期望的目标值”的一个中间值

## 官方文档：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191126134118801.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
带有“Constant”的，表示匀速插值（线性插值）；没带有“Constant”的，表示缓冲插值（非线性插值），当前位置的距离到达目标的距离，有一种更平滑的感觉。

