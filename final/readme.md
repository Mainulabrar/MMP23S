```python
import numpy as np
import matplotlib.pyplot as plt

# Load data from file
data = np.loadtxt('https://www.cdslab.org/recipes/programming/regression-predicting-future-global-land-temperature-maxlikelihood/usaTemperatureHistory.txt', skiprows=70)

# Define x-axis values as year + month/12
x = data[:, 0] + (data[:, 1] - 1) / 12

# Define y-axis values as monthly anomaly
y = data[:, 2]

# Plot monthly anomaly against time
plt.plot(x, y)
plt.xlabel('Year')
plt.ylabel('Monthly anomaly (°C)')
plt.title('Global land temperature anomaly')
plt.show()
```
using the linear likelihood regression model with gaussian knowledge:

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.optimize import minimize

# Load data from file
data = np.loadtxt('https://www.cdslab.org/recipes/programming/regression-predicting-future-global-land-temperature-maxlikelihood/usaTemperatureHistory.txt', skiprows=70)

# Define x-axis values as year + month/12
x = data[:, 0] + (data[:, 1] - 1) / 12

# Define y-axis values as monthly anomaly
y = data[:, 2]

# Define likelihood function for linear regression
def likelihood(params, x, y):
    slope, intercept = params
    yPred = slope * x + intercept
    residual = y - yPred
    sigma = np.std(residual)
    return -np.sum(np.log(1 / np.sqrt(2 * np.pi * sigma ** 2) * np.exp(-residual ** 2 / (2 * sigma ** 2))))

# Fit line to data using maximum likelihood
mask = (x >= 1970) & (x <= 2013)
xFit = x[mask]
yFit = y[mask]
paramsInit = [0, 0]
result = minimize(likelihood, paramsInit, args=(xFit, yFit))
slope, intercept = result.x

# Plot data and fitted line
year = np.arange(1700, 2051, dtype=np.float64)
plt.plot(x, y, label='Data')
plt.plot(year, slope * year + intercept, label='Fit')
plt.xlabel('Year')
plt.ylabel('Monthly anomaly (°C)')
plt.title('Global land temperature anomaly')
plt.legend()

# Predict temperature anomaly in 2050
xPred = 2050
yPred = slope * xPred + intercept
print(f'The predicted temperature anomaly in 2050 is {yPred:.2f} °C')

plt.show()
```
