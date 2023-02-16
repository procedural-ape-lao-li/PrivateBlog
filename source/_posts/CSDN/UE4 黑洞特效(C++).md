# 代码

**
 .h
**

    #pragma once
    
    #include "CoreMinimal.h"
    #include "GameFramework/Actor.h"
    #include "MyActor.generated.h"
    
    UCLASS()
    class FPSGAME_API AMyActor : public AActor
    {
    	GENERATED_BODY()
    	
    public:	
    	AMyActor();
    
    protected:
    	//创建一个圆的静态网格物体
    	UPROPERTY(VisibleAnywhere, Category = "Components")
    		class UStaticMeshComponent* MyMeshcomp;
    
    	UPROPERTY(VisibleAnywhere,Category = "Components")
    		class USphereComponent* MySphereComp;
    
    	UPROPERTY(VisibleAnywhere, Category = "Components")
    		class USphereComponent* InnerSphereComponent;
    
    	UPROPERTY(VisibleAnywhere, Category = "Components")
    		class USphereComponent* OuterSphereComponet;
    
    	UFUNCTION()
    	//设置一个 Ue4 能识别的函数
    	virtual void OverLapInnerShpere(UPrimitiveComponent* OverlappedComponent, AActor* 
    		OtherActor, UPrimitiveComponent* OtherComp, int32 OtherBodyIndex,
    		bool bFromSweep, const FHitResult& SweepResult);
    		
    	virtual void BeginPlay() override;
    
    public:	
    	virtual void Tick(float DeltaTime) override;
    };
    
**
 .cpp
**

    #include "MyActor.h"
    #include "Components/SphereComponent.h"
    #include "Components/StaticMeshComponent.h"
    
    AMyActor::AMyActor()
    {
    	PrimaryActorTick.bCanEverTick = true;
    
    	MyMeshcomp = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("MyMeshcomp"));
    	MyMeshcomp->SetCollisionEnabled(ECollisionEnabled::NoCollision);   //取消物体的碰撞
    	RootComponent = MyMeshcomp;	  //设置 MyMeshcomp 为根组件
    	
    	MySphereComp = CreateDefaultSubobject<USphereComponent>(TEXT("MySphereComp"));
    	MySphereComp->SetupAttachment(MyMeshcomp);
    	// MySphereComp 设置为 MyMeshcomp 得子组件
    
    	InnerSphereComponent = CreateDefaultSubobject<USphereComponent>(TEXT("InnerSphereComponent"));
    	InnerSphereComponent->SetSphereRadius(100);
    	
    	//设置半径
    	InnerSphereComponent->SetupAttachment(MyMeshcomp);
    	InnerSphereComponent->OnComponentBeginOverlap.AddDynamic(this,&AMyActor::OverLapInnerShpere);
    	//为 OverlapComp 绑定函数 HandleOverlap，基本结构为  组件名->OnComponentBeginOverlap.AddDynamic(this, &A + 本文件的名字 :: 函数名);
    
    
    	///SetSphereRadius	SetSphereRadius改变组件的半径
    	OuterSphereComponet = CreateDefaultSubobject<USphereComponent>(TEXT("OuterSphereComponet"));
    	OuterSphereComponet->SetSphereRadius(3000);
    	OuterSphereComponet->SetupAttachment(MyMeshcomp);
    
    }
    void AMyActor::BeginPlay()
    {
    	Super::BeginPlay();
    }
    
    void AMyActor::OverLapInnerShpere(UPrimitiveComponent* OverlappedComponent,AActor* 
    	OtherActor,UPrimitiveComponent* OtherComp,int32 OtherBodyIndex,
    	bool bFromSweep,const FHitResult& SweepResult)
    {
    	if (OtherActor)
    	{
    		OtherActor->Destroy();
    	}
    }
    
    // Called every frame
    void AMyActor::Tick(float DeltaTime)
    {
    	Super::Tick(DeltaTime);
    
    	TArray<UPrimitiveComponent *> OverlappingComps;
    	//UPrimitiveComponent 指的是一类组件，能拥有变换
    	//不断重复的获取发生重叠的组件，直到找到元组件，仅对支持物理作用力的对象有效
    
    	OuterSphereComponet->GetOverlappingComponents(OverlappingComps);
    	//GetOverlappingComponents (获得重叠组件)
    	//获取跟自身发生重叠的物体，并设为一个数组 获取一种类型，并存为数组
    
    	//OverlappingComps.Num()数组的长度
    	for (int32 i = 0; i < OverlappingComps.Num(); i++)
    	{
    		UPrimitiveComponent* PrimComp = OverlappingComps[i];
    		//声明一个 UPrimitiveComponent 类型的指针指向 OverlappingComps数组
    
    		if (PrimComp && PrimComp->IsSimulatingPhysics())
    		{
    			const float SphereRadius = OuterSphereComponet->GetScaledSphereRadius();
    			const float ForceStrength = -2000;
    			//声明一个Float类型的变量
    			PrimComp->AddRadialForce(GetActorLocation(), SphereRadius, ForceStrength, ERadialImpulseFalloff::RIF_Constant, true);
    			//给物体施加一个力
    		}
    	}  
    }

创建类

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181114173250314.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181114173330748.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)

添加静态网格物体

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181114173416309.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)


特别注意一定要勾选GenerateOverlapEvwnts


![在这里插入图片描述](https://img-blog.csdnimg.cn/20181114173529457.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)

实现效果

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181114174033519.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)


**仅供参考**
