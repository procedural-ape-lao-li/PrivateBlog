
**初始设置**

![在这里插入图片描述](https://img-blog.csdnimg.cn/2018111517180637.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)

**取消物块对导航的影响**

![在这里插入图片描述](https://img-blog.csdnimg.cn/2018111517172913.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)

## 实例代码：

**.h**

    protected:
    	// 声明布尔值是否巡逻
    	UPROPERTY(EditInstanceOnly, Category = "AI")
    		bool bPatrol;
    
    	// 在bPatrol为真时，设置第一个巡逻位置
    	UPROPERTY(EditInstanceOnly, Category = "AI", meta = (EditCondition = "bPatrol"))
    		AActor* FirstPatrolPoint;
    
    	// 第二个巡逻位置
    	UPROPERTY(EditInstanceOnly, Category = "AI", meta = (EditCondition = "bPatrol"))
    		AActor* SecondPatrolPoint;
    
    	// 巡逻变量
    	AActor* CurrentPatrolPoint;
    
    	// 移动函数
    	void MoveToNextPatrolPoint();


**.cpp**


    void AFPSAIGuard::MoveToNextPatrolPoint()
    {
    	// 当巡逻不在巡逻点上，或在第二个巡逻点上，移动到第一巡逻点
    	if (CurrentPatrolPoint == nullptr || CurrentPatrolPoint == SecondPatrolPoint) {
    		CurrentPatrolPoint = FirstPatrolPoint;
    	}
    	else
    	{
    		CurrentPatrolPoint = SecondPatrolPoint;
    	}
    	// SimpleMoveToActor 移动到 GetController() 返回控制器。
    	UNavigationSystem::SimpleMoveToActor(GetController(),CurrentPatrolPoint);
    }
    
    
    //调用移动函数
    void AFPSAIGuard::BeginPlay()
    {
    	Super::BeginPlay();
    	if (bPatrol)
    	{
    		MoveToNextPatrolPoint();
    	}
    }
    
    
    //判断是否到达巡逻点，切换移动到下一个巡逻点
    void AFPSAIGuard::Tick(float DeltaTime)
    {
    	Super::Tick(DeltaTime);
    	if (CurrentPatrolPoint)
    	{
    		//自身的位置减去巡逻点的位置
    		FVector Delte = GetActorLocation() - CurrentPatrolPoint->GetActorLocation();
    		//类型转换
    		float DistanceToGoal = Delte.Size();
    		if (DistanceToGoal < 100)
    		{
    			MoveToNextPatrolPoint();
    		}
    	}
    }


	// 停止移动   GetController() 返回控制器。
	AController* Controller = GetController();
	if (Controller)
	{
		Controller->StopMovement();
	}
	
**搜索目标点，放在巡逻地点**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181115174435716.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)

**勾选巡逻，选中要巡逻的两个目标点**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181115174310323.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)


**仅供参考**
