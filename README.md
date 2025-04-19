import pygame
import random

# Initialize pygame
pygame.init()

# Set up screen
screen = pygame.display.set_mode((800, 600))
pygame.display.set_caption("Voxel-like Game")

# Colors
WHITE = (255, 255, 255)
GREEN = (0, 255, 0)
BROWN = (139, 69, 19)

# Player class (just a basic rectangle for now)
class Player(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image = pygame.Surface((50, 50))
        self.image.fill(GREEN)
        self.rect = self.image.get_rect()
        self.rect.center = (400, 300)
        self.speed = 5

    def update(self):
        keys = pygame.key.get_pressed()
        if keys[pygame.K_LEFT]:
            self.rect.x -= self.speed
        if keys[pygame.K_RIGHT]:
            self.rect.x += self.speed
        if keys[pygame.K_UP]:
            self.rect.y -= self.speed
        if keys[pygame.K_DOWN]:
            self.rect.y += self.speed

# Voxel block class (representing a simple block)
class Voxel(pygame.sprite.Sprite):
    def __init__(self, x, y, color):
        super().__init__()
        self.image = pygame.Surface((50, 50))
        self.image.fill(color)
        self.rect = self.image.get_rect()
        self.rect.x = x
        self.rect.y = y

# Setup sprite groups
all_sprites = pygame.sprite.Group()
voxels = pygame.sprite.Group()

# Create player
player = Player()
all_sprites.add(player)

# Create some voxels
for i in range(10):
    for j in range(10):
        voxel = Voxel(i * 50, j * 50, BROWN)
        voxels.add(voxel)
        all_sprites.add(voxel)

# Game loop
running = True
clock = pygame.time.Clock()

while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Update
    all_sprites.update()

    # Drawing
    screen.fill(WHITE)
    all_sprites.draw(screen)

    # Update the display
    pygame.display.flip()

    # Frame rate
    clock.tick(60)

# Quit pygame
pygame.quit()
