# Problem 6

In lecture, we explored the concept of a random walk, using a set of different models of drunks. Below is the code we used for locations and fields and the base class of drunks – you should not have to study this code in detail, since you have seen it in lecture.

## Code from Lecture

```python

import pylab

class Location(object):
    def __init__(self, x, y):
        """x and y are floats"""
        self.x = x
        self.y = y

    def move(self, deltaX, deltaY):
        """deltaX and deltaY are floats"""
        return Location(self.x + deltaX, self.y + deltaY)

    def getX(self):
        return self.x

    def getY(self):
        return self.y

    def distFrom(self, other):
        ox = other.x
        oy = other.y
        xDist = self.x - ox
        yDist = self.y - oy
        return (xDist**2 + yDist**2)**0.5

    def __str__(self):
        return '<' + str(self.x) + ', ' + str(self.y) + '>'

class Field(object):
    def __init__(self):
        self.drunks = {}

    def addDrunk(self, drunk, loc):
        if drunk in self.drunks:
            raise ValueError('Duplicate drunk')
        else:
            self.drunks[drunk] = loc

    def moveDrunk(self, drunk):
        if not drunk in self.drunks:
            raise ValueError('Drunk not in field')
        xDist, yDist = drunk.takeStep()
        currentLocation = self.drunks[drunk]
        #use move method of Location to get new location
        self.drunks[drunk] = currentLocation.move(xDist, yDist)

    def getLoc(self, drunk):
        if not drunk in self.drunks:
            raise ValueError('Drunk not in field')
        return self.drunks[drunk]


import random

class Drunk(object):
    def __init__(self, name):
        self.name = name
    def __str__(self):
        return 'This drunk is named ' + self.name
```


## New code

The following function is new, and returns the actual x and y distance from the start point to the end point of a random walk.

```python
def walkVector(f, d, numSteps):
    start = f.getLoc(d)
    for s in range(numSteps):
        f.moveDrunk(d)
    return(f.getLoc(d).getX() - start.getX(),
           f.getLoc(d).getY() - start.getY())
```

## drunk variations

Here are several different variations on a drunk.

```python
class UsualDrunk(Drunk):
    def takeStep(self):
        stepChoices =\
            [(0.0,1.0), (0.0,-1.0), (1.0, 0.0), (-1.0, 0.0)]
        return random.choice(stepChoices)

class ColdDrunk(Drunk):
    def takeStep(self):
        stepChoices =\
            [(0.0,0.9), (0.0,-1.03), (1.03, 0.0), (-1.03, 0.0)]
        return random.choice(stepChoices)

class EDrunk(Drunk):
    def takeStep(self):
        ang = 2 * math.pi * random.random()
        length = 0.5 + 0.5 * random.random()
        return (length * math.sin(ang), length * math.cos(ang))

class PhotoDrunk(Drunk):
    def takeStep(self):
        stepChoices =\
                    [(0.0, 0.5),(0.0, -0.5),
                     (1.5, 0.0),(-1.5, 0.0)]
        return random.choice(stepChoices)

class DDrunk(Drunk):
    def takeStep(self):
        stepChoices =\
                    [(0.85, 0.85), (-0.85, -0.85),
                     (-0.56, 0.56), (0.56, -0.56)]
        return random.choice(stepChoices)
```

## problem

Suppose we use a simulation to simulate a random walk of a class of drunk, returning a collection of actual distances from the origin for a set of trials.

Each graph below was generated by using one of the above five classes of a drunk (UsualDrunk, ColdDrunk, EDrunk, PhotoDrunk, or DDrunk). For each graph, indicate which Drunk class is mostly likely to have resulted in that distribution of distances. Click on each image to see a larger view.

---

## Problem 6-1
2.0/2.0 points (graded)
![alt text](https://d37djvu3ytnwxt.cloudfront.net/assets/courseware/v1/27c6764619bb9956a92f1130789d3fcd/asset-v1:MITx+6.00.2x_7+1T2017+type@asset+block/files_exam2_files_6-2.png)

UsualDrunk correct

## Problem 6-2
2.0/2.0 points (graded)
![alt text](https://d37djvu3ytnwxt.cloudfront.net/assets/courseware/v1/a46c2c230e029710ef248f7f24dd5e42/asset-v1:MITx+6.00.2x_7+1T2017+type@asset+block/files_exam2_files_6-1.png)

PhotoDrunk correct

## Problem 6-3
2.0/2.0 points (graded)
![alt text](https://d37djvu3ytnwxt.cloudfront.net/assets/courseware/v1/cee7778220726f5a66df4dcdd6ee589e/asset-v1:MITx+6.00.2x_7+1T2017+type@asset+block/files_exam2_files_6-4.png)

ColdDrunk correct

## Problem 6-4
2.0/2.0 points (graded)
![alt text](https://d37djvu3ytnwxt.cloudfront.net/assets/courseware/v1/749982b14d0da5d22aeca2a0dfc71fdb/asset-v1:MITx+6.00.2x_7+1T2017+type@asset+block/files_exam2_files_6-5.png)

DDrunk correct

## Problem 6-5
2.0/2.0 points (graded)
![alt text](https://d37djvu3ytnwxt.cloudfront.net/assets/courseware/v1/1237c59b512aab31504f38ec9a0fac7d/asset-v1:MITx+6.00.2x_7+1T2017+type@asset+block/files_exam2_files_6-3.png)

EDrunk correct