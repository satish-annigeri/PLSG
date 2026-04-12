# Session 7

#### Planned Schedule: 18-04-2026 4:00 pm to 6:00 pm

## Agenda

1. Review of previous sessions
2. Answers to queries
3. NumPy (contd. from Session 6)

## NumPy arrays (contd. from Session 6)

### Creating special arrays

Creating arrays with all elements equal to `0` or `1` is possible with the functions `numpy.zeros()` and `numpy.ones()`.

Creating a one-dimensioned array of size `5` consisting of all `0` or all `1` is as follows:

```pycon
>>> import numpy as np
>>> a = np.zeros((5,))
>>> print(type(a), len(a), a.shape, a.size, a.dtype)
<class 'numpy.ndarray'> 5 (5,) 5 float64
>>> a = np.zeros((5,), dtype=int)
>>> print(type(a), len(a), a.shape, a.size, a.dtype)
<class 'numpy.ndarray'> 5 (5,) 5 int64
>>> a = np.zeros(5)
>>> a
array([0., 0., 0., 0., 0.])
```

**Note**

1. Size of a one-dimensioned array of zeros can be specified either as `tuple` (`(5,)`) or as an `int`.
2. When `dtype` of the array is not specified, it defaults to `float`.
3. To create an array of zeros of a specific type, specify `dtype` to the required type.

Similar behaviour is seen with `numpy.ones()` that creates arrays with all elements equal to `1`.

```pycon
>>> a = np.ones(5)
>>> a
array([1., 1., 1., 1., 1.])
>>> print(type(a), len(a), a.shape, a.size, a.dtype)
<class 'numpy.ndarray'> 5 (5,) 5 float64
>>> a = np.ones((5,), dtype=int)
>>> a
array([1, 1, 1, 1, 1])
>>> print(type(a), len(a), a.shape, a.size, a.dtype)
<class 'numpy.ndarray'> 5 (5,) 5 int64
```

Creating a square two-dimensioned array with the elements along the main diagonal specified by the programmer are created as follows:

```pycon
>>> a = np.diag([1, 2, 3])
>>> a
array([[1, 0, 0],
       [0, 2, 0],
       [0, 0, 3]])
>>> print(type(a), len(a), a.shape, a.size, a.dtype)
<class 'numpy.ndarray'> 3 (3, 3) 9 int64
```

**Note**

1. The argument to `numpy.diag()` is a `list` or a `tuple`. The elements of the argument are placed on the main diagonal.
2. The array is two-dimensioned and square.
3. The `dtype` of the array is determined by the elements in the argument. If the elements are of different types, the `dtype` of the array is determined by the type to whch all elements can be converted automatically, for example, from `int` to ``float` if one or more of the elements is of type `float`.

### NumPy arrays using range-based array creation

NumPy has a function named `arange()`, which is similar to the `range()` function that waas studied in earlier sessions. But there are some differences:

1. `arange()` can have `float` values for `start`, `stop` and `step`.
2. `arange()` returns a `numpy.ndarray` instead of a `list`.

```pycon
>>> a = np.arange(0, 5, 0.5)
>>> a
array([0. , 0.5, 1. , 1.5, 2. , 2.5, 3. , 3.5, 4. , 4.5])
>>> print(type(a), len(a), a.shape, a.size, a.dtype)
<class 'numpy.ndarray'> 10 (10,) 10 float64
>>> b = np.arange(10, 0, -2.5)
>>> b
array([10. ,  7.5,  5. ,  2.5])
```

**Note**

1. `strat` value is inclusive. The start value is `0.0`.
2. `stop` value is not inclusive. The last value is `4.5`, not `5.0`.
3. `step` can be a positive or negative `float`.

The function `np.linspace()` creates `num` evenly spaced values over a specified interval `start` to `stop`, and both `start` and `stop` are included.

```pycon
>>> x = np.linspace(0, 2 * np.pi, 17)
>>> x = np.linspace(0, 2 * np.pi, 17)
>>> x
array([0.        , 0.39269908, 0.78539816, 1.17809725, 1.57079633,
       1.96349541, 2.35619449, 2.74889357, 3.14159265, 3.53429174,
       3.92699082, 4.3196899 , 4.71238898, 5.10508806, 5.49778714,
       5.89048623, 6.28318531])
```

**Note**

1. The last argument is **the number of points to be generated**, including the `start` and `stop` values. Thus, to create say `10` equal intervals between `start` and `stop`, `num = 11`.
2. The number of points `num` is optional and defaults to `50`, that is `49` equal intervals.

### Creating multi-dimensioned arrays

Creating multi-dimensioned arrays is an extension of the approach used in the previous examples. Creating a two-dimensioned array requires a two-dimensioned `list`, with equal number of columns in each row.
```pycon
>>> a = np.array([ [1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]])
>>> print(a.ndim, a.shape, a.size, a.dtype)
2 (3, 4) 12 int64
```
Creating a three-dimensioned array with two cards, each with 3 rows and 4 columns is as follows:
```pycon
>>> a = np.array([
... [ [1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12] ],
... [ [21, 22, 23, 24], [25, 26, 27, 28], [29, 30, 31, 32] ]
... ])
>>> print(a.ndim, a.shape, a.size, a.dtype)
3 (2, 3, 4) 24 int64
>>> a
array([[[ 1,  2,  3,  4],
        [ 5,  6,  7,  8],
        [ 9, 10, 11, 12]],

       [[21, 22, 23, 24],
        [25, 26, 27, 28],
        [29, 30, 31, 32]]])
```
This may require a little attention in the beginning but with experience it will get easier. Not forgetting the commas between the elements of a row, the commas separating the rows and the commas separating the cards is important. It is a good practice to enterthe data as shown in the output above. Empty lines between cards is acceptable and visually helpful.

!!! note
    The number of left brackets at the start is equal to `ndim`, the number of dimensions.


### Operations on arrays

Operations dfined in linear algebra, such as addition, subtraction, multiplication of an array by a scalar, element-wise product of two array, matrix product of two arrays etc. follow the rules defined for the respective operations.

**Transpose of an array**

Transpose interchanges the rows and columns of a two-dimensioned array.

```pycon
>>> a.T
array([[1, 5],
       [2, 6],
       [3, 7],
       [4, 8]])
```
!!! note
    A one-dimensioned has no specific orientation in terms of whether it is a row array or a column array. Thus, transposing a one-dimensioned array returns a one-dimensioned array.
    ```pycon
    >>> c = np.array([1, 2, 3, 4])
    >>> c.T
    array([1, 2, 3, 4])
    ```
The definition of transpose can be extended to higher dimensions. For example, transpose of an array with shape `(2, 3, 4)` returns an array with shape `(4, 3, 2)`

```pycon
>>> x = np.array([
       [[ 1,  2,  3,  4],
        [ 5,  6,  7,  8],
        [ 9, 10, 11, 12]],
       [[21, 22, 23, 24],
        [25, 26, 27, 28],
        [29, 30, 31, 32]]])
>>> x.T
array([[[ 1, 21],
        [ 5, 25],
        [ 9, 29]],

       [[ 2, 22],
        [ 6, 26],
        [10, 30]],

       [[ 3, 23],
        [ 7, 27],
        [11, 31]],

       [[ 4, 24],
        [ 8, 28],
        [12, 32]]])
```

**Multiplication of an array by a scalar**

```pycon
>>> a = np.array([[1, 2, 3, 4], [5, 6, 7, 8]])
>>> 2 * a  # Multiplication by the scalar 2
array([[ 2,  4,  6,  8],
       [10, 12, 14, 16]])
```

**Addition and subtraction of two arrays**

Two arrays must have the same `shape` for addition or subtraction to be valid.

```pycon
>>> a = np.array([[1, 2, 3, 4], [5, 6, 7, 8]])
>>> b = np.array([[10, 20, 30, 40], [50, 60, 70, 80]])
>>> a + b
array([[11, 22, 33, 44],
       [55, 66, 77, 88]])
>>> b - a
array([[ 9, 18, 27, 36],
       [45, 54, 63, 72]])
```

**Element-wise multiplication of two arrays**

The arrays must have the same `shape` for the element-wise multiplication of two arrays. The element in the result is the product of the two elements at the same location in the given arrays.

```pycon
>>> a * b
array([[ 10,  40,  90, 160],
       [250, 360, 490, 640]])
```

**Matrix multiplication of two arrays**

For the case of two-dimensioned arrays, matrix multiplications requires thatt the number of columns in the first array must equal the number of rows in the second. The result has the same number of rows as the first array and the same number of columns as the second. The matrix multiplication operator is `@`. There is a NumPy function for the same operation, namely `#!python np.dot(a, b.T)` and is the same as `#!python a @ b.T`.

```pycon
>>> a
array([[1, 2, 3, 4],
       [5, 6, 7, 8]])
>>> b
array([[10, 20, 30, 40],
       [50, 60, 70, 80]])
>>> y = a @ b.T
>>> y
array([[ 300,  700],
       [ 700, 1740]])
>>> print(a.shape, b.T.shape, y.shape)
(2, 4) (4, 2) (2, 2)
```
### Reshaping and resizing arrays

NumPy provides two families of operations for changing array shape:

1. **Reshaping:** changes only the view of the data (no copy when possible).
2. **Resizing:** changes the size of the underlying buffer (may reallocate, may fill new values).

#### Reshaping arrays

```pycon
>>> a = np.arange(12)
>>> a
array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11])
>>> b = a.reshape(3, 4)
>>> b
array([[ 0,  1,  2,  3],
       [ 4,  5,  6,  7],
       [ 8,  9, 10, 11]])
>>> a.reshape(2, -1)
array([[ 0,  1,  2,  3,  4,  5],
       [ 6,  7,  8,  9, 10, 11]])
>>> a.reshape(5, -1)
Traceback (most recent call last):
  File "<python-input-70>", line 1, in <module>
    a.reshape(5, -1)
    ~~~~~~~~~^^^^^^^
ValueError: cannot reshape array of size 12 into shape (5,newaxis)
```

The `reshape()` method can calculate the second dimension provided it is feasible.

#### Resizing arrays

The function from NumPy `numpy.resize()` changes the size by truncating the array if the new size is smaller than the current size and by repeating the values if the new size is larger then the current size. This operation createsa new array with the specified size, while the original array remains unchanged.

```pycon
>>> a = np.array([1, 2, 3])
>>> b = np.resize(a, 5)
>>> b
array([1, 2, 3, 1, 2])
>>> a
array([1, 2, 3])
```

The `numpy.resize()` **function** can reshape the array after resizing it - just give a `tuple` as the second argument to the function call.
```pycon
>>> a = np.array([1, 2, 3])
>>> np.resize(a, (2, 4))
array([[1, 2, 3, 1],
       [2, 3, 1, 2]])
>>> a
array([1, 2, 3])
```

An array has a `numpy.ndarray.resize()` **method**, which fills the extended portion of an array with zeros if the new dimension is larger than the current size. As usual, the original array `a` remains unchanged.

```pycon
>>> a = np.array([1, 2, 3])
>>> a.resize(5)
>>> a
array([1, 2, 3, 0, 0])
```

!!! warning
     The `numpy.ndarray.resize()` method resizes the array **in-place**. It does not return a new array like the `numpy.resize()` function.

### Array indexing

Array indexing is similar to indexing a `list` or a `tuple`. One change is the way the indices of multi-dimensioned arrays are written - array indices are enclosed between a single pair of square brackets `[i, j]` while `list` indices written as `[i][j]`.

The first index of a two-dimensioned array represents the row index and the xecond index represents the column index. The first index of a three-dimensioned array represents the card index, the second index represents the row index and the third index represents the column index. Extending this logic to higher dimensions, the four-dimensioned array can be thought of as bundles of decks of cards, each card containing rows and columns. Start index is zero (`0`). An individual element of an array can be identified by its indices, the number of indices being equal to the dimension of the array, namely `ndim`. Negative index for any axis is considered to be counted backward starting from the last element along that axis, starting with `-1` for the last element.

One-dimensioned arrays are the easiest to understand:

```pycon
>>> a = np.arange(1, 11)
>>> a
array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10])
>>> a[0]
np.int64(1)
>>> a[-1]
np.int64(10)
>>> a[2]
np.int64(3)
```

Two-dimensioned arrays require two indices, separated by a comma (`,`), the first index is the row and the second index is the column.

```pycon
>>> b = np.array([np.arange(1, 6), np.arange(11, 16)])
>>> b
array([[ 1,  2,  3,  4,  5],
       [11, 12, 13, 14, 15]])
>>> b[0, 0]
np.int64(1)
>>> b[0, 1]
np.int64(2)
>>> b[1, 0]
np.int64(11)
>>> b[1, 1]
np.int64(12)
>>> b[-1, -1]
np.int64(15)
```

Three-dimensional arrays require three indices, the first index is the card, the second index is the row within a card, and the third index is the column within the row.

```python
>>> c = np.array([
... [np.arange(1, 6), np.arange(11, 16), np.arange(21, 26)],
... [np.arange(11, 16), np.arange(21, 26), np.arange(31, 36)]])
>>> c
array([[[ 1,  2,  3,  4,  5],
        [11, 12, 13, 14, 15],
        [21, 22, 23, 24, 25]],

       [[11, 12, 13, 14, 15],
        [21, 22, 23, 24, 25],
        [31, 32, 33, 34, 35]]])
>>> c[0, 0, 0]
np.int64(1)
>>> c[-1, -1, -1]
np.int64(35)
>>> c[0, 0, 1]
np.int64(2)
>>> c[1, 0, 1]
np.int64(12)
```

### Array slicing

Working with the same three arrays `a`, `b` and `c` created above, slicing works similar to the way slicing works with `lists`. Here are a few examples:
```pycon
>>> a
array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10])
>>> a[0:3]             # From index 0 to index 2. 3 not included
array([1, 2, 3])       # returns an array
>>> a[0::2]            # From index 0, to the last index (default) at step 2
array([1, 3, 5, 7, 9])
>>> a[-1::-2]          # From index -1 (last) to the first index (default) at step -2
array([10,  8,  6,  4,  2])
>>> a[::-1]            # From index -1 (default) to -10 (default) at step -2
array([10,  9,  8,  7,  6,  5,  4,  3,  2,  1])
```
Similarly, with the two-dimensioned array `b`:
```pycon
>>> b
array([[ 1,  2,  3,  4,  5],
       [11, 12, 13, 14, 15]])
>>> b[0,:]              # Row index 0, column indices 0 (default) to last (default)
array([1, 2, 3, 4, 5])
array([1, 2, 3, 4, 5])
>>> b[1, 0:3]           # Row index 1, column indices 0 to 2
array([11, 12, 13])
>>> b[:, 0]             # Row indices 0 (default) to las t (default), column index 0
array([ 1, 11])         # Returns a one-dimensioned arrat
>>> b[:, 2]             # Row indices 0 (default) to las t (default), column index 2
array([ 3, 13])
>>> b[::-1, ::-1]       # Reverse both the rows and columns
array([[15, 14, 13, 12, 11],
       [ 5,  4,  3,  2,  1]])
>>> b[:, ::-1]          # Keep rows unchanged, reverse the columns of each row
array([[ 5,  4,  3,  2,  1],
       [15, 14, 13, 12, 11]])
```

Three-dimensioned arrays may pose some challenege initially, but with practice and experience, slicing must become second nature to a NumPy user:

```pycon
>>> c
array([[[ 1,  2,  3,  4,  5],
        [11, 12, 13, 14, 15],
        [21, 22, 23, 24, 25]],

       [[11, 12, 13, 14, 15],
        [21, 22, 23, 24, 25],
        [31, 32, 33, 34, 35]]])
>>> c[0, :, :]         # Card index 0, all rows and all columns of that card
array([[ 1,  2,  3,  4,  5],
       [11, 12, 13, 14, 15],
       [21, 22, 23, 24, 25]])
>>> c[0, 1:, 1:3]      # Card index 0, rows 1 to last (default), columns 1 to 2
array([[12, 13],
       [22, 23]])
>>> c[:, 0:2, 0:2]     # All cards (default), rows 0 to 1 and columns 0 to 1 of each card
array([[[ 1,  2],
        [11, 12]],

       [[11, 12],
        [21, 22]]])
>>> c[::-1, :, :]      # Reverse only the cards, keep rows and columns unchanged
array([[[11, 12, 13, 14, 15],
        [21, 22, 23, 24, 25],
        [31, 32, 33, 34, 35]],

       [[ 1,  2,  3,  4,  5],
        [11, 12, 13, 14, 15],
        [21, 22, 23, 24, 25]]])
```
### Filtering arrays

Slicing is useful contiguous or regularly spaced elements from an array and are very useful in a large number of situations. However, sometimes it is required to select elements from an array that satisfy some condition - this is called filtering.

As an example, to select all elements of array `a` with value greater than 4. While this can be done with a single statement, it is important to break it down and explain how filtering works.

```pycon
>>> a
>>> a
array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10])
>>> a > 4
array([False, False, False, False,  True,  True,  True,  True,  True,
        True])
>>> a[a > 4]
array([ 5,  6,  7,  8,  9, 10])
```
This is how to think about what is happeining:

1. Array `a` has 10 elements. In this specific example the values of the elements are a sequence starting from `1` up to `10` at an increment of `1`. But the same works for any array.
2. `a > 4` returns an array of the same size as `a` but with elements either `True`, if the specific values it True for that element, or `False` otherwise.
3. The array with `bool` values is used as a **mask** to filter the values of `a` - an element is not selected if the corresponding element in the `bool` array is `False` and is selected it it is `True`.
4. A new array is created by selecting the elements from the given array where the corresponding element in the mask array is `True` and discarding those corresponding to `False`.