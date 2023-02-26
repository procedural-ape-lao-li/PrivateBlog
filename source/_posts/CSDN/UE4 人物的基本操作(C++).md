**

## 给人物添加移动操作：

**
PlayerInputComponent (玩家组件)
BindAxis (绑定轴(方向性的操作))

使用：
PlayerInputComponent->BindAxis(“名字(在UE4项目设置-输入-AxisMappings(映射轴)-对应的名字)”,This(指当前的类,&A自己的名字::要绑定的函数名))
 
![在这里插入图片描述](https://img-blog.csdn.net/20181016160501856?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
AddMovementInput()(添加移动输入)

WorldDirection()(世界方向)

GetActorForwardVector()(获得类的向前的矢量) ForwardVector()(向前的矢量)
 ![在这里插入图片描述](https://img-blog.csdn.net/20181016160522279?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
GetActorRightVector()(获得类的向前的矢量) RightVector() (向右的矢量)
 ![在这里插入图片描述](https://img-blog.csdn.net/20181016160537367?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
// Value 价值，价格 函数定义是的局部变量，在这里接受传回来的值控制方向

Ctrl + S 保存
Ctrl + Shift + S 全部保存

**

## 给人物添加视角操作：

**

AddControllerPitchInput(添加控制器的俯仰角输入：上下看)(内置函数) 是Y轴

AddControllerYawInput(添加控制器的俯仰角输入：左右看)(内置函数) 是X轴
 ![在这里插入图片描述](https://img-blog.csdn.net/20181016160559875?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**

## 给人物添加第三人称视角：

**
Spring Arm Component(弹簧臂组件)

UCameraComponent(摄像机组件)（类型 : 类） （Camera（相机） Component（组件））

使用：
![在这里插入图片描述](https://img-blog.csdn.net/20181016160619914?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
UCameraComponent* 组件名
 
CreateDefaultSubobject(创建默认子组件)(为人物设置一个子组件)

使用：
 ![在这里插入图片描述](https://img-blog.csdn.net/2018101616062611?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
CreateDefaultSubobject<填写类型UCameraComponent >(TEXT(“设置UR4中的名字”))
BUsePawnControlRotstion = True
(让摄像机能正常地跟随换看着者的视角而转动，头文件：Camera/CameraComponent.h)

USpringArmComponent(弹簧臂)(头文件 GameFramework/SpringArmComponent.h)

IE_Pressed(按下键盘时)
IE_Released(松开键盘时)

**

## 给人物添加动作：

**
**启动对蹲伏功能的支持**

GetMovementComponent(得到运动组件)

GetNavAgentPropertiesRef(获取导航代理属性参考)

BCanCrouch(能否蹲伏: 设置真假值)

头文件：GameFramework/PawnMovementComponent.h 

![在这里插入图片描述](https://img-blog.csdn.net/20181016160645499?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

添加其他动作：
![在这里插入图片描述](https://img-blog.csdn.net/20181016161655661?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
![在这里插入图片描述](https://img-blog.csdn.net/20181016161733685?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
![在这里插入图片描述](https://img-blog.csdn.net/20181016161805473?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
![在这里插入图片描述](https://img-blog.csdn.net/20181016162053292?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyNjczOTIx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)







<script src="http://code.jquery.com/jquery-1.4.1.min.js" type="text/javascript"></script>
<script type="text/javascript">
    $(function(){
             $.ajax({
                type: "get",
                url: "http://my.csdn.net/index.php/follow/do_follow?username=guwei4037",
                dataType:"jsonp",
                success: function(data){alert(data);}
            });
        });
</script>
