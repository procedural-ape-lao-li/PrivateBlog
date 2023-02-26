## 根据文件夹路径生成文件夹下的所有静态网格体

1. 获取文件夹下的所有文件。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200713152754333.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
红色的框标出来的是文件夹路径，获取文件夹下的所有文件，循环转换为StaticMesh如果成功表明获取到的文件为静态网格文件。

2. 创建一个类，类里的模型有一个 StaticMeshComponent 组件，再声明一个StaticMesh类型的变量，设置为在生成时可见。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200713153702745.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
3. 初始化类时把模型赋值给组件。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200713153725628.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
4. 获取文件夹下的所有静态网格模型，并赋值给新生成的类。
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020071315383927.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)

注 ： FindOrLoadAssetsByPath函数的声明

.h

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201029120400496.png#pic_center)
.cpp![在这里插入图片描述](https://img-blog.csdnimg.cn/20201029120420927.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70#pic_center)



