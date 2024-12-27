#导入库
import pygame
import sys
#初始化
pygame.init()                

#窗口大小
screen = pygame.display.set_mode((1500,800))

#标题
pygame.display.set_caption("智能轮椅")         

#颜色
color=(127,127,127) 

#导入图片区
lunyi=pygame.image.load(r"image\轮椅.png")
ren=pygame.image.load(r"image\人.png")
wenzi1=pygame.image.load(r"image\文字.png")
qiangbi=pygame.image.load(r"image\墙壁.png")
lunyiren=pygame.image.load(r"image\轮椅人.png")
waimai=pygame.image.load(r"image\外卖.png")
wenzi2=pygame.image.load(r"image\文字2.png")
#转为rect区
renrect=ren.get_rect()
lunyirect=lunyi.get_rect()
wenzi1rect=wenzi1.get_rect()
qiangbirect=qiangbi.get_rect()
lunyirenrect=lunyiren.get_rect()
waimairect=waimai.get_rect()
wenzi2rect=wenzi2.get_rect()
#mask


#设置坐标与大小区
lunyirect.x=150
lunyirect.y = 650
renrect.x = 0
renrect.y = 600                     
lunyirenrect.x=210
lunyirenrect.y=610
waimairect.x=400
waimairect.y=200
wenzi1rect.x = 0
wenzi1rect.y = 0
qiangbirect.x = 0
qiangbirect.y = 0
wenzi2rect.x=1000
wenzi2rect.y=1000
lunyi=pygame.transform.scale(lunyi,(200,150))
lunyiren=pygame.transform.scale(lunyiren,(200,100))
waimai=pygame.transform.scale(waimai,(100,100))
qiangbi=pygame.transform.scale(qiangbi,(1500,800))

#设置变量区
guanqia=0
a=0
b=0


#无限循环
while True:                                                      
#检测区
    for event in pygame.event.get():                
        if event.type==pygame.QUIT:                
            sys.exit()
            pygame.quit()
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_d:
                a=10
            if event.key == pygame.K_w:
                b=-10
            if event.key == pygame.K_s:
                b=10
            elif event.key==pygame.K_a:
                a=-10
        elif event.type==pygame.KEYUP:
            a=0
            b=0
        
    lunyirenrect.x += a
    lunyirenrect.y += b
    lunyirect.x += a
    renrect.x += a
    lunyirect.y+=b
    renrect.y+=b                                                                                                                    
#刷新区
    screen.fill(color)
    screen.blit(qiangbi,qiangbirect)
    screen.blit(ren,renrect)    
    screen.blit(lunyi,lunyirect)
    screen.blit(waimai,waimairect)
    screen.blit(lunyiren,lunyirenrect)
    screen.blit(wenzi2,wenzi2rect)
    """#颜色检测
    pix = pygame.PixelArray(screen)
    pix1 = pix[lunyirenrect.x:lunyirenrect.x + lunyirenrect.width,lunyirenrect.y:lunyirenrect.y + lunyirenrect.height]
    pygame.PixelArray.close(pix)
    if pygame.Color('black') in pix1:
        print("碰到黑色")"""
    #碰撞
    waimaimask = pygame.mask.from_surface(waimai)
    lunyirenmask = pygame.mask.from_surface(lunyiren)
    offset = (waimairect.x - lunyirenrect.x,waimairect.y - lunyirenrect.y)
    if waimaimask.overlap(lunyirenmask,offset):
        wenzi2rect.x=100
        wenzi2rect.y=200
        renrect.x = 10
        renrect.y = 200
        qiangbirect.x=0
        qiangbirect.y=0
        lunyirect.x=150
        lunyirect.y = 650
        lunyirenrect.x=210
        lunyirenrect.y=610
    pygame.display.flip()

    
    



