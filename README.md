# Pong_Game
This game is made on python using the standard python libraries.
import turtle
import os

nm = turtle.Screen()
nm.title("Pong game by Neeraj")
nm.bgcolor("black")
nm.setup(width=800, height=600)
nm.tracer(0)

# Score
score_1 = 0
score_2 = 0

# Paddle 1
paddle1 = turtle.Turtle()
paddle1.speed(0)
paddle1.shape("square")
paddle1.color("white")
paddle1.shapesize(stretch_wid=5, stretch_len=1)
paddle1.penup()
paddle1.goto(-350, 0)

# Paddle 2
paddle2 = turtle.Turtle()
paddle2.speed(0)
paddle2.shape("square")
paddle2.color("white")
paddle2.shapesize(stretch_wid=5, stretch_len=1)
paddle2.penup()
paddle2.goto(350, 0)

# Ball
ball = turtle.Turtle()
ball.speed(0)
ball.shape("square")
ball.color("white")
# ball.shapesize(stretch_wid=5, stretch_len=1)
ball.penup()
ball.goto(0, 0)
ball.dx = 2
ball.dy = 2

# Pen
pen = turtle.Turtle()
pen.speed(0)
pen.shape("square")
pen.color("white")
pen.penup()
pen.hideturtle()
pen.goto(0, 260)
pen.write("Player 1: 0  Player 2: 0 ", align="center", font=("Courier", 24, "normal"))


# Function
def paddle1up():
    y = paddle1.ycor()
    y += 20
    paddle1.sety(y)


def paddle1down():
    y = paddle1.ycor()
    y -= 20
    paddle1.sety(y)


def paddle2up():
    y = paddle2.ycor()
    y += 20
    paddle2.sety(y)


def paddle2down():
    y = paddle2.ycor()
    y -= 20
    paddle2.sety(y)


# Keyboard binding

nm.listen()
nm.onkeypress(paddle1up, "w")
nm.onkeypress(paddle1down, "s")
nm.onkeypress(paddle2up, "Up")
nm.onkeypress(paddle2down, "Down")

# Main game loop
while True:
    nm.update()

    # Move the ball
    ball.setx(ball.xcor() + ball.dx)
    ball.sety(ball.ycor() + ball.dy)

    # Border Checking
    # Top and bottom
    if ball.ycor() > 290:
        ball.sety(290)
        ball.dy *= -1
        os.system("afplay bounce.wav&")

    elif ball.ycor() < -290:
        ball.sety(-290)
        ball.dy *= -1
        os.system("afplay bounce.wav&")

        # Left and right
    if ball.xcor() > 350:
        score_1 += 1
        pen.clear()
        pen.write("Player 1: {}    Player 2: {}".format(score_1, score_2), align="center",
                  font=("Courier", 24, "normal"))
        ball.goto(0, 0)
        ball.dx *= -1

    elif ball.xcor() < - 350:
        score_2 += 1
        pen.clear()
        pen.write("Player 1: {}    Player 2: {}".format(score_1, score_2), align="center",
                  font=("Courier", 24, "normal"))
        ball.goto(0, 0)
        ball.dx *= -1

    # paddle and ball collisions
    if (ball.xcor() < -340) and (ball.ycor() < paddle1.ycor() + 50) and (ball.ycor() > paddle2.ycor() - 50):
        ball.dx += -1
        os.system("afplay bounce.wav&")
