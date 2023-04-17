```python
class ProjLocX():  
    def __init__(self, velInitX):  
        self.velInitX = velInitX # initial velocity along the x direction.  
    def getLocX(self, time):  
        """  
        Return the location of the projectile at the specific given `time` and initial velocity.  
        Input  
            time    :   An input real (float) representing the time  
                        past since the start of the projectile motion.  
        """  
        return self.velInitX * time 
    def eval(self, time): return self.getLocX(time) 
    
class ProjLocY():  
    def __init__(self, velInitY, g = 9.8):  
        self.velInitY = velInitY # initial velocity along the y direction.  
        self.gravityConstant = g # gravityConstant, 9.81 on earth.  
    def getLocY(self, time):  
        """  
        Return the location of the projectile at the specific given `time` and initial velocity.  
        Input  
            time    :   An input real (float) representing the time  
                        past since the start of the projectile motion.  
        """  
        return self.velInitY * time - 0.5 * self.gravityConstant * time**2  
    def eval(self, time): return self.getLocY(time) 
    
projLocX = ProjLocX(velInitX = 10)
projLocY = ProjLocY(velInitY = 10)

def getDiff(func, t, deltaT = 1.e-5):  
    """  
    Return the derivative of the function contained with the input `func` object.  
    The `func` object must contain a method that returns the value of the function  
    """  
    return (func.eval(t + deltaT) - func.eval(t)) / deltaT # finite differencing 

print(getDiff(projLocX, t = 1), getDiff(projLocY, t = 1)) 
```
