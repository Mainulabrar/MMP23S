```python
import numpy as np
def matmul(matA, matB):

    resultMat = []
    rowMatA, colMatA = len(matA), len(matA[0])
    rowMatB, colMatB = len(matB), len(matB[0])

    if colMatA != rowMatB:
        print("Matrices can't be multiplied")
        return None

    for i in range(rowMatA):
        row = []
        for j in range(colMatB):
            row.append(0)
        resultMat.append(row)

    for i in range(rowMatA):
        for j in range(colMatB):
            for k in range(colMatA):
                resultMat[i][j] += matA[i][k]*matB[k][j]

    return resultMat

matA =  [ [12, 7, 3]
        , [4 , 4, 6]
        , [5 , 3, 3]
        ]
matB =  [ [0, 1, 1, 7]
        , [6, 7, 3, 1]
        , [2, 5, 8, 3]
        ]
print(matmul(matA, matB))

import numpy as np
print(matA)
print(matB)

import time
sizes = [2,4,16,32,64,128,256,512,1024]
for n in sizes:
    matA = np.random.rand(n, n)
    matB = np.random.rand(n, n)

    startTime = time.time()
    np.matmul(matA, matB)
    npTime = time.time() - startTime
 
    startTime = time.time()
    matmul(matA,matB)
    myTime = time.time()-startTime
 
    print(f"Matrix size: {n}x{n}")
    print(f"Numpy time: {npTime:.6f} seconds")
    print(f"My time: {myTime:0.6f} seconds")
    print("-"*40)

fig, ax=plt.subplots()
ax.plot(sizes, myTimes, label = 'My Method')
ax.plot(sizes, numpyTimes, label = 'NumPy Method')
ax.set_xlabel('Matrix Rank')
ax.set_ylabel('Times(s)')
ax.set_title('Matrix Multiplication Benchmark')
ax.legend()
plt.show()

```
