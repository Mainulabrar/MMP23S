The hypothesis is that earth's temperature-anomaly is increasing linearly. Mathematically, it can be expressed as :<br> 
y = slope*x + intercept<br>
Here, the parameters are slope and intercept.<br>
There is data scatter. We take the gaussian model for the scatter.<br>
The standard deviation sigma can be calculated from my originally-proposed deterministic model. The parameters slope and intercept are unknown and has to found using the fitting process.<br>
I need to constrain two parameters.<br>
 
Using the knowledge of the hints we write the following codes. First of all, to plot the data: 

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
using the linear likelihood regression model with gaussian noise:

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
Here, we maximized the log-likelihood instead of the likelihood because the likelihood function is the multiplication of many small probabilites. So the multiplied result can go very close to zero and cause numerical underflow, meaning computer can round it up to zero as it can not represent such a small number precisely.<br>

Using the hypothesis that the temperature anomaly is flat from the year 1970

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
    intercept = params
    yPred = intercept
    residual = y - yPred
    sigma = np.std(residual)
    return -np.sum(np.log(1 / np.sqrt(2 * np.pi * sigma ** 2) * np.exp(-residual ** 2 / (2 * sigma ** 2))))

# Fit line to data using maximum likelihood
mask = (x >= 1970) & (x <= 2013)
xFit = x[mask]
yFit = y[mask]
paramsInit = [0]
result = minimize(likelihood, paramsInit, args=(xFit, yFit))
intercept = result.x

# Plot data and fitted line
year = np.arange(1700, 2051, dtype=np.float64)
plt.plot(x, y, label='Data')
plt.plot(year, 0.0 * year + intercept, label='Fit')
plt.xlabel('Year')
plt.ylabel('Monthly anomaly (°C)')
plt.title('Global land temperature anomaly')
plt.legend()

# Predict temperature anomaly in 2050
xPred = 2050
yPred = intercept
print(f'The predicted temperature anomaly in 2050 is {yPred} °C')

plt.show()
```
Calculating the BIC

```python
import numpy as np
from scipy.optimize import minimize

# Load data from file
data = np.loadtxt('https://www.cdslab.org/recipes/programming/regression-predicting-future-global-land-temperature-maxlikelihood/usaTemperatureHistory.txt', skiprows=70)

# Define x-axis values as year + month/12
xInit = data[:, 0] + (data[:, 1] - 1) / 12

# Define y-axis values as monthly anomaly
yInit = data[:, 2]

mask = (xInit >= 1970) & (xInit <= 2013)
x = xInit[mask]
y = yInit[mask]

# Define likelihood function for linear regression with Gaussian noise
def likelihood_linear(params, x, y):
    m, b, sigma = params
    y_pred = m * x + b
    residual = y - y_pred
    log_likelihood = -0.5 * np.log(2 * np.pi * sigma ** 2) - 0.5 * residual ** 2 / sigma ** 2
    return -np.sum(log_likelihood)

# Fit linear model with Gaussian noise to data using maximum likelihood
params_init = [0, 0, 1]
result_linear = minimize(likelihood_linear, params_init, args=(x, y))
m, b, sigma = result_linear.x

# Calculate log-likelihood and BIC value for linear regression model
log_likelihood_linear = -0.5 * np.sum(np.log(2 * np.pi * sigma ** 2) + ((y - (m * x + b)) / sigma) ** 2)
n = len(x)
k_linear = 3
bic_linear = -2 * log_likelihood_linear + k_linear * np.log(n)

# Define likelihood function for flat model with Gaussian noise
def likelihood_flat(param, x, y):
    mu, sigma = param
    residual = y - mu
    log_likelihood = -0.5 * np.log(2 * np.pi * sigma ** 2) - 0.5 * residual ** 2 / sigma ** 2
    return -np.sum(log_likelihood)

# Fit flat model with Gaussian noise to data using maximum likelihood
param_init_flat = [np.mean(y), 1]
result_flat = minimize(likelihood_flat, param_init_flat, args=(x, y))
mu, sigma = result_flat.x

# Calculate log-likelihood and BIC value for flat model
log_likelihood_flat = -0.5 * np.sum(np.log(2 * np.pi * sigma ** 2) + ((y - mu) / sigma) ** 2)
k_flat = 1
bic_flat = -2 * log_likelihood_flat + k_flat * np.log(n)

# Print the BIC values for both models
print(f'BIC for linear regression model: {bic_linear:.2f}')
print(f'BIC for flat model: {bic_flat:.2f}')
```
