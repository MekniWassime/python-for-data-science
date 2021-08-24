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
### packages
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

 
