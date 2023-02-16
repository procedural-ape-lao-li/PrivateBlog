参考版本 4.20

 FindPathToActorSynchronously 函数的使用方法：
 
    UNavigationSystemV1::FindPathToActorSynchronously(UObject* WorldContextObject, const FVector& PathStart, AActor* GoalActor, float TetherDistance = 50.f, AActor* PathfindingContext = NULL, TSubclassOf<UNavigationQueryFilter> FilterClass = NULL);
    
注意：使用该函数需要修改 <项目名.Build.cs> 文件的，添加  "NavigationSystem" 模块儿

    PublicDependencyModuleNames.AddRange(new string[] { "Core", "CoreUObject", "Engine", "InputCore", "NavigationSystem" });
