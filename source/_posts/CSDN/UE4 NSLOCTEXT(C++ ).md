开发多语言程序时，经常使用：所有文字将通过本地化系统传递。

```cpp
// UE4 引擎定义了宏，使用时不需要再定义宏
LOCTEXT( In Key ,  文本文字)

// 自定义宏
#define LOCTEXT_NAMESPACE " 字符串 "
NSLOCTEXT(LOCTEXT_NAMESPACE , In Key , 文本文字)
```

