
参考 4.19 版本
## 1.创建新的插件

***

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190611182846882.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20190611182920864.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
## 创建空插件 Blank , 命名为 Tom_Plugins.
***
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190611183026382.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
## 创建成功
***
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190611183105324.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
## 2.在插件里创建 C++ 文件
***
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190611183135473.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
## 选中要添加的到的插件
***
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190611183228671.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)

扩展：在UE4窗口上输出文本
***
头文件 #include " Engine.h "
 GEngine->AddOnScreenDebugMessage(-1,时间,颜色,TEXT(“文本内容”))
