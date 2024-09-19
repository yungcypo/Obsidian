# Pygame
[Pygame](https://www.pygame.org/news) is set of [Python](./Python.md) modules designed for writing games  

# Initialization
> Note: Before using Pygame, make sure to install it via console (`pip install pygame` or `pacman -S python-pygame`, depending on your system)  

```python
import pygame

pygame.init()
CLOCK = pygame.time.Clock()
FPS = 60
W, H = 1280, 720
SCREEN = pygame.display.set_mode((W, H))
TITLE = pygame.display.set_caption("PyngPong")
```

Displaying custom icon

```python
ICON = pygame.image.load("assets\images\icon.png")
pygame.display.set_icon(ICON)
```

## Game loop
```python
while True:
	# event handling
	# updating elements

    CLOCK.tick(FPS)
    pygame.display.update()
```

### Event handling
Example on handling events  
Put it inside Game loop  
```python
for event in pygame.event.get():
    if event.type == pygame.QUIT:
	    pygame.quit()
        sys.exit()
    if event.type == pygame.KEYDOWN:
        if event.key == pygame.K_ESCAPE:
            # event on pressing <esc>
```

