```python
def getBinLinear(x, edges):
    for i in range(len(edges)-1):
        if edges[i] <= x<edges[i+1]:
            return i
    if x>= edges[-i]:
        return len(edges)-1
    else:
        return -1

def getBinBinary(x, edges):
    left, right = 0, len(edges)-1
    
    while left<=right:
        mid =(left+right)//2
        
        if x<edges[mid]:
            right = mid -1
        elif x>= edges[mid+1]:
            left = mid+1
        else:
            return mid
        
    if x>=edges[-1]:
        return len(edges)-1
    else:
        return -1

import time
import random
import matplotlib.pyplot as plt

def benchmark(getBinFunc):
    times = []
    for size in range(100, 10000, 100):
        edges = range(size)
        x = random.uniform(0, size - 1)

        startTime = time.time()
        getBinFunc(x, edges)
        endTime = time.time()

        times.append(endTime - startTime)

    return times

linearTimes = benchmark(getBinLinear)
binaryTimes = benchmark(getBinBinary)

plt.plot(linearTimes, label='Linear Search')
plt.plot(binaryTimes, label='Binary Search')
plt.xlabel('Array Size')
plt.ylabel('Time (seconds)')
plt.legend()
plt.show()
```
The binary search works better when the number of elements in the array is large, whereas the linear search works better where the number of elements in the array is small. This is because the binary search has fewer iterations.
