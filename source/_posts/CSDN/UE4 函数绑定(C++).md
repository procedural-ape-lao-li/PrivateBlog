DECLARE_DELEGATE_变量个数（Name，变量）

> 声明 .h
> 
> Name NewName

    绑定 .cpp
    
    NewName.BindRaw(this,要绑定的函数)
    
    NewName.ExecuteIfBound(执行绑定函数要传入的变量)
    
    注：函数变量的个数等于声明 Name 变量的个数

本人也不太会仅供参考哦！
