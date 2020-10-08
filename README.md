# TileTraveller2
Repo for Assignment 13 in T-111-PROG, Reykjavík University

## Question 1
```py
i = {"n":0,"e":1, "s":2, "w":3}
d = ("(N)orth","(E)ast","(S)outh","(W)est")
m = [(0,-1),(1,0),(0,1),(-1,0)]

class Tile:
    def __init__(self, n=False, e=False, s=False, w=False, leaver=False):
        self.dirs = [d[x]for x,elem in enumerate((n,e,s,w)) if elem]
        self.possible = (n,e,s,w)
        self.leaver = leaver
    
    def __str__(self):
        return " or ".join(self.dirs)
    
    __repr__ = __str__

l = [
    [Tile(0,1,1,0,0), Tile(0,1,0,1,1), Tile(0,0,1,1,0)],
    [Tile(1,1,1,0,1), Tile(0,0,1,1,1), Tile(1,0,1,0,1)],
    [Tile(1,0,0,0,0), Tile(1,0,0,0,0), Tile(0,0,0,0,0)]
]

X,Y=0,2
t = l[Y][X]
coins = 0
while str(t) != "":
    print("You can travel: {}.".format(t))
    ans = input("Direction: ").lower()
    if ans in i:
        if t.possible[i[ans]]:
            x,y = m[i[ans]]
            X+=x
            Y+=y
            t=l[Y][X]
            if t.leaver:
                if input("Pull a lever (y/n): ").lower() == "y":
                    coins+=1
                    print("You received 1 coin, your total is now {}.".format(coins))
        else:
            print("Not a valid direction!")
            t.leaver=False
    else:
        print("Not a valid direction!")
        t.leaver=False
print("Victory! Total coins {}.".format(coins))
```
## Question 2
```py
i = {"n":0,"e":1, "s":2, "w":3}
d = ("(N)orth","(E)ast","(S)outh","(W)est")
m = [(0,-1),(1,0),(0,1),(-1,0)]

class Tile:
    def __init__(self, n=False, e=False, s=False, w=False, leaver=False):
        self.dirs = [d[x]for x,elem in enumerate((n,e,s,w)) if elem]
        self.possible = (n,e,s,w)
        self.leaver = leaver
    
    def __str__(self):
        return " or ".join(self.dirs)
    
    __repr__ = __str__

l = [
    [Tile(0,1,1,0,0), Tile(0,1,0,1,1), Tile(0,0,1,1,0)],
    [Tile(1,1,1,0,1), Tile(0,0,1,1,1), Tile(1,0,1,0,1)],
    [Tile(1,0,0,0,0), Tile(1,0,0,0,0), Tile(0,0,0,0,0)]
]

def game():
    X,Y=0,2
    t = l[Y][X]
    coins = 0
    while str(t) != "":
        print("You can travel: {}.".format(t))
        ans = input("Direction: ").lower()
        if ans in i:
            if t.possible[i[ans]]:
                x,y = m[i[ans]]
                X+=x
                Y+=y
                t=l[Y][X]
                if t.leaver:
                    if input("Pull a lever (y/n): ").lower() == "y":
                        coins+=1
                        print("You received 1 coin, your total is now {}.".format(coins))
            else:
                print("Not a valid direction!")
                t.leaver=False
        else:
            print("Not a valid direction!")
            t.leaver=False
    print("Victory! Total coins {}.".format(coins))

game()
while input("Play again (y/n): ").lower() == "y": game()
```
## Question 3
```py
from random import seed, choice

i = {"n":0,"e":1, "s":2, "w":3}
d = ("(N)orth","(E)ast","(S)outh","(W)est")
m = [(0,-1),(1,0),(0,1),(-1,0)]

seed(int(input("Input seed: ")))

def rinput(s):
    c=None
    if "(y/n)" in s:
        c = choice("yn")
    else:
        c = choice([*i.keys()])
    print(s + c)
    return c

class Tile:
    def __init__(self, n=False, e=False, s=False, w=False, leaver=False):
        self.dirs = [d[x]for x,elem in enumerate((n,e,s,w)) if elem]
        self.possible = (n,e,s,w)
        self.leaver = leaver
    
    def __str__(self):
        return " or ".join(self.dirs)
    
    __repr__ = __str__

l = [
    [Tile(0,1,1,0,0), Tile(0,1,0,1,1), Tile(0,0,1,1,0)],
    [Tile(1,1,1,0,1), Tile(0,0,1,1,1), Tile(1,0,1,0,1)],
    [Tile(1,0,0,0,0), Tile(1,0,0,0,0), Tile(0,0,0,0,0)]
]

def game():
    X,Y=0,2
    t = l[Y][X]
    coins = 0
    moves = 0
    while str(t) != "":
        moves+=1
        print("You can travel: {}.".format(t))
        ans = rinput("Direction: ").lower()
        if ans in i:
            if t.possible[i[ans]]:
                x,y = m[i[ans]]
                X+=x
                Y+=y
                t=l[Y][X]
                if t.leaver:
                    if rinput("Pull a lever (y/n): ").lower() == "y":
                        coins+=1
                        print("You received 1 coin, your total is now {}.".format(coins))
            else:
                print("Not a valid direction!")
                #t.leaver=False
        else:
            print("Not a valid direction!")
            #t.leaver=False
    print("Victory! Total coins {}. Moves {}.".format(coins, moves))

game()
while input("Play again (y/n): ").lower() == "y": game()
```
