import pygame
import random

pygame.init()

WIDTH, HEIGHT = 1000, 800
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Happy Women's Day 8/3")

PINK = (255, 192, 203)
WHITE = (255, 255, 255)

font = pygame.font.Font(None, 70)

heart_img = pygame.image.load("heartss.png")
heart_img.set_colorkey((255, 255, 255)) 

heart_img = pygame.transform.scale(heart_img, (30, 30)) 

background=pygame.image.load("01.jpg")
background=pygame.transform.scale(background,(WIDTH,HEIGHT))
screen.blit(background,(0,0))
pygame.display.update()
pygame.time.delay(3000)

pygame.mixer.music.load("background_music.mp3") 
pygame.mixer.music.play(-1) 

class Heart:
    def __init__(self):
        self.x = random.randint(0, WIDTH)
        self.y = random.randint(-100, -10)
        self.speed = random.uniform(2, 5)
        self.size = random.randint(20, 40)
        self.image = pygame.transform.scale(heart_img, (self.size, self.size))

    def fall(self):
        self.y += self.speed
        if self.y > HEIGHT:
            self.y = random.randint(-100, -10)
            self.x = random.randint(0, WIDTH)
            self.speed = random.uniform(2, 5)

    def draw(self):
        screen.blit(self.image, (self.x, self.y))

hearts = [Heart() for _ in range(50)]

running = True
clock = pygame.time.Clock()
while running:
    screen.fill(PINK)
    screen.blit(background,(0,0))
    
    text_surface = font.render("Happy Women's Day 8/3", True, WHITE)
    screen.blit(text_surface, (WIDTH//2 - text_surface.get_width()//2, HEIGHT//4))
    
    for heart in hearts:
        heart.fall()
        heart.draw()
    
    pygame.display.update()
    
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
    
    clock.tick(30)

pygame.quit()
