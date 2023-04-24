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
```
