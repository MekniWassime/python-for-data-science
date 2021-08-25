# Python Cheat Sheet
### Lists
lists in python are reference types which means that the following

    x = [1, 2, 3]
    y = x
    y[1] = 4 #x=y=[1, 4, 3]
will result in the change on `y` to be reflected in `x`
to get around these problems we need to copy the contents of one list into another like below

    y = list(x)
    y = x[:]
#### element access
 - `list[-1]` we can use negative indexes to access the last elements in a list, negative indexes need to be strictly larger than `-len(list)`
 - `list[inf:sup]` returns the elements within a given range inf (inclusive) to sup (exclusive), we can also not specify one or both bounds and let python fill them in. `list[inf:]` will return elements from inf to the end of the list *(inf and sup can be negative)*
#### list operations
 - `len(list)` length of list
 - `list1 + list2` concatenates both lists
 - `del(list[4])` delete an element of a list, you can also use intervals to delete more than one element
 - `list[1:3]=[1,2,3]` replace elements within range with elements on the right operand
 - `list.index(element)` returns the index of the `element` in the list, throws an error if `element` is not in `list`
 - `element in list` True if element is in list, False otherwise
 - `list.count(element)` returns the number of occurances of `element` in `list`
 - `list.append(element)` appends `element` to `list`
 - `sorted(iterable, key=None, reverse=False)` sorts `iterable`, `key` and `reverse` are optional named parameters, if we need to specify `reverse`we would have to call `sorted` like this `sorted(list, reverse=true)`
	 - `key` is a function that is applied to the elements one by one during sorting that transforms elements in a way without affecting the output, let's take a list of strings as an example we can pass `key=len` so that our sort will be applied on the lengths of each string instead of the strings themselves
	 - `reverse`if True, the list is sorted in reverse order *(descending for integers)*
### Comparison operators
we can use comparison operators on objects of the same type or compatible types such as bools, integers and floats, strings and integers won't work
also note that `==` and `!=` operators work on different datatypes but return False and True respectively in most cases
in python Boolean operators are `and`, `or` and `not`
### Control structures


    if condition:                     while condition :
	    expression                    	expression
    elif condition:
	    expression                    for var in seq :
    else :                            	expression
	    expression                    
#### for loop
 - to iterate over a list with the index value we can use `for index, var in enumerate(seq)`
 - you can also use the `,` separated variables to access elements of an array of arrays where `var1, var2` would correspond to `var1=element[0]` and `var2=element[1]`
 - to iterate over a dictionary we use `for key, value in dict.items():`
 - to iterate over a 2d numpy array we could use `for elem in 2d_array:` but the value of `elem` would contain 1d arrays, in order to iterate over the elements of a nd-array element by element we could use the following `for elem in np.nditer(nd_array)`
 - to iterate over a Pandas *DataFrame* simply calling `for elem in dataFrame` would result in elem iterating over just the column name
 - the proper way is to call `for label, row in dataFrame.iterrows():` where `label` contains the row-label and `row` contains a *Series* of the row.
 in order to create a new column based on the value of each row we have to assign `dataFrame[label,'new_col_name']='new_value'`
 but using a for loop is inefficient. We could use `dataFrame['new_col_name'] = dataFrame.apply(function)` where `function` takes a row as a parameter and returns the desired value to add, we can also use `dataFrame['col'].apply` to user a single column value instead of a whole row

### Dictionaries

    dict = {key: value}

 - `dict.keys()` returns a list of the keys contained in the dictionary
 - `dict[key]` to access the value corresponding to the key
 - `key in dict` returns true if key is in the dictionary
 - `del(dict[key])` deletes the key from the dictionary 

### Packages
`ìmport math as mt` import package `math` under the alias `mt`
`from math import pi as pie` import `pi` from `math` under the alias `pie` *(specifying an alias is optional in both cases)*
### NumPy

> NumPy arrays facilitate advanced mathematical and other types of
> operations on large numbers of data. Typically, such operations are
> executed more efficiently and with less code than is possible using
> Python's built-in sequences.

all elements in a NumPy array need to have the same dataType, if multiple dataTypes are included in the list, all elements are promoted to the smallest possible common type, the follwing order is a general rule of thumb `bool<int<float<string`

    import numpy as np
    np_array = np.array(list)
this coverts `list` into a numpy array called `np_array`

 - `np_array1 + np_array2` returns a new array with the sum of elements from both arrays that have the same index, for example `[1,2,3]+[4,5,6]=[5,7,9]`other operators such as `*` `/` `-` can all be used in a similar manner, one of the operands can also be a *scalar value* or a *vector*
 - `array < 7` returns an array of Booleans where each element is True if the corresponding element in the original array satisfies the condition `< 7`and false otherwise
 - array[array < 7] returns only the elements that satisfy the condition `< 7` (any boolean array can be passed inside the `[]`)
 - you can access an n-dimensional array's elements by chaining `[]`or by separating the idexes by a `,` `[,,]`, for example `array_2d[1][2]` and `array_2d[1,2]` are equivalent, you can also use intervals instead of indexes
 - `np_array.shape` retruns the dimentions of the array, the output for a 2d array is `(nbRows, nbCols)` 
 - `np.median(array)` returns the [median](https://www.investopedia.com/terms/m/median.asp) of the dataset 
 - `np.mean(array)` returns the mean or avrage of the dataset
 - np.std(array) returns the [standard deviation](https://www.investopedia.com/terms/s/standarddeviation.asp) of the dataset
 - np.var(array) returns the [variance](https://www.investopedia.com/terms/v/variance.asp) of the dataset
 
	 you can add nan prefix to all these function names so that they ignore array elements that can't be converted to a number `nanstd` for example
	 
 - `np.corrcoef(x,y)` returns the [correlation coefficient](https://www.investopedia.com/ask/answers/032515/what-does-it-mean-if-correlation-coefficient-positive-negative-or-zero.asp) of the dataset, simmilarly `np.cov` is used to calculate the [covariance](https://www.investopedia.com/terms/c/covariance.asp) 
 - `np.logical_and`, `np.logical_or` and `np.logical_not` can be used to perform element wise Boolean operations on two bool arrays
#### numpy.random
 - `np.random.seed(seed)` here seed is an integer that the package uses to generate random numbers, if not specified a random seed is selected
 - `np.random.rand()` gives us a pseudo-random float between 0 and 1
 - `np.random.randint(inf, sup)` generates an integer inside the half-open interval `[inf, sup[`
 - 

### Matplotlib

> matplotlib. pyplot is a collection of functions that make matplotlib
> work like MATLAB

in order to use this package we need to import it like so

    import matplotlib.pyplot as plt

 - `plt.plot(dataset1, dataset2)` to prepare for a plot line graph that uses dataset1 as x-axis and dataset2 as y-axis
 we then have to call `plt.show()` in order to show the graph
 - there are other types of graphs that are used simmilar to plot lines such as scatter
 - we can call `plt.xscale('log')` before `plt.show()` to display the x-axis (resp y-axis) on a logarithmic scale. Other graph configurations are available
 - if we have more than one graph we need to call `plt.clf()` after `plt.show()` in order to reset the configurations of the previous graph
 ##### other types of graphs
 - `plt.hist(dataset, bins=10)` is used to plot histograms, `bins` specify the number to divide the interval by, the default value is 10
 - `plt.scatter(dataset1, dataset2, s=None, c=None, alpha=1)` build a scatter graph
	 - `s` is assigned a list that controls the size of each dot in the graph
	 - `c` is a list of colors that controls the color of each dot in the graph
	 - `alpha` is the alpha of each dot (value from 0 to 1)
##### graph customizations
 - `plt.xlabel(label)` add a label on the x-axis (resp y-axis)
 - `plt.title(title)` add a title to the graph
 - `plt.xticks(tick_val, tick_lab)` customize ticks of the x-axis, `tick_val` and `tick_lab` are lists containing the values of ticks and the labels of each tick respectively
 - `plt.text(x,y,text)` shows text on the graph on the point `(x,y)`
 - `plt.grid(True)` enables grid

### Pandas

> The DataFrame is one of Pandas' most important data structures. It's
> basically a way to store tabular data where you can label the rows and
> the columns.

 

    import pandas as pd



One way to build a *DataFrame* is from a dictionary where the keys represent column names and the values are lists of the corresponding data

    dict = {'cities':[...],'population':[...]}
    dataFrame = pd.DataFrame(dict)

  by default *DataFrame* labels are indexed 0, 1, 2 ... and so on, we can change this by passing a list of labels to the `dataFrame.index = labels` property
  
  We can also build a *DataFrame* from a CSV (comma seperated values) file like so

    dataFrame = pd.read_csv('file-path')
if the file contains row labels we need to tell this function what's the index of that column, if it's the first column we set `index_col` to `0`

    dataFrame = pd.read_csv('file-path', index_col = 0)

 - to access data from a *DataFrame* we can use `dataFrame['col_name']` which will give us a *Series* which is a 1d-array of the values of the column in addition to the row-labels 
 - another way is to "select" one or more columns and return a new *DataFrame* with just those columns, we do so using `dataFrame[['col1','col2',...]]`
 - if we use `dataFrame[index]` we can access rows at `index`, we can also use intervals just like a list, this gives us a new *DataFrame* that contain only the selected rows
 - a versatile way to access data in a *DataFrame* is to use the methods `loc` and `iloc`
	 - `dataFrame.loc['row_name']` will give us a *Series* containing the data of the specified role
	 - `dataFrame.loc[['row1','row2',...],['col1','col2',...]]` we can select one or more rows and columns using this syntax, in order to only select columns and leave all the rows in we can use `dataFrame.loc[:,['col1',...]]`, similarly, if we only specify the rows list we get all columns of each row (if it's a single column or row we can omit the `[]` and just write `['row',['col1',...]]` Note that this will return a *Series* and not a *DataFrame*)
	 - `iloc` method works just like `loc` but instead of using row and column labels we use their indexes instead treating the *DataFrame* as if it's a 2d-array, we can use `[index]` to select a single row as a series or `[[index_row,...],[index_col,...]]` to select multiple rows and columns, same rules apply with the benefit of being able to use intervals to select either rows or columns
 - we can create bool *Series* from a regular *Series* by using comparison operators `bool_series = dataFrame['col_name'] < 10` after that we can use the result to select rows that correspond to values of `'col_name'` that satisfy the condition by writing `dataFrame[bool_series]`
 Note that `np.logical_and` , `logical_or` and `logical_not` work on Boolean *Series* as well 
 #### Inspecting DataFrames
 
 - `df.head()` return the first few rows of `df`
 - `df.info()` returns info about each column like dataType and number of missing values
 - `df.describe()` returns statistics for each column if possible
 - `df.shape()` returns the dimensions of `df`
 - `df.values` contains a numpy 2d array that contains the values
 -  `df.columns` contains the list of column names
 - `df.index` contains the list of either numeric row indexes or row-labels
#### Data manipulation
 - `df.sort_values('col_name',ascending=True)` sorts *DataFrame* on `'col_name`
 - `df.sort_values(['col1',...], ascending=[True,...])` sorts *DataFrame* based on multiple columns
 - we can filter with multiple conditions by using `&` and `|` operators `df[(df["col1"] > 60) & (dogs["col2"] == "test")]` which will result in a bool array (the parentheses are required)
 - `df['col_name'].isin(['val1',...])` filter by values that are equal to one of the elements of the list
 - `df['col_name'] = def['col'] ** 2` just like numpy arrays we can assign columns the result of arithmetic operations done on the same or other columns, this can also be used to create new columns
 - we can calculate statistical data of columns by calling the following methods `df.mean(); df.mode(); df.min(); df.max(); df.var(); df.std(); df.sum(); df.quantile();`some methods have a cummulative version by adding the prefix cum `cumsum()` for example
 - `df['col'].agg(aggFunction)` aggregate functions act on the whole column and return a value usually a statistical value, aggregate functions can act on multiple columns and multiple functions can be called each resulting in a function `def[['col1',...]].agg([aggFun1, ...])`
 - `df.drop_duplicates(subset='col_name')` remove rows with duplicate occurrences in `col_name`, you can assign a list of column names to subset too
 - `df['col'].values_counts(sort=False, normalize=False, ascending=True)` returns the number of occurrences of each value in the column
	 - works on *Series* aka single columns only
	 - if `normalize` is set to true, number of occurrences will be  divided by the total number of elements giving us the ration of each unique element in the column
 - `df.groupby('col-name')[['col1',...]].sum()`groups the unique values of `col_name` and apply a function over the values `sum` for example, selecting columns is optional
 - `df.groupby('col-name').agg([sum, min, max, np.mean])` we use this to  get multiple statistics about each group
 - `df.pivot_table(values='new-col', index='col1',columns='col2', aggfunc=np.mean, margins=False, fill_value=0)` the pivot table method can do what groupby does and more
	 - `values` column that agg function is going to use
	 - `index` the column that is going to be grouped and used as row-labels
	 - `columns` the column that is going to be grouped and used as column-labels
	 - `aggfunc`a function or a list of functions, by default `pivot_table` calculates means
	 - `margins` if margins is set to true, a row and a column called 'All' is added and it shows the statistics applied to each column and row respectively 
	 - `fill_value` if specified, set the missing data to the value of `fill_value`
