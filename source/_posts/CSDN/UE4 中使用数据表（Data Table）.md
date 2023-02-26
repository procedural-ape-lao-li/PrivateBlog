1. 新建 Excel 表格，在表格中添加数据，并将 Excel 另存为 .CSV 格式
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701095458274.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020070109571666.png)
2. UE4 中新建结构体，添加与 Excel 相对应的列表变量

	![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701095912211.png)

3. 拖拽表格到UE4内容浏览器，选择对应的结构体，导入成功
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701100118968.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701100149667.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)


UE4 导出 CSV 表格报以下错误：
```
Cannot find Property for column '???' in struct '?'
```
中文乱码，因为不识别数据结构中声明的中文名的变量。修改成英文就好了。

