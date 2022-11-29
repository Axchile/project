# SNAKE GAME
#### Video Demo: [https://youtu.be/aC83N_r5UlY]
#### Description: In this singleplayer game, the user controls a moving snake using WASD keys on the keyboard. The objective is for the user to move the snake to eat fruits that appear randomly on the screen.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
Two types of fruit:

Non-flashing fruit: Worth 10 points; Flashing fruit: Gives snake a speed boost

If the snake touches itself, the game is over. 
As the snake eats more fruits, it becomes difficult to control as it grows longer and longer.
The goal is to get the highest score possible. The session’s score and highest score is shown on top of the screen.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
Project Code:

import snake_objects
import eating
from snake import *
import time

print("Welcome to the Snake Game\n")
while True:
	print("Choose difficulty levels:")
	print("1) Easy")
	print("2) Normal")
	print("3) Difficult")
	print("4) Expert")
	try:
		difficulty = int(input("Choose the corresponding number (1-4): "))
		if (difficulty > 4 or difficulty < 1):
			print("Try again.\n\n")
			continue
	except:
		print("Try again.\n\n")
		continue
	break

print("Starting the game...")
time.sleep(1)
start(difficulty)
# turtle.mainloop()


import turtle
import time
import random

# game settings
initial_delay = 0.1
delay = 0.1
difficulty = 0.001
score = 0
high_score = 0
creation_time = -1
SPECIAL_FOOD_DURATION = 10
SPECIAL_FOOD_CONDITION = 50
SPECIAL_FOOD_SCORE = 30

screen_width = 800
screen_height = 800

wn = turtle.Screen()
wn.title("Snake Game")
wn.bgcolor("black")
wn.setup(width = screen_width, height = screen_height, startx=0, starty=0)
wn.tracer(0)

#snake head
head = turtle.Turtle()
head.speed(0)
head.shape("square")
head.color("blue")
head.penup()
head.goto(0, 0)
head.direction = "stop"

#food
food = turtle.Turtle()
food.speed(0)
food.shape("circle")
food.color("green")
food.penup()
food.goto(0, 100)

#special food
s_food = turtle.Turtle()
s_food.speed(0)
s_food.shape("turtle")
s_food.color("red")
s_food.penup()
s_food.goto(screen_width+200, screen_height+200)

segments = []

#Pen
pen = turtle.Turtle()
pen.speed(0)
pen.shape("square")
pen.color("white")
pen.penup()
pen.hideturtle()
pen.goto(0, (screen_height/2) - 40)
pen.write("Score: 0 High Score: 0", align = "center", font = ("Courier", 24, "normal"))

#functions
def go_up():
	if head.direction != "down":
		head.direction = "up"

def go_down():
	if head.direction != "up":
		head.direction = "down"

def go_right():
	if head.direction != "left":
		head.direction = "right"

def go_left():
	if head.direction != "right":
		head.direction = "left"


def move():
	y = head.ycor()
	x = head.xcor()
	if head.direction == "up":
		head.sety(y + 20)

	if head.direction == "down":
		head.sety(y - 20)

	if head.direction == "right":
		head.setx(x + 20)

	if head.direction == "left":
		head.setx(x - 20)

#keyboard
wn.listen()
wn.onkey(go_up, "w")
wn.onkey(go_down, "s")
wn.onkey(go_right, "d")

from snake_objects import *
import asyncio

#functions
def go_up():
	if head.direction != "down":
		head.direction = "up"

def go_down():
	if head.direction != "up":
		head.direction = "down"

def go_right():
	if head.direction != "left":
		head.direction = "right"

def go_left():
	if head.direction != "right":
		head.direction = "left"

async def waiter(duration):
	await asyncio.sleep(duration)

from snake_objects import *

def eating_food():
	if head.distance(food) < 20:
		#move food to random place
		x = random.randint(-1*(screen_width/2-20), (screen_width/2-20))
		x = x-(x%10)
		y = random.randint(-1*(screen_height/2-20), (screen_height/2-20))
		y = y-(y%10)
		if x%20 != 0:
			x+=10
		if y%20 != 0:
			y+=10
		food.goto(x, y)

		return True

	return False
