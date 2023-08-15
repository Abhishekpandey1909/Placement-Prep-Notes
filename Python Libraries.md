# Numpy
NumPy is one of the most popular, easy-to-use, versatile, open-source, python-based, general-purpose package that is used for processing arrays. NumPy is short for NUMerical PYthon. This is very famous for its highly optimized tools that result in high performance and powerful N-Dimensional array processing feature that is designed explicitly to work on complex arrays. Due to its popularity and powerful performance and its flexibility to perform various operations like trigonometric operations, algebraic and statistical computations, it is most commonly used in performing scientific computations and various broadcasting functions
- How are NumPy arrays advantageous over python lists?
- The list data structure of python is very highly efficient and is capable of performing various functions. But, they have severe limitations when it comes to the computation of vectorized operations which deals with element-wise multiplication and addition. The python lists also require the information regarding the type of every element which results in overhead as type dispatching code gets executes every time any operation is performed on any element. This is where the NumPy arrays come into the picture as all the limitations of python lists are handled in NumPy arrays.
- Additionally, as the size of the NumPy arrays increases, NumPy becomes around 30x times faster than the Python List. This is because the Numpy arrays are densely packed in the memory due to their homogenous nature. This ensures the memory free up is also faster.
Create an Array
```
# Creating an array from a list
my_list = [1,2,3,4,5]

arr1= np.array(my_list)
arr2 = np.array([1, 2, 3, 4,5])

#output: [1 2 3 4 5]
```
Generate arrays of zeros or ones
```
np.zeros((5,5))
np.ones(3)
```
Create arr of evenly spaced numbers over a specified interval.
```
my_array = np.arange(0,10,2)
print(my_array)
#output: [0 2 4 6 8]

#Using linspace
np.linspace(0,10,5)
```
Creates an identity matrix
```
np.eye(4)
#output: array([[ 1.,  0.,  0.,  0.],
       [ 0.,  1.,  0.,  0.],
       [ 0.,  0.,  1.,  0.],
       [ 0.,  0.,  0.,  1.]])
```
Array Attributes
```
# Shape
arr.shape
arr.ndim

#DataType
arr.dtype

#Total number of elements in an array
arr.size

my_array.shape
my_array.dtype

#output:
(2,3)
dtype('int64')
```
Reshaping, Flattening, transposing an array 
```
#Reshape
arr.reshape((5,1))

#Flatten an array or convert to 1D
arr.flatten()

#Traspose
arr.T

#Examples

my_array.reshape(2,3)
#output: [[1 2 3] [4 5 6]]

my_array = np.array([[1 2 3],[4 5 6]])
transposed_arr = np.transpose(my_array)
print(transposed_arr)
#output:  [[1 4] [2 5] [3 6]]
```
Accessing Elements in 1D array
```
# Accessing Single Element
my_array[2]
#output: 3

# Accessing a range of Elements
my_array[1:4]
#output: [2 3 4]
```
Indexing a 2D array (matrices)
```
arr_2d = np.array(([5,10,15],[20,25,30],[35,40,45]))

#Access row
arr_2d[1]
#output:  array([20, 25, 30])

#Access element
arr_2d[1][0]
arr_2d[1,0]
#output:  20

#Column
arr[:,2]

#Subarray
arr[0:2,1:3]

arr2d[[6,4,2,7]]
```

Selection
```
arr = np.arange(1,11)
bool_arr = arr>4
arr[bool_arr]
arr[arr>4]
```

Arithmetic Operations
```
arr = np.arange(0,10)
arr + arr
#output: array([ 0,  2,  4,  6,  8, 10, 12, 14, 16, 18])

arr * arr
#output: array([ 0,  1,  4,  9, 16, 25, 36, 49, 64, 81])

arr**3
#output: array([  0,   1,   8,  27,  64, 125, 216, 343, 512, 729])

arr - arr
#output: array([0, 0, 0, 0, 0, 0, 0, 0, 0, 0])

arr/arr # Warning on division by zero, but not an error,Just replaced with nan!
#output: array([ nan,   1.,   1.,   1.,   1.,   1.,   1.,   1.,   1.,   1.])

1/arr  #Also warning, but not an error instead infinity
#output:  array([        inf,  1.        ,  0.5       ,  0.33333333,  0.25      ,
        0.2       ,  0.16666667,  0.14285714,  0.125     ,  0.11111111])
```
Dot Product
```
np.dot(arr1,arr2)
```
Element-wise mathematical functions
```
np.sum(arr) #Sum of array elements
np.sum(arr,axis =0) #Sum of array elements along a specified axis

np.sqrt(arr)
np.exp(arr)
np.max(arr)  #same as arr.max()
np.sin(arr)
np.log(arr)
np.cumsum(arr) #Cumulative sum along a specified axis
np.prod(arr,axis=0) # Element-wise product along a specified axis
```
Computing mean, median, and standard deviation
```
my_array = np.array([1,2,3,4,5])
mean = np.mean(my_array)
median = np.median(my_array)
std_dev = np.std_dev(my_array)
std_dev = np.std(my_array)
np.corrcoef(arr) # Calculate the correlation coefficient matrix
```
Computing Correlation coefficient
```
arr1 = np.array([1,2,3,4,5])
arr2 = np.array([5,4,3,2,1])
corr_corf = np.corrcoef(arr1,arr2)
print(corr_coef)
#output: [[1,-1] [-1,1]]
```
Concatenating & Splitting Arrays
```
#Concatenate
np.concatenate((arr1,arr2),axis=0)

#Split
np.split(arr1,2)
#Examples
arr1 = np.array([1,2,3])
arr2 = np.array([4,5,6])
con_array = np.concatenate((arr1,arr2))
print(con_array)
#output: [1 2 3 4 5 6]
```
Sorting and searching
```
#Sorting an array
np.sort(arr)

#Indices that would sort the array
indices = np.argsort(arr)

#Searching for elements in an array
indices_of_values = np.where(arr1==3)
```

Max Min Argmax Argmin used to find their index locations
```
ranarr
array([10, 12, 41, 17, 49,  2, 46,  3, 19, 39])

ranarr.max()
49

ranarr.argmax()
4

ranarr.min()
2

ranarr.argmin()
5
```
Missing Values
```
#Check for NaN values
has_nan = np.isnan(arr1)

#Replace NaN values with 0
arr1[np.isnan(arr1)] = 0
```

### Rand
Create an array of the given shape and populate it with random samples from a uniform distribution over [0, 1).
```
# Uniform_Random
np.random.rand(2)
#output: array([ 0.11570539,  0.35279769])

np.random.rand(5,5)
#output: array([[ 0.66660768,  0.87589888,  0.12421056,  0.65074126,  0.60260888],
       [ 0.70027668,  0.85572434,  0.8464595 ,  0.2735416 ,  0.10955384],
       [ 0.0670566 ,  0.83267738,  0.9082729 ,  0.58249129,  0.12305748],
       [ 0.27948423,  0.66422017,  0.95639833,  0.34238788,  0.9578872 ],
       [ 0.72155386,  0.3035422 ,  0.85249683,  0.30414307,  0.79718816]])
```
### randn
Return a sample (or samples) from the "standard normal" distribution. Unlike rand which is uniform:
```
# normal_Random

np.random.randn(2)
#output: array([-0.27954018,  0.90078368])

np.random.randn(5,5)
#output:  array([[ 0.70154515,  0.22441999,  1.33563186,  0.82872577, -0.28247509],
       [ 0.64489788,  0.61815094, -0.81693168, -0.30102424, -0.29030574],
       [ 0.8695976 ,  0.413755  ,  2.20047208,  0.17955692, -0.82159344],
       [ 0.59264235,  1.29869894, -1.18870241,  0.11590888, -0.09181687],
       [-0.96924265, -1.62888685, -2.05787102, -0.29705576,  0.68915542]])
```
### randint
Return random integers from `low` (inclusive) to `high` (exclusive).
```
np.random.randint(1,100)
#output:   44

np.random.randint(1,100,10)
#output:   array([13, 64, 27, 63, 46, 68, 92, 10, 58, 24])
```
Set random seed for reproductivity 
```
np.random.seed(42)
```
## Broadcasting
Numpy arrays differ from a normal Python list because of their ability to broadcast:
```
#Setting a value with index range (Broadcasting)
arr[0:5]=100

#Broadcasting scaler to an array
arr2*2

#Broadcasting arrays of different shapes
arr2+arr3.reshape((3,1))
```
Slices: 
the changes also occur in our original array! Data is not copied, it's a view of the original array! This avoids memory problems!
```
arr = np.arange(0,11)
slice_of_arr = arr[0:6]
slice_of_arr[:]=99 
#output:  array([99, 99, 99, 99, 99, 99,  6,  7,  8,  9, 10])
```
To get a copy, need to be explicit
```
arr_copy = arr.copy()
```

2D array slicing
```
#Shape (2,2) from the top right corner
arr_2d[:2,1:]
array([[10, 15],
       [25, 30]])
```
# Python-Libraries
## Pandas
Pandas is an open-source, python-based library used in data manipulation
applications requiring high performance. The name is derived from “Panel Data” having multidimensional data. This was developed in 2008 by Wes McKinney and was developed for data analysis.
Pandas are useful in performing 5 major steps of data analysis - Load the data,
clean/manipulate it, prepare it, model it, and analyze the data.
## DataFrame
A DataFrame is a 2D mutable and tabular structure for representing data labeled with axes - rows and columns.
```
import pandas as pd
```
From a dictionary
```
Data = {‘col1’:[1,2,3],
‘col2’:[‘a’,’b’,’c’]}
dataframe = pd.DataFrame( data, index, columns, dtype)
```
- data: Represents various forms like series, map, ndarray, lists, dict etc.
- index: Optional argument that represents an index to row labels.
- columns: Optional argument for column labels.
- Dtype: the data type of each column.
From a CSV file
```
df = pd.read_csv('file.csv')
pd.read_excel('Excel_Sample.xlsx',sheetname='Sheet1')
```
Viewing/ Exploring Data
```
df.head() #Display the first n rows (default n =5)
df.tail() #Display the last n rows (default n =5)
df.shape #Get the dimension of the DataFrame (rows, columns)
df.info() # Get summary information about the DataFrame
df.describe() #generate descriptive statistics of numerical columns
df.columns #Show the column names
```
### Selection and Filtering
Accessing Columns 
```
df['col_name'] # Get a single column by name
df['col1','col2'] # Get multiple columns by name
```
Selecting rows and columns
```
df.loc[:,'col'] #Select all rows for a specific column
df.iloc[:,col_index] #Select all rows for a specific column by index
df.loc[row_label,'col'] # Get a specific value based on row label and column name
df.iloc[row_index,col_index] # Get a specific value based on row index and column index
```
Accessing Rows 
```
df.loc[row_label] #Get a row by label/index
df.iloc[row_index] #Get a row by index (integer)
df.[start:end] # Get row by slicing
df.loc['A']
df.iloc[2]
df.loc['B','Y']
df.loc[['A','B'],['W','Y']]
```
```
df = pd.read_csv('file.csv')
```df = pd.DataFrame(randn(5,4),index='A B C D E'.split(),columns='W X Y Z'.split())
df['W']
df[['W','Z']]
type(df['W']) #DataFrame Columns are just Series
df['new'] = df['W'] + df['Y'] #Creating a new column
```

Conditional Filtering
```
df[df['col']>value] #Filter rows based on a condtion
df[df['col']>5] 

df[df['col1']>value1 & df['col2']<value2] #Filter rows based on multiple condtion
df[df>0]
df[df['W']>0]
df[df['W']>0][['Y','X']]
df[(df['W']>0) & (df['Y'] > 1)]

df.query('col>5')  # Alternate way to filter rows based on a conditions
df.query('city=="Bareilly"')
```
### Data Manipulation
Sorting Data
```
df.sort_values('col') # Sort DataFrame by a column
df.sort_values(by='Salary') 
df.sort_values('col', ascending = False) # Sort in descending order
df.sort_values(['col1','col2'])
df.sort_values(by='col2') #inplace=False by default
```
Adding/Removing columns
```
df['new_col'] = values #Add a new column
df['new_col'] = df['old_col']*12 # Apply a function to create a new column

df.drop('col_name',axis=1,inplae = True) #Remove a column
df.drop('new',axis=1)
df.drop('new',axis=1,inplace=True)
df.drop([1,3],axis=0)

df.rename(columns={'name':'Full Name', 'age':'Age(years)'})
```

### Data Cleaning
```
df.duplicated() #Check for duplicate rows
df.drop_duplicates() #Remove duplicate rows
df.replace(old,new) #Replace values
df.rename(columns = {'old_name':'new_name'}) #Rename Columns
del df['col1']  #Permanently Removing a Column
```
Missing Data
```
df.isnull() #Check for missing values
df.dropna() # Remove rows with misisng values
df.dropna(thresh=2)
df.fillna(value) #Replace misisng values with a specific value
df['A'].fillna(value=df['A'].mean())
```
### Handling data
```
# Handling outliers
threshold = df['value'].quantile(0.95)
outliers_df = df[df['value']>threshold]

#Handling Categorical Data
df['category'] = df['category'].astype('category')
df['category_codes'] = df['category'].cat.codes
```
Handling Dates and Time
```
df.['datetime'] = pd.to_datetime(df.['datetime']) #Convert a column to date time
df['month'] = df.['datetime'].dt.month #Extract month from datetime
df['dayofweek'] = df.['datetime'].dt.dayofweek #Extract day of the week
```
Merging and Concatenating DataFrames
```
df1.merge(df2,on='col') #Inner join based on a column
pd.merge(d1,d2,how='inner',on='key')
pd.merge(d1, d2, how='left', on=['key1', 'key2'])
df1.join(df2,on='col') #Join based on index or column
df_merged = pd.merge(df1,df2,on='col') #Merge DataFrame based on a common column
df_concatenated = pd.concat([df1,df2]) #Concatenate DataFrame vertically (along rows)
pd.concat([df1,df2,df3],axis=1) #Concatenate DataFrame along columns
```
### Misc
Grouping and Aggregation
```
df.groupby('col').mean() #Group by a column and calculate the mean
df.groupby(['col1','col2']).sum() #Group by multiple columns and calculate the sum
df.groupby('col').agg('mean','sum') #Apply multiple aggregations
```
Applying Functions
```
df.apply(function) #Apply a function to each element/column/row
df.applymap(function) #Apply a function to each element
def times2(x):
    return x*2
df['col1'].apply(times2)
df['col3'].apply(len)
df['col1'].sum()
```

Data Reshaping
```
df.pivot(index='col1',columns='col2',values='col3') #Pivot Table
df.pivot_table(values='D',index=['A', 'B'],columns=['C'])
df.melt(id_vars=['col1','col2'],value_vars=['col3','col4']) #Convert wide to long format
```
Exporting Data
```
df.to_csv('file.csv',index=False) #Export DataFrame to a CSV file
df.to_excel('file.xlsx',index=False) #Export DataFrame to a Excel file
df.to_excel('Excel_Sample.xlsx',sheet_name='Sheet1')
```

## Series
```
labels = ['a','b','c']
my_list = [10,20,30]
arr = np.array([10,20,30])
d = {'a':10,'b':20,'c':30}
# Using List
pd.Series(data=my_list)
pd.Series(data=my_list,index=labels)
pd.Series(my_list,labels)
# NumPy Arrays
pd.Series(arr)
pd.Series(arr,labels)
# Dictionary
pd.Series(d)
# Functions
pd.Series([sum,print,len])
# Output
0      <built-in function sum>
1    <built-in function print>
2      <built-in function len>
```
Using Index
```
ser1 = pd.Series([1,2,3,4],index = ['USA', 'Germany','USSR', 'Japan'])
ser2 = pd.Series([1,2,5,4],index = ['USA', 'Germany','Italy', 'Japan'])    ser1 + ser2
# Output
Germany    4.0
Italy      NaN
Japan      8.0
USA        2.0
USSR       NaN
dtype: float64                                                         
```
Index  
```
df.reset_index()  # Reset to default 0,1...n index
newind = 'CA NY WY OR CO'.split()
df['States'] = newind
df.set_index('States',inplace=True)
```
MultiLevel Indexing
```
outside = ['G1','G1','G1','G2','G2','G2']
inside = [1,2,3,1,2,3]
hier_index = list(zip(outside,inside))
hier_index = pd.MultiIndex.from_tuples(hier_index)
df = pd.DataFrame(np.random.randn(6,2),index=hier_index,columns=['A','B'])
df.loc['G1']
df.loc['G1'].loc[1]
df.xs('G1')
df.xs(['G1',1])
df.xs(1,level='Num')
df.index.names = ['Group','Num']
```
Operations
```
df.head()
df['col2'].unique()
df['col2'].nunique()
df['col2'].value_counts()
```
Get column & Index names
```
df.columns
df.index
```


