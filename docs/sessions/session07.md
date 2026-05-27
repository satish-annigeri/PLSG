# Session 7: Working with NumPy - Part 2

**Date: 18-04-2026 4:00 pm to 6:00 pm**

## Agenda

1. Review of previous sessions
2. Answers to queries
3. NumPy (contd. from Session 6)

## NumPy arrays (contd. from Session 6)

### Empty array

Creating an empty array of given `shape` and `dtype` results in an array whose elements are **uninitialized**, that is, memory is allocated for the elements but their values are not set to any specific value.
```pycon
>>> a = np.empty((2, 3), float)
>>> print(a.ndim, a.shape, a.dtype)
2 (2, 3) float64
>>> a
array([[-6.95293776e-310, -5.62781092e-131,  9.01802659e-312],
       [ 9.01802659e-312,  6.91691904e-323,  0.00000000e+000]])
```
**Note:** The elements in the example above are not zeros, if they are, it is a coincidence. The values must be treated as **unknown** and cannot be relied upon as having any specific value.

`np.empty_like()` creates an empty array having the same `shape` and `dtype` as an existing array.
```pycon
>>> a = np.array([[1, 2, 3], [4, 5, 6]])
>>> a
array([[1, 2, 3],
       [4, 5, 6]])
>>> b = np.empty_like(a)
>>> b
array([[0, 0, 0],
       [0, 0, 0]])
```

It is possible to create an empty array with no elements:
```pycon
>>> a = np.array([])
>>> print(type(a), a.shape, a.dtype)
<class 'numpy.ndarray'> (0,) float64
>>> b = np.empty((0,))
>>> print(type(b), b.shape, b.dtype)
<class 'numpy.ndarray'> (0,) float64
```

### Special Arrays

Use `np.zeros()` and `np.ones()` to create arrays filled with `0` or `1`.

**1D Array Example:**
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

**Notes:**  
1. For 1D arrays, specify size as a `tuple` `(5,)` or an `int` `5`.  
2. Default `dtype` is `float`.  
3. Use the `dtype` argument to specify a custom type.

To create an array having the same `shape` and `dtpye` as an existing array but all values equal to `1`, use the `np.zeros_like()` function:
```pycon
>>> a = np.array([[1, 3, 5, 7], [-2, 8, 2, 1]])
>>> a
array([[ 1,  3,  5,  7],
       [-2,  8,  2,  1]])
>>> b = np.ones_like(a)
>>> b
>>> a
array([[ 1,  3,  5,  7],
       [-2,  8,  2,  1]])
>>> b = np.ones_like(a)
>>> b
array([[1, 1, 1, 1],
       [1, 1, 1, 1]])
```

**`np.ones()` works similarly, filling arrays with `1`:**
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

**`np.ones_like()`** works similar to `np.zeros_like()`
```pycon
>>> c = np.ones(a)
>>> c
>>> a
array([[ 1,  3,  5,  7],
       [-2,  8,  2,  1]])
>>> b = np.ones_like(a)
>>> b
array([[1, 1, 1, 1],
       [1, 1, 1, 1]])
```

**`np.full(shape: tuple, fill_value)`** creates an array of the specified `shape` filled with `fill_value`. **`np.full_like(a: ndarray, fill_value)`** creates an array with the same `shape` as the specified array `a` filled with `fill_value`.
```pycon
>>> x = np.full((3, 4), 100)
>>> y = np.full_like(x, 200)
>>> y
array([[200, 200, 200, 200],
       [200, 200, 200, 200],
       [200, 200, 200, 200]])
```

**`np.asarray()`** converts the input into an array. The input can be a `list`, `list` of `list`s, `list` of `tuple`s, `tuple`s, `tuple`s of `tuple`s, `tuple`s of `list`s or `ndarray`s.
```pycon
>>> a = [1, 2, 3]
>>> type(a)
<class 'list'>
>>> a
[1, 2, 3]
>>> b = np.asarray(a)
>>> print(type(b), b.shape, b.dtype)
<class 'numpy.ndarray'> (3,) int64
>>> b
array([1, 2, 3])
```

**Diagonal Arrays:**
`np.diag()` creates a square 2D array with specified elements on the main diagonal.
```pycon
>>> a = np.diag([1, 2, 3])
>>> a
array([[1, 0, 0],
       [0, 2, 0],
       [0, 0, 3]])
>>> print(type(a), len(a), a.shape, a.size, a.dtype)
<class 'numpy.ndarray'> 3 (3, 3) 9 int64
```

**Notes:**  
1. Argument must be a `list` or `tuple`.  
2. The resulting array is always square and 2D.  
3. `dtype` is determined by the input elements. Mixed types are automatically upcast (e.g., `int` to `float`).

`numpy.diag()` can be used to place an list/array of numbers on a matrix diagonal. The k argument determines the position:

- **`k = 0` (default):** The main (center) diagonal.
- **`k > 0`:** Shifts the list/array above the main diagonal.
- **`k < 0`:** Shifts the list/array below the main diagonal.

The size of the array created is decided by the size of the list/array of numbers in the first argument:
```pycon
>>> x = np.diag([10, 20, 30], 1)
>>> x
array([[ 0, 10,  0,  0],
       [ 0,  0, 20,  0],
       [ 0,  0,  0, 30],
       [ 0,  0,  0,  0]])
>>> y = np.diag([10, 20, 30], -1)
>>> y
array([[ 0,  0,  0,  0],
       [10,  0,  0,  0],
       [ 0, 20,  0,  0],
       [ 0,  0, 30,  0]])
```

### Range-based Array Creation

`np.arange()` is similar to Python's `range()`, but:  
1. It supports `float` values for `start`, `stop`, and `step`.  
2. It returns a `numpy.ndarray` instead of a `list`.  

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
1. `start` is inclusive.  
2. `stop` is exclusive.  
3. `step` can be a positive or negative `float`.

**`np.linspace()`** generates `num` evenly spaced values over the interval `[start, stop]`. Both endpoints are **included**.

```pycon
>>> x = np.linspace(0, 2 * np.pi, 17)
>>> x = np.linspace(0, 2 * np.pi, 17)
>>> x
array([0.        , 0.39269908, 0.78539816, 1.17809725, 1.57079633,
       1.96349541, 2.35619449, 2.74889357, 3.14159265, 3.53429174,
       3.92699082, 4.3196899 , 4.71238898, 5.10508806, 5.49778714,
       5.89048623, 6.28318531])
```

**Notes:**  
1. The last argument is the **number of points** generated. For 10 equal intervals, use `num = 11`.  
2. `num` is optional and defaults to `50`.

### Creating Multi-dimensional Arrays

2D arrays require a nested list with an equal number of columns in each row.
```pycon
>>> a = np.array([ [1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]])
>>> print(a.ndim, a.shape, a.size, a.dtype)
2 (3, 4) 12 int64
```

A 3D array consists of multiple "cards" (2D arrays), each with specified rows and columns:
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

!!! tip "Tip"
    Pay close attention to commas between elements, rows, and cards. Formatting the input data vertically as shown above improves readability.

    The number of leading left brackets equals `ndim`.


### Operations on Arrays

NumPy supports standard linear algebra operations.

**Transpose**
The `.T` attribute interchanges rows and columns in 2D arrays.
```pycon
>>> a.T
array([[1, 5],
       [2, 6],
       [3, 7],
       [4, 8]])
```
!!! note
    A 1D array has no row/column orientation; transposing it returns the same array.
    ```pycon
    >>> c = np.array([1, 2, 3, 4])
    >>> c.T
    array([1, 2, 3, 4])
    ```
    For higher dimensions, `.T` reverses the axis order (e.g., `(2, 3, 4)` becomes `(4, 3, 2)`).

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

**Scalar Multiplication**
```pycon
>>> a = np.array([[1, 2, 3, 4], [5, 6, 7, 8]])
>>> 2 * a  # Multiplication by the scalar 2
array([[ 2,  4,  6,  8],
       [10, 12, 14, 16]])
```

**Addition and Subtraction**
Arrays must have the same `shape`.
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

**Element-wise Multiplication**
Requires the same `shape`. Each element is multiplied by its corresponding partner.
```pycon
>>> a * b
array([[ 10,  40,  90, 160],
       [250, 360, 490, 640]])
```

**Matrix Multiplication**
For 2D arrays, the number of columns in the first array must equal the number of rows in the second. Use the `@` operator or `np.dot()`.
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

### Reshaping and Resizing

!!! note
    1. **Reshaping:** Changes the *view* of the data (minimal memory overhead).
    2. **Resizing:** Changes the *size* of the underlying buffer (may reallocate memory).

#### Reshaping
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
The `-1` placeholder tells NumPy to automatically calculate the necessary dimension.

#### Resizing
The `np.resize()` **function** creates a *new* array. It truncates the array if the new size is smaller or repeats values if it is larger.
```pycon
>>> a = np.array([1, 2, 3])
>>> b = np.resize(a, 5)
>>> b
array([1, 2, 3, 1, 2])
>>> a
array([1, 2, 3])
```
You can reshape while resizing by passing a `tuple`:
```pycon
>>> a = np.array([1, 2, 3])
>>> np.resize(a, (2, 4))
array([[1, 2, 3, 1],
       [2, 3, 1, 2]])
>>> a
array([1, 2, 3])
```

The `ndarray.resize()` **method** modifies the array **in-place**, filling new slots with zeros.
```pycon
>>> a = np.array([1, 2, 3])
>>> a.resize(5)
>>> a
array([1, 2, 3, 0, 0])
```
!!! warning
     The `.resize()` method is **in-place**. It does not return a new array.

### Combining different methods of creating arrays

With the knowledge of basic operations of arrays, it is possible to create more complex arrays by combining the different methods of combining arrays.
```pycon
>>> a = np.diag(np.ones(3) * 10) + np.diag(np.ones(2) * 5, 1) + np.diag(np.ones(2) * 5, -1)
>>> a
array([[10.,  5.,  0.],
       [ 5., 10.,  5.],
       [ 0.,  5., 10.]])
```

**Note**

1. `a` is the sum of three matrices (two-dimensioned arrays).
2. `np.ones(3) * 10` returns a one-dimensioned array of three elements, each element equal to `10`, and `np.diag()` places this array on the main  diagonal of an array of size `3x3`.
3. `np.diag(np.ones(2) * 5, 1)` does the same with an array of two elements, each element equal to `5` placed **above** the main diagonal resulting in a `3x3` array. This array is then added to the `3x3` array created in the previous step.
4. `np.diag(np.ones(2) * 5, -1)` does the same with an array of two elements, each element equal to `5` placed **below** the main diagonal resulting in a `3x3` array. This array is then added to the `3x3` array created in the previous step.

### Array Indexing

NumPy indices are enclosed in a single pair of square brackets: `[i, j]`.

* **2D:** `[row, column]`
* **3D:** `[card, row, column]`
* **Negative Indexing:** `-1` is the last element along a chosen axis.

**1D Array:**
```pycon
>>> a = np.arange(1, 11)
>>> a[0]
np.int64(1)
>>> a[-1]
np.int64(10)
```

**2D Array:**
```pycon
>>> b = np.array([np.arange(1, 6), np.arange(11, 16)])
>>> b[0, 0]
np.int64(1)
>>> b[-1, -1]
np.int64(15)
```

**3D Array:**
```python
>>> c = np.array([
... [np.arange(1, 6), np.arange(11, 16), np.arange(21, 26)],
... [np.arange(11, 16), np.arange(21, 26), np.arange(31, 36)]])
>>> c[0, 0, 0]
np.int64(1)
>>> c[-1, -1, -1]
np.int64(35)
```

### Array Slicing

Slicing uses `[start:stop:step]`. The `stop` index is exclusive.

**1D Slicing:**
```pycon
>>> a = np.arange(1, 11)
>>> a[0:3]             # Indices 0 to 2
array([1, 2, 3])
>>> a[0::2]            # Every second element from index 0
array([1, 3, 5, 7, 9])
>>> a[::-1]            # Reverse the array
array([10,  9,  8,  7,  6,  5,  4,  3,  2,  1])
```

**2D Slicing:**
```pycon
>>> b = np.array([[ 1,  2,  3,  4,  5],
       [11, 12, 13, 14, 15]])
>>> b[0,:]              # All of row 0
array([1, 2, 3, 4, 5])
>>> b[1, 0:3]           # Row 1, columns 0 to 2
array([11, 12, 13])
>>> b[:, 0]             # All rows, column 0
array([ 1, 11])
>>> b[::-1, ::-1]       # Reverse both rows and columns
array([[15, 14, 13, 12, 11],
       [ 5,  4,  3,  2,  1]])
```

**3D Slicing:**
```pycon
>>> c[0, :, :]         # Card 0, all rows and columns
array([[ 1,  2,  3,  4,  5],
       [11, 12, 13, 14, 15],
       [21, 22, 23, 24, 25]])
>>> c[:, 0:2, 0:2]     # All cards, rows 0-1, columns 0-1
array([[[ 1,  2],
        [11, 12]],

       [[11, 12],
        [21, 22]]])
```

### Filtering Arrays

Filtering selects elements that satisfy a condition using a **boolean mask**.

```pycon
>>> a = np.array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10])
>>> a > 4
array([False, False, False, False,  True,  True,  True,  True,  True,
        True])
>>> a[a > 4]
array([ 5,  6,  7,  8,  9, 10])
```

**Logic:**  
1. `a > 4` creates a boolean array (the **mask**) of the same size as `a`.  
2. Elements are `True` if they meet the condition, `False` otherwise.  
3. `a[mask]` returns a new array containing only the elements where the mask is `True`.

### Concatenating arrays

```pycon
>>> a = np.array([[1, 2], [3, 4]])   # Two-dimensioned array with shape = (2, 2)
>>> b = np.array([[5, 6]])           # Two-dimensioned array with shape = (1, 2)
>>> a
array([[1, 2],
       [3, 4]])
>>> b
array([[5, 6]])
>>> np.concatenate((a, b), axis=0)    # a.shape = (2, 2), b.shape = (1, 2)
array([[1, 2],
       [3, 4],
       [5, 6]])
>>> np.concatenate((a, b.T), axis=1)  # a.shape = (2, 2), b.T.shape = (2, 1)
array([[1, 2, 5],
       [3, 4, 6]])
```

**Note**

1. `axis = 0` adds new **rows** to the first two-dimensioned array
2. `axis = 1` adds new **columns** to the first two-dimensioned array
3. This logic can be extended to n-dimensioned arrays. All the input array dimensions except for the concatenation axis must match exactly

```pycon
>>> x = np.zeros((2, 3, 4), dtype=float)  # shape = (2, 3, 4)
>>> y = np.ones((1, 3, 4))                # shape = (1, 3, 4)
>>> z = np.ones((2, 2, 4))                # shape = (2, 2, 4)
>>> x
array([[[0., 0., 0., 0.],
        [0., 0., 0., 0.],
        [0., 0., 0., 0.]],

       [[0., 0., 0., 0.],
        [0., 0., 0., 0.],
        [0., 0., 0., 0.]]])
>>> y
array([[[1., 1., 1., 1.],
        [1., 1., 1., 1.],
        [1., 1., 1., 1.]]])
>>> z
array([[[1., 1., 1., 1.],
        [1., 1., 1., 1.]],

       [[1., 1., 1., 1.],
        [1., 1., 1., 1.]]])
>>> np.concatenate((x, y), axis=0)  # axis = 0, shape(2, 3, 4) shape(1, 3, 4) = shape(3, 3, 3)
array([[[0., 0., 0., 0.],
        [0., 0., 0., 0.],  # axis = 0, shape(2, 3, 4) shape(1, 3, 4) = shape(3, 3, 4)
        [0., 0., 0., 0.]],

       [[0., 0., 0., 0.],
        [0., 0., 0., 0.],
        [0., 0., 0., 0.]],

       [[1., 1., 1., 1.],
        [1., 1., 1., 1.],
        [1., 1., 1., 1.]]])
>>> np.concatenate((x, z), axis=1)  # axis = 0, shape(2, 3, 4) shape(2, 2, 4) = shape(2, 5, 4)
array([[[0., 0., 0., 0.],
        [0., 0., 0., 0.],
        [0., 0., 0., 0.],
        [1., 1., 1., 1.],
        [1., 1., 1., 1.]],

       [[0., 0., 0., 0.],
        [0., 0., 0., 0.],
        [0., 0., 0., 0.],
        [1., 1., 1., 1.],
        [1., 1., 1., 1.]]])
```

**Note**

1. `np.concat()` is the same as `np.concatenate()`.
2. `np.concatenate((a, b), axis=0)` is the same as `np.vstack((a, b))` provided the shapes are compatible.
3. `np.concatenate((a, b), axis=1)` is the same as `np.hstack((a, b))` provided the shapes are compatible.

### Mathematical functions

NumPy’s primary strength lies in its ability to perform **vectorized operations**. Rather than manually looping through elements, NumPy applies mathematical functions to every element in an array simultaneously, returning a new array of the same shape.

```pycon
>>> import numpy as np
>>> x = np.linspace(0, 2 * np.pi, 33)
>>> y = np.sin(x)
>>> print(x.shape, y.shape)
(33,) (33,)
```

While NumPy supports all standard functions available in Python's math module, it also provides specialized functions for array manipulation, such as `np.sum()` and `np.cumsum()`. These operations are compatible with arrays of any dimension. By eliminating the need for explicit loops, NumPy makes code more efficient and allows mathematical expressions to closely resemble their formal notation.

For a complete list of operations, refer to the [NumPy mathematical function documentation](https://numpy.org/doc/stable/reference/routines.math.html#).

