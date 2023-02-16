## 设置碰撞

    // 组件 ->SetCollisionEnabled(ECollisionEnabled::NoCollision);     注释：没有碰撞
    // 组件 ->SetCollisionEnabled(ECollisionEnabled::PhysicsOnly);     注释：只有物理
    // 组件 ->SetCollisionEnabled(ECollisionEnabled::QueryAndPhysics); 注释：查询和物理
    // 组件 ->SetCollisionEnabled(ECollisionEnabled::QueryOnly);       注释：只有查询
    // 组件 ->SetCollisionEnabled(ECollisionEnabled::Type);			注释：目前理解为自定义

## 人物的重叠事件

    
	

> 注释：设置所有通道的冲突响应 SetCollisionResponseToAllChannels

     组件 ->SetCollisionEnabled(ECollisionEnabled::QueryOnly);

> 注释：将冲突响应设置为通道 SetCollisionResponseToChannel（相关参数：ECR_Overlap 重叠,
>     ECR_Block 物块，ECR_Ignore 忽略, ECR_MAX ?）
>     
 
    组件 ->SetCollisionResponseToAllChannels(ECR_Ignore); // ECR_Ignore 全部忽略


> 注释：ECC_Pawn 指向人物
> 

  

    组件 ->SetCollisionResponseToChannel(ECC_Pawn, ECR_Ignore);

        

相关函数：NotifyActorBeginOverlap  通知（Notify）类开始重叠

应用：
.h
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181114170649313.png)
.cpp
![在这里插入图片描述](https://img-blog.csdnimg.cn/2018111417073879.png)

**仅供参考**


