Python飞机大战代码，分五个文件存放，每个文件代表着不同的功能！

main.py

    import pygame
    import sys
    import traceback
    import myplane
    import enemy
    import bullet
    import supply
    
    from pygame.locals import *
    from random import *
    
    pygame.init()
    pygame.mixer.init()
    
    
    bg_size = width,height = 480 , 852
    screen = pygame.display.set_mode(bg_size)
    pygame.display.set_caption("打飞机！！！")
    BLACK = (0,0,0)
    GREEN = (0,0,255)
    RED = (255,0,0)
    WHITE = (255,255,255)
    
    background = pygame.image.load("masturbation/image/background.png").convert()
    
    #  载入音乐
    pygame.mixer.music.load("masturbation/bg_music/game_music.ogg")
    pygame.mixer.music.set_volume(0.2)
    bullet_sound = pygame.mixer.Sound("masturbation/bg_music/bullet.wav")
    bullet_sound.set_volume(0.2)
    bomb_sound = pygame.mixer.Sound("masturbation/bg_music/use_bomb.ogg")
    bomb_sound.set_volume(0.2)
    supply_sound = pygame.mixer.Sound("masturbation/bg_music/out_porp.ogg")
    supply_sound.set_volume(0.2)
    get_bomb_sound = pygame.mixer.Sound("masturbation/bg_music/get_bomb.ogg")
    get_bomb_sound.set_volume(0.2)
    get_bullet_sound = pygame.mixer.Sound("masturbation/bg_music/get_double_laser.ogg")
    get_bullet_sound.set_volume(0.2)
    upgrade_sound = pygame.mixer.Sound("masturbation/bg_music/achievement.ogg")
    upgrade_sound.set_volume(0.2)
    enemy3_fly_sound = pygame.mixer.Sound("masturbation/bg_music/big_spaceship_flying.ogg")
    enemy3_fly_sound.set_volume(0.2)
    enemy3_down_sound = pygame.mixer.Sound("masturbation/bg_music/enemy2_down.wav")
    enemy3_down_sound.set_volume(0.1)
    enemy2_down_sound = pygame.mixer.Sound("masturbation/bg_music/enemy3_down.wav")
    enemy2_down_sound.set_volume(0.2)
    enemy1_down_sound = pygame.mixer.Sound("masturbation/bg_music/enemy1_down.wav")
    enemy1_down_sound.set_volume(0.5)
    me_down_sound = pygame.mixer.Sound("masturbation/bg_music/game_over.ogg")
    me_down_sound.set_volume(0.2)
    
    def add_small_enemies(group1,group2,num):
          for i in range(num):
                e1 = enemy.SmallEnemy(bg_size)
                group1.add(e1)
                group2.add(e1)
    
    def add_mid_enemies(group1,group2,num):
          for i in range(num):
                e2 = enemy.MidEnemy(bg_size)
                group1.add(e2)
                group2.add(e2)
                
    def add_big_enemies(group1,group2,num):
          for i in range(num):
                e3 = enemy.BigEnemy(bg_size)
                group1.add(e3)
                group2.add(e3)
                
    def inc_speed(target, inc):
          for each in target:
                each.speed += inc
          
    
    def main():
          # 绘制分数
          score = 0
          # 难度级别
          level = 1
          
          score_font = pygame.font.Font("masturbation/font/CAIPIRINHA.woff.ttf" , 36)
          
          pygame.mixer.music.play(-1)
    
          # 生成我方飞机
          me = myplane.MyPlane(bg_size)
    
          enemies = pygame.sprite.Group()
    
          # 生成敌方小型飞机
          small_enemies = pygame.sprite.Group()
          add_small_enemies(small_enemies,enemies,15)
          
          # 生成敌方中型飞机
          mid_enemies = pygame.sprite.Group()
          add_mid_enemies(mid_enemies,enemies,5)
          
          # 生成敌方大型飞机
          big_enemies = pygame.sprite.Group()
          add_big_enemies(big_enemies,enemies,2)
          
          clock = pygame.time.Clock()
    
          # 中单图片索引
          e1_destroy_index = 0
          e2_destroy_index = 0
          e3_destroy_index = 0
          me_destroy_index = 0
    
          running = True
          
          # 用于切换图片
          switch_image = True
          
          # 用于延迟
          delay = 100
    
          # 加载暂停游戏图片
          #是否暂停游戏
          paused = False
          pause_nor_image = pygame.image.load("masturbation/image/game_pause_nor.png").convert_alpha()
          pause_pressed_image = pygame.image.load("masturbation/image/game_pause_pressed.png").convert_alpha()
          resume_nor_image = pygame.image.load("masturbation/image/game_resume_nor.png").convert_alpha()
          resume_pressed_image = pygame.image.load("masturbation/image/game_resume_pressed.png").convert_alpha()
          paused_rect = pause_nor_image.get_rect()
          paused_rect.left, paused_rect.top = width - paused_rect.width - 10 , 10
          # 默认显示
          paused_image = pause_nor_image
    
          # 全屏炸弹
          bomb_image = pygame.image.load("masturbation/image/bomb.png").convert_alpha()
          bomb_rect = bomb_image.get_rect()
          bomb_font = pygame.font.Font("masturbation/font/CAIPIRINHA.woff.ttf",48)
          bomb_num = 3
    
          # 每30秒发放一个补给包
          bomb_supply = supply.Bomb_Supply(bg_size)
          bullet_supply = supply.Bullet_Supply(bg_size)
          SUPPLY_TIME = USEREVENT
          pygame.time.set_timer(SUPPLY_TIME, 30 *1000)
          
          # 生成子弹
          bullet1 = []
          bullet1_index = 0
          BULLET1_NUM = 4
          for i in range(BULLET1_NUM):
                bullet1.append(bullet.Bullet1(me.rect.midtop))
                
          # 生成超级子弹
          bullet2 = []
          bullet2_index = 0
          BULLET2_NUM =8
          for i in range(BULLET2_NUM // 2):
                bullet2.append(bullet.Bullet2((me.rect.centerx - 30,me.rect.centery)))
                bullet2.append(bullet.Bullet2((me.rect.centerx + 30,me.rect.centery)))
                
          # 超级子弹定时器
          DOUBLE_BULLET_TIME = USEREVENT + 1
          # 是否使用超级子弹
          is_double_bullet = False
    
          # 生命数量
          life_image = pygame.image.load("masturbation/image/life_image.png").convert_alpha()
          life_rect = life_image.get_rect()
          life_num = 3
    
          # 解除我方的无敌状态
          INVINCIBLE_TIME = USEREVENT + 2
    
          # 用于阻止重复打开记录文件
          recorded = False
          # 游戏的结束画面
          gameover_font = pygame.font.Font("masturbation/font/CAIPIRINHA.woff.ttf",48)
          again_image = pygame.image.load("masturbation/image/game_Reagain.png").convert_alpha()
          again_rect = again_image.get_rect()
          gameover_image = pygame.image.load("masturbation/image/game_over.png").convert_alpha()
          gameover_rect = gameover_image.get_rect()
          
          while running:
                # 绘制背景
                screen.blit(background,(0,0))
                
                for event in pygame.event.get():
                      if event.type == QUIT:
                            pygame.quit()
                            sys.exit()
                      # 随机产生补给
                      elif event.type == SUPPLY_TIME:
                            supply_sound.play()
                            if choice([True,False]):
                                  bomb_supply.reset()
                            else:
                                  bullet_supply.reset()
                      elif event.type == DOUBLE_BULLET_TIME:
                            is_double_bullet = False
                            pygame.time.set_timer(DOUBLE_BULLET_TIME,0)
                      # 解除无敌
                      elif event.type == INVINCIBLE_TIME:
                            me.invincible = False
                            pygame.time.set_timer(INVINCIBLE_TIME, 0)
                      # 炸弹按键检测
                      elif event.type == KEYDOWN:
                            if event.key == K_SPACE:
                                  if bomb_num:
                                        bomb_num -= 1
                                        # 背景音乐停止
                                        pygame.mixer.music.stop()
                                        # 停止所有音效
                                        pygame.mixer.stop()
                                        bomb_sound.play()
                                        for each in enemies:
                                              if each.rect.bottom > 0:
                                                    each.active = False
                      # 检测鼠标
                      elif event.type == MOUSEBUTTONDOWN:
                            if event.button == 1 and paused_rect.collidepoint(event.pos):
                                  paused = not paused
                                  # 暂停时停止播放音乐和停止发放补给
                                  if paused:
                                        pygame.time.set_timer(SUPPLY_TIME, 0)
                                        pygame.mixer.music.pause()
                                        pygame.mixer.pause()
                                  else:
                                        pygame.time.set_timer(SUPPLY_TIME, 30 * 1000)
                                        pygame.mixer.music.unpause()
                                        pygame.mixer.unpause()
                      elif event.type == MOUSEMOTION:
                            if paused_rect.collidepoint(event.pos):
                                  if paused:
                                        paused_image = resume_pressed_image
                                  else:
                                        paused_image = pause_pressed_image
                            else:
                                  if paused:
                                        paused_image = resume_nor_image
                                  else:
                                        paused_image = pause_nor_image
                
                # 检测用户的键盘操作
                key_pressed = pygame.key.get_pressed()
    
                if key_pressed[K_w] or key_pressed[K_UP]:
                      me.moveUp()
                if key_pressed[K_s] or key_pressed[K_DOWN]:
                      me.moveDown()
                if key_pressed[K_a] or key_pressed[K_LEFT]:
                      me.moveLeft()
                if key_pressed[K_d] or key_pressed[K_RIGHT]:
                      me.moveRight()
    
                if life_num and not paused:           
                      # 绘制大型敌机
                      for each in big_enemies:
                            if each.active:
                                  each.move()
                                  # 大型飞机被击中时
                                  if each.hit:
                                        screen.blit(each.image_hit,each.rect)
                                        each.hit = False
                                  else:
                                        # 
                                        if switch_image:
                                              screen.blit(each.image1, each.rect)
                                        else:
                                              screen.blit(each.image2, each.rect)
                                  # 即将出现时播放音效
                                  if each.rect.bottom == -50:
                                        enemy3_fly_sound.play(-1)
                                  # 绘制血槽
                                  pygame.draw.line(screen,BLACK, (each.rect.left , each.rect.top - 5) , (each.rect.right , each.rect.top - 5) , 2)
                                  # 生命大于20%显示绿色，否则显示红色
                                  energy_remain = each.energy / enemy.BigEnemy.energy
                                  if energy_remain > 0.2:
                                        energy_color = GREEN
                                  else:
                                        energy_color = RED
                                  pygame.draw.line(screen, energy_color ,  (each.rect.left , each.rect.top - 5) , (each.rect.left + each.rect.width * energy_remain , each.rect.top - 5) , 2)
                            else:
                                  # 毁灭
                                  if not(delay % 3):
                                        if e3_destroy_index == 0:
                                              enemy3_down_sound.play()
                                        screen.blit(each.destroy_images[e3_destroy_index], each.rect)
                                        e3_destroy_index = (e3_destroy_index + 1) % 6
                                        if e3_destroy_index == 0:
                                              # 加分
                                              score += 10000
                                              enemy3_fly_sound.stop()
                                              each.reset()
                                  
                      # 绘制中型敌机     
                      for each in mid_enemies:
                            if each.active:
                                  # 大型飞机被击中时
                                  each.move()
                                  if each.hit:
                                        screen.blit(each.image_hit,each.rect)
                                        each.hit = False
                                  else:
                                        screen.blit(each.image, each.rect)
                            else:
                                  # 毁灭
                                  if not(delay % 3):
                                        if e2_destroy_index == 0:
                                              enemy2_down_sound.play()
                                        screen.blit(each.destroy_images[e2_destroy_index], each.rect)
                                        e2_destroy_index = (e2_destroy_index + 1) % 4
                                        if e2_destroy_index == 0:
                                              # 加分
                                              score += 6000
                                              each.reset()
                            
                      # 绘制小型敌机      
                      for each in small_enemies:
                            if each.active:
                                  each.move()
                                  screen.blit(each.image, each.rect)
                            else:
                                  # 毁灭
                                  if not(delay % 3):
                                        if e1_destroy_index == 0:
                                              enemy1_down_sound.play()
                                        screen.blit(each.destroy_images[e1_destroy_index], each.rect)
                                        e1_destroy_index = (e1_destroy_index + 1)  %  4
                                        if e1_destroy_index == 0:
                                              # 加分
                                              score += 1000
                                              each.reset()
    
                      # 检测飞机碰撞
                      enemies_down = pygame.sprite.spritecollide(me,enemies,False,pygame.sprite.collide_mask)
                      if enemies_down and not me.invincible:
                            me.active = False
                            for e in enemies_down:
                                  e.active = False
                            
                      
                      # 绘制我方飞机
                      if me.active:
                            if switch_image:
                                  screen.blit(me.image1,me.rect)
                            else:
                                  screen.blit(me.image2,me.rect)
                      else:
                            # 毁灭
                            if not(delay % 3):
                                  if me_destroy_index == 0:
                                        me_down_sound.play()
                                  screen.blit(me.destroy_images[me_destroy_index], me.rect)
                                  me_destroy_index = (me_destroy_index + 1) % 4
                                  if me_destroy_index == 0:
                                        life_num -= 1
                                        me.reset()
                                        pygame.time.set_timer(INVINCIBLE_TIME, 3 * 1000)
                                        # running = False
                      # 绘制剩余的生命数量
                      if life_num:
                            for i in range(life_num):
                                  screen.blit(life_image, \
                                              (width - 10 - (i + 1) * life_rect.width, height - 10 - life_rect.height))
    
                      # 绘制超级子弹补给并检测是否获得
                      if bullet_supply.active:
                            bullet_supply.move()
                            screen.blit(bullet_supply.image, bullet_supply.rect)
                            if pygame.sprite.collide_mask(bullet_supply, me):
                                  get_bullet_sound.play()
                                  is_double_bullet = True
                                  # 超级子弹限制时间18秒
                                  pygame.time.set_timer(DOUBLE_BULLET_TIME, 18 * 1000)
                                  bullet_supply.active = False
                      # 发射子弹
                      if not(delay %10):
                            bullet_sound.play()
                            if is_double_bullet:
                                  bullets = bullet2
                                  # print(len(bullets))
                                  bullets[bullet2_index + 0].reset((me.rect.centerx - 30,me.rect.centery))
                                  bullets[bullet2_index + 1].reset((me.rect.centerx + 30,me.rect.centery))
                                  bullet2_index = (bullet2_index + 2) % BULLET2_NUM
                            else:
                                  bullets = bullet1
                                  bullets[bullet1_index].reset(me.rect.midtop)
                                  bullet1_index = (bullet1_index + 1) % BULLET1_NUM
    
                      # 检测子弹是否击中敌机
                      for b in bullets:
                            if b.active:
                                  b.move()
                                  screen.blit(b.image, b.rect)
                                  enemy_hit = pygame.sprite.spritecollide(\
                                        b,enemies,False,pygame.sprite.collide_mask)
                                  if enemy_hit:
                                        b.active = False
                                        for e in enemy_hit:
                                              if e in mid_enemies or e in big_enemies:
                                                    e.hit = True
                                                    e.energy -= 1
                                                    if e.energy == 0:
                                                          e.active = False
                                              else:
                                                    e.active = False
                      # 绘制全屏炸弹补给并检测是否获得
                      if bomb_supply.active:
                            bomb_supply.move()
                            screen.blit(bomb_supply.image, bomb_supply.rect)
                            if pygame.sprite.collide_mask(bomb_supply, me):
                                  get_bomb_sound.play()
                                  if bomb_num < 3:
                                        bomb_num += 1
                                  bomb_supply.active = False
                                  
                      # 绘制分数
                      score_text = score_font.render(\
                            "Score : %s" % str(score), True , WHITE)
                      screen.blit(score_text , (20 , 10))
                      # 绘制全屏炸弹
                      bomb_text = bomb_font.render("x %d" % bomb_num,True,WHITE)
                      text_rect = bomb_text.get_rect()
                      screen.blit(bomb_image, (10, height - 10 - bomb_rect.height))
                      screen.blit(bomb_text, (20 + bomb_rect.width, height - 13 - text_rect.height))
    
                      # 根据用户的分数来增加难度
                      if level == 1 and score > 50000:
                            level = 2
                            upgrade_sound.play()
                            # 增加三架小型敌机，两架中性敌机，一架大兴敌机
                            add_small_enemies(small_enemies,enemies,3)
                            add_mid_enemies(mid_enemies,enemies,2)
                            add_big_enemies(big_enemies,enemies,1)
                            # 提高小型飞机的速度
                            inc_speed(small_enemies, 1)
                      if level == 2 and score > 300000:
                            level = 3
                            upgrade_sound.play()
                            # 增加5架小型敌机，3架中性敌机，2架大兴敌机
                            add_small_enemies(small_enemies,enemies,5)
                            add_mid_enemies(mid_enemies,enemies,3)
                            add_big_enemies(big_enemies,enemies,2)
                            # 提高小，中型飞机的速度
                            inc_speed(small_enemies, 1)
                            inc_speed(mid_enemies, 1)
                      if level == 3 and score > 600000:
                            level = 4
                            upgrade_sound.play()
                            # 增加5架小型敌机，3架中性敌机，2架大兴敌机
                            add_small_enemies(small_enemies,enemies,5)
                            add_mid_enemies(mid_enemies,enemies,3)
                            add_big_enemies(big_enemies,enemies,2)
                            # 提高小，中型飞机的速度
                            inc_speed(small_enemies, 1)
                            inc_speed(mid_enemies, 1)
                      if level == 4 and score > 1000000:
                            level = 5
                            upgrade_sound.play()
                            # 增加5架小型敌机，3架中性敌机，2架大兴敌机
                            add_small_enemies(small_enemies,enemies,5)
                            add_mid_enemies(mid_enemies,enemies,3)
                            add_big_enemies(big_enemies,enemies,2)
                            # 提高小，中，大型飞机的速度
                            inc_speed(small_enemies, 1)
                            inc_speed(mid_enemies, 1)
                            inc_speed(big_enemies, 1)
                      
                      # 切换图片
                      if not (delay % 5):
                            switch_image = not switch_image
    
                      delay -= 1
                      if not delay:
                            delay = 100
                            
                # 玩家死亡                                       
                elif life_num == 0:
                      # 背景音乐停止
                      pygame.mixer.music.stop()
                      # 停止所有音效
                      pygame.mixer.stop()
                      # 停止发放补给
                      pygame.time.set_timer(SUPPLY_TIME, 0)
                      if not recorded:
                            recorded = True
                            # 读取历史最高分
                            with open("record.txt", "r") as f:
                                  record_score = int(f.read())
                            # 如果玩家得分高于历史最高得分，归档
                            if score >record_score:
                                  with open("record.txt", "w") as f:
                                        f.write(str(score))
                      # 绘制结束画面
                      record_scorer_text = score_font.render( \
                            "Best  :  %d" % record_score, True, (255,255,255))
                      screen.blit(record_scorer_text, (50, 50))
                      gameover_text1 = gameover_font.render( \
                            "Your Scroe", True, (255,255,255))
                      gameover_text1_rect = gameover_text1.get_rect()
                      gameover_text1_rect.left, gameover_text1_rect.top = \
                                                (width - gameover_text1_rect.width) // 2, height // 3
                      screen.blit(gameover_text1, gameover_text1_rect)
                      gameover_text2 = gameover_font.render( \
                            str(score), True, (255,255,255))
                      
                      gameover_text2_rect = gameover_text2.get_rect()
                      gameover_text2_rect.left, gameover_text2_rect.top = \
                                                (width - gameover_text2_rect.width) // 2, gameover_text1_rect.bottom + 10 
                      screen.blit(gameover_text2, gameover_text2_rect)
    
                      again_rect.left, again_rect.top = \
                                       (width - again_rect.width) // 2, \
                                       gameover_text2_rect.bottom + 50
                      screen.blit(again_image, again_rect)
                      gameover_rect.left, gameover_rect.top = (width - again_rect.width) // 2,again_rect.bottom + 10
                      screen.blit(gameover_image,gameover_rect)
    
                      if pygame.mouse.get_pressed()[0]:
                            pos = pygame.mouse.get_pos()
                            if again_rect.left <pos[0] <again_rect.right \
                               and again_rect.top < pos[1] < again_rect.bottom:
                                  main()
                            elif gameover_rect.left < pos[0] < \
                                 gameover_rect.right and gameover_rect.top < pos[1] < \
                                 gameover_rect.bottom:
                                  pygame.quit()
                                  sys.exit()
                      
                # 绘制暂停按钮
                screen.blit(paused_image, paused_rect)
                
                pygame.display.flip()
                clock.tick(60)
    
    if __name__ == "__main__":
          try:
                main()
          except SystemExit:
                pass
          except:
                traceback.print_exc()
                pygame.quit()
                input()
                


enemy.py

    import pygame
    from random import *
    
    # 小型飞机的定义
    class SmallEnemy(pygame.sprite.Sprite):
          def __init__(self,bg_size):
                pygame.sprite.Sprite.__init__(self)
                self.image = pygame.image.load("masturbation/image/enemy1.png").convert_alpha()
                self.destroy_images = []
                self.destroy_images.extend([\
                        pygame.image.load("masturbation/image/enemy1_down1.png").convert_alpha(), \
                        pygame.image.load("masturbation/image/enemy1_down2.png").convert_alpha(), \
                        pygame.image.load("masturbation/image/enemy1_down3.png").convert_alpha(), \
                        pygame.image.load("masturbation/image/enemy1_down4.png").convert_alpha()  \
                        ])
                self.rect = self.image.get_rect()
                self.width,self.height = bg_size[0],bg_size[1]
                self.speed = 2
                self.active = True
                self.rect.left,self.rect.top = \
                                                   randint(0,self.width - self.rect.width),\
                                                   randint(-5 * self.height,0)
                self.mask = pygame.mask.from_surface(self.image)
          def move(self):
                if self.rect.top < self.height:
                      self.rect.top += self.speed
                else:
                      self.reset()
    
          def reset(self):
                self.active = True
                self.rect.left,self.rect.top = \
                                                   randint(0,self.width - self.rect.width),\
                                                   randint(-5 * self.height,0)
    
    # 中型飞机的定义
    class MidEnemy(pygame.sprite.Sprite):
          energy = 8
          def __init__(self,bg_size):
                pygame.sprite.Sprite.__init__(self)
                self.image = pygame.image.load("masturbation/image/enemy2.png").convert_alpha()
                self.image_hit = pygame.image.load("masturbation/image/enemy2_hit.png").convert_alpha()
                self.destroy_images = []
                self.destroy_images.extend([\
                        pygame.image.load("masturbation/image/enemy2_down1.png").convert_alpha(), \
                        pygame.image.load("masturbation/image/enemy2_down2.png").convert_alpha(), \
                        pygame.image.load("masturbation/image/enemy2_down3.png").convert_alpha(), \
                        pygame.image.load("masturbation/image/enemy2_down4.png").convert_alpha()  \
                        ])
                self.rect = self.image.get_rect()
                self.width,self.height = bg_size[0],bg_size[1]
                self.speed = 1
                self.active = True
                self.hit = False
                self.rect.left,self.rect.top = \
                                                   randint(0 , self.width - self.rect.width),\
                                                   randint(-10 * self.height , -self.height)
                self.mask = pygame.mask.from_surface(self.image)
                self.energy = MidEnemy.energy
          def move(self):
                if self.rect.top < self.height:
                      self.rect.top += self.speed
                else:
                      self.reset()
          def reset(self):
                self.active = True
                self.rect.left,self.rect.top = \
                                                   randint(0 , self.width - self.rect.width),\
                                                   randint(-10 * self.height , -self.height)
                self.energy = MidEnemy.energy
    
    # 大型飞机的定义
    class BigEnemy(pygame.sprite.Sprite):
          energy = 20
          def __init__(self,bg_size):
                pygame.sprite.Sprite.__init__(self)
                self.image1 = pygame.image.load("masturbation/image/enemy3_n1.png").convert_alpha()
                self.image2 = pygame.image.load("masturbation/image/enemy3_n2.png").convert_alpha()
                self.image_hit = pygame.image.load("masturbation/image/enemy3_hit.png").convert_alpha()
                self.destroy_images = []
                self.destroy_images.extend([\
                        pygame.image.load("masturbation/image/enemy3_down1.png").convert_alpha(), \
                        pygame.image.load("masturbation/image/enemy3_down2.png").convert_alpha(), \
                        pygame.image.load("masturbation/image/enemy3_down3.png").convert_alpha(), \
                        pygame.image.load("masturbation/image/enemy3_down4.png").convert_alpha(), \
                        pygame.image.load("masturbation/image/enemy3_down5.png").convert_alpha(), \
                        pygame.image.load("masturbation/image/enemy3_down6.png").convert_alpha()  \
                        ])
                self.rect = self.image1.get_rect()
                self.width,self.height = bg_size[0],bg_size[1]
                self.speed = 1
                self.active = True
                self.hit = False
                self.rect.left,self.rect.top = \
                                                   randint(0 , self.width - self.rect.width),\
                                                   randint(-15 * self.height , -5 * self.height)
                                                   # randint(-5 * self.height,0)
                self.mask = pygame.mask.from_surface(self.image1)
                self.energy = BigEnemy.energy
          def move(self):
                if self.rect.top < self.height:
                      self.rect.top += self.speed
                else:
                      self.reset()
          def reset(self):
                self.active = True
                self.rect.left,self.rect.top = \
                                                   randint(0 , self.width - self.rect.width),\
                                                   randint(-15 * self.height , -5 * self.height)
                self.energy = BigEnemy.energy




myplane.py


        import pygame
        class MyPlane(pygame.sprite.Sprite):
               def __init__(self,bg_size):
                     pygame.sprite.Sprite.__init__(self)
                     self.image1 = pygame.image.load("masturbation/image/hero2.png").convert_alpha()
                     self.image2 = pygame.image.load("masturbation/image/hero1.png").convert_alpha()
                     self.destroy_images = []
                     self.destroy_images.extend([\
                            pygame.image.load("masturbation/image/hero_blowup_n1.png").convert_alpha(), \
                            pygame.image.load("masturbation/image/hero_blowup_n2.png").convert_alpha(), \
                            pygame.image.load("masturbation/image/hero_blowup_n3.png").convert_alpha(), \
                            pygame.image.load("masturbation/image/hero_blowup_n4.png").convert_alpha()  \
                            ])
                     self.rect = self.image1.get_rect()
                     self.width,self.height = bg_size[0] , bg_size[1]
                     self.rect.left,self.rect.top = \
                                                  (self.width - self.rect.width) // 2, \
                                                  (self.height - self.rect.height - 40)
        
                     self.speed = 10
                     self.active = True
                     self.mask = pygame.mask.from_surface(self.image1)
                     self.invincible = False
               def moveUp(self):
                     if self.rect.top > 0:
                           self.rect.top -= self.speed
                     else:
                           self.rect.top = 0
        
               def moveDown(self):
                     if self.rect.bottom < self.height:
                           self.rect.top += self.speed
                     else:
                           self.rect.bottom = self.height
        
               def moveLeft(self):
                     if self.rect.left > 0:
                           self.rect.left -= self.speed
                     else:
                           self.rect.left = 0
        
               def moveRight(self):
                     if self.rect.right < self.width:
                           self.rect.left += self.speed
                     else:
                           self.rect.right = self.width
                           
               def reset(self):
                      self.rect.left,self.rect.top = \
                                                   (self.width - self.rect.width) // 2, \
                                                   (self.height - self.rect.height - 40)
                      self.active = True
                      self.invincible = True
    
    
    
    
    bullet.py
    
    
    import pygame
    
    class Bullet1(pygame.sprite.Sprite):
          def __init__(self , position):
                pygame.sprite.Sprite.__init__(self)
                self.image = pygame.image.load("masturbation/image/bullet1.png").convert_alpha()
                self.rect = self.image.get_rect()
                self.rect.left , self.rect.top = position
                self.speed = 12
                self.active = True
                self.mask = pygame.mask.from_surface(self.image)
    
          def move(self):
                self.rect.top -= self.speed
                if self.rect.top < 0:
                      self.active = False
    
          def reset(self,position):
                self.rect.left,self.rect.top = position
                self.active = True
    
    # 双子弹
    class Bullet2(pygame.sprite.Sprite):
          def __init__(self , position):
                pygame.sprite.Sprite.__init__(self)
                self.image = pygame.image.load("masturbation/image/bullet1.png").convert_alpha()
                self.rect = self.image.get_rect()
                self.rect.left , self.rect.top = position
                self.speed = 14
                self.active = True
                self.mask = pygame.mask.from_surface(self.image)
    
          def move(self):
                self.rect.top -= self.speed
                if self.rect.top < 0:
                      self.active = False
    
          def reset(self,position):
                self.rect.left,self.rect.top = position
                self.active = True


supply.py

                        
    import pygame
    from random import *
    
    class Bullet_Supply(pygame.sprite.Sprite):
          def __init__(self, bg_size):
                pygame.sprite.Sprite.__init__(self)
                self.image = pygame.image.load("masturbation/image/ufo1.png").convert_alpha()
                self.rect = self.image.get_rect()
                self.width, self.height = bg_size[0], bg_size[1]
                self.rect.left, self.rect.bottom = randint(0 , self.width - self.rect.width), -100
                self.speed = 5
                self.active = False
                self.mask = pygame.mask.from_surface(self.image)
    
          def move(self):
                if self.rect.top < self.height:
                      self.rect.top += self.speed
                else:
                      self.active = False
                      
          def reset(self):
                self.active = True
                self.rect.left, self.rect.bottom = randint(0 , self.width - self.rect.width), -100
    
    
    class Bomb_Supply(pygame.sprite.Sprite):
          def __init__(self, bg_size):
                pygame.sprite.Sprite.__init__(self)
                self.image = pygame.image.load("masturbation/image/ufo2.png").convert_alpha()
                self.rect = self.image.get_rect()
                self.width, self.height = bg_size[0], bg_size[1]
                self.rect.left, self.rect.bottom = randint(0 , self.width - self.rect.width), -100
                self.speed = 5
                self.active = False
                self.mask = pygame.mask.from_surface(self.image)
    
          def move(self):
                if self.rect.top < self.height:
                      self.rect.top += self.speed
                else:
                      self.active = False
                      
          def reset(self):
                self.active = True
                self.rect.left, self.rect.bottom = randint(0 , self.width - self.rect.width), -100
            

可到：https://download.csdn.net/download/qq_42673921/10746951 下载素材和源代码















