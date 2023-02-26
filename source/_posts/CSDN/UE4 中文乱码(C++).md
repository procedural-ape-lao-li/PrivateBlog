<br>
创建一个变量

    
    .h
    UPROPERTY(BlueprintReadOnly, Category = "IndividualWord")
    TArray<FString> strChina;
    
    
	.cpp
	strChina.Push(UTF8_TO_TCHAR("加快"));
	strChina.Push(UTF8_TO_TCHAR("能力"));
	strChina.Push(UTF8_TO_TCHAR("有能力的"));
	
<br>

调用![在这里插入图片描述](https://img-blog.csdnimg.cn/20181104103211606.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx,size_16,color_FFFFFF,t_70)
<br>

打印

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181104103051565.png)
	

