 1. 创建一个数组

		TArray<int32> IntArray;

 1. 通过同一个元素填充初始化

		IntArray.Init(10, 5);   
		
		等同于// IntArray == [10, 10, 10, 10, 10]

 1. 增加新元素

		// Add会引入临时对象，优先使用EmplaceT
		// Push提供了两个一样功能的重载函数可以分别代替Add和Emplace。
		所以无论何时使用Push比Add和Emplace更加方便了：
		
		TArray<FString> StrArr;
		
		StrArr.Add(TEXT("Hello"));
		
		StrArr.Emplace(TEXT("World"));

		StrArr.Push("Hello World");
		

 1. 追加多个元素
		
		FString Arr[] = { TEXT("of"), TEXT("Tomorrow") };
		
		StrArr.Append(Arr, ARRAY_COUNT(Arr));
		
		// StrArr == ["Hello", "World", "of", "Tomorrow"]

 1. 只有容器中不存在该元素的时候，才添加

		StrArr.AddUnique(TEXT("!"));
		
		// StrArr = ["Hello", "World", "of", "Tomorrow", "!"]
		
		StrArr.AddUnique(TEXT("!"));
		
		// StrArr没有变

 1.  插入

			StrArr.Insert(TEXT("Brave"), 1);
			
			//StrArr == ["Hello","Brave","World","of","Tomorrow","!"]

 1.  直接设置数组的元素个数 // 如果大于当前值，那么使用元素类型的默认构造函数创建新元素 // 如果小于当前值，相当于删除元素

   
			StrArr.SetNum(8);
		
			// StrArr ==["Hello","Brave","World","of","Tomorrow","!","",""]   
		
			StrArr.SetNum(6); 
			
			// StrArr ==["Hello","Brave","World","of","Tomorrow", "!"]

 

