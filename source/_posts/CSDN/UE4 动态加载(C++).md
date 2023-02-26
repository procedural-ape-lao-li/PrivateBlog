```cpp
UFUNCTION(BlueprintCallable)
void ScanDirectory(TArray<FString>& AllFiles, const FString & FilePath, const FString& Postfix);

UFUNCTION(BlueprintCallable)
static TArray<UObject*> FindOrLoadAssetsByPath(const FString& FilePath);
```

```cpp
// 遍历文件夹下指定类型文件

void UDynamicLoadObjectLibrary::ScanDirectory(TArray<FString>& AllFiles, const FString & FilePath, const FString& Postfix)
{
	FString SearchedFiles = FilePath + Postfix;

	TArray<FString> FindedFiles;

	/*
			------------  FindFiles  ------------

			* 使用指定的文件扩展名筛选器查找给定目录中的所有文件。
			*
			* 目录，要搜索的目录的 '''绝对路径'''。例:“C:\UE4\Image”
			*
			* 文件扩展名，如果文件扩展名是空的，或者是一个空字符串“”，那么所有的文件都会被找到。
			*
			* 所有匹配可选 FileExtension 筛选器的文件，或者所有文件(如果没有指定)。
			*
			* FindFiles( TArray<FString>& FileNames, const TCHAR* Filename, bool Files, bool Directories)
			*
			* bool Files = true 返回文件
			* bool Directories = true 返回文件夹
	*/

	IFileManager::Get().FindFiles(FindedFiles, *SearchedFiles, true, false);

	for (int i = 0; i < FindedFiles.Num(); i++)
	{
		FString SearchFile = FilePath + FindedFiles[i];

		AllFiles.Add(SearchFile);
	}
}
```

```cpp
TArray<UObject*> UDynamicLoadObjectLibrary::FindOrLoadAssetsByPath(const FString& FilePath)
{
	TArray<UObject*> LoadedObjects;

	// 加载指定路径和子路径中找到的所有文件
	// 这里的路径不是绝对路径，'/Game/Blueprint/'
	EngineUtils::FindOrLoadAssetsByPath(FilePath, LoadedObjects, EngineUtils::ATL_Regular);
	
	return LoadedObjects;
}
```

