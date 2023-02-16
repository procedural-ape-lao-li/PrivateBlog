## UE4导入CSV文件出现乱码问题，解决方法如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200702175450208.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
**一，把 Excel 文件保存为 UTF-8 格式，设置方法如下**：
1. 文件 -> 另存为
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200702172924863.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
2.工具->Web选项
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200702174302437.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)

3.编码->选择UTF-8编码
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200702174441230.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
**二， 使用辅助工具进行编码转换以 VS2017 为例：**
1. 文件右键选择 VS2017
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200702174947245.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)

2. 高级保存选项->设置为 UTF-8 编码格式（[VS2017高级保存设置](https://blog.csdn.net/qq_42673921/article/details/107090072)）
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020070217512581.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)

## 设置完成重新导入后显示内容：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200702175553531.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
