# Session 9: Object Oriented Programming - Part 1

**Date: 02-05-2026 4:00 pm to 6:00 pm**

## Agenda

1. Review of previous sessions
2. Answers to queries
3. Object Oriented Programming in Python
4. Reading and writing data with Pandas


## Programming Paradigms

A programming paradigm is an approach or "style" of designing and implementing software. While you can design a program's logic independently of a specific language, actually building (implementing) it requires a language that supports your chosen paradigm.

### Procedural vs. Object-Oriented Programming

The **procedural paradigm** focuses on **algorithms** (procedures) as the core of program design.

*   **Design:** It starts with a main task and breaks it down into smaller, simpler sub-tasks. This is represented as a hierarchy of functions. Each function achieves a well-defined result; higher-level functions depend on lower-level ones to work.
*   **Implementation:** Development begins with the lowest-level functions and progresses toward the "top" until the `main` function is complete.

The **object-oriented paradigm (OOP)** puts **objects** at the center of design and implementation (See [OOP](../resources/prog_paradigms.md#object-oriented-paradigm-oo-paradigm)).

*   **Design:** It identifies the objects within a problem statement. For each object, it defines its **attributes** (data) and the **operations** (logic) needed to transform input into the desired output. This design is often visualized using class diagrams and state diagrams.
*   **Implementation:** Development starts with the most independent classes and moves toward dependent ones. Once the classes are built, the `main` function creates (**instantiates**) the objects and calls their methods to produce the final result.

---

## Object Oriented Programming in Python

In his 1976 book, *Algorithms + Data Structures = Programs*, Niklaus Wirth explained that algorithms and data structures are inherently related. 

In traditional procedural programming, functions organize logic, but there is no formal way to "bind" that logic to specific data. Programmers have to manually keep track of which function belongs to which data through naming conventions or documentation.

**Classes** are user-defined types designed to unify logic and data into a single entity. (See [Allen B. Downey, Think Python, 3ed.](https://allendowney.github.io/ThinkPython/chap14.html#classes-and-functions)). A class consists of:

*   **Attributes:** Data fields that represent the characteristics or "state" of an entity.
*   **Methods:** Functions defined within the class that operate specifically on its attributes.

By grouping these together, classes use **encapsulation** to make the relationship between data and logic explicit. This makes the program's intent clearer and easier to maintain, as the data and the tools used to change it are housed in the same "blueprint."

### Blueprints and Instances

While a class is a **blueprint**, the objects created from it are **instances**. Think of a class as an empty registration form that defines what information is required. An instance is the actual filled-out form, containing unique data for a specific person.

### Modeling the Real World

Classes allow us to model real-world entities through **abstraction**. By identifying the essential qualities of an object and the actions it performs, we create a digital version of it. 

#### Example 1: Structural Engineering
Consider a program designed to model a structural beam:

*   **Attributes:** Span, cross-section shape, size and location, and design forces at cross-sections.
*   **Operations (Methods):** Calculating the required reinforcement or determining how to detail the steel between sections.

#### Example 2: Library Management
Consider a program for a library. While the library has many parts (users, shelves, etc.), let's look at the **Book** object:

*   **Attributes:** Title, authors, publisher, and ISBN.
*   **Operations (Methods):** Lending the book to a user, returning it to the shelf, or displaying its bibliographic information.

In practice, a Python program defines the classes needed for a specific problem and creates instances of them. It then triggers methods to transform the data within those instances or to help different objects interact—using data from one object to generate new information for another.

### Example: A Line Counting Program

The task is to write a program to scan a specified directory for filenames with a specified pattern (such as `*.txt`) and, if found, to print the name of the file and the number of lines contained in the file.

#### Design

The program has one main object: the starting directory from where to begin the search. Its attributes are:

1. Directory name
2. File pattern
3. Flag to recursively search sub-directories

The operations to perform on the directory are:

1. Search the directory and make a list of matching filenames
2. Process each file by counting the number of lines contained in the file
3. Display the filename and number of lines

Python is said to be "batteries included" because it provides a large number of built-in and third-party packages to efficiently accomplish tasks without us having to write our own code from scratch. Searching directories for matching filename patterns is one such task. The built-in package [`pathlib`](https://docs.python.org/3/library/pathlib.html) is well-suited for this task, and we will make use of it.

Having prepared a list of matching filenames, counting the number of lines is a process known to us from [Session 6: Reading and writing files](https://plsg.netlify.app/sessions/session06/#reading-and-writing-files).

#### Implementation

Before we begin implementing the class, let us learn the basics of the built-in package `pathlib`, by trying it out in the Python REPL:

```pycon
>>> from pathlib import Path
>>> p = Path(".")
>>> p.absolute()
PosixPath('/home/satish/Python/sci')
>>> p.exists()
True
>>> p.is_dir()
True
>>> p.is_file()
False
>>> flist = p.glob("*.py")
>>> type(flist)
<class 'map'>
>>> for f in flist:
...     print(f.name)
...     
vector.py
main.py
vector2.py
searchdir.py
```

**Note**

1. `Path` is the path object imported from the `pathlib` package.
2. A `Path` object has methods such as `absolute()` that returns the absolute path of a directory, `exists()` that returns `True` if a file or a directory with the specified path exists, `is_dir()` that returns `True` if the path is a directory, and `is_file()` that returns `True` if the path is a file and [many more](https://docs.python.org/3/library/pathlib.html).
3. The method `glob()` returns a collection of paths that match a given pattern, such as `"*.py"`. If there are files with matching names, we can loop over them and process them one at a time. **Useful tip:** `glob()` returns a *generator* (not a `list`), which can be directly iterated over without having to first convert it to a list.

Let us begin by naming the class `SearchDir`. Python convention is to name classes starting with a capital letter and using capital letters for each word in the name (PascalCase). This is in contrast to the `snake_case` style used for functions. Here is the code to define our class:

```python linenums="1" title="searchdir.py"
from pathlib import Path


class SearchDir:
    def __init__(self, dirpath: str, pattern: str, recurse: bool=False):
        p = Path(dirpath).absolute()
        if p.is_dir():
            self.path = Path(dirpath)
            self.pattern = pattern
            self.recurse = recurse
        else:
            raise ValueError(f"Path {dirpath} must be a directory")

    def __str__(self) -> str:
        return f"SearchDir({self.path.absolute()}, {self.pattern}, {self.recurse})"


if __name__ == "__main__":
    dir1 = SearchDir(".", "*.py")
    print(dir1)
    dir2 = SearchDir(".", "*.py", False)
    print(dir2)
```

!!! tip
    `self` is the variable that represents an instance of the class. While it could be assigned a different name, Python convention is to name this variable `self`. It represents, at the time of defining a class, the specific instance of the object that will be created later. Since the object to be created later may have a name chosen at runtime, `self` acts as a placeholder for that name within the class definition.

!!! note
    Methods with names beginning and ending with double underscore characters (`__`) are called **dunder** (**D**ouble **UNDER**score) methods. They have special meanings in the Python language and must not be used as names for regular user-defined functions or methods. We will learn more dunder methods later on.

**Note**

1. `__init__()` is a special method which is used to initialize an object when it is first created (C++ clalls such a function a **constructor**). It merely copies the values from the arguments into the **data field** of the object. This calss has three data fields, namely `self.dirpath`, `self.pattern` and `self.recurse`.
2. The last data field `self.recurse` defaults to `False` if not specified at the time of creating the instance.
3. `__str__()` is a dunder method that is expected to return a string representation of the object. If present, `print()` uses this method to print the value of the object instead of using the default repesentation.

The test run must produce an output similar to the following, depending on the name of the directory in your specific case:

```pycon
> uv run -- python searchdir.py
SearchDir(/home/satish/Python/sci, *.py, True)
SearchDir(/home/satish/Python/sci, *.py, False)
```
**Note:**

1. `pathlib` is cross-platform and understands how filesystems are repersented on Windows, GNU/Linux, macOS and any other on which it runs.
2. It correctly reerpsents the path separator as the forward slah (`/`) on GNU/Linux and macOS and the backslash (`\\`). The backslash is hsown as two backslashes becuase the backslash is used as the escape sequence, such as in representing a newline (`\n`) and the backslash itself is repersented as two backslashes.
3. The above code was run on GNU/Linux. The output will differ slightly in Windows. For example, it would be similar to `C:\\Users\\satish\\Documents\\Python\\sci` on Windows.

Let us add the functionality to count the number of lines in the file by adding the method `linecount()` and test it.

```python linenums="13" hl_lines="5 6 7 8 13" title="serachdir.py"
    # Previous lines not shown
    def __str__(self) -> str:
        return f"SearchDir({self.dirpath}, {self.pattern}, {self.recurse})"

    def linecount(self, fname):
        with open(fname) as f:
            lines = f.readlines()
        return len(lines)

if __name__ == "__main__":
    dir = SearchDir(".", "*.py")
    print(dir)
    print(dir.linecount("searchdir.py"))
```

We can now add another method `search_print()` to search for filenames matching a pattern and print their names along with the number of lines in the file using the method `linecount()`:

```python linenums="16" title="searchdir.py" hl_lines="7-19 24"
    # Previous lines not shown
    def linecount(self, fname):
        with open(fname) as f:
            lines = f.readlines()
        return len(lines)

    def search_print(self):
        flist = self.path.rglob(self.pattern) if self.recurse else self.path.glob(self.pattern)
        flist = list(flist)
        if len(flist) == 0:
            print(f"No files matching {self.pattern} found")
            return

        total_lines = 0
        for i, f in enumerate(sorted(flist), 1):
            num_lines = self.linecount(f)
            total_lines += num_lines
            print(f"{f} ({num_lines})")
        print(f"Files: {i}, Total lines: {total_lines}")

if __name__ == "__main__":
    dir = SearchDir(".", "*.py")
    print(dir, "\n")
    dir.search_print()
```


**Note**

1. `enumerate(<container_object>, <start_value>=0)` returns a `tuple` consisting of an integer and an element from `<container_object>`, one element at a time, starting with `<start_value>` for the first element and defaults to `0` when not specified. That way the elements of a container object can be indexed without having to use `for i in range(len(container)):` looping index.
2. The list of files returned by `glob()` or `rglob()` are not in alphabetical order, and may need the use of `sorted()` in case they are to be listed in alphabetical order.

The output may look similar to the following:
```pycon
SearchDir(/home/satish/Python/sci, *.py, False)

main.py (10)
searchdir.py (34)
vector.py (37)
vector2.py (41)
Files: 4, Total lines: 122
```

!!! tip
    To check if there are no filenames matching the specified pattern, it is best to convert `flist`, which is a `map` to a `list` and check if the length of the list is `0`, and print an appropriate message if that is true.

## Pandas

Pandas is a software library for the Python programming language for data manipulation and analysis. In particular, it offers data structures and operations for manipulating numerical tables and time series. It is free software released under the three-clause BSD license. The name is derived from the term "panel data", an econometrics term for data sets that include observations over multiple time periods for the same individuals, as well as a play on the phrase "Python data analysis" (See [Pandas - Wikipedia](https://en.wikipedia.org/wiki/Pandas_(software))).

The library is built around two primary data structures: the Series (a one-dimensional labeled array) and the DataFrame (a two-dimensional labeled tabular structure). A DataFrame is analogous to a spreadsheet or SQL table, where columns can contain different data types (integers, strings, floats, etc.). It acts as an "invisible spreadsheet" that allows you to perform complex data operations programmatically and at scale.

While it is widely known for reading and writing CSV and Microsoft Excel files, Pandas is also compatible with a vast array of formats including JSON, SQL databases, HDF5, and Apache Parquet.

The typical data science workflow involves importing raw data from these formats, performing data cleaning and exploratory analysis, and then either exporting the refined data back to a file (such as .csv or .xlsx) or passing it directly into a machine learning pipeline. The structural engineer's workflow may involve reading data output by structural analysis prorgams such as STAAD.Pro, ETABS, SAP2000 etc., carry out design of sections and members and write a design summary to a file.

At present [Polars](https://pola.rs/) offers a similar data structure with a different API but being much faster, is gaining ground. [Narwhals](https://narwhals-dev.github.io/narwhals/) offers a compatibility layer between dataframe libraries thereby enabling writing code once and being able to change the backend dataframe engine at any time. Pandas being the first dataframe library is still popular and is evolving to catch up with the likes of Polars.

### Install
Install using `uv` or `pip` and test that it is installed correctly.

=== "Using `uv`"
    ```doscon
    > uv add pandas
    > uv run -- python -c 'import pandas; print(pandas.__version__)'
    3.0.2
    ```

=== "Using `pip`"
    ```doscon
    > pip install pandas
    > .venv\Scripts\activate
    (.venv) > python -c 'import pandas; print(pandas.__version__)'
    3.0.2
    ```

### Basic Example

DataFrame object can be created using a `dict` as input:

```pycon
>>> import pandas as pd
>>> df = pd.DataFrame({
... "A": [10, 20, 30, 40],
... "B": ["Sunday", "Monday", "Tuesday", "Wednesday"]
... })
>>> df
    A          B
0  10     Sunday
1  20     Monday
2  30    Tuesday
3  40  Wednesday
>>> len(df)
4
>>> df["A"]
0    10
1    20
2    30
3    40
Name: A, dtype: int64
>>> df["B"]
0       Sunday
1       Monday
2      Tuesday
3    Wednesday
Name: B, dtype: str
>>> df["A"].sum()
np.int64(100)
```
**Note**

1. The **key** in the `dict` becomes the name of the column.
2. The **value** is a list of elements and becomes the rows of that column.

### Reading data from files

Pandas can read data from files in a variety of formats, including `.CSV` and `.xlsx`. Consider the data in the following CSV file named **sales_data.csv**:

```csv title="sales_data.csv"
order_id,order_date,customer_name,category,product,quantity,unit_price,region
1001,2023-01-15,Alice Johnson,Electronics,Headphones,1,50.00,North
1002,2023-01-16,Bob Smith,Furniture,Office Chair,2,120.00,South
1003,2023-01-17,Charlie Brown,Electronics,USB Cable,3,15.00,North
1004,2023-01-18,Alice Johnson,Furniture,Desk Lamp,1,35.00,North
1005,2023-01-19,David Miller,Clothing,T-Shirt,5,20.00,East
1006,2023-01-20,,Clothing,Hoodie,2,45.00,West
1007,2023-01-21,Frank White,Electronics,Smartphone,1,600.00,South
1008,2023-01-22,Bob Smith,Clothing,T-Shirt,3,20.00,South
1009,2023-01-23,Grace Lee,Furniture,Bookshelf,1,150.00,East
1010,2023-01-23,Grace Lee,Furniture,Bookshelf,1,150.00,East

```
Copy the above data and paste into a text editor and save it with the name `sales_data.csv`. Type the following code into the Python REPL:
```pycon linenums="1" hl_lines="1 2 4 5 14 16 18 22 24 34"
>>> import pandas as pd       # Import pandas package
>>> print(pd.__version__)     # Print pandas version
3.0.2
>>> df = pd.read_csv("sales_data.csv")     # Read data from CSV file
>>> print(df.head())                       # Print first 5 lines
   order_id  order_date  customer_name  ... quantity unit_price  region
0      1001  2023-01-15  Alice Johnson  ...        1       50.0   North
1      1002  2023-01-16      Bob Smith  ...        2      120.0   South
2      1003  2023-01-17  Charlie Brown  ...        3       15.0   North
3      1004  2023-01-18  Alice Johnson  ...        1       35.0   North
4      1005  2023-01-19   David Miller  ...        5       20.0    East

[5 rows x 8 columns]
>>> len(df)            # Print the number of rows
10
>>> len(df.columns)    # Print the number of columns
8
>>> df.columns         # Print names of columns
Index(['order_id', 'order_date', 'customer_name', 'category', 'product',
       'quantity', 'unit_price', 'region'],
      dtype='str')
>>> df.index           # Print row index
RangeIndex(start=0, stop=10, step=1)
>>> df.dtypes          % Print dtype of each column
order_id           int64
order_date           str
customer_name        str
category             str
product              str
quantity           int64
unit_price       float64
region               str
dtype: object
>>> df.describe()
         order_id   quantity  unit_price
count    10.00000  10.000000   10.000000
mean   1005.50000   2.000000  120.500000
std       3.02765   1.333333  176.689464
min    1001.00000   1.000000   15.000000
25%    1003.25000   1.000000   23.750000
50%    1005.50000   1.500000   47.500000
75%    1007.75000   2.750000  142.500000
max    1010.00000   5.000000  600.000000
```

**Note**

1. **Line 1:** Import the pandas package. It is convention to assign the alias `pd` to pandas.
2. **Line 2:** Print the version of pandas being used.
3. **Line 4:** Read data from the CSV file **sales_data.csv** and store it in the **DataFrame** object `df`.
4. **Line 5:** Print the first five lines of the DataFrame.
5. **Line 14:** Print the number of rows in the DataFrame.
6. **Line 16:** Print the number of columns in the DataFrame.
7. **Line 18:** Print the names of the columns of the DataFrame.
8. **Line 21:** Print the indices of the rows of the DataFrame.
9. **Line 24:** Print the `dtype` of each column of the DataFrame.
10. **Line 34:** Print a summary statistics of all columns containing numerical data.

### Recap

This session covered or mentioned several topics that are not the main topics of discussion. They are listed here as a reminder to study their documentation in detail for future use:

1. The online free book [Think Python, 3ed., Allen B. Downey]() is an excellent resource for beginners and experts alike. It is worthwhile digging deep into this book.
2. The [`pathlib`](https://docs.python.org/3/library/pathlib.html) built-in package is a comprehensive library for manipulating files paths, files and directories. It is extremely useful when automating tasks that use the file system.

The [Pandas](https://pandas.pydata.org/) package is gigantic and we have not even scratched the surface. Pandas has stiff competition from [Polars](https://pola.rs/) which is worth exploring. [Narwhals](https://narwhals-dev.github.io/narwhals/) may help you use either of them and quickly switch from one to the other without having to rewrite your code.
