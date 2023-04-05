1.
i) This implies only certain real numbers can be stored in the computers. All real numbers can not be stored as they are continuous.
ii) real32 can present  -3.4 x 10^38 to 3.4 x 10^38 real bumbers.
    real64 can present -1.8 x 10^308 to 1.8 x 10^308 real numbers
    real128 can represent -1.2 x 10^4932 to 1.2 x 10^4932 real numbers
ii)

2.
If we type cast an integer integer larger than 127 to the type int8 we will have an overflow and it would be truncated to 127. Similar for integers smaller than the lowest range of int8. If we put in an integer lower than -128 it will be truncated to -128.
For Matlab
```matlab
int16_min = intmin('int16')
int16_max = intmax('int16')
```
For python
```python
import numpy as np

int32_info = np.iinfo(np.int32)
int32_min = int32_info.min
int32_max = int32_info.max
```

3.
A) At first we assign an integer value 5 to the variable a. Then we assign the value of a to b using the line `b=a`. Then when we print the ID of a and b we see that they have the same ID because they refer to same memory location. As python treats integer like objects when b is assigned the same value of a, both refer to the same memory location. Next we assign the value of c to be equal to b by `c=b`. So, now c also has the same ID as a and b. But if we assign a new value to b using `b=3` , then b will have a new ID as it will refer to a new memory location. Printing a, b and c will show their respective value of 3, 5 and 3. Finally we assign b to have the same value as a again. This brings the ID of b back to be the same as a. Now if I assign b to be equal to 5 using `b=5` b still has the same ID because 5 is still the same value that b currently has. So there is no change in the memory location fo b.
B) First we create a list object a containing integer value 5. then we assign it to the variable b. Now, both a and b will have the same location. But then if we append b with the value 1. Then both of the variable will be appended as they share the same memory location. And they have the same value [5,1] and the same ID.
C) Here the first step is the same as the previous one. But the difference is this time b is list object with a as an argument. This means they have different ID even though they have the same value. It is because b is created as a different list object in a different memory location. Finally we create a new list object b and assign it a value that is the copy of the list object a. So now again b refers to a new memory location than a even though they have the same value.
D) Here the same procedure as the previous step is happenning with the only difference being a is touple object and b is touple object containing a as it's argument. But both of them have different ID all throughout the process.

4.
```bash
#!/usr/bin/env python3.5

print("This is Python version 3.5.2\n")
print("Python is the best language for String manipulation!\n")
print("!noitalupinam gnirtS rof egaugnal tseb eht si nohtyP\n")
print("!otlpnmgit o gunlte h inhy\n")
print("pYTHON IS THE BEST LANGUAGE FOR sTRING MANIPULATION!\n")

sentence = "Python is the best language for String manipulation!"
a_count = sentence.count('a')
A_count = sentence.count('A')
print("The sentence '{0}' contains\n{1} 'a' letters, and\n{2} 'A' letters!\n".format(sentence, a_count, A_count))

words = sentence.split()
print(*words, sep='\n')
print()

print(*map(str.upper, words), sep='\n')
print()
```
5. 
The result is that the numbers list ends up containing only the elements at the even-numbered indices: [0, 2, 6, 8]. This is because each time an element is deleted, the indices of the remaining elements go down by one. So the next element to be deleted is always the one that is halfway between the current index and the end of the list.

6.
This code is trying to find the smallest value for 'eps' for which 1.0+eps is no longer equal to 1.0. Here the output of the code are values of eps that are halved in each step. 1.0 ~= 1.0+ eps can be false when eps has a value that is less than less than the precision of floating point numbers. So, the number that is displayed for 1.0+eps is the closest number to the actual value of 1.0+eps which is 1.0. So then 1.0 become equal to 1.0 and the aforementioned statement become incorrect.
For the python code we do the same thing as above but in python language. The output is
```python
............... 1.0
............... 0.5
............... 0.25
............... 0.125
............... 0.0625
............... 0.03125
............... 0.015625
............... 0.0078125
............... 0.00390625
............... 0.001953125
............... 0.0009765625
............... 0.00048828125
............... 0.000244140625
............... 0.0001220703125
............... 6.103515625e-05
............... 3.0517578125e-05
final eps: 1.52587890625e-05
```

7.
```matlab
q = {{'a', 'b', 'c'}, {'d', 'e', 'f'}, {'g', 'h'}}
str = ''
for i = 1:numel(q)
    for j = 1:numel(q{i})
        str = [str q{i}{j}]
    end
end
disp(str)
```

```python
q = {{'a', 'b', 'c'}, {'d', 'e', 'f'}, {'g', 'h'}}
str = ''
for i = 1:numel(q)
    for j = 1:numel(q{i})
        str = [str q{i}{j}]
    end
end
disp(str)
```

9.
MATLAB-A)
```python
function f = fib(n)
    if ~isnumeric(n) || numel(n) ~= 1 || n < 0 || n ~= round(n)
        error('Please enter a non-negative integer');
    end
    f = getFib(n);
    runtime = timeit(@() getFib(n));
    fprintf('fib(%d) = %d\naverage runtime: %.5f seconds\n', n, f, runtime);
end

function f = getFib(n)
    if n == 0 || n == 1
        f = n;
    else
        f = getFib(n-1) + getFib(n-2);
    end
end
```
MATLAB-B)
```matlab
function f = fibLoop(n)
    if ~isnumeric(n) || numel(n) ~= 1 || n < 0 || n ~= round(n)
        error('Please enter a non-negative integer');
    end
    
    f = 0;
    a = 0;
    b = 1;
    
    tic; % start timer
    for i = 1:n
        f = a + b;
        a = b;
        b = f;
    end
    runtime = toc; % stop timer
    
    fprintf('fibLoop(%d) = %d\naverage runtime: %.5f seconds\n', n, f, runtime);
end
```
MATLAB-C)
Here are the runtime for the modified fib() function:
```matlab
Please enter a non-negative integer or type stop: 10
    fib(10) = 55
    average runtime: 1.0748e-05 seconds

Please enter a non-negative integer or type stop: 15
    fib(15) = 610
    average runtime: 7.4207e-05 seconds

Please enter a non-negative integer or type stop: 20
    fib(20) = 6765
    average runtime: 0.00079566 seconds

Please enter a non-negative integer or type stop: 25
    fib(25) = 75025
    average runtime: 0.0090159 seconds

Please enter a non-negative integer or type stop: 30
    fib(30) = 832040
    average runtime: 0.10087 seconds

Please enter a non-negative integer or type stop: 35
    fib(35) = 9227465
    average runtime: 1.1453 seconds

Please enter a non-negative integer or type stop: stop
```
Here are the runtime for the fibloop function
```matlab
Please enter a non-negative integer or type stop: 10
    fibLoop(10) = 89
    average runtime: 0.00000 seconds

Please enter a non-negative integer or type stop: 15
    fibLoop(15) = 987
    average runtime: 0.00000 seconds

Please enter a non-negative integer or type stop: 20
    fibLoop(20) = 10946
    average runtime: 0.00001 seconds

Please enter a non-negative integer or type stop: 25
    fibLoop(25) = 121393
    average runtime: 0.00017 seconds

Please enter a non-negative integer or type stop: 30
    fibLoop(30) = 1346269
    average runtime: 0.00188 seconds

Please enter a non-negative integer or type stop: 35
    fibLoop(35) = 14930352
    average runtime: 0.02322 seconds

Please enter a non-negative integer or type stop: stop
```
The fibloop functions are faster than the fib function because the fib function uses loop while the fib function uses recursion.
MATLAB-D)
Here are the output funcitons timeFib(n) timeFibloop(n)
```matlab
function output = timeFib(n)
% Calculate the nth Fibonacci number and return the runtime
if ischar(n) || ~isreal(n) || n < 0 || round(n) ~= n
    error('The input argument is not a non-negative integer!');
end

fib = fib(n);
runtime = timeit(@()fib(n));

output.n = n;
output.fib = fib;
output.runtime = runtime;

end
```
```matlab
function output = timeFibLoop(n)
% Calculate the nth Fibonacci number using a loop and return the runtime
if ischar(n) || ~isreal(n) || n < 0 || round(n) ~= n
    error('The input argument is not a non-negative integer!');
end

fib = fibLoop(n);
runtime = timeit(@()fibLoop(n));

output.n = n;
output.fib = fib;
output.runtime = runtime;

end
```
MATLAB-E)
```matlab
% Set up the range of n values
n_values = 10:2:35;

% Loop over the values and call the timeFib functions
for i = 1:length(n_values)
    n = n_values(i);
    
    % Call timeFib and write the result to file
    try
        fib_result = timeFib(n);
        fprintf('n=%d, fib=%d, runtime=%.4f s\n', fib_result.n, fib_result.fib, fib_result.runtime);
        
        fid = fopen('fibOutput.txt', 'a');
        fprintf(fid, 'n=%d, fib=%d, runtime=%.4f s\n', fib_result.n, fib_result.fib, fib_result.runtime);
        fclose(fid);
    catch ME
        fprintf('Error: %s\n', ME.message);
    end
    
    % Call timeFibLoop and write the result to file
    try
        fib_loop_result = timeFibLoop(n);
        fprintf('n=%d, fib_loop=%d, runtime=%.4f s\n', fib_loop_result.n, fib_loop_result.fib, fib_loop_result.runtime);
        
        fid = fopen('fibLoopOutput.txt', 'a');
        fprintf(fid, 'n=%d, fib_loop=%d, runtime=%.4f s\n', fib_loop_result.n, fib_loop_result.fib, fib_loop_result.runtime);
        fclose(fid);
    catch ME
        fprintf('Error: %s\n', ME.message);
    end
    
    fprintf('\n');
end
```
python-A)
```python
import time

def fib():
    while True:
        num = input("Please enter a non-negative integer or type stop: ")
        if num == "stop":
            break
        elif not num.isnumeric() or float(num) < 0:
            print("Invalid input! Please enter a non-negative integer.")
        else:
            n = int(num)
            start = time.process_time()
            res = getFib(n)
            end = time.process_time()
            print("fib({}) = {}".format(n, res))
            print("average runtime: {} seconds".format((end - start) / n))

def getFib(n):
    if n <= 1:
        return n
    else:
        return getFib(n-1) + getFib(n-2)
```
Python Part-B)
```python
import time

def fibLoop():
    while True:
        try:
            n = int(input("Please enter a non-negative integer or type stop: "))
            if n < 0:
                print("The input argument is not a non-negative integer!")
            elif n == 0:
                print("fib({0}) = 0".format(n))
                print("average runtime: 0.0 seconds")
            else:
                start_time = time.process_time()
                a, b = 0, 1
                for i in range(n-1):
                    a, b = b, a + b
                end_time = time.process_time()
                print("fib({0}) = {1}".format(n, b))
                print("average runtime: {0} seconds".format(end_time-start_time))
        except ValueError:
            if input_val.lower() == 'stop':
                break
            else:
                print("The input argument is not a non-negative integer!")
```
Python Part-C)
For fib():

fib(10) took 9.5367431640625e-07 seconds
fib(15) took 1.9073486328125e-06 seconds
fib(20) took 2.1457672119140625e-05 seconds
fib(25) took 0.00035858154296875 seconds
fib(30) took 0.0030333995819091797 seconds
fib(35) took 0.04422426223754883 seconds

For fibLoop():

fibLoop(10) took 2.86102294921875e-06 seconds
fibLoop(15) took 5.9604644775390625e-06 seconds
fibLoop(20) took 2.5033950805664062e-05 seconds
fibLoop(25) took 0.00014495849609375 seconds
fibLoop(30) took 0.0009586811065673828 seconds
fibLoop(35) took 0.012261629104614258 seconds
we can see that fibLoop are faster than fib. Because fib uses recursion where fibLoop uses loop which is faster.

10.
```matlab
function p = getLargestPrime(n)
% GETLARGESTPRIME finds the largest prime number that is smaller than n
% using a for-loop, break, and MATLAB's isprime() function.

% Start checking for primes from n-1 downwards
for p = n-1:-1:2
    if isprime(p)
        % If p is prime, return it
        return;
    end
end

% If no prime was found, return an error message
error('No prime number found smaller than %d.', n)

end
```
Python-
A) get_primes_for(n) will be
```python
def get_primes_for(n):
    count = 0
    for i in range(2, n):
        if isPrime_for(i):
            count += 1
    return count
```
isPrime_for(n)
```python
def isPrime_for(n):
    if n < 2:
        return False
    for divisor in range(2, int(n**0.5)+1):
        if n % divisor == 0:
            return False
    return True
```
B) getNumPrimes_for(n) will be slower thatn getPrimes_for(n) as it uses recursion rather than loop.

11. In Python
```python
def fib():
    while True:
        n = input("Please enter a non-negative integer or type stop: ")
        if n == "stop":
            break
        try:
            n = int(n)
            if n < 0:
                print("The input argument is not a non-negative integer!")
                continue
            elif n == 0:
                print("fib(0) = 0")
            else:
                a, b = 0, 1
                for i in range(1, n):
                    a, b = b, a + b
                print(f"fib({n}) = {b}")
        except ValueError:
            print("The input argument is not a non-negative integer!")
```
In matlab
```matlab
function fib()
    while true
        n = input('Please enter a non-negative integer or type stop: ', 's');
        if strcmp(n, 'stop')
            break
        end
        try
            n = str2double(n);
            if isnan(n) || n < 0 || rem(n, 1) ~= 0
                disp('The input argument is not a non-negative integer!')
                continue
            elseif n == 0
                disp('fib(0) = 0')
            else
                a = 0;
                b = 1;
                for i = 1:n-1
                    [a, b] = deal(b, a + b);
                end
                disp(['fib(' num2str(n) ') = ' num2str(b)])
            end
        catch
            disp('The input argument is not a non-negative integer!')
        end
    end
end
```

12.
```python
def findMaxValMaxLoc(arr):
    if len(arr) == 0:
        return None
    if len(arr) == 1:
        return (arr[0], 0)
    else:
        sub_max, sub_max_loc = findMaxValMaxLoc(arr[1:])
        if arr[0] >= sub_max:
            return (arr[0], 0)
        else:
            return (sub_max, sub_max_loc + 1)
```

13. 
The first one.

14.
Rewriting fib_recursive.py
```python
def fibonacci_recursive(n):
    if n <= 1:
        return n
    else:
        return fibonacci_recursive(n-1) + fibonacci_recursive(n-2)
```
Rewriting fib_loop.py
```python
def fibonacci_loop(n):
    if n <= 1:
        return n
    else:
        fib_n_minus_2, fib_n_minus_1 = 0, 1
        for _ in range(2, n+1):
            fib_n = fib_n_minus_1 + fib_n_minus_2
            fib_n_minus_2, fib_n_minus_1 = fib_n_minus_1, fib_n
        return fib_n
```

15.
```python
import csv
import matplotlib.pyplot as plt
from mpl_toolkits.basemap import Basemap

# Open the CSV file
with open('precipitation.csv') as csv_file:
    csv_reader = csv.reader(csv_file, delimiter=',')

    # Skip the header row
    next(csv_reader)

    # Create empty lists to store state names and precipitation values
    states = []
    precip = []

    # Loop through each row in the CSV file
    for row in csv_reader:
        # Append the state name and precipitation value to the appropriate lists
        states.append(row[0])
        precip.append(float(row[1]))

    # Set up the basemap
    m = Basemap(llcrnrlon=-119, llcrnrlat=22, urcrnrlon=-64, urcrnrlat=49, projection='lcc', lat_1=33, lat_2=45, lon_0=-95)

    # Draw the state boundaries and coastlines
    m.drawcoastlines()
    m.drawstates()

    # Define the color range and colormap
    colors = plt.cm.YlGnBu(precip / max(precip))
    cmap = plt.cm.ScalarMappable(cmap=colors)
    cmap.set_array([])

    # Plot the choropleth
    for index, state in enumerate(states):
        # Get the coordinates for the state
        coords = m.states[state]

        # Plot the state and fill with the appropriate color
        m.plot(coords[0], coords[1], color=colors[index], linewidth=0.5, zorder=1)
        m.fillcontinents(color='white', lake_color='white', zorder=0)

    # Add a colorbar
    plt.colorbar(cmap)

    # Display the plot
    plt.show()
```

16.
In python-
```python
import sys

# Get input and output file names from command-line arguments
if len(sys.argv) != 3:
    print("Usage: python formatted2csv.py input_file output_file")
    sys.exit(1)

input_file = sys.argv[1]
output_file = sys.argv[2]

# Open input and output files
with open(input_file, 'r') as f_in, open(output_file, 'w') as f_out:
    # Read input data and split by lines
    input_lines = f_in.read().strip().split('\n')

    # Write CSV formatted data to output file
    for line in input_lines:
        # Split the line by whitespace
        values = line.strip().split()

        # Write the comma-separated values to the output file
        f_out.write(','.join(values) + '\n')
```
In matlab
```matlab
% Check for correct number of input arguments
if nargin ~= 2
    fprintf('Usage: formatted2csv(input_file, output_file)\n');
    return;
end

% Get input and output file names
input_file = char(varargin(1));
output_file = char(varargin(2));

% Open input and output files
fid_in = fopen(input_file, 'r');
fid_out = fopen(output_file, 'w');

% Read input data and write CSV formatted data to output file
input_data = fscanf(fid_in, '%f');
input_data = reshape(input_data, 4, [])';
for i = 1:size(input_data, 1)
    fprintf(fid_out, '%g,', input_data(i, 1:end-1));
    fprintf(fid_out, '%g\n', input_data(i, end));
end

% Close files
fclose(fid_in);
fclose(fid_out);
```

17.
```python
Consider the following web-page address https://cdslaborg.github.io/DataRepos_SwiftBat/index.html. This is a data table in HTML language containing data from the NASA Swift satellite. Each row in this table represents information about a Gamma-Ray Burst (GRB) detection that Swift has made in the past years.

Each event is labeled by an ID that appears in the first column of the table named GRB (Trig#). Write a code that (downloads) and reads this HTML page from the web, then extracts the IDs of GRB events from the first column (IDs are the numbers that appear in parentheses in the first column). Then, writes the extracted IDs to an external output file on your system with the name nasa.swift.grb.ids.txt.

Note that the IDs must be outputted as strings to preserve the preceding zeros. Each ID must appear on a separate line in the output file.
```

18.


19.
A) 
```python
import random

def doRandomWalk(nstep, startPosition):
    currentPosition = startPosition
    for i in range(nstep):
        # take a step in a random direction with a random step size between [0,1]
        stepSize = random.uniform(0, 1)
        direction = random.choice([-1, 1])
        step = stepSize * direction
        # move one step in the chosen direction with the random step size
        currentPosition += step
    # return the final position after nstep steps
    return currentPosition
```
B)
```python
import random

def doRandomWalk(nstep, startPosition):
    currentPosition = startPosition
    for i in range(nstep):
        # take a step in a random direction with a random step size between [0,1]
        stepSize = random.uniform(0, 1)
        direction = random.choice([-1, 1])
        step = stepSize * direction
        # move one step in the chosen direction with the random step size
        currentPosition += step
    # return the final position after nstep steps
    return currentPosition

def simulateRandomWalk(nsim, nstep, startPosition):
    finalPositions = []
    for i in range(nsim):
        finalPosition = doRandomWalk(nstep, startPosition)
        finalPositions.append(finalPosition)
    return finalPositions
```
C)
```python
import matplotlib.pyplot as plt
import random

def doRandomWalk(nstep, startPosition):
    currentPosition = startPosition
    for i in range(nstep):
        # take a step in a random direction with a random step size between [0,1]
        stepSize = random.uniform(0, 1)
        direction = random.choice([-1, 1])
        step = stepSize * direction
        # move one step in the chosen direction with the random step size
        currentPosition += step
    # return the final position after nstep steps
    return currentPosition

def simulateRandomWalk(nsim, nstep, startPosition):
    finalPositions = []
    for i in range(nsim):
        finalPosition = doRandomWalk(nstep, startPosition)
        finalPositions.append(finalPosition)
    return finalPositions

nsim = 10000
nstep = 10
startPosition = -10

finalPositions = simulateRandomWalk(nsim, nstep, startPosition)

plt.hist(finalPositions, bins=50, density=True, alpha=0.7)
plt.xlabel('Final Position')
plt.ylabel('Probability Density')
plt.title(f'{nsim} Random Walks with {nstep} Steps from Start Position {startPosition}')
plt.show()
```
The distribution has a bell shape because of central limit theorem which states that, under certain conditions, the sum of a large number of independent random variables will tend towards as normal distribution, even if the individual random variables themselves are not normally distributed

20.
```python
import numpy as np
import matplotlib.pyplot as plt

# Define the equation for the heart shape
def heart(x, y):
    return (x**2 + y**2 - 1)**3 - (x**2 * y**3)

# Define the bounds of the bounding box
xmin, xmax = -2, 2
ymin, ymax = -2, 2

# Generate random points inside the heart shape
num_points = 100000
points_in_heart = []
while len(points_in_heart) < num_points:
    x = np.random.uniform(xmin, xmax)
    y = np.random.uniform(ymin, ymax)
    if heart(x, y) < 0:
        points_in_heart.append((x, y))

# Plot the heart shape and the sampled points
fig, ax = plt.subplots(figsize=(8,8))
ax.set_xlim(xmin, xmax)
ax.set_ylim(ymin, ymax)
x_vals = np.linspace(xmin, xmax, 500)
y_vals = np.linspace(ymin, ymax, 500)
X, Y = np.meshgrid(x_vals, y_vals)
Z = heart(X, Y)
ax.contour(X, Y, Z, levels=[0], colors='red')
x_samples, y_samples = zip(*points_in_heart)
ax.scatter(x_samples, y_samples, s=1, color='blue')

# Estimate the area of the heart by sampling points uniformly from the bounding box
num_samples = 1000000
samples_in_box = []
while len(samples_in_box) < num_samples:
    x = np.random.uniform(xmin, xmax)
    y = np.random.uniform(ymin, ymax)
    samples_in_box.append((x, y))

# Count the number of samples that fall inside the heart
num_samples_in_heart = 0
for x, y in samples_in_box:
    if heart(x, y) < 0:
        num_samples_in_heart += 1

# Estimate the area of the heart as the fraction of samples that fell inside the heart multiplied by the area of the bounding box
area_box = (xmax - xmin) * (ymax - ymin)
area_heart = area_box * num_samples_in_heart / num_samples
print(f"Estimated area of heart: {area_heart}")
```

21. Yes, it is to my advantage to switch to the other door in the long term.
```python
import random
import matplotlib.pyplot as plt

ngames = 100000
