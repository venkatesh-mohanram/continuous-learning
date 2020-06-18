# NumPy
NumPy is the very popular library user in most of the Machine Learning and Data Science projects.
## Installing NumPy
We can install NumPy using Python *pip* Python Package installer command
```shell script
$ pip install numpy 
``` 
And in the python code, we need to import this library
```
import numpy as np
```
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
```