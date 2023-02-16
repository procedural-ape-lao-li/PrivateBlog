
"typename"是一个C++程序设计语言中的关键字。当用于泛型编程时是另一术语"class"的同义词。这个关键字用于指出模板声明（或定义）中的非独立名称（dependentnames）是类型名，而非变量名。

    template<typename T>
    class TApple
    {
    public:
    	T Add(T a, T b)
    	{
    		return a + b;
    	}
    };

Typename 关键字 告诉 编译把一个特殊的名字解释成一个类型，在下列情况下必须对一个name使用typename关键字：

1一个唯一的name(可以作为类型理解)，嵌套在另一个类型中；

2 依赖于一个模板参数，就是说模板参数在某种程度上包含这个name，当模板参数是编译器在指认一个类型时便会产生误解

为了保险起见，应该在所有编译可能错把一个type当成一个变量的地方使用typename,如果你的类型在模板参数中是有限制的，那就必须使用typename
