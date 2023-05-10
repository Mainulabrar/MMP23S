The faster code:

```python
import numpy as np
const = 256.
x = np.arange(1, 100000)
z = np.sqrt(const) * x
```

The benchmarking code:
```python
import timeit
import numpy as np

# Original code
t1 = timeit.timeit("""
import numpy as np
const = 256.
x = [i for i in range(1, 100000)]
z = np.zeros(len(x))
for i, element in enumerate(x):
    z[i] = np.sqrt(const) * x[i]
""", number=100)

# Revised code
t2 = timeit.timeit("""
import numpy as np
const = 256.
x = np.arange(1, 100000)
z = np.sqrt(const) * x
""", number=100)

print(f"Original code: {t1:.6f} seconds")
print(f"Revised code: {t2:.6f} seconds")
print(f"Performance improvement: {t1/t2:.2f}x")
```

The result:

```python
Original code: 16.272790 seconds
Revised code: 0.023326 seconds
Performance improvement: 697.63x
```
The improvement is almost 700 times.

