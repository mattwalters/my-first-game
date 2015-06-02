from random import *

spawnrate1 = 40
spawnrate2 = 70
spawnrate3 = 90
kill_count = 0
battlefield = [ 0 for i in range (40)]




class Enemy():
    def __init__(self,):
        health_check = randint(0,100)
        if health_check < spawnrate1:
            self.health = 1
        elif health_check < spawnrate2:
            self.health = 2
        elif health_check < spawnrate3:
            self.health = 3
        else:
            self.health = 4
        self.position = 0
    def move(self):
        battlefield.insert((self.position + 5), battlefield.pop(self.position))
        self.position = self.position + 5



class Defender():
    def __init__(self):
        pass
    def column_strike(self,column):
        for i in range (8):
            if battlefield[(i*5) + int(column)] != 0:
                battlefield[ (i*5) + int(column)].health -= 1
                if  battlefield[ (i*5) + int(column)].health == 0:
                    battlefield[ (i*5) + int(column)] = 0


def get_battlefield():
    battlefield_display = []
    print ('___________________')
    print ('___________________')
    print ('___________________')
    for i in range(len(battlefield)):
        if battlefield[i] == 0:
            battlefield_display.append(0)
        else:
            battlefield_display.append(battlefield[i].health)
    lower = 0
    upper = 5
    for i in range(8):
        print (battlefield_display[lower:upper])
        lower += 5
        upper +=5


def spawn():
    for i in range (5):
        spawn_check = randint(0,100)
        if spawn_check < 50:
            battlefield[i] = Enemy()
            battlefield[i].position = i
def move_team():
    for i in reversed(battlefield):
        if i != 0:
            i.move()



def get_move():
    move = input('Which column shall i strike?')
    mitchell.column_strike(move)



mitchell = Defender()

def check_lose_condition():
    for i in range(5):
        if battlefield[i+35] != 0:
            print ('The castle has been lost')
            break


while battlefield[35] == 0 and battlefield[36] == 0 and battlefield[37] == 0 and battlefield[38] == 0 and  battlefield[39] == 0:
    spawn()
    get_battlefield()
    get_move()
    move_team()
    check_lose_condition()

