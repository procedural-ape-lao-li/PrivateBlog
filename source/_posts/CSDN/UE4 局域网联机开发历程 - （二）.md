## UE4 局域网项目打包设置

1.在项目的配置文件 DefaultEngine.ini 添加 

```csharp
[OnlineSubsystem] 
DefaultPlatformService=Null （不一定是 MULL 也可能是 Steam 等）
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201020142909548.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70#pic_center)
2. 在 “项目名称 + .Build.cs”的文件下添加
`PrivateDependencyModuleNames.Add("OnlineSubsystemNull");`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201020143220710.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70#pic_center)

打包后，两台电脑无法联机可以查看：[UE4 局域网联机开发历程 - （三）](https://blog.csdn.net/qq_42673921/article/details/109181852)
