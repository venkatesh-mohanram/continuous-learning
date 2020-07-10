# Pandas
Pandas is a powerful library which can do operations equivalent to what an excel worksheet can do. One major difference from NumPy is that it can hold labels and items can be accessed using labels where as in NumPy if we want to access array items then we need to use numerical index only.
1. [Series](#series)
2. [DataFrame](#dataframe)
3. [Missing Data](#missing-data)
4. [GroupBy](#groupby)
5. [Concatenation, Merge, Join](#concatenation-merge-join)

## Installing Pandas
We need install in the same as we install any other python package
```shell script
$ pip install pandas 
``` 
Import pandas library as below
```shell script
import pandas as pd
```
<a name="series"></a>
## Series
Pandas series are like 1D array where the array items can be any objects including some function definition. And we can assign labels (though optional) for each item and use that to access instead of using numberical index
```shell script
series1 = pd.Series(data=[10, 20, 30], index=['US', 'UK', 'IND']) # Data is a python array
series2 = pd.Series(data={'US':10, 'UK':20, 'INDIA':30})          # We can pass dictionary
series3 = pd.Series(np.array([10, 20, 30]))                       # It can accept numPy array 
``` 
For accessing items in the series
```shell script
series1['US']       # This will return 10
```
We can perform operations in the series, all operations are based on the label/index
```shell script
series4 = series1 + series2    # Will add two series based on the label 
```
<a name="dataframe"></a>
## DataFrame
DataFrame is a multidimentional array or can be seen as a bunch of Series
```shell script
dataframe_obj = pd.DataFrame([[1,2], [3, 4], [5,6]], index=['US', 'UK', 'IND'], columns=['A', 'B', 'C'])   # Creation
```
#### Selection
```shell script
dataframe_obj['A']                   # Select column A
dataframe_obj[['A', 'B']]            # Selects column A and B
dataframe_obj.loc['US']              # Selects the row US
dataframe_obj.iloc[1]                # Selection based on the position, it selects UK
dataframe_obj.loc['US', 'A']         # Selecting a cell in a DataFrame
dataframe_obj['A']['US']             # First reference is always the column name which will return a series and then we can use the label to get the value
dataframe_obj.loc[['US', 'IND'],['B']] # Selecting multiple Rows and Columns
```
#### Conditional Selection
```shell script
dataframe_obj[dataframe_obj > 2]   # Selects all the rows and column which matches the condition
dataframe_obj[dataframe_obj > 2]['B']  # Selects only the specified column
```
#### Operations
```
dataframe_obj['D'] = dataframe_obj['A'] + dataframe_obj['B']   # Creates a new column named 'D' and assigns the sum of A and B
dataframe_obj.drop('D', axis=1)                                # Removes column D and returns a new DataFrame, if wanted to change same should use 'inplace=True'
dataframe_obj.drop('US', axis=0)                               # Removes a particular row
```
#### Indexes

DataFrame allows us to reset the existing indexes and create a new set of indexes etc
```shell script
dataframe_obj.reset_index()    # Will remove any index like US, UK, IND and resets to 0,1,2 etc and returns a new DataFrame

dataframe_obj['Countries'] = ['Country1', 'Country2', 'Country3']
dataframe_obj.set_index('Countries')           # Sets the new index as Countries column
``` 

#### Multi-index and Index hierarchy

Multi-Index is a good feature in DataFrame and creates a multiple levels of labels

<a name="missing-data"></a>
## Missing Data
During conditional selection we will get many N.A.N values (Not a Number), we can either drop those or we can fill with some other dummy values
```shell script
dataframe_obj.dropna()  # Drops all the rows which contains NAN and return only the rows where there is no NAN
dataframe_obj.dropna(axis=1)  # Drops all the columns which contains NAN
dataframe_obj.dropna(thres=2) # Drops all the rows which has more than or equal to 2 NAN
dataframe_obj.fillna(value='NEW VALUE')   # Replaces NAN with NEW VALUE
```
<a name="groupby"></a>
## Groupby
Group by is simliar to the SQL concept where we want to group the rows based on certain column and then apply aggregation functions like sum(), min(), std(), avg() etc
```shell script
df.groupby('company').mean()
df.groupby('company').std()
df.groupby('company').describe() # Applies common aggregation functions and produces a result
```
<a name="concatenation-merge-join"></a>
## Concatenation, Merge, Join
#### Concatenation
By default panda concatenates based on the column but we can override by setting the axis
```shell script
pd.concat([df1, df2])       # Concats rows from both the DataFrame, we should ensure column name matches
pd.concat([df1, df2], axis=1)
```
#### Merge
Merge is based on a specified common column name
```shell script
pd.merge(left, right, how='inner', on='key')  # Here 'key' is a column name
pd.merge(left, right, how='outer', on='key')
pd.merge(left, right, how='left', on='key')
pd.merge(left, right, how='right', on='key')
```
### Join
Join works on on the index column where as in Merge we can specify the column name against which the join should happen
```shell script
pd.join(left, right, how='outer')
```
## Operations
There are lots of inbuilt functions to do usual operations
```shell script
df['col1'].unique()           # returns the unique items in the series
df['col1'].nunique()          # returns the number of unique items
df['col1'].value_counts()     # How many times each item appears
df['col1'].apply(lamda x: x * x) # For each item in the series, it performs the square
df.sort_values(by='col1')
df.isnull()
```
## Data Input and Output
Most often in real case scenario, we will read the data from a external file or link. Padas provides the ability to read from external source and write back
```shell script
df = pd.read_csv('file.csv')   # Will return the DataFrame equivalent of the csv file
df = pd.read_html('http://www.fdic.gov/bank/individual/failed/banklist.html')   # Will return df array
df = pd.read_excel('Excel.xlsx', sheetname='Sheet1')  
pd.to_csv('example.csv', index=False)
```


