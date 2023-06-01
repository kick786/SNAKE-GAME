# SNAKE-GAME
import pygame
import random

# Initialize the game
pygame.init()

# Set up the screen
width, height = 640, 480
screen = pygame.display.set_mode((width, height))
pygame.display.set_caption("Snake Game")

# Define colors
BLACK = (0, 0, 0)
GREEN = (0, 255, 0)
RED = (255, 0, 0)

# Define the snake and food size
snake_size = 20
food_size = 20

# Initialize the snake position and movement
snake_x = width // 2
snake_y = height // 2
snake_dx = 0
snake_dy = 0

# Initialize the food position
food_x = random.randint(0, (width - food_size) // food_size) * food_size
food_y = random.randint(0, (height - food_size) // food_size) * food_size

# Set up the clock
clock = pygame.time.Clock()

# Game loop
running = True
while running:
    # Handle events
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_UP:
                snake_dy = -snake_size
                snake_dx = 0
            elif event.key == pygame.K_DOWN:
                snake_dy = snake_size
                snake_dx = 0
            elif event.key == pygame.K_LEFT:
                snake_dx = -snake_size
                snake_dy = 0
            elif event.key == pygame.K_RIGHT:
                snake_dx = snake_size
                snake_dy = 0

    # Update snake position
    snake_x += snake_dx
    snake_y += snake_dy

    # Check collision with boundaries
    if snake_x < 0 or snake_x >= width or snake_y < 0 or snake_y >= height:
        running = False

    # Check collision with food
    if snake_x == food_x and snake_y == food_y:
        # Generate new food position
        food_x = random.randint(0, (width - food_size) // food_size) * food_size
        food_y = random.randint(0, (height - food_size) // food_size) * food_size

    # Clear the screen
    screen.fill(BLACK)

    # Draw the snake and food
    pygame.draw.rect(screen, GREEN, (snake_x, snake_y, snake_size, snake_size))
    pygame.draw.rect(screen, RED, (food_x, food_y, food_size, food_size))

    # Update the display
    pygame.display.flip()

    # Set the game speed
    clock.tick(10)

# Quit the game
pygame.quit()
