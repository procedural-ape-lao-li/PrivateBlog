初学Slate（Slate、VS、UE4小知识）
刚开始接触slate，内容比较散，脑袋略混乱，稍微记一下

初学Slate（Slate、VS、UE4小知识）
部分快捷键和快捷方法（VS以及UE4都有）
前缀单词的意思
寻找变量、参数或任何内容的方法
slate小知识
其他小知识
智能指针与垃圾回收
解决方案配置（编译配置）
部分快捷键和快捷方法（VS以及UE4都有）
根据首字母搜索头文件 Ctrl + J
代码(逆)缩进 (Shift + )Tab
UE4命令行 `
找定义 Alt + G
搜索Ctrl + F
通过VS的调试来运行UE4F5
在VS中直接运行虚幻编辑器Ctrl + F5
从断点处逐句执行程序 F10
断点调试时进入某个函数F11
断点调试时快速执行完某个函数，返回堆栈上层 Shift + F11
添加VA插件后寻找.h或者.cpp文件 Shift + Alt + O
添加VA插件后快速实现函数

前缀单词的意思
 - U   继承自UObject的子类以U为前缀 
 - A   继承自AActor的子类以A为前缀
 - T   模板
 - S   Slate
 - F   自定义的
1
2
3
4
5
寻找变量、参数或任何内容的方法
源码万岁！！！

寻找UMG可视化版本，看该功能如何使用，然后去Slate中寻找对应内容：在VS中搜索关键字或者相应的注释 找到对应C++位置
UE4是使用Slate制作界面，因此可以从UE4的源码中寻找使用Slate制作的部分，查看ue4的slate创建案例的代码，作为参考
调用WidgetReflector，点击Picking来抓取元素，点击Esc捕获到抓取的元素，然后就可以找到源代码的行数，继续调试来探索其本质，先尝试用最简单的代码完成功能，然后逐步自己封装升级优化 
 


怎么写参数？ 
Alt+G 看源码

再加一句，怎么改bug？ 
排除法，从最近的一行开始还原，依次往上，看哪行的问题，直到问题修复，锁定出错代码

slate小知识
Overlay：有点类似于PhotoShop的图层，是一层一层堆叠的，在代码中或者UE4中放置的位置越往下，图层越偏上；所有图层都可以显示
Widget Switcher：也是一层一层堆叠结构，但是每次只显示一个图层
collapsed ：塌陷，彻底消失，不显示，也不在视口中占位置 
hidden：占位消失，看不见，但仍在视口中占位置
Slot：插槽。在slate中，控件分为三种类型：Leaf Widgets不带子槽的控件如TextBlock；Panels子槽数量为动态的控件；Compound Widgets子槽数量固定的控件如SDockTab，Border，Button等
return FReply::Handled(); :截断消息。表示该消息在这一层已经被截断，不会继续向下分发，通常在该层就进行了处理
SLATE_EVENT：传递代理 （代理名称、参数类型） 
SLATE_ARGUMENT：可以传递函数 
SLATE_ATTRIBUTE：只能传递变量
其他小知识
初始化顺序：引擎 -> Game Instance -> Game Mode
出现汉字警告：先将鼠标点击进代码中，表示要对当前的文档进行调整。然后“文件 - 高级保存选项 - 65001”或者“File - Advanced save options… - 65001”
Super的使用：在子类的构造方法中调用父类的构造方法。如果用在子类的构造器中，必须是第一个语句！
分清逻辑和业务，写界面就写界面逻辑，记住代理是个好东西。①按钮被点击 ②按钮被点击时打印“被点击”。（可能目前理解的不到位，以后再做修改）
使用UMG做界面时先去掉自带的画布，因为那个画布有很大的限制，取的是绝对位置，可以添加一个overlay或者border来作为最底层的容器
MVC模式：Manage-View-Control 代理在其中起了很大的作用
打包出来的文件夹中会有一个.pak文件位于Content文件夹中，这里面存放的都是一些压缩优化后的资源；.exe是代码
在一个类的构造函数里加断点，你能找到世界的起源！
什么是Actor？具备挂载组件的能力！如果是Actor，他一定被放进了世界里，一定能在World Outliner中被看到，他可以有坐标（Transform被封装在了SceneComponent组件中）；反之，如果你能在世界中看到的所有，一定是继承自AActor
Actor和Component的关系：在构建的时候，SpawnActor一定会先调用到SpawnRootComponent，Actor就是Component上边的一层，组件一层一层的构造完毕的时候，Actor就创建好了
PlayerState：当前关卡玩家的游戏数据
GameState：当前关卡的游戏数据
GameInstance：跨关卡的数据统计

智能指针与垃圾回收
这么理解对吗？！！！

我想结合一下UE4的垃圾回收机制，垃圾回收机制对于所有未被领养的东西（具体是啥？）会在一分钟后进行回收，而什么样的东西未被领养呢？UObject的东东。而继承自AActor的东东都被“世界”领养了，参考上边第9条，于是乎，一个神奇的叫做AddtoRoot()的函数就出现了，帮我们领养所有UObject的东东，防止被垃圾回收
转过来看智能指针，这是c++的东西，里边比较重要的概念就是“引用计数”，这时候又出现了一个叫做弱指针的东东，是不会贡献引用计数的。
普通指针变为智能指针，这个函数就是MakeShareable()，举个例子
TSharedPtr<FMyFunction> MyFunction;
MyFunction = MakeShareable(new FMyFunction());
1
2
解决方案配置（编译配置）
官方文档传送门编译游戏项目 
编译配置由两个关键字组成：编译状态加编译对象 
编译状态： 
1. Debug：调试模式，加断点进行调试等都是在这个状态下进行调试的，会生成大量的.dll，.pdf等中间文件方便调试，同时调试引擎代码和游戏代码，最常用的 
2. DebugGame：只能调试游戏代码，无法调试引擎代码。按最优方式编译引擎 
3. Development：半发布、封测状态下。引擎和游戏代码都将在此配置中被编译 
4. Shipping：非调试模块，发布状态。可达到最佳性能并能发行游戏 
5. Test：测试 
编译对象： 
1. 空白：该配置编译了您项目的一个独立可执行版本，但需要平台特定的已烘焙内容。编译的对象是发布之后的资源（已经被压缩优化） 
2. Editor：为能在虚幻编辑器内打开项目并查看所有变更的代码，该项目必须在 Editor （编辑器）配置内进行编译。对象是发布之前的资源，未被压缩优化

顺带扯一句，最常用的就是Debug Editor
--------------------- 
版权声明：本文为CSDN博主「fee_liang」的原创文章，遵循CC 4.0 by-sa版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/fee_liang/article/details/79870920
