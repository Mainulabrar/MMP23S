```python
def integrate(evalIntegrand, lowerLimit, upperLimit, numBin):
    h = (upperLimit-lowerLimit)/numBin
    sum = 0
    for i in range(numBin):
        sum = sum + evalIntegrand(lowerLimit + (i-1)*h + 0.5*h )
    return h*sum

import numpy as np
integrate(np.sin,0,2*np.pi,100)

class Projectile():
    gravityConstant = 9.81
    def __init__(self, initVelocity):
        self.initVelocity = initVelocity
    def getVelocity(self, time):
        return self.initVelocity - self.gravityConstant*time

projectile = Projectile(initVelocity=10)
print( "v(time=1) =", projectile.getVelocity(time=1) )
print( "Total distance traveled after 1 second: {} meters".format(integrate(projectile,0,1)))
```
