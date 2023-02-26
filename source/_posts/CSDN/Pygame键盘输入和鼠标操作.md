    '''
    ================Pygame模拟键盘输入和鼠标操作----------------------------------------
    姓名 : 昔年
    时间 : 2018/10/9
    '''
    import sys
    
    ##初始化
    
    pygame.init()
    
    ##变量存放处
    
    size = width,height = 600,400
    bgColor = (0,0,0)
    
    ##設置界面寬高
    
    screen = pygame.display.set_mode(size)
    
    ##設置標題
    
    pygame.display.set_caption("Pygame事件")
    ~~# event_texts = []~~ 
    
    ##要在Pygame中使用文本，必须创建Font对象
    
    ##第一个参数指定字体 ，第二个参数指定字体大小
    
    font =pygame.font.Font(None,20)
    
    ##调用get_linesize()方法获得每行文本的高度
    
    line_height = font.get_linesize()
    position = 0
    screen.fill(bgColor)
    
    ##创建一个存放的文本TXT
    
    f = open("record.txt",'w')
    
    while True:
          for event in pygame.event.get():
                f.write(str(event) + '\n')
                if event.type == pygame.QUIT:
    	  # 關閉文件
                      f.close()
                      sys.exit()
    
                # render()将文本渲染成Surface对象
                # 第一个参数是带渲染的文本
                # 第二个参数指定是否消除锯齿
                # 第三个参数指定文本的颜色
                screen.blit(font.render(str(event) , True , (0,255,0)) , (0,position))
                position += line_height
                if position >= height:
                      position = 0
                      screen.fill(bgColor)
          pygame.display.flip()


一些常用鍵盤輸入操作 :


send_keys(Keys.LEFT)                  左

send_keys(Keys.RIGHT)               右

send_keys(Keys.UP)                    上

send_keys(Keys.DOWN)              下

send_keys(Keys.BACK_SPACE)     删除键（BackSpace）


send_keys(Keys.SPACE)               空格键(Space)


send_keys(Keys.TAB)                   制表键(Tab)


send_keys(Keys.ESCAPE)             回退键（Esc）


send_keys(Keys.ENTER)               回车键（Enter）


send_keys(Keys.CONTROL,’a’) 全选（Ctrl+A）


send_keys(Keys.CONTROL,’c’) 复制（Ctrl+C）


send_keys(Keys.CONTROL,’x’) 剪切（Ctrl+X）


send_keys(Keys.CONTROL,’v’) 粘贴（Ctrl+V）





列舉 ：鍵盤輸入的使用



    '''
    
    ================初学Pygame-------------------------------------------------
     姓名 : 昔年 
     时间 : 2018/10/9
    
    '''
    
        import pygame
        import sys   ##退出時要用
        from pygame.locals import * # pygame 的所有常亮名导入进来
        
        ##初始化Pygame , 待命随时调用
        
        pygame.init()
        
        ##变量存放区
        
        size = width,height = 600,400 #是一个数组
        speed = [0,0]
        bgColor = (255,255,255)
        fullscreen = False
        
        
        ##创建制定大小窗口 返回一个 Surface
        
        screen = pygame.display.set_mode(size)
        
        ##设置窗口标题
        
        pygame.display.set_caption("初次见面 , 请多多关照 ！")
        
        ##加载图片
        
        turtle = pygame.image.load("Hello.jpg(要打開的圖片名)")
        
        ##获取图片的位置
        
        position = turtle.get_rect()
        
        l_head = turtle
        r_head = pygame.transform.flip(turtle,True,False)
        
        
        ##获取当前电脑支持的分辨率
        
        a = pygame.display.list_modes()
        F11size = width,height = a[0][0],a[0][1]
        while True:
              for event in pygame.event.get():
                    if event.type == QUIT:
                          sys.exit()
                    if event.type == KEYDOWN:
                           if event.key == K_LEFT:
                                speed = [-1,0]
                                turtle = l_head
                                 
                           if event.key == K_RIGHT:
                                speed = [1,0]
                                turtle = r_head
        
                           if event.key == K_UP:
                                 speed = [0,-1]
        
                           if event.key == K_DOWN:
                                 speed = [0,1]
        
                          # 全屏设置
                           if event.key == K_F11:
                                 fullscreen = not fullscreen
                                 if fullscreen:
                                       screen = pygame.display.set_mode(F11size, FULLSCREEN | HWSURFACE)
                                 else:
                                       screen = pygame.display.set_mode(size)
                           if event.key == K_ESCAPE:
                                 fullscreen = False
                                 screen = pygame.display.set_mode(size)
                          
        
              #移动图像
              position = position.move(speed)
        
              if position.left < 0 or position.right > width:
                    # 翻转图片 第一个参数：图片 第二个参数：左右反转 第三个参数：上下反转
                    turtle = pygame.transform.flip(turtle,True,False)
                    # 翻转方向
                    speed[0] = -speed[0]
              if position.top < 0 or position.bottom > height:
                    speed[1] = -speed[1]
        
              # 填充背景
              screen.fill(bgColor)
              # 更新图像
              screen.blit(turtle,position)
              # 更新界面
              pygame.display.flip()
              # 延迟10毫秒
              pygame.time.delay(10)








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
