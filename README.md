# bionicarm
import pygame
import sys

# Initialize Pygame
pygame.init()

# Define screen dimensions
screen_width = 800
screen_height = 600

# Colors
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
RED = (255, 0, 0)
GREEN = (0, 255, 0)

# Initialize screen
screen = pygame.display.set_mode((screen_width, screen_height))
pygame.display.set_caption("Bionic Arm Control")

# Bionic Arm class
class BionicArm:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        self.arm_length = 100
        self.angle = 0

    def draw(self):
        # Draw the arm (line) based on angle
        end_x = self.x + self.arm_length * pygame.math.cos(self.angle)
        end_y = self.y - self.arm_length * pygame.math.sin(self.angle)
        pygame.draw.line(screen, BLACK, (self.x, self.y), (end_x, end_y), 5)

    def rotate(self, angle_change):
        self.angle += angle_change

# Create an instance of the bionic arm
bionic_arm = BionicArm(screen_width // 2, screen_height // 2)

# Main loop
running = True
while running:
    # Handle events
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
            pygame.quit()
            sys.exit()
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                bionic_arm.rotate(-0.1)
            elif event.key == pygame.K_RIGHT:
                bionic_arm.rotate(0.1)

    # Fill the screen with white
    screen.fill(WHITE)

    # Draw the bionic arm
    bionic_arm.draw()

    # Update the display
    pygame.display.flip()

# Quit Pygame
pygame.quit()
