---
title: UE4 序列化和反序列化
date: 2023-03-16 14:00:00
tags: [UE4]
categories: [UE4]
---

FString 转 Int 

	int IntVal = FCString::Atoi(*StrVal);  

Int 转 FString:

	FString StrVal = FString::FromInt(IntVal);

<!-- more -->

FString 转 Float

	float FloatVal = FCString::Atof(*StrVal);  

Float 转 FString

	FString StrVal = FString::SanitizeFloat(FloatVal);  

FString To double

	FCString::Atod(*StrVal);

double To FString

	FString StrVal = FString::Printf(TEXT("%.15f"), DoubleVal);

FString 转 FText

	FText TextVal = FText::FromString(StrVal);  

FText 转 FString

	FString StrVal = TextVal.ToString();  		

FString 转 FName

	FName NameVal = FName(*StrVal);

FName 转 FString

	FString StrVal = NameVal.ToString();

FString 转 std::string

	std::string std::strVal(TCHAR_TO_UTF8(*StrVal));

std::string 转 FString

	FString StrVal(std::strVal.c_str());

FString 转 TCHAR*

	TCHAR CharVal = *StrVal;

FString To const char*

	const char* Val = TCHAR_TO_ANSI(*StrVal);

FString To bool

	bool bVal = StrVal.ToBool();

注：
	
	FText 转 FName

	需先转 FString，再转 FName

	FName 转 FText

	TextVal = FText::FromName(NameVal);

TChar* 与 char* 的互相转换

	TCHAR_TO_ANSI(*StrVal)

	ANSI_TO_TCHAR(*StrVal)  

	TCHAR_TO_UTF8(*StrVal) 
 
	UTF8_TO_TCHAR(*StrVal)