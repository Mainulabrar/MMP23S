```python
class func():
	def __init__(self, c0, c1):
		self.intercept = c0
		self.slope = c1
	def eval(x):
		return self.intercept + self.slope*x

class Parabola(func):
	def __init__(self, c0, c1, c2):
		func.__init__(self, c0, c1)
		self.third = c2
	def eval(x):
		return self.intercept + self.slope*x + self.third*x**2

parabola = Parabola(1, -2, 2)
print(parabola(x = 2.5))
```
