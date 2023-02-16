
statunit 整体帧长、游戏线程时长、渲染线程时长、GPU 时长。

stat Slow [-ms=0.3] [-maxdepth=5]

此命令将显示游戏线程和渲染线程的统计。所有 stats 将作为一个 stats 大群组进行渲染。无法访问分析工具或日志文件、或需要测试游戏的基础性能时，此命令十分实用。（默认只显示大于 1.0 毫秒的 stat 项目，以及超过 4 个关卡未被套入的 stat 项目。

注意：降低毫秒或增加深度均可能对整体性能产生影响。）

statShadowRendering

显示阴影计算时间，与实际阴影渲染时间分开（已包含在statLightRendering中）。

statSceneRendering

显示总体渲染统计。可从此处着手寻找渲染过程中性能较慢的大体区域。Draw Call 的数量是一个关注点

stat Particles 显示粒子计算时间和 sprite 渲染时间。

stat LightRendering 反馈灯光和阴影所需的渲染时间。

ShowFlag.VisualizeSSR 将所有受屏幕空间反射影响的像素渲染为亮橙色（速度较慢）。显橙色说明计算较慢的区域

stat InitViews 显示可视性剔除所花费的时间和效率。关于渲染线程性能，可视部分数量是最重要的个体 stat，它由 STAT INITVIEWS 下的可视静态网格体元素支配，但可视动态原语也对其存在影响。

ShowFlag.Translucency

切换半透明渲染。关闭后将不显示带有半透的材质

ShowFlag.ScreenSpaceReflections

切换屏幕空间反射，可能会产生大量性能成本，仅影响像素直至特定粗糙度（通过r.SSR.MaxRoughness进行调整，或在后处理设置中进行调整）。关闭后受屏幕空间反射的物体画面细节变低

ShowFlag.Rendering 切换当前视口画面。关闭后视口画面保持在当前渲染帧上。

ShowFlag.PostProcessing 切换所有后处理过程。关闭后没有后期灯光效果

ShowFlag.LightFunctions 切换光照函数渲染。关闭后会增加光照亮度



ShowFlag.Landscape

ShowFlag.Brushes

ShowFlag.StaticMeshes

ShowFlag.SkeletalMeshes 切换所渲染的几何体。只显示当前渲染的类型

ShowFlag.IndirectLightingCache

切换具有已失效的光照贴图的动态对象或静态对象是否使用间接照明缓存。（对性能损耗非常大）

ShowFlag.DirectionalLights

ShowFlag.PointLights

ShowFlag.SpotLights

切换不同的光源类型（对于了解各类光源的效果及性能影响非常有用）。关闭打开平行光，点光源，聚光灯。

ShowFlag.DeferredLighting

切换所有延迟照明处理过程。关闭后相当于关闭所有光源对物体的影响。

ShowFlag.Decals 切换贴花渲染。关闭显示贴花。

ShowFlag.Bounds 显示编辑器中选择的对象的界限量。

ShowFlag.Bloom 根据镜头光斑和高光功能来影响图像。主要是太阳光的反射影响，会变得更亮。

ShowFlag.AntiAliasing　 切换各种抗锯齿（TemporalAA 和 FXAA，FXAA更快，但效果较差）。

ShowFlag.AmbientOcclusion 屏幕空间环境遮挡（有些场景对于在光照中烘烤AO的静态物体只有很少的帮助）。关闭后场景会更亮些。

r.VSync 开启/关闭垂直同步（可能依赖于是否原生全屏）。

r.VisualizeOccludedPrimitives 显示被裁剪掉的物件的外盒框，良好的关卡设计需要考虑遮挡剔除（为了获得更好的性能，添加可见性阻挡程序）。显示视野内被遮挡不需要渲染的物体边框呈绿色显示

r.TiledDeferredShading 能够关闭基于 Tile 的延迟光照技术（GPU粒子的光影则没有退回方法）。关闭后灯光效果下降

r.SSR.MaxRoughness 0.9 屏幕反射0.9为最佳质量，0.1速度较快。数越大效果越好。

r.SeparateTranslucency 这是一个用于修复半透明情况下景深的问题的功能，如果不需要的时候可以把它关闭，并有其他影响（查阅SceneColor）

r.ScreenPercentage 用于减小内部实际渲染分辨率，画面会在重新放大。

r.AllowOcclusionQueries 用于禁用遮挡（可以让场景运行的更慢）。不显示遮挡绿框

ShowFlag.DeferredLighting 切换所有延迟照明处理过程。关闭后画面会明显变暗。

r.TiledDeferredShading.MinimumCount 能够调整使用多少灯光应用在基于Tile的延迟光照技术（视觉上并没有差异但性能会有不同）

r.SceneColorFormat 能够选用不同的SceneColor格式（默认是64bit的最佳质量，并支持屏幕空间子表面散射）。关闭后画面质量明显下降。

STATLEVELS

查看内存中加载的关卡。红色：关卡已加载并且可见橘黄色：正在使关卡可见的过程中　　黄色：关卡已加载但不可见　　蓝色：关卡没有被加载，但是处在内存中，当发生垃圾回收时，它将会被清除。绿色：关卡没有被加载　紫色：正在预加载关卡。　黄色的关卡是不需要进行加载及推迟加载的最好备选项

如果一个大的动态载入的关卡，尽量把它进行分隔或者进行优化。

r.Shadow.MaxResolution 减小阴影的质量

FX.FreezeParticleSimulation 禁止粒子的更新。 、

FX.AllowGPUSorting 禁用粒子排序（在大量粒子的使用可以妥协使用）。

sg.ShadowQuality 调整阴影质量。关闭后画面变亮消耗变低

stat.rhi 检查各种贴图和triangle的消耗。

r.HZBOcclusion

用于计算HZB遮蔽，同时也会被屏幕空间内的射线演算使用。关闭后损耗减小
