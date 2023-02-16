
一，UE4封装好的一个函数

使用方法：

	// 打开外部目标文件夹
	FPlatformProcess::ExploreFolder(*文件夹路径);
	
函数实现方法：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190711161427943.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)

二，用 CreateProc 打开，注意

使用方法：

	FilePath = explorer.exe  + 想要的开文件夹的路径
	FPlatformProcess::CreateProc(*FilePath, nullptr, true, false, false, nullptr, -1, nullptr, nullptr);
	
可以到：
http://api.unrealengine.com/INT/API/Runtime/Core/GenericPlatform/FGenericPlatformProcess/CreateProc/index.html
查看此函数详细介绍
	
就像 ：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190711160805418.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
cmd
explorer.exe  + 想要的开文件夹的路径


我也是新手，仅供参考哦！

