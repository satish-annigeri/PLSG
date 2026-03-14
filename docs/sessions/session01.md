# Session 1: 2026-03-07 Saturday
#### From 4:00 pm to 6:00 pm

## Python REPL

The Python REPL has the following features:

1. It permits interactive execution of Python code
2. It has its own Python environment and memory space where the objects, modules and packages are stored
3. Typing the name of an object immediately displays its value, unlike in a on-interactive environment where the value of an object must be explicitly displayed with the `print()` function

``` pycon
>>> a = "Hello, world!"
>>> a
'Hello, world!'
>>> print(a)
Hello, world!
```
Note the presence of `'` around the value in the first line of output and their absence in the seconf line of output.

## Python Built-in Data Types
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

#### Creating a string
A string (`str`) data type consists of an array of characters. A string constant can be created in one of the following ways:

1. Enclose the characters within a pair of double quotes (`"`) or a pair of single quotes (`'`), but these characters must fit on a single line
2. Enclose the characters between a pair of triple double quotes (`"`) or triple single quotes (`'`), and the characters can extend on multiple lines. The ++enter++ key pressed to take the string to the next line is stored as the newlinr character (`\n`) within the string and when printed, moves the cursor to the next line.
3. If a string does not fit on a single line (or the user wants to spread on multiple lines), the line must end with the backslash (`\`) character, in which case the next line is presumed to be a continuation of the previous line. The ++enter++ key pressed after the `\` is not stored in the string.

``` pycon
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
'Hello,\mworld!'
>>> print(s4)
Hello,
world!
```
You can embed a single quote (`'`) within a string delimited by double quotes (`"`) and vice versa.

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

You can use the backslash (`\`) to escape a character so that it is treated as a character and not as a delimiter.

``` pycon
>>> s = 'This isn\'t difficult'
>>> s
"This isn\'t difficult"
>>> s = "He said \"How are you?\""
'He said "How are you?"'
```

#### Operations on `str`
Addition and multiplication with an integer are permitted.

``` pycon
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
'HelloHello
>>> "*" * 10
'**********'
```
Multiplying a string with `2` is equivalent to creating a new string by adding the string **two** times.

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

Here are some examples of slicing in the **forward** direction (from start to end), using the same object `a` defined above. Before we start, one important rule for the end index: **The end index itself is not included in the range, whereas the start eindex is included**.

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
#### `str` as a list

You can treat a string as a list of characters in that you can perform indexing and slicing operations on a string.

``` pycon
>>> s = "The quick brown fox jumped over the lazy dog"
>>> len(s)
44
>>> s[:3]    # Indexes 0, 1, 2. 3 not included. First 3 characters
'The'
>>> s[::-`]  # List of characters in reverse order
'god yzal eht revo depmuj xof nworb kciuq ehT'
>>> s[4:9]   # s[4] to s[8], s[9] not included
'quick'
```

## Installing marimo

[marimo](../resources/working_with_python.md#marimo-reactive-notebooks) is a reactive notebook. It runs within a web browser and consists of cells. A cell can contain Python code or [Markdown](https://www.markdownguide.org/basic-syntax/) markup text. Code in a Python cell can be executed and the output is displayed above/below the cell. Text content in a Markdown cell is rendered as HTML text. Markdown text can contain mathematical equations written in \(LaTeX\) format.

Here are the steps to install marimo, create a new notebook named `demo01.py`:

=== "Using `uv`"

    ``` doscon
    > uv add marimo
    > uv run -- marimo edit demo01.py
    ```

=== "Using `pip`"

    ``` doscon
    > .venv\Scripts\activate
    (.venv) > pip install marimo
    (.venv) > marimo edit demo01.py
    ```

This will open a local webserver, open a new browser window/browser tab and show the notebook in **edit** mode where you can make changes to the notebook.

Here are some tips to work with a marimo notebook:

1. The first cell **must** start with the statement `#!python import marimo as mo`
2. Add a new cell above/below  an existing cell by clicking the `+` to the left edge of the cell at its top/bottom of the cell
3. By default, a new cell is a **Python code cell**. To change it t a **Markdown cell**, click on the small Markdown icon :simple-markdown: at the bottom right edge of the cell.
4. To execute the Python code in a code cell, press either ++ctrl+enter++ (execute the code but stay in the same cell) or ++shift+enter++ (execute the code and go to the next cell if one exists or create a new cell below and go to that cell). Pressing the **Run** (:lucide-circle-play:) button at the top right edge of the cell is equivalent to ++ctrl+enter++.
5. When the content of a cell is changed, the :lucide-circle-play: button changes colour to light yellow to indicate that the changed code has not been run.
6. Changes to the notebook are saved automatically, there is a **Save** (:lucide-save:) button but you won't ever need to use it.
7. To close and exit the notebook, press the light red coloured **Shutdown** (:lucide-circle-x:) button at the top right corner of the notebook.
8. Alternately, you can go to the Command Prompt or the terminal from where you issued the `marimo edit` command and press ++ctrl+c++ and type ++y++ and manually close the browser tab with the notebook.
9. If for any reason you wish to restart the notebook, you can do so without first closing the notebook and opening it again. Go to the **Actions** (:lucide-menu:) menu button at the top right of the notebook and click on the **Restart kernel** oprion and click on the **Restart** button.
10. Explore the **Show command palette** (:lucide-command:), **Stop (interrupt) execution** (:lucide-square:) and **Run all stale cells** (:lucide-circle-play:) buttons to the bottom right of the notebook.
11. You can change the **Settings** with the :lucide-settings: button at the top right of the notebook