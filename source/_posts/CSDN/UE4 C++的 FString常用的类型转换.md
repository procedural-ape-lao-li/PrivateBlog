将 Int 转换为 FString:
FString NewString = FString::FromInt(MyInt);

将 Float 转换为 FString:
FString VeryCleanString = FString::SanitizeFloat(MyFloat);  

将FString转换为 Char *：
FString MyString;  
Char *MyChar = *MyString;  

将 FString 转换为 Int 
int32 MyShinyNewInt = FCString::Atoi(*MySting);  

 将 FString 转换为 Float：
float MyShinyNewFloat = FCString::Atof(*MyFloat);  

字符串切割
TArray \< FString \> StringArray;  
MyString.ParseIntoArray(StringArray, TEXT(","), false);  

字符串截取：
FString::Left(int count);  
FString::Right(int count);  
