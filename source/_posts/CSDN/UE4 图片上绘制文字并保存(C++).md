.h

    // Fill out your copyright notice in the Description page of Project Settings.
    
    #pragma once
    
    #include "CoreMinimal.h"
    #include "GameFramework/HUD.h"
    #include "Engine/Canvas.h"
    #include <Engine/CanvasRenderTarget2D.h>
    #include "MyHUD.generated.h"
    
    /**
     * 
     */
    UCLASS()
    class MYPROJECT_API AMyHUD : public AHUD
    {
    	GENERATED_BODY()	
    	
    public:
    
    	AMyHUD();
    
    	virtual void BeginPlay() override;
    
    protected:
    	//字体
    	UFont * FindFont;
    	//图片
    	UTexture*  FindTexture;
    
    	FCanvasIcon  FindIcons;
    
    protected:
    	//
    	void TomDrawHUD();
    	
    	//绘制画布和文字，绑定在一事件上
    	UFUNCTION()
    	void OnCanvasUpdate(UCanvas* InCanvas, int32 Width, int32 Height);
    
    	//保存UTextureRenderTarget2D到本地文件
    	static bool SaveRenderTargetToFile(UTextureRenderTarget2D* rt, const FString& fileDestination);
    };

.cpp

    // Fill out your copyright notice in the Description page of Project Settings.
    
    #include "MyHUD.h"
    #include <ConstructorHelpers.h>
    #include <FileHelper.h>
    #include <ImageUtils.h>
    #include "Engine/CanvasRenderTarget2D.h"
    #include <Engine/Engine.h>
    
    // 在图片上绘制文字
    
    AMyHUD::AMyHUD()
    {
    	// 加载图片 // 仅供参考还有一种加载图片方式
    	static ConstructorHelpers::FObjectFinder<UTexture> FindTextureOb(TEXT("/Game/UI/One"));
    	FindTexture= FindTextureOb.Object;
    	// FindIcons= UCanvas::MakeIcon(FindTextureOb, 0, 0, 0, 0);
    
    	// 加载字体
    	static ConstructorHelpers::FObjectFinder<UFont> FindFontOb(TEXT("/Game/UI/Roboto51_Font"));
    	FindFont= FontOb.Object;
    }   
    
    void AMyHUD::DrawHUD ()
    {
    	Super::DrawHUD ();
    	// 开始绘制，只是参考，如果一直创建画布的话会很卡的（此函数每贞调用）
    	CanvasRender->UpdateResource();
    }
    
    void AMyHUD::BeginPlay()
    {
    	Super::BeginPlay();
    	TomDrawHUD();
    }
    
    void AMyHUD::TomDrawHUD()
    {
    
    	// 1. CanvasRenderTarget2D呈现目标.使用CreateCanvasRenderTarget2D()建呈现目标纹理. 创建画布
    	UCanvasRenderTarget2D* CanvasRender = Cast<UCanvasRenderTarget2D>(UCanvasRenderTarget2D::CreateCanvasRenderTarget2D(this, UCanvasRenderTarget2D::StaticClass(), 1920, 1080));
    
    	// 2. 将函数绑定到OnCanvasRenderTargetUpdate委托，在更新呈现目标时调用该委托。
    
    	CanvasRender->OnCanvasRenderTargetUpdate.AddDynamic(this, &AMyHUD::OnCanvasUpdate);
    }
    
    
    void AMyHUD::OnCanvasUpdate(UCanvas* InCanvas, int32 Width, int32 Height)
    {
	// 把图片绘制到画板上 
	InCanvas->K2_DrawTexture(加载图片的路径, FVector2D(0, 0), FVector2D(图片的宽, 图片的高（可以自定义）), UV坐标：FVector2D(0, 0), FVector2D(1, 1));

	//加载系统字体
	UObject* DefaultFontRes = StaticLoadObject(UFont::StaticClass(), nullptr, TEXT("Font'/Engine/EngineFonts/Roboto.Roboto'"));
	UFont* DefaultFont = Cast<UFont>(DefaultFontRes);

	// 3. 用 ProjectWorldToScreen(3D -> 2D);
	FVector2D ScreenPos;
	UGameplayStatics::ProjectWorldToScreen(Controller,3D坐标, 2D坐标（ScreenPos）);

	// 绘制的名字
	InCanvas->K2_DrawText(DefaultFont, 要绘制的文字, ScreenPos, FLinearColor::Red);
	
	// 保存
    if (InCanvas)
    {
    	SaveRenderTargetToFile(InCanvas, TEXT("保存位置格式"));
    }
	}
   
    
    
     // 保存绘制好的图片
     bool APanelAssembly::SaveRenderTargetToFile(UTextureRenderTarget2D* TextureRender, const FString& FileDestination)
    {
    	FTextureRenderTargetResource* Resource = TextureRender->GameThread_GetRenderTargetResource();
    
    	FReadSurfaceDataFlags ReadPixelFlags(RCM_UNorm);
    
    	TArray<FColor> OutBMP;
    	OutBMP.AddUninitialized(TextureRender->GetSurfaceWidth() * TextureRender->GetSurfaceHeight());
    	Resource->ReadPixels(OutBMP, ReadPixelFlags);
    
    	FIntPoint DestSize(TextureRender->GetSurfaceWidth(), TextureRender->GetSurfaceHeight());
    	TArray<uint8> CompressedBitmap;
    	FImageUtils::CompressImageArray(DestSize.X, DestSize.Y, OutBMP, CompressedBitmap);
    
    	bool ImageSavedOk = FFileHelper::SaveArrayToFile(CompressedBitmap, *FileDestination);
    	
    	return ImageSavedOk;
    }


警告：想要绘制画布只能在 DrawHUD 函数运行时调用。

仅供参考！！！

	.AddDynamic(函数);// 绑定函数
	.RemoveDynamic(函数);// 函数绑定
