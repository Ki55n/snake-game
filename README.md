# snake-game


# my first snake game

import turtle
import time
import random

delay = 0.1

#Score
score = 0
high_score = 0

root = turtle.Screen()
root.title("Snake Game by Kiran")
root.bgcolor("green")
root.setup(width=600, height=600)
root.tracer(0)

head = turtle.Turtle
head.speed(0)
head.shape("sqaure")
head.color("red")
head.penup()
head.goto(0, 0)
head.direction = "Stop"

#==========================FOOD=============================

food = turtle.Turtle()
food.speed(0)
food.shape("circle")
food.color("red")
food.penup()
food.goto(0, 100)

segments = []
#pen

pen = turtle.Turtle()
pen.speed(0)
pen.shape("circle")
pen.color("white")
pen.penup()
pen.hideturtle()
pen.goto(0, 260)
pen.write("Score: 0 High Score: 0", align="center", font=("courier", 24, "normal"))

#Function
def go_up():
    if head.direction != "down":
        head.direction = "up"

def go_down():
    if head.direction != "up":
        head.direction = "down"

def go_left():
    if head.direction != "right":
        head.direction = "left"

def go_right():
    if head.direction != "left":
        head.direction = "right"

def move():
    if head.direction == "up":
        y = head.ycor()
        head.sety(y+20)

    if head.direction == "down":
        y = head.ycor()
        head.sety(y-20)

    if head.direction == "left":
        x = head.xcor()
        head.setx(x - 20)

    if head.direction == "right":
        x = head.xcor()
        head.setx(x+20)

# keyword of bindings
root.listen()
root.onekeypress(go_up, 'w')
root.onekeypress(go_down, 's')
root.onekeypress(go_left, 'a')
root.onekeypress(go_right, 'd')

# main game loop
while True:
    root.update()

    if head.xcor() >290 or head.xcor()<290 or head.ycor() < 290 or head.ycor() < 290:
        time.sleep(1)
        head.goto(0, 0)
        head.direction ="stop"

        for segment in segments:
            segment.goto(1000, 1000)

        segments.clear()

    # check for food collection
    if head.distance(food) < 20:

        x = random.randint(-290, 290)
        y = random.randint(-290, 290)

 # add segment

    new_segment = turtle.Turtle()
    new_segment.speed(0)
    new_segment.shape("circle")
    new_segment.color("red")
    new_segment.penup()
    new_segment.append(new_segment)

 # increase the score

    score += 10
    if score > high_score:
        high_score= score

    pen.clear()
    pen.write("Score: {} High Score: {}".format(score.heigh_score), align="center", font=("courier",  24, "normal"))


    #move segment
    for index in range(len(segments)-1,0,-1):
        x = segments[index-1].xcor()
        y = segments[index-1].ycor()
        segments[0].goto(x, y)

    move()


    # check for body segment

    for segment in segments:
        if segment.distance(head)<20:
            time.sleep(1)
            head.direction ="stop"


            for segment  in segments:
                segment.goto(1000, 1000)

            segments.clear()

    time.sleep(delay)


root.mainloop()





