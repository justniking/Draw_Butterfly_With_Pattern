# Draw_Butterfly_With_Pattern
import turtle
import math

# Initialize the turtle
turtle.speed(0)  # Fastest speed
turtle.bgcolor("white")  # Set the background color
turtle.hideturtle()  # Hide the turtle for smoother drawing
turtle.Screen().tracer(0)  # Disable animation for instant drawing
turtle.Screen().delay(0)  # No delay
turtle.screensize(1.0, 1.0)  # Set the screen size

# Global variable for animation
scale_factor = 1
increasing = True

# Function to draw the pattern behind the butterfly
def draw_pattern(scale):
    turtle.penup()
    turtle.goto(0, -60)  # Start at the center and move down by 200
    turtle.pendown()
    turtle.color("turquoise")
    for _ in range(36):
        turtle.circle(100 * scale)
        turtle.right(170)

# Function to draw the butterfly pattern
def draw_butterfly(scale):
    # Draw the butterfly
    turtle.penup()
    turtle.goto(0, 0)  # Start at the center
    turtle.pendown()
    turtle.color("yellow green", "hotpink")  # Set the stroke color and the fill color
    turtle.begin_fill()  # Begin filling
    for t_val in range(0, 6283):  # Loop from 0 to 2*pi (in hundredths)
        t = t_val / 1000  # Convert to float and scale down
        x = scale * 100 * (math.sin(t) * (math.exp(math.cos(t)) - 2 * math.cos(4 * t) - math.sin(t / 12) ** 5))
        y = scale * 100 * (math.cos(t) * (math.exp(math.cos(t)) - 2 * math.cos(4 * t) - math.sin(t / 12) ** 5))
        turtle.goto(x, y)
    turtle.end_fill()  # End filling

# Function to animate
def animate():
    global scale_factor, increasing
    turtle.clear()
    draw_pattern(scale_factor)
    draw_butterfly(scale_factor)
    turtle.Screen().update()  # Update the screen

    # Update scale_factor for next frame
    if increasing:
        scale_factor += 0.05
        if scale_factor >= 2:
            increasing = False
    else:
        scale_factor -= 0.05
        if scale_factor <= 1:
            increasing = True

    turtle.ontimer(animate, 100)  # Set the timer for the next frame

# Call animate function to start animation
animate()

# Keep the window open
turtle.done()
