```python
def genBinlinear(x, edges):
    for i in range(len(edges)-1):
        if edges[i] <= x<edges[i+1]:
            return i
    if x>= edges[-i]:
        return len(edges)-1
    else:
        return -1
```
