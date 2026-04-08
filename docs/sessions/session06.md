# Session 6

#### Planned Schedule: 11-04-2026 4:00 pm to 6:00 pm

## Agenda

1. Review of previous sessions
2. Answers to queries
3. Reading and writing files
4. NumPy


## Reading and writing files
Reading from or writing to a file involves opening the file, reding from or writing to it and closing the file.It is good programming practice to close files that have been opened even though all open files will be closed when a program terminates.

The data in a file can be text or binary format. Text data consists of ASCII or UTF-8 characters and can be displayed on the screen and be understood by humans. Binary data consists of bytes and when displayed on the screen, it cannot be read by humans although computers can interpret the contents.

Python provides the context manager `with` so that when the program goes out of the scope of the context manager, the file is autmatically closed without having to explicitly close it.

### Reading text files

Create a text file named `sample.txt` using a text editor such as Notepad on Windows or `nano` or `gedit` on GNU/Linux and type the following lines in it and save it in the same directory as the program `read_file.py`.

``` title="File: samle.txt"
Hello, world!
10, 20, 30

```

Now let us open this file, read its contents and then close it in the traditional way:

```pycon
>>> f = open("sample.txt", "r")
>>> type(f)
<class '_io.TextIOWrapper'>
>>> lines = f.readlines()
>>> type(lines)
<class 'list'>
>>> len(lines)
3
print(lines)
['Hello, world!\n', '10, 20, 30\n', '\n']
>>> type(lines[0])
<class 'str'>
>>> lines[0]
'Hello, world!\n'
>>> ;ines[1]
'10, 20, 30\n'
>>> lines[2]
'\n'
f.close()
```
**Note**

1. `f = open("sample.txt", "r")` opens the file and and stores a reference to the opened file for future use. `f` is of type `<class '_io.TextIOWrapper'>`.
2. The `"r"` argument specifies the file is to be opened for reading. To write to a file, one must use `"w":"`.
3. By default, the file is opened in text format, which can be explicitly specified as `"rt"` or `"wt"`. The other mode is binary format, which is specified by `"rb"` or `"wb"`.
5. `f.readlines()` reads all lines from the file as a `list` of `str`. Each string ends with the newline character `\n`. The entire file is read in as `str`, the programmer must split and convert the strings into the required type.
6. The last line is an empty line, and contains only a newline character `\n`.
7. File must be closed when no more operations are required to be performed on it.

The alternative way is to use a **context manager**, a protocol that sets up a resource, uses it safely inside a block, and guarantees clean upafterward. A context manager can be used with such resources as a file on the filesystem, connection to a database, connection to a server etc. The typical syntax is `#!python with resource as handle_to_resource:`, followed by an indented set of statements that is treated as a block of code to be executed safely. Upon exiting the block, the resource is cleaned up, which in the case of a file means to close the file..

Here is the code to use a context manager to read the file:
```pycon
>>> with open("sample.txt", "r") as f:
...     lines = f.readlines()
...     
>>> print(lines)
['Hello, world!\n', '10, 20, 30\n', '\n']
```

**Note**

1. The context manager is indicated by the keyword `with`.
2. The function call `open("sample.txt", "r")` returns a file object.
3. The file returned by the `open()` function call is assigned the name `f`, or any other chosen by the programmer.
4. The `with` statement is followed by a block of code, indicated by the indentation of the statements.
5. There is no need to close the file as it is automatically closed when the context manager is exited.

The file can also be read one line at a time, instead of reading the entire file in one go. This is useful when the file is very large and will use substantial amount of memory. Here is the code that uses a context manager and reads one line at a time until all lines are read:
```pycon
>>> with open("sample.txt", "r") as f:
...     for line in f:
...         print(line)
...         
Hello, world!

10, 20, 30




```

**Note**

1. Using the context manager, the file `sample.txt` is opened in read mode and a file handle `f` is assigned to the opened file for future use.
2. `for line in f:` reads one line at a time from the file using the file handle `f`.
3. The `for` loop is terminated when there are no more lines to be read.
4. An empty line is printed at the end of each line because of the newline character `\n` at the end of each line read from the file. The REPL itself prints a newline. That is the reason for two empty lines for each line read from the file. The trailing newline character can be stripped at the time of printing, with `print(line.rstrip("\n"))`.

**It is a good idea to use a context manager for file operations, and must always be used unless there is a reeason not to do so.**

### Writing text files

Writing to a text file is similar to reading from a file.
```pycon
>>> with open("demo.txt", "w") as f:
...     f.write("Hello, world!\n")
...     f.write(f"{10}, {20}, {30}\n")
...
14
11
```

**Note**

1. `f.write()` takes exactly one argument. To print multiple values, use a f-string to prepare a formatted string as the argument.
2. `f.write()` does not print a newline character `\n` at the end of each erite, like `print()` does. to write the next output on a new line, end the string with a `\n`.
3. `f.write()` return the number of characters written to the file. That is the reason for the output `14` and `11`, the number of characters, including the `\n` character in the two lines written t the file.

You can open the `demo.txt` file in a text editor and read its contents.

!!! warning
    Remember what happens when you open a file for writing:

    1. If a file with the specified name exists, it overwritten from the beginning of the file.
    2. If a file with the specified name does not exist, a new file with the specified name is created.
    3. A file can be opened for writing from the end of the file, that is, appending, instead of from the start of the file. The write mode must then be specified as `"a"`. In this case, the file is not overwritten if it exists.

### Writing to a binary file

Writing to a binary file is identical to writing to a text file, except that the argument must be of type `byte` or byte-like. 

```pycon
>>> with open("demo2", "wb") as f:
...     f.write(b"Hello, world!")
```

Open the file `demo2" in a text editor and the contents can be read.

Attempting to write a `str` to a file opened for writing in binary mode raises a `typeError` exception.

```pycon
>>> with open("demo2", "wb") as f:
...     f.write("Hello, world!")
...     
Traceback (most recent call last):
  File "<python-input-9>", line 2, in <module>
    f.write("Hello, world!")
    ~~~~~~~^^^^^^^^^^^^^^^^^
TypeError: a bytes-like object is required, not 'str'
```

To write values other than strings in binary format, the value must first be converted to binary format. Here is a way to convert an integer to binary format:
```pycon
>>> import struct
>>> with open("demo3", "wb") as f:
...     f.write(struct.pack("i", 10))    # Write the integer 10 as a 4-byte signed-integer
```

Opening the file `demo2` in a text editor does not display anything human-readable. A binary/hex editor can display the contents, but as a sequence of bytes, which is difficult for humans tounderstand. However, reading file fetches the exact value of the file.
```pycon
>>> with open("demo3", "rb") as f:
...     raw = f.read(4)
...     value = struct.unpack("i", raw)[0]
...     print(value)
...     
10
```

**Note**

1. There are no newlines in a binary file. Data is a continuous stream of bytes. It is for the program to read the correct number of bytes and convert the bytes to a meaningful form. Remember, an integer could be written as a signed or an unsigned integer with either a 16-bit integer or a 32-bit size, the difference being the maximum and minimum values it can store. While reading, it must be known what format was used when the value was written, otherwise the bytes can be interpreted incorrectly.
2. For this reason, most data read and written in human readable form is in text format. Text format only contains text, it is readable in a text editor, and therefore easy to write the appropriate `read()` statements and convert the characters into data of the required types. Typically, spaces, commas, newlines and sometime specific characters such as tab, semi-colon are used as separators.
3. Binary files are efficient compared to text format, as long as the format of the file adheres to a well defined protocol. Some examples of binary files are image files in JPEG or PNG format, audio and video files in various standard formats such as MP3, FLV etc. PDF files are binary files and used to represent documents specifically for the print media.
4. Archive files in ZIP, 7ZIP format are also in binary format. All Microsoft Office files are in fact in in XML format (which is a text format) packaged inside a ZIP archive format, making them a binary file.
5. Some program can export their data from the standard binary format to a text format. Such a translation may sometimes result in a loss of richness of content. For example, an Excel file can be exported to a CSV format, but it cann represent only one sheet and cannot preserve cell formatting, formulae and macros. On the other hand, an AutoCAD DWG file can be exported to a DXF format, which is a text format with almost all features but a few such as dynamic blocks, parametric constraints, annotative objects cannot be preserved.

!!! note
    1. As a rule of thumb, use text files to read or write data from or to files unless there is a well defined format that is understood by others. If data is not understandable to humans, the storage format is of little use.
    2. When converting binary formats to text, one must be aware what information cannot be preserved and whether that loss of information is acceptable.

## NumPy

### Installing NumPy
Open Command Prompt and navigate to your project directory.

Install using `uv`
```doscon
> uv add numpy
```
or using `pip` **after** activating the virtual environment woth the command `doscon .venv\Scripts\activate`

```doscon
(.venv) > pip install numpy
```

### NumPy basics

An array, like a `list` is a container, but has stricter definition for how they are structured:

1. All elements of an array **must** be of the same type. It cannot contain a mix of types. For example, while both integers and floats are numbers, an array must contain either all integers or all floats. Thus mixing an integer with floats is not permitted, although converting an integer to a float before storing it as an element of an array is accepted,
2. In a two-dimensioned array, every row must contain the same number of columns. A "ragged" array is not permitted, for example the first row containing 3 columns while the fourth row containing 5 columns does not fit the requirements of an array. The same can be extended for higher dimensions. For example, every card in a three-dimensioned array must consist of the same number of rows and each row must consist the same number of columns.
3. An array has a fixed size once created. It is however possible to make them appear dynamic by creating a new array of a different size and copying the required elements of the original array (or add new elements not the original array) to give an appearance of dynamic size.

Arrays have the advantage of being an efficient representation of data. Since they are well structured, its elements can be efficiently repesented in binary format in memory, as well as writte to or read from files. The elements of an array are stored contiguous in memory, either ir row-major or column-major format.

1. In **row-major** format, rows are stored contiguously and the last index varies fastest. Arrays in C/C++, Python/NumPy use the row-major repesentation.
2. In **column-major** format, columns are stored contiguously and the first index varies fastest. Arrays in Fortran, Matlab, R use the row-major repesentation.

For example, consider the following two-dimensioned array, normally called a matrix:

$$
A =
\begin{bmatrix}
a_{00} & a_{01} & a_{02} \\
a_{10} & a_{11} & a_{12} \\
a_{20} & a_{21} & a_{22}
\end{bmatrix}
$$

The elements of $A$ in row-major format are stored in the following sequence in memory:

$$
a_{00}, a_{01}, a_{02}, a_{10}, a_{11}, a_{12}, a_{20}, a_{21}, a_{22}
$$

while the elements of $A$ in column-major format are stored in the following sequence in memory:

$$
a_{00}, a_{10}, a_{20}, a_{01}, a_{11}, a_{21}, a_{02}, a_{12}, a_{22}
$$

Each have their relative merits and some array operations are faster when arrays are stored in one of these two ways compared to the other. But the more important outcome is that arrays need to be translated from one format to the other if they are stored in binary format in either a file when exporting from one language to the other or in memory when exchanging array during calls from one language to the other during program execution. For example, both Python and Matlab make use of Fortran libraries, such as BLAS/LAPACK, to do the heavy lifting when implementing linear algebra operations. Thus, Python must translate its row-major array to a column-major array before handing it to a Fortran function/subroutine and vice-versa when receiving an array returned by a Fortran function/subroutine.

On the otherhand, the elements of a list require a complex arrangement in memory as different elements are of different sizes and lists are dynamic in that elements can be inserted into or deleted from a list. For this reason, a `list` is easy for humans tounderstand but difficult for programming languages to organize in memory while arrays are the opposite.

Python arrays are not a part of the definition of the language, like other indexed containers such as `list` and `tuple` are. The array data type is defined in an external package named NumPy. In addition to providing a **grammar** for array operations, NumPy provides a rich set of operators such as addition, subtraction, multiplication of a scalar with an array, multiplication of an array with another compatible array etc. This package also provides a large set of numerical algorithms from linear algebra, statistics, random number generation and Fourier transforms. NumPy makes Python similar to Matlab.

Here are the terminology used in Python with reference to **n-dimensioned** arrays:

1. The type of a NumPy array is `ndim`, short for n-dimensioned array or a multi-dimensioned array. These terms are used interchangeably.
2. The type of each element of an array is the same and for a NumPy array, this attribute is called `dtype`
3. Indices start with zero (`0`).
4. The number of dimensions of an array is called `ndim`. Thus, for a one-dimensioned array, `ndim=1`. A two-dimensioned array has `ndim=2`, a three-dimensioned array has `ndim=3` and so on. An empty array (with zero elements) has `ndim=1`.
5. Each dimension of an array is called an `axis`. Thus, in a two-dimensioned array, rows have `axis=0` and columns have `axis=1`. A one-dimensioned array has only `axis-0`, where as a three-dimensioned array has three axes. `axis=0` is one card with a specified number of rows and columns in it. `axis=1` is one specific row on one of the cards. `axis=2` is one specific column in a chosen row. The last index varies fastes or alternately, left most index varies slowest.
6. The `shape` of an array is a `tuple` repesenting the size of of the array along each axis. Thus, the shape of a one-dimensioed array with five elements is `(5,)` (do not neglect the required comma (`,`) after the number `5`). The shape of a two-dimensioned array with 3 rows and four columns is `(3, 4)`. The shape of a three-dimensioned array with two cards, each with three rows and four columns is `(2, 3, 4)`.
7. The `size` of an array is the total number of elements of an array along all its axes.
8. Elements of an array can be accessed using its indices along each axis. Thus, accessing an element of a one-dimensioned array requires one index. Accessing an element of a two-dimensioned array requires two indices, the first index along the first axis (the row index) and the second index along the second axis (the column). Thus the element in the first row and first column has the index `[0, 0]` as indexing starts with `0`. Typically, an element in the row `i` and column `j` of a two-dimensioned array have the indices `[i-1, j-1]`, `i-1` being the row index and `j-1` being the column index.
9. Indexing is written differently for an array compared to that of a list. While index of an element in row `0` and column `0` of a list `a` is written as `a[0][0]`, the same eement in an array with the the name `b` is written as `b[0, 0]`.
10. Slice operation on an array is similar to a slice operation on a list.

### Creating NumPy arrays

NumPy provides several methods to easily create arrays:

1. `array()` creates an array from a `list` or `tuple`, but arrays are mutable like a `list`.
2. `zeros()` creates an array of a specified size and type, with all elements initialized to `0`.
3. `ones()` creates an array of a specified size, with all elements initialized to `1`.
4. `diag()` creates a diagonal array using the given `list` of elements placed along the main diagonal of the array.

By convention the NumPy array is imported as `np` although it could be assigned any other name by the programmer. Here is the code to create a one-dimensioned array with the elements `10`, `20`, `30`, `40`, and `50`.

```pycon
>>> import numpy as np
>>> a = np.array([10, 20, 30, 40, 50])
>>> print(a.ndim, a.shape, a.size, a.dtype)
1 (5,) 5 int64
>>> print(a[0])
10
```

**Note**

1. This creates a one-dimensioned array from a one-dimensioned list. Since all elements of the lsit are integers, Python automatically creates an array with `dtype = int64`, an 64-bit (8-byte) integer.
2. `ndim = 1`
3. `shape = (5,)`, a `tuple` with one integer element, repesenting the size of the array.
4. `size = 5`, the number of elements in the array.

If one of the elements in the list is a `float`, NumPy automatically makes the entire array of type `float`.

```pycon
>>> import numpy as np
>>> a = np.array([10.0, 20, 30, 40, 50])
>>> print(a.ndim, a.shape, a.size, a.dtype)
1 (5,) 5 float64
>>> print(a[0])
10.0
```

Looping over the array can be done as follows:
```pycon
>>> a = np.array([10, 20, 30, 40, 50])
>>> for i in range(len(a)):
...     print(a[i], end=" ")
...     
10 20 30 40 50
```

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

### Creating NumPy arrays using `range`

NumPy has a function named `arange()`, which is similar to the `range()` function that waas studied in earlier sessions. But there are some differences:

1. `arange()` can have `float` values for `start`, `stop` and `step`.
2. `arange()` returns a `numpy.ndarray` instead of a `list`.

```pycon
>>> a = np.arange(0, 5, 0.5)
>>> a
array([0. , 0.5, 1. , 1.5, 2. , 2.5, 3. , 3.5, 4. , 4.5])
>>> print(type(a), len(a), a.shape, a.size, a.dtype)
<class 'numpy.ndarray'> 10 (10,) 10 float64
```