# chinookh-A
import pygame
pygame.init()
width=600
height=600
drawing=False

colors=[(0, 0, 0), (255, 255, 255), (255, 0, 0), (255,89, 65), (255, 0, 125),(45, 95, 255), (0, 0, 255), (150, 50, 255),(255, 0, 255), (255, 150, 200), (150, 75, 0)]

draw_color =colors[0]
draw_size=10

color_width = int(width/len(colors))

color_position=[]
for i in range(len(colors)):
    color_position.append(i * color_width)
    
window = pygame.display.set_mode([width, height])
window.fill((255,255,255))

done=False
while not done:
    
    x, y = pygame.mouse.get_pos()
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            done = True
        if event.type == pygame.MOUSEBUTTONDOWN:

            if y > 30:
                drawing = True

            else:

                for i in range (len(color_position)):
               
                    edge = color_position[i]
                    if edge < x and x < edge + color_width:
                        draw_color = colors[i] 
                
        if event.type == pygame.MOUSEBUTTONUP:
            drawing= False

        if event.type == pygame.KEYDOWN:

            if event.key == pygame.K_UP:
                draw_size+=2

            elif event.key == pygame.K_DOWN:
                draw_size-=2

            if draw_size < 2:
                draw_size = 2
            if draw_size > 100:
                draw_size = 100


    if drawing:
        pygame.draw.circle(window, (draw_color),(x, y),draw_size)
        
    for i in range (len(colors)):

        position = color_position[i]

        rect = pygame.Rect(position, 0, color_width, 30)
        pygame.draw.rect(window,colors[i],rect)

    clock.tick(30)
    pygame.display.flip()
