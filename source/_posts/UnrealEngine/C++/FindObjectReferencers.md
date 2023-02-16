---
title: 获取涉及到的对象

toc: true
recommend: 2
keywords: UE4-C++
date: 2021-6-29 13:44:27
thumbnail: https://cdn.jsdelivr.net/gh/privateblogs/blogimages@master/Starry/1.jpg
tags: [UE4,C++]
categories: [UnrealEngine]
---

获取对象的引用对象，例如： 创建了一个 UTexture对象，在 UMaterial 对象中引用了 UTexture 对象，我们怎么通过 UTexture 对象获取到 UMaterial 对象呢？

<!-- more -->

Editor

	void UTextureFilterAsset::QueriedReferencerAssetData(const FString& InQueriedPath)
	{
	    UObject* QueriedObject = nullptr;
	
	    QueriedObject = LoadObject<UTexture>(this. *InQueriedPath);
	
	    if (!QueriedObject)
	    return;
	
	    TArray<FName> DiskReferences;
	
	    // Load the asset registry module
	    FAssetRegistryModule& AssetRegistryModule = FModuleManager::LoadModuleChecked<FAssetRegistryModule>(TEXT("AssetRegistry"));
	
	    // Load referencer assets
	    AssetRegistryModule.Get().GetReferencers(QueriedObject->GetOutermost()->GetFName(), DiskReferences);
	
	    // 过滤查询的 Object
	    for (FName& Reference : DiskReferences)
	    {
	        if (QueriedObject->GetOutermost()->GetFName() == Reference)
	            DiskReferences.Remove(Reference);
	    }
	
	    // Load all assets
	    TArray<FAssetData> QueriedAssetItems;
	    AssetRegistryModule.Get().GetAllAssets(QueriedAssetItems);
	
	    AssetItems.Empty();
	
	    for (int32 AssetIndex = QueriedAssetItems.Num() - 1; AssetIndex >= 0; AssetIndex--)
	    {
	        if (QuariedAssetItems[AssetIandex]. IsRedirector() && !QueriedssetItems[AssetIndaz].IsUAsset()
	        {
	            continses;
	        }
	
	        if DiskReferences.Contains(QuerledAssetItems[AssetIndex].PackageName))
	        {
	            AssetItems.Add(QueriedAssetItems[AssetIandex]);
	        }
	    }
	}


DebugGame