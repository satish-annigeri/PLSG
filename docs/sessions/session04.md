# Session 4

#### Planned Schedule: 28-03-2026 4:00 pm to 6:00 pm

## Agenda

1. Review of previous sessions
2. Answers to queries
3. [Comments in Python code](#comments-in-python-code)
4. [Formatted output](#formatted-output)
5. [Function signature](#function-signature)
6. [Designing functions](#designing-functions)


## Comments in Python Code

There are two types of comments in Python:

1. **Single-line comments**: A comment starts with the hash (`#`) character and continues until the end of the line. Everything after `#` is ignored by the interpreter. A comment can occupy an entire line or appear after code on the same line.
2. **Multi-line comments**: Multi-line comments are written using triple double quotes (`"""`) or triple single quotes (`'''`). They can span multiple lines or appear on a single line.

!!! note "Note"
    Triple-quoted strings are often used like multi-line comments, but they are actually string literals. They are ignored only when not assigned to a variable or used in expressions.

Following are examples of comments:
```py
a = 0  # initialize a to zero
# This entire line is a comment, and is ignored
## This is also a comment since it begins with the # character
"""
This is a multi-line comment
and can continue on multiple lines
"""
"""This is also a comment"""
'''
This too is a multi-line comment
Here is the second line
'''
```

## Formatted Output
Python provides several ways to produce formatted output to meet requirements such as displaying a specified number of decimal places, justifying a string within a specified width, and more. The method discussed here uses **f-strings**, which are the recommended way to produce formatted output.

* f-strings provide a convenient way to perform *string interpolation* in Python.
* String interpolation allows values to be embedded directly inside strings.
* Anything in an f-string enclosed within curly braces (`{ }`) is replaced by its value.
* Curly braces can enclose a constant, a variable, a function that returns a value, or any expression that can be converted to a string.
* Anything **not** enclosed in curly braces is reproduced as-is, without any change.
* An f-string returns a string that can be printed or stored in a variable for future use.

Here are some examples:

```pycon
>>> n = 5
>>> print(f"{n:5}")   # Field of width 5, numbers are right justified
    5
>>> print(f"{n:05}")  # Field width 5, padded with 0 if necessary
00005
>>> print(f"{n:+}")   # Preceding + sign for positive numbers
+5
>>> print(f"{n:+05}") # Preceding + sign and padded with 0
+0005
>>> x = 4 / 3
>>> print(x)          # Print the value of floating point number x
1.3333333333333333
>>> print(f"{x:.2f}") # Automatic field width, decimal places 2, displayed value is rounded
1.33
>>> print(f"{2.5:.4f}") # Automatic field width, decimal places 4
2.5000
>>> print(f"{x:10.2f}") # Field width 5, decimal places 2
      1.33
```

Here are some examples of formatting strings using f-strings:

```pycon
>>> s = "Hello, world!"
>>> print(f"Greeting string: {s}")  # Anything not enclosed in curly braces is reproduced as-is
Greeting string: Hello, world!
>>> print(f"|{s:20}|")      # Field width 20, left justified by default
|Hello, world!       |
>>> print(f"|{s:>20}|")     # Field width 20, right justified using >
|       Hello, world!|
>>> print(f"|{s:^20}|")     # Field width 20, centre justified using ^
|   Hello, world!    |
```

## Functions

A function is a self-contained unit that performs a specific task. It has well-defined inputs, outputs, and a sequence of operations. Functions promote modularity, allowing programs to be organized into smaller, manageable components.

---

### Attributes of a function

A function has the following attributes:

1. **Name**  
   The function must have a unique name. If a function is redefined, the latest definition replaces the previous one.  

2. **Input parameters**  
   A function can have zero or more input parameters, specified within parentheses. Type annotations are optional but recommended.  

3. **Return value(s)**  
   The `return` statement specifies the output. If no value is returned, the function returns `None`.  

4. **Function body**  
   The body consists of one or more indented statements that define the function’s behavior.  

---

### Defining a function

A function is defined using the `def` keyword, followed by the function name and parentheses. The definition ends with a colon (`:`), and the body must be indented (typically by 4 spaces).

```pycon
>>> def product(a: float, b: float) -> float:
...     return a * b
...
>>> type(product)
<class 'function'>

>>> product
<function product at 0x7fff36029010>
```

The parameters `a` and `b` are placeholders. When the function is called, actual values (called *arguments*) are passed to these parameters.

---

### Calling a function

```pycon
>>> product(2, 3)
6

>>> product(2.5, 3)
7.5
```

In these calls:

- `a = 2`, `b = 3` in the first call  
- `a = 2.5`, `b = 3` in the second call  

---

!!! note
    Type annotations are intended for the programmer and are ignored by the Python interpreter.  
    They help document intent and improve code readability. Many code editors display function signatures based on these annotations.

---

### Returning multiple values

A function can return multiple values as a tuple.

```pycon
>>> def stats(a: list[float]) -> tuple[int, float, float]:
...     n = len(a)
...     s = sum(a)
...     mean = s / n
...     return n, s, mean
...
```

When calling such a function, multiple variables must be used to receive the returned values:

```pycon
>>> num, total, avg = stats([1, 2, 3, 4, 5])
>>> print(num, total, avg)
5 15 3.0
```

---

!!! note
    The names of parameters in a function definition and the names of variables used in a function call do not need to match.  
    This flexibility is a key aspect of modular programming.  

## Designing functions

Designing a function involves a systematic approach.

---

### Steps in function design

1. Clearly define what the function is expected to do  

2. Identify the input data required and the output to be produced  

3. Determine the procedure to transform the input into the output  
   This may involve domain knowledge, mathematics, and algorithm design  

4. Define the function signature  

    1. **Function name**  
       It must be unique, concise, and descriptive of the task  

    2. **Input parameters**  
       Specify the number, types, and names  

    3. **Return values**  
       Specify the number and types of outputs  

5. Represent the algorithm using pseudocode or a flowchart  

6. Prepare test cases (inputs and expected outputs)  

---

Once these steps are complete, implementation can begin.

---

### Dealing with complex functions

If the algorithm appears too complex:

- Break the problem into smaller sub-tasks  
- Design separate functions for each sub-task  
- Combine these functions to achieve the final result  

This process is often iterative. Even during implementation, if a function becomes difficult to manage:

- Pause and reconsider the design  
- Decompose the problem further  
- Implement and test smaller components before integrating them  

## Example of function design

#### Requirements to Be Met by the Function
The function must calculate the roots $x_1$ and $x_2$ of a quadratic equation expressed as $a x^2 + b x + c = 0$.

#### Input to the Function
The inputs to the function are the coefficients of the quadratic equation, namely $a$, $b$, and $c$. The coefficients are real numbers, and $a \neq 0$. If $a = 0$, the equation is no longer quadratic but linear.

#### Output from the Function
The function must return the roots of the quadratic equation, $x_1$ and $x_2$. The roots are real when $b^2 - 4ac \geq 0$ and complex otherwise.

1. If $b^2 - 4ac = 0$, the roots are real and equal, that is, $x_1 = x_2$
2. If $b^2 - 4ac > 0$, the roots are real and unequal, that is, $x_1 \neq x_2$
3. If $b^2 - 4ac < 0$, the roots are complex conjugates, that is, $x_1 = \alpha + i\beta$ and $x_2 = \alpha - i\beta$

#### Procedure

1. Check if $a = 0$. If so, raise an error stating that the equation is not quadratic
2. If $a \neq 0$, calculate the discriminant $d = b^2 - 4ac$
3. If $d < 0$, raise an error stating that the roots are complex
4. If $d \geq 0$, calculate and return the values of the two real roots

#### Function Signature

1. Name: `qroots`
2. Input parameters: `a: float, b: float, c: float`
3. Output parameters: `x1: float, x2: float`
4. Exceptions:
   1. If `a == 0`, raise a "Not a quadratic equation" exception
   2. If `d < 0`, raise a "Complex roots" exception

#### Code
``` py title="File: main.py"
from math import sqrt


def qroots(a: float, b: float, c: float) -> tuple[float, float]:
    if a == 0:
        raise ValueError(f"Coefficient a = {a}. Not a quadratic equation")

    d = b * b - 4 * a * c
    if d < 0:
        raise ValueError(f"Discriminant d = {d}. Complex roots")

    x1 = (-b - sqrt(d)) / (2 * a)
    x2 = (-b + sqrt(d)) / (2 * a)

    return x1, x2
```

#### Test the Function

Define a function `main()` to test the function `qroots()`. This function can be placed in the file `qroots.py`, which also contains the definition of `qroots()`:

```py title="File: main.py"

# Place these lines below the function qroots() in the main.py file

def main():
   x1, x2 = qroots(1.0, -2.0, -4.0)
   print(x1, x2)

   x1, x2 = qroots(0.0, 2, 3)
   x1, x2 = qroots(1.0, 2.0, 2.0)

if __name__ == "__main__":
   main()
```

Write this code in VS Code or any preferred code editor, and run the script. When an error occurs, execution stops and a traceback is displayed. The following output is produced:

```pycon
-1.2360679774997898 3.23606797749979
  File "/home/satish/python/sci/qroots.py", line 26, in <module>
    main()
    ~~~~^^
  File "/home/satish/python/sci/qroots.py", line 22, in main
    x1, x2 = qroots(0.0, 2, 3)
             ~~~~~~^^^^^^^^^^^
  File "/home/satish/python/sci/qroots.py", line 6, in qroots
    raise ValueError(f"Coefficient a = {a}. Not a quadratic equation")
ValueError: Coefficient a = 0.0. Not a quadratic equation
```

Modify the last call to `qroots()` as follows:

```python
    x1, x2 = qroots(1.0, 2, 3)
```

Run the script again:

```pycon
Traceback (most recent call last):
  File "/home/satish/python/sci/qroots.py", line 27, in <module>
    main()
    ~~~~^^
  File "/home/satish/python/sci/qroots.py", line 23, in main
    x1, x2 = qroots(1.0, 2, 3)
             ~~~~~~^^^^^^^^^^^
  File "/home/satish/python/sci/qroots.py", line 10, in qroots
    raise ValueError(f"Discriminant d = {d}. Complex roots")
ValueError: Discriminant d = -8.0. Complex roots
```

- There is an elegant way to catch exceptions, which will be discussed later.
- Functions can have default parameters which will be taken up later.
- Functions can have a variable number of parameters, which will be taken up later

#### Suggested Improvements
1. Python supports complex numbers and therefore it is quite easy to calculate the complex conjugate roots when $b^2 - 4ac < 0$, instead of raising an exception.
2. If $a = 0$, the equation is linear and the solution is $x = - \frac{c}{b}$ and it is easy to return the solution instead of raising an exception. However, careful thought must be given as to how to indicate to the caller that the equation is linear and therefore only one solution exists.

Here is the improved version for the case with complex roots:
``` python
import math
import cmath


def qroots(a: float, b: float, c: float) -> tuple[float, float]:
    if a == 0:
        raise ValueError(f"Coefficient a = {a}. Not a quadratic equation")

    d = b * b - 4 * a * c

    if d < 0:
        sqrt = cmath.sqrt
    else:
        sqrt = math.sqrt

    x1 = (-b - sqrt(d)) / (2 * a)
    x2 = (-b + sqrt(d)) / (2 * a)

    return x1, x2

def main():
    print(qroots(1, 2, -1))
    print(qroots(1, 2, 4))

if __name__ == "__main__":
    main()
```

#### Note

1. Both `math` and `cmath` modules are imported
2. A new object named `sqrt` of type `<class 'function'>` is created by assigning it the value of the function `sqrt` from `cmath` if `d < 0` or from `math` if `d >= 0`
3. Since Python functions are objects, just as variables are objects, they can be assigned to variables
4. Once the correct `sqrt` function is chosen the calculation of the roots is the same for both cases

The output printed from within the `main()` function is as follows:
```pycon
(-2.414213562373095, 0.41421356237309515)
((-1-1.7320508075688772j), (-1+1.7320508075688772j))
```

The imaginary part is suffixed with the letter `j`.

## Unit-testing using `pytest`

### What is Unit Testing?

Unit testing is the process of testing individual pieces (units) of code—typically functions—to ensure they behave as expected.

Benefits:

- Catch bugs early
- Improve code reliability
- Make refactoring safer
- Document expected behavior

### Installing `pytest`

Install `pytest` using `uv` and verify installation:
```doscon
> uv add pytest
> uv run -- pytest --version
pytest 9.0.2
```
or using  `pip`:
```doscon
> pip install pytest
> pytest --version
pytest 9.0.2
```

### Example Python module
Assuming there is a file called `quad.py` containing the function `qroots(a: float, b: float, c: float)` to be tested:
```python title="File: quad.py"
import math
import cmath


def qroots(a: float, b: float, c: float) -> tuple[float, float]:
    if a == 0:
        raise ValueError(f"Coefficient a = {a}. Not a quadratic equation")

    d = b * b - 4 * a * c

    if d < 0:
        sqrt = cmath.sqrt
    else:
        sqrt = math.sqrt

    x1 = (-b - sqrt(d)) / (2 * a)
    x2 = (-b + sqrt(d)) / (2 * a)

    return x1, x2
```
### Creating the test file
Create a new file, in the same directory as `quad.py` named `test_quad.py`. `pytest` automatically discovers files with names starting with `test_`,

### Writing basic tests

Add the following lines to `test_quad.py`:
```python title="File: test_quad.py"
import math
import cmath
import pytest

from quad import qroots


def test_real_equal_roots():
    x1, x2 = qroots(1, 2, 1)
    assert x1 == x2

def test_real_unequal():
    x1, x2 = qroots(1, 3, 1)
    assert x1 != x2

def test_complex_roots():
    x1, x2 = qroots(2, 2, 2)
    assert isinstance(x1, complex) and isinstance(x2, complex)

def test_real():
    a, b, c = (1, 3, 1)
    x1, x2 = qroots(a, b, c)
    d = b * b - 4 * a * c
    assert x1 == (-b - math.sqrt(d)) / (2 * a)
    assert x2 == (-b + math.sqrt(d)) / (2 * a)

def test_complex():
    a, b, c = (2, 2, 2)
    x1, x2 = qroots(a, b, c)
    re = -b / (2 * a)
    im = cmath.sqrt(b * b - 4 * a * c) / (2 * a)
    assert x1 == re - im
    assert x2 == re + im

def test_zero_coeff():
    with pytest.raises(ValueError):
        x1, x2 = qroots(0, 1, 2)
```
**Key ideas**

1. `pytest` executes all functions in the `test_quad.py` file with names beginning with `test`
2. `assert` statement checks for the expected output
3. `#!python with pytest.raises(ValueError):` tests if the `ValueError` exception is raised

### Run the tests
Run the tests using `uv`
```doscon
> uv run -- pytest
```
or in the active virtual environment
```doscon
(.venv) > pytest
```
The output should show that all tests passed.
```doscon
============================= test session starts ==============================
platform linux -- Python 3.13.9, pytest-9.0.2, pluggy-1.6.0
rootdir: /home/satish/python/sci
configfile: pyproject.toml
plugins: anyio-4.12.1
collected 6 items                                                              

test_quad.py ......                                                      [100%]

============================== 6 passed in 0.04s ===============================
```
**Key Ideas**

1. `pytest` considers all files in the current directory with names starting with `test` to be files containing items to be tested
2. An item may consist of one or more `assert` statements and `pytest.raises()` function calls
3. Irrespective of the number of `assert` statements or `pytest.raises()` calls in an item, it is considerd as one test
4. `pytest` reports the results of the tests as passed or failed, and reports details for failed tests

*Note:*

1. The above test was run on GNU/Linux operating system, output on Windows operating system will be slightly different.
2. Important lines to study are the lines showing the number of items collected (the 6 functions starting with `test` in the `test_quad.py` file) and the number of tests that passed, shown on the last line.