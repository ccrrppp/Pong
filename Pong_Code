# CodeSkulptor runs Python programs in your browser.
# Click the upper left button to run this simple demo.

# CodeSkulptor runs in Chrome 18+, Firefox 11+, and Safari 6+.
# Some features may work in other browsers, but do not expect
# full functionality.  It does NOT run in Internet Explorer.

# http://www.codeskulptor.org/


import simplegui
import random

WIDTH = 600
HEIGHT = 400
BALL_RADIUS = 20
PAD_WIDTH = 8
PAD_HEIGHT = 80
HALF_PAD_WIDTH = PAD_WIDTH / 2
HALF_PAD_HEIGHT = PAD_HEIGHT / 2
LEFT = False
RIGHT = True

ball_pos = [300,200]
ball_vel = [-2,-2]

paddle1_vel = 0
paddle2_vel = 0

paddle1_pos = 0
paddle2_pos = 0
paddle1_flag = False
paddle2_flag = False

score1 = 0
score2 = 0

direction = 0

def spawn_ball(direction):
    global ball_pos, ball_vel
    
def new_game():
    global paddle1_pos, paddle2_pos, paddle1_vel, paddle2_vel,ball_pos,ball_vel
    global score1,score2,paddle1_flag,paddle2_flag,direction
    direction += 1
    ball_pos = [300,200]
    if direction % 2 ==1:
        ball_vel = [-3,-3]
    else:
        ball_vel = [3,-3]

    paddle1_vel = 0
    paddle2_vel = 0

    paddle1_pos = 0
    paddle2_pos = 0
    paddle1_flag = False
    paddle2_flag = False
    
def draw(c):
    global score1, score2, paddle1_pos, paddle2_pos, ball_pos, ball_vel
    global paddle1_vel,paddle2_vel,paddle1_flag,paddle2_flag
    global score1,score2
    
    c.draw_line([WIDTH / 2, 0],[WIDTH / 2, HEIGHT], 1, "White")
    c.draw_line([PAD_WIDTH, 0],[PAD_WIDTH, HEIGHT], 1, "White")
    c.draw_line([WIDTH - PAD_WIDTH, 0],[WIDTH - PAD_WIDTH, HEIGHT], 1, "White")
    
    #update ball
    if ball_pos[1] <= BALL_RADIUS:
        ball_vel[1] = -ball_vel[1]
    if ball_pos[1] >= 400 - BALL_RADIUS:
        ball_vel[1] = -ball_vel[1]
    if ball_pos[0] <=BALL_RADIUS+15:
        if ball_pos[1] >= paddle1_pos and ball_pos[1] <= paddle1_pos + 100:
            ball_vel[0] = -ball_vel[0]
    if ball_pos[0] < BALL_RADIUS:
        score2 += 1
        new_game()
    if ball_pos[0] >= 600 - BALL_RADIUS - 15:
        if ball_pos[1] >= paddle2_pos and ball_pos[1] <= paddle2_pos + 100:
            ball_vel[0] = -ball_vel[0]
    if ball_pos[0] > 600 - BALL_RADIUS :
        score1 += 1
        new_game()
    #draw ball
    ball_pos[0] += ball_vel[0]
    ball_pos[1] += ball_vel[1]
    
    c.draw_circle(ball_pos, BALL_RADIUS, 2, "Red", "White")
    

    #update paddle's vertical position, keep paddle on the screen
    if paddle1_flag ==True:
#        if paddle1_pos >= 0 and paddle1_pos <= 300:
            paddle1_pos += paddle1_vel
            
    if paddle2_flag == True:
#        if paddle2_pos >= 0 and paddle2_pos <= 300:
            paddle2_pos += paddle2_vel
        
        
    #draw paddles
    c.draw_polyline([(0,paddle1_pos), (0, 100 + paddle1_pos)], 15, 'White')
    c.draw_polyline([(600, paddle2_pos), (600, 100+paddle2_pos)], 15, 'White')
    
    
    #draw scores
    mes = str(score1 / 10) +str(score1 % 10) + " : " + str(score2 / 10) +str(score2 % 10)
    c.draw_text(mes, [WIDTH / 2 -83,60], 48, "Red")
    
def keydown(key):
    global paddle1_flag, paddle2_flag
    acc = 6
    global paddle1_vel, paddle2_vel
    if key ==simplegui.KEY_MAP["down"]:
        paddle2_vel += acc
        paddle2_flag = True
    if key ==simplegui.KEY_MAP["up"]:
        paddle2_vel -= acc
        paddle2_flag = True
    if key ==simplegui.KEY_MAP["s"]:
        paddle1_vel += acc
        paddle1_flag = True
    if key ==simplegui.KEY_MAP["w"]:
        paddle1_vel -= acc
        paddle1_flag = True
    print paddle1_vel,paddle1_pos
    
    
def keyup(key):
    global paddle1_vel,paddle2_vel
    if key ==simplegui.KEY_MAP["down"]:
        paddle2_vel = 0
        paddle2_flag = False
    if key ==simplegui.KEY_MAP["up"]:
        paddle2_vel = 0
        paddle2_flag = False
    if key ==simplegui.KEY_MAP["s"]:
        paddle1_vel = 0
        paddle1_flag = False
    if key ==simplegui.KEY_MAP["w"]:
        paddle1_vel = 0
        paddle1_flag = False
def timer_handler():
    global ball_vel
    X = ball_vel[0]
    if X > 0:
        X += 1
    else:
        X -= 1
    Y = ball_vel[1] / ball_vel[0] * X
    ball_vel[0] = X
    ball_vel[1] = Y
    print ball_vel
    
#create frame
frame = simplegui.create_frame("Pong",WIDTH, HEIGHT)
frame.set_draw_handler(draw)
frame.set_keydown_handler(keydown)
frame.set_keyup_handler(keyup)
timer = simplegui.create_timer(500, timer_handler)
#start frame

new_game()
frame.start()
timer.start()
