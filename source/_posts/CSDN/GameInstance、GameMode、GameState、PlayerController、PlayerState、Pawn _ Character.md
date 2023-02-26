
|  | 生命周期 | 存在 | 复制 |
|--|--|--|--|
| GameInstace | 整个进程 | 服/客 | 否 |
| GameMode | 关卡| 服 | N/A |
| GameState | 关卡 | 服/客 | 是 |
| PlayerController（有输入事件） | 关卡 | 服/客 | 是 |
| PlayerState | 关卡 | 服/客 | 是 |
| Pawn / Character（有输入事件） | 逻辑控制 | 服/客 | 是 |
GameState 可以复制但是 GameMode 不能复制，为了数据安全 GameMode 只能在服务器上存在。
GameInstance 跨关卡存在，切换关卡不会被销毁。
GameMode 和 PlayerController 会在切换关卡或者游戏模式时摧毁重置。
<br>

官网说明[链接](https://docs.unrealengine.com/zh-CN/GettingStarted/Terminology/index.html)：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191203165517998.png)![在这里插入图片描述](https://img-blog.csdnimg.cn/20191203165534431.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20191203165404150.png)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191203165554637.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191203165121103.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191203165343999.png)

