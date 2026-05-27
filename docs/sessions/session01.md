# Session 1: Working with Python

**Date: 2026-03-07 4:00 pm to 6:00 pm**

## Python REPL

The Python REPL (Read–Eval–Print Loop) has the following features:

1. It allows interactive execution of Python code  
2. It has its own Python environment and memory space where objects, modules, and packages are stored  
3. Typing the name of an object immediately displays its value, unlike in a non-interactive environment where the value must be explicitly displayed using the `print()` function  

```pycon
>>> a = "Hello, world!"
>>> a
'Hello, world!'
>>> print(a)
Hello, world!
```

Note the presence of `'` around the value in the first output and their absence in the second output.

## Python Built-in Types
You can inquire the data type of a constant or an object with the `type()` function. Here are a few examples to try out in the Python REPL:

### Inquiring the type of the constant or object

``` pycon
>>> type(True)
<class 'bool'>
>>> type("Hello, world!")
<class 'str'>
>>> type(2)
<class 'int'>
>>> type(2.0)
<class 'float'>
>>> type([1, 2, 3])
<class 'list'>
>>> type((1, 2, 3))
<class 'tuple'>
>>> type({"month": "January", "date": 10})
<class 'dict'>
>>> type({1, 2, 3})
<class 'set'>
>>> a = {"month": "January", "date": 10}
>>> type(a)
<class 'dict'>
>>> type(len)
<class 'builtin_function_or_method'>
>>> import math
>>> type(math)
<class 'module'>
>>> type(math.sqrt)
<class 'builtin_function_or_method'>
```
Note the following points:

1. Argument to `type()` can be a constant or an object
2. In Python everything is an object, not just variables. Thus, a function and a module are also objects.

### `str` Data Type

#### Creating a String

A string (`str`) data type consists of a sequence of characters. A string constant can be created in the following ways:

1. Enclose the characters within a pair of double quotes (`"`) or single quotes (`'`). The string must be on a single line.  
2. Enclose the characters within triple double quotes (`"""`) or triple single quotes (`'''`). The string can span multiple lines. The newline created by pressing Enter is stored as the newline character (`\n`) and moves the cursor to the next line when printed.  
3. If a string is split across lines using a backslash (`\`) at the end of a line, the next line is treated as a continuation. The newline is not stored in the string.  

```pycon
>>> s1 = "Sunday"
>>> s1
'Sunday'
>>> len(s1)
6

>>> s2 = 'Monday'
>>> s2
'Monday'

>>> s3 = "Hello, \
... world!"
>>> s3
'Hello, world!'

>>> s4 = """Hello,
... world!"""
>>> s4
'Hello,\nworld!'
>>> print(s4)
Hello,
world!
```

You can embed a single quote (`'`) inside a string delimited by double quotes (`"`) and vice versa.

```pycon
>>> s1 = "This isn't difficult"
>>> s1
"This isn't difficult"

>>> s2 = 'He asked "How are you?"'
>>> s2
'He asked "How are you?"'

>>> s3 = """This isn't difficult. "How are you?"."""
>>> s3
'This isn\'t difficult. "How are you?".'
```

You can use the backslash (`\`) to escape characters so they are treated as part of the string rather than delimiters.

```pycon
>>> s = 'This isn\'t difficult'
>>> s
"This isn\'t difficult"

>>> s = "He said \"How are you?\""
>>> s
'He said "How are you?"'
```

#### Operations on `str`

Strings support addition (concatenation) and multiplication with integers.

```pycon
>>> s1 = "Hello"
>>> s1
'Hello'

>>> s2 = "world!"
>>> s2
'world!'

>>> s = s1 + s2
>>> s
'Helloworld!'

>>> s = s1 + ", " + s2
>>> s
'Hello, world!'

>>> s = "Hello"
>>> s * 2
'HelloHello'

>>> "*" * 10
'**********'
```

Multiplying a string by an integer (e.g., `2`) creates a new string by repeating the original string that many times.

### `list` Data Type

A list is an ordered collection of elements. A list constant is created by enclosing the elements separated by commas within a pair of matching square brackets (`a = [ 1, 2, 3, 4]`).

1. All elements need not be of the same data type
2. Elements are indexed starting with `0` for the first element
3. Number of elements in a list is obtained using the function `len(a)`, where `a` is an object of type `list`
4. When the index is a positive integer greater than or equal to `0`, indexing is assumed to be from start to end
5. When the index is a negative integer less than or equal to `-1`, index is assumed to be from end to start
6. Multiple elements can be obtained by an operation called **slicing**. Slicing can involve a ste size which can be positive when going from start to end and negative when going from end to start
7. The slicing operation can be written in the form `a[start:end:step]`
8. When indexing/slicing from start to end:
     * If start value is not specified, it is assumed to `0`
     * If end value is not specified, it is assumed to be `len()`
     * The step size can be any **positive integer**
     * If step size is not specified, it is assumed to be `1`
9. When indexing/slicing from end to start:
     * If start value is not specified, it is assumed to `-1`
     * If end value is not specified, it is assumed to be `-(len()+1)`
     * The step size can be any **negative integer**
     * Step size must be specified, it is not automatically assumed

Let us see some examples of indexing.<br>**Note:** Anything following a `#`, including the `#` is a comment and is ignored by the interpreter. When trying out the following code, you need not to type the comments.

``` py 
>>> a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
>>> a
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
>>> len(a)
10
>>> a[0]  # First element
1
>>> a[1]  # Second element
2
>>> a[9]  # Last element
10
>>> a[10] # Invalid index
Traceback (most recent call last):
File "<python-input-26>", line 1, in <module>
    a[10]
    ~^^^^
IndexError: list index out of range
>>> a[-1]  # First element from the end
10
>>> a[-2]  # Second element from the end
9
>>> a[-10] # Last element from the end
1
>>> a[-11] # Invalid index
Traceback (most recent call last):
File "<python-input-30>", line 1, in <module>
    a[-11]
    ~^^^^
IndexError: list index out of range
```

Here are some examples of slicing in the **forward** direction (from start to end), using the same object `a` defined above. Before we start, one important rule for the end index: **The end index itself is not included in the range, whereas the start index is included**.

``` pycon
>>> a[0:2]  # a[0] and a[1]. a[2] not included. A list with two elements
[1, 2]
>>> a[1:2]  # a[1] only, a[2] not included. A list with one element
[2]
>>> a[:2]   # Same as a[0:2:1]
[1, 2]
>>> a[6:10] # From a[6], a[7], a[8] and a[9], a[10] not included. A list with 4 elements
[7, 8, 9, 10]
>>> a[6:]   # Same as a[6:10:1]
>>> a[:]    # Same as a[0:10:1]
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
>>> a[::]   # Same as a[0:10:1]
>>> a[::2]  # Same as a[0:10:2]. Step size 2. Indices 0, 2, 4, 6, 8
[1, 3, 5, 7, 9]
>>> a[::3]  # Same as a[0:10:3]. Step size 3. Indices 0, 2, 5, 8
[1, 4, 7, 10]
```

Here are some examples of slicing in the **reverse** direction (end to from start)

``` pycon
>>> a[-1:-3:-1]  # a[-1] and a[-2], a[-3] is not included. Return as list
[10, 9]
>>> a[::-1]   # Same as a[-1:-11:-1]
[10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
>>> a[-1:-11] # Same as a[-1:-11:1], that returns an empty list
[]
>>> a[-1:-11:-2] # Same as a[::-2]
[10, 8, 6, 4, 2]
>>> a[::-3]   # Same as a[-1:-11:-3]
[10, 7, 4, 1]
>>> a[-2::-2] # Same as a[-2:-11:-2]
[9, 7, 5, 3, 1]
```

Finally, you can create an empty list with no elements.

``` pycon
>>> b = []
>>> b
[]
>>> len(b)
0
```

You can create a list using `list()`.

``` pycon
>>> b = list([1, 2, 3, 4])  # Same as b = [1, 2, 3, 4]
>>> b
[1, 2, 3, 4]
>>> c = list()    # same as c = []
>>> c
[]
```

#### `str` as a List

A string can be treated as a sequence of characters, similar to a list. This means you can perform indexing and slicing operations on a string.

```pycon
>>> s = "The quick brown fox jumped over the lazy dog"

>>> len(s)
44

>>> s[:3]    # Indices 0, 1, 2 (3 not included)
'The'

>>> s[::-1]  # Characters in reverse order
'god yzal eht revo depmuj xof nworb kciuq ehT'

>>> s[4:9]   # s[4] to s[8] (9 not included)
'quick'
```

## Installing marimo

[marimo](../resources/working_with_python.md#marimo-reactive-notebooks) is a reactive notebook that runs in a web browser and consists of cells. A cell can contain Python code or [Markdown](https://www.markdownguide.org/basic-syntax/) text.

- Code cells can be executed, and their output is displayed above or below the cell  
- Markdown cells are rendered as formatted text  
- Markdown can include mathematical expressions written in LaTeX format  

### Installation and Creating a Notebook

Create a new notebook named `demo01.py` using one of the following methods:

#### Using `uv`

```doscon
> uv add marimo
> uv run -- marimo edit demo01.py
```

#### Using `pip`

```doscon
> .venv\Scripts\activate
(.venv) > pip install marimo
(.venv) > marimo edit demo01.py
```

This will start a local web server, open a browser window/tab, and display the notebook in **edit** mode.

---

## Working with a marimo Notebook

1. The first cell **must** contain:
   ```python
   import marimo as mo
   ```

2. Add a new cell above or below an existing one by clicking the `+` button on the left edge of the cell  

3. By default, new cells are **Python code cells**. You can convert them to **Markdown cells** using the Markdown toggle in the cell toolbar  

4. To execute a code cell:
   - `Ctrl + Enter`: run and stay in the same cell  
   - `Shift + Enter`: run and move to the next cell (or create a new one)  
   - The **Run** button is equivalent to `Ctrl + Enter`  

5. When a cell is modified, the Run button changes color to indicate that the code has not been executed  

6. Changes are saved automatically; manual saving is usually unnecessary  

7. To close the notebook, use the **Shutdown** button in the interface  

8. Alternatively, in the terminal:
   - Press `Ctrl + C`  
   - Confirm with `y`  
   - Close the browser tab manually  

9. To restart the notebook:
   - Open the **Actions** menu  
   - Select **Restart kernel**  

10. Explore additional controls such as:
    - Command palette  
    - Interrupt execution  
    - Run all pending cells  

11. You can modify preferences using the **Settings** option in the interface  
