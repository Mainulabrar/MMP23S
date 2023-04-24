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

        start_time = time.time()
        getBinFunc(x, edges)
        end_time = time.time()

        times.append(end_time - start_time)

    return times

linear_times = benchmark(getBinLinear)
binary_times = benchmark(getBinBinary)

plt.plot(linear_times, label='Linear Search')
plt.plot(binary_times, label='Binary Search')
plt.xlabel('Array Size')
plt.ylabel('Time (seconds)')
plt.legend()
plt.show()
```
