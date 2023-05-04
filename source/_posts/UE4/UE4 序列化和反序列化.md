---
title: UE4 序列化和反序列化
date: 2023-03-24 21:00:00
tags: [UE4]
categories: [UE4]
---

序列化和反序列化


	所需头文件
	#include "CoreMinimal.h"
	#include "Serialization/ObjectAndNameAsStringProxyArchive.h"

<!-- more -->

处理保存数据

	// 创建写入器
	FMemoryWriter MemoryWriter(ObjectData, true);
	
	// 创建翻译器
	FObjectAndNameAsStringProxyArchive Ar(MemoryWriter, false);
	
	// 设置翻译器标识
	Ar.ArIsSaveGame = true;
	Ar.ArNoDelta = true;
	
	// 将 Object 写入 ObjectData
	Object->Serialize(Ar);

<!--  -->

处理加载数据

	// 创建阅读器
	FMemoryReader MemoryReader(ObjectData, true);
	
	// 创建翻译器
	FObjectAndNameAsStringProxyArchive Ar(MemoryReader, false);
	
	// 设置翻译器标识
	Ar.ArIsSaveGame = true;
	Ar.ArNoDelta = true;
	
	// 将 ObjectData 写入 Object
	Object->Serialize(Ar);

保存和加载的区别, 保存时使用 FMemoryWriter, 加载时使用 FMemoryReader

Object：要保存的带有变量值的类的实例

ObjectData：将要写入文件或从文件中读取的字节数组，它的类型为`TArray<uint8>`

ArIsSaveGame：

- true：仅将 SaveGame 为 true 的属性进行序列化

- false：不进行 SaveGame 检查，将所有属性进行序列化

ArNoDelta：如果一个属性在序列化时检测为默认值，那么即使它拥有 UPROPERTY(SaveGame) 标识也不会序列化。为了使具有默认值的属性也依旧能够被序列化，将此值设置为 true