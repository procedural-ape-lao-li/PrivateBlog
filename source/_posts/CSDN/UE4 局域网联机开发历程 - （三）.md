UE4局域网打包后，在多台电脑上无法链接。两台电脑相互 ping IP 查看是否可以通信
	（1）.不能通信，检查下路由设置或者打开手机热点进行测试。
	（2）.可以正常通信，两台电脑就是无法联机，可以参考以下设置。 
	![在这里插入图片描述](https://img-blog.csdnimg.cn/20201020152553788.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70#pic_center)
红：点击“网络和Internet设置”
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201020154412190.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70#pic_center)

红（更改适配器选项）：点击进入，禁用 VMnet
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201020152740169.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70#pic_center)
黄（共享选项）：检查专用，来宾或者共用和所有网络，启用网络发现，启用文件和 大打印机共享
![加粗样式](https://img-blog.csdnimg.cn/20201020152845906.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70#pic_center)

补充 ：open ip 可以进入创建好的房间，那就要检查一下电脑网络的共享设置。
