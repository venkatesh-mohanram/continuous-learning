# NumPy
NumPy is the very popular library user in most of the Machine Learning and Data Science projects. Some of its inbuilt function and broadcast feature are some key differences of NumPy from a normal Python array
1. [NumPy Array](#numpyarray)  
2. [NumPy Indexing and Selection](#numpy-indexing-and-selection)
3. [NumPy Operations](#numpy-operations)
## Installing NumPy
We can install NumPy using Python *pip* Python Package installer command
```shell script
$ pip install numpy 
``` 
And in the python code, we need to import this library
```
import numpy as np
```
<a name="numpyarray"></a>
## NumPy Array
It supports both 1 dimentional, 2 dimentional and multi-dimentional array
```
my_list = [ 1, 2, 3]
np.array(my_list)
```
```
my_matrix = [[1, 2, 3], [4, 5, 6], [7, 8 , 9]]
np.array(my_matrix)
```
### Built-in functions
It has lots of inbuilt functions to work with
```
np.arange(0, 10)    # It will create an array with number 0 to 9
np.arange(0, 11, 2) # Creates with interval
np.zeros(3)         # 1D array with 3 0's
np.zeros((5,5))     #2D matrix of size 5x5
np.ones(4)
np.ones((4, 4))
np.linspace(0, 10, 3) # Evenly spaced number over specified interval
np.eye(4)             # Create identity matrix of size 4x4
np.random.rand(2)     # Create an 1D array of size using the *uniform distribution* between 0 and 1
np.random.rand(5, 6)
np.random.randn(3)    # Create random number using *Standard normal distribution*
np.random.randn(4, 5) 
np.random.randint(low, high) # Returns a random integer between the range low and high
np.random.randint(low, high, size) # Creates a 1D array of length size
arr.reshape(5,5)                   # Converts the array into a 5x5 matrix
arr.reshare(1, 25)                 # Converts the matrix into a 1D array
arr.shape                          # Prints the size of the array 
```
<a name="numpy-indexing-and-selection"></a>
## NumPy Indexing and Selection
Bracket selection
```
arr[8]
arr[startIndex:endIndex]        # Returns items in an array from startIndex to endIndex
```
### Broadcast
Broadcast is another important concept in NumPy, we can slice a part of the array from parent and any change in the slice will take effect in parent too. We can override the behavior
```
slice_list = arr[0:6]        # Sliced array will contain only 7 items
slice_list[:] = 100          # This assigns all the items in slice_list with value 100 and the same will be refleceted in arr array
arr_copy = arr.copy()        # To avoid broadcast, we need to copy the original array using .copy() function
```
### 2D array / Matrix indexing
There are two ways to perform a selection in a matrix
```shell script
arr_2d[1][2]     # [rowIndex][columnIndex]
arr_2d[1,2]      # [rowIndex, columnIndex]
``` 
To select part of the matrix
```shell script
 arr_2d[:2, 1:]   # Select all the rows before index 2; select all the columns from index 1
```
### Fancy Indexing
Fancy indexing allows selection of custom rows from 2D matrix
```shell script
arr_2d[[2, 7, 4, 3]]   # Selects the rows 2, 7, 4, 3 and prints in the same order
```
### Selection
Selection means to select particular row or column based on some conditions
```shell script
arr > 4       # Will return a boolean array containing True and False for each item  
arr[arr>4]    # Selects only the items which are greater than 4
```
<a name="numpy-operations"></a>
## NumPy Operations
Supports all basic arithmetic operations
```shell script
arr + arr2   # Add 2 array
arr - arr2   
arr * arr2 
arr / arr2   # Division by 0 will result into NAN (not a number); division by NAN result into INF (infinity)
arr ** 3     # Raise to the power of 3  
```
Also it supports all the universal functions like squareRoot, max, min, trigonometry functions
```shell script
np.sqrt(arr)  # Square root
np.exp(arr)   # Exponential 
np.max(arr)
np.sin(arr)   
np.log(arr)  # logarithm 
```
We can run all the function against the np array object too
```shell script
arr.max()
arr.sum()
...
```

