
FString 转 Int 

	int IntVal = FCString::Atoi(*StrVal);  

Int 转 FString:

	FString StrVal = FString::FromInt(IntVal);

FString 转 Float

	float FloatVal = FCString::Atof(*StrVal);  

Float 转 FString

	FString StrVal = FString::SanitizeFloat(FloatVal);  

FString 转 FText

	FText TextVal = FText::FromString(StrVal);  

FText 转 FString

	FString StrVal = TextVal.ToString();  		

FString 转 FName

	FName NameVal = FName(*StrVal);

FName 转 FString

	FString StrVal = NameVal.ToString();

FString 转 TCHAR*

	TCHAR CharVal = *StrVal;

TCHAR* 转 FString


FString 转 std::string

	std::string std::strVal(TCHAR_TO_UTF8(*StrVal));

std::string 转 FString

	FString StrVal(std::strVal.c_str());

注：
	
	FText 转 FName

	需先转 FString，再转 FName

	FName 转 FText

	TextVal = FText::FromName(NameVal);