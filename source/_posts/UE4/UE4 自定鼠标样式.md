---
title: UE4 自定鼠标样式
date: 2023-04-18 12:00:00
tags: [UE4]
categories: [UE4]
---

引擎版本 4.21

修改枚举（EMouseCursor）对应的鼠标样式

<!-- more -->

EMouseCursor 在 ICurves 中声明，FWindowsCursor 构造函数中加载对应鼠标样式

	namespace EMouseCursor
	{
		enum Type
		{
			/** Causes no mouse cursor to be visible */
			None,
	
			/** Default cursor (arrow) */
			Default,
	
			/** Text edit beam */
			TextEditBeam,
	
			/** Resize horizontal */
			ResizeLeftRight,
	
			/** Resize vertical */
			ResizeUpDown,
	
			/** Resize diagonal */
			ResizeSouthEast,
	
			/** Resize other diagonal */
			ResizeSouthWest,
	
			/** MoveItem */
			CardinalCross,
	
			/** Target Cross */
			Crosshairs,
	
			/** Hand cursor */
			Hand,
	
			/** Grab Hand cursor */
			GrabHand,
	
			/** Grab Hand cursor closed */
			GrabHandClosed,
	
			/** a circle with a diagonal line through it */
			SlashedCircle,
	
			/** Eye-dropper cursor for picking colors */
			EyeDropper,
	
			/** Custom cursor shape for platforms that support setting a native cursor shape. Same as specifying None if not set. */
			Custom,
	
			/** Number of cursors we support */
			TotalCursorCount
		};
	}

方法一 :

	UGameViewportClient

	// 自定义图标，创建鼠标样式 UI, 替换已有鼠标样式
	UGameViewportClient->SetVirtualCursorWidget(EMouseCursor::Type, UUserWidget*);
	
	// 控制是否使用自定义图标
	UGameViewportClient->SetUseSoftwareCursorWidgets(bool);							


方法二 :

	TSharedPtr<GenericApplication> PlatformApplication = FSlateApplication::Get().GetPlatformApplication();

	if (PlatformApplication->IsValid())
	{
		// 加载鼠标鼠标样式，文件格式 .cur
		HCURSOR CursorHandle = LoadCursorFromFile((LPCTSTR)*CurPath);

		// 修改鼠标样式，修改方式跟上面不同
		PlatformApplication->Cursor->SetTypeShape(EMouseCursor::EyeDropper, CursorHandle);
	}