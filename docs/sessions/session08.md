# Session 8

### Planned Date 25-04-2026 4:00 pm to 6:00 pm

## Agenda

1. Review of previous sessions
2. Answers to queries
3. Introduction to Matplotlib

## Introduction to Matplotlib

The [Matplotlib homepage](https://matplotlib.org/stable/) describes Matplotlib as:

!!! note "From Matplotlib home page"
    Matplotlib is a comprehensive library for creating static, animated, and interactive visualizations in Python. Matplotlib makes easy things easy and hard things possible.

It relies on NumPy for the `ndarray` data structure to store data and provides the functions to plot a wide variety of graphs. Being one of the earliest data visualization library for Python, it is very popular and widely used. There are several more recent plotting libraries for Python, but Matplotlib remains relevant and popular.

Matplotlib will appear familiar to Matlab users as its traditional approach to generating plots parallel those of Matlab. However, the current style of using Matplotlib uses the object oriented approach that is a little different. While Matplotlib can generate several types of graphs, this introduction will restrict itself primarily to plotting line graphs and perhaps a few other realted graphs.

### Installing Matplotlib

=== "Using `uv`"
    ```doscon
    > uv add matplotlib
    ```

=== "Using `pip`"
    ```doscon
    > pip install matplotlib
    ```

Matplotlib depends on NumPy and if NumPy is not already installed, it will be installed automatically.

Once installed, open the Python REPL, import `matplotlib` and check its version to confirm it was installed correctly:
```pycon
>>> import matplotlib
>>> matplotlib.__version__
`3.10.8`
```
Matplotlib is extremely well documented. It offers a [Quick start guide](https://matplotlib.org/stable/users/explain/quick_start.html), a [User guide](https://matplotlib.org/stable/users/index.html), [Tutorials](https://matplotlib.org/stable/tutorials/index.html) and [FAQs](https://matplotlib.org/stable/users/faq.html). Yu can browse the [plot types](https://matplotlib.org/stable/plot_types/index.html) and [examples](https://matplotlib.org/stable/gallery/index.html).

The typical workflow consists of:

1. Import the `matplotlib.pyplot` subpackage as `plt` once in each script or program which uses `matplotlib`.
2. Prepare or create the data to be plotted.
3. Initialize a `plt.subplots()` and store the values of **figure** and **axis** returned by it.
4. Use the **axis** to execute one or more `plot()` or `set()` methods.
5. Display the plot with the `plt.show()` function call.

### Plot graphs of `sin` and `cos`

The example below plots a graph of `sin` and `cos` for values from $0$ to say $2 \pi$:

```pucon
>>> import matplotlib.pyplot as plt
>>> import numpy as np
>>> x = np.linspace(0, 2 * np.pi, 129)
>>> y1 = np.sin(x)
>>> y2 = np.cos(x)
>>> fig, ax = plt.subplots()
>>> ax.plot(x, y1)
>>> ax.plot(x, y2)
>>> ax.grid()
>>> ax.set_xlabel("x")
>>> ax.set_ylabel("y")
>>> ax.set_title(r"Graphs of $\sin$ and $\cos$")
>>> plt.show()
```

This will pop up a window with the plot, and the menu at the bottom lets you save the image to the filesystem.

![Plot produced by Matplotlib](/assets/sin_cos.png)

**Note**

1. The colours of the lines are chosen automatically, but it can be specified if needed.
2. Other settings allow the programmer to choose the thickness of the lines, the style of the lines, markers at the data points, limits for the axes, intervals for the tic marks etc.
3. The labels can contain $\LaTeX$ markup to generate greek letters, super and sub-scripts etc.
4. It is possible to place a legend at one of the corners (or other specific location).
5. It is possible to annotate the plots.

### Multiple sub-plots

```python
import matplotlib.pyplot as plt
import numpy as np


def f(t):
    return np.exp(-t) * np.cos(2*np.pi*t)

t1 = np.arange(0.0, 5.0, 0.1)
t2 = np.arange(0.0, 5.0, 0.02)

fig, ax = plt.subplots(nrows=2, ncols=1)
ax[0].plot(t1, f(t1), 'bo', t2, f(t2), 'k')

ax[1].plot(t2, np.cos(2*np.pi*t2), 'r--')
plt.show()
```

![Subplots](/assets/subplots.png)

**Note**

1. The arguments `nrows=2` and `ncols=1` to `plt.subplots()` specify the number of rows and columns to split the figure into.
2. The list `ax` therefore has two elements (2 rows and 1 column) and each is indexed as `ax[0]` and `ax[1]`.
3. The plot output is directed to the specific subplot based on the chosen `ax`.

See the [Matplotlib Tutorials](https://matplotlib.org/stable/tutorials/pyplot.html) page for more examples.


The stress-strain relation for concrete is given by the expression:

$$
\begin{align*}
f_c &= \begin{cases}
    0 & \text{if } \epsilon_c < 0 \text{ or } \epsilon > \epsilon_{cu} \\
    0.67 f_{ck} & \text{if } \epsilon_{cy} \leq \epsilon_c \leq \epsilon_{cu} \\
    0.67 f_{ck} \left[ 2 \left( \frac{\epsilon_c}{\epsilon_{cy}} \right) - \left( \frac{\epsilon_c}{\epsilon_{cy}} \right)^2 \right] & \text{if } 0 \leq \epsilon_c \leq \epsilon_{cy}
\end{cases} \\
\epsilon_{cy} &= 0.002 \\
\epsilon_{cu} &= 0.0035
\end{align*}
$$

Define a function to calculate the stress ($f_c$) for given value of strain ($\epsilon_c$) and plot a graph of strain vs stress.
```python linenums="1"
import numpy as np
import matplotlib.pyplot as plt


ecy: float = 0.002
ecu: float = 0.0035


def fc(ec: float, fck: float, ecy: float=0.002, ecu: float=0.0035) -> float:
    if 0 <= ec < ecy:
        ec_ecy = ec / ecy
        return 0.67 * fck * (2 * ec_ecy - ec_ecy ** 2)
    elif ecy <= ec <= ecu:
        return 0.67 * fck
    else:
        return 0.0

v_fc = np.vectorize(fc)
```

**Note**

1. The function `fc(ec, fck, ecy, ecu)` calculates the stress `fc` for one given value of `ec`
2. The `v_fc = np.vectorize(fc)` converts the function `fc()` to vector form `v_fc()` so that the function `fc()` can be applied to each element of an `ndarray` without writing a `for` loop.

Create the array `ec` to store the data points at which $f_c$ is to be calculated. Since there are two distinct portins of the graph, namely $0 \leq \epsilon_c < \epsilon_{cy}$ and $\epsilon_{cy} \leq \epsilon_c \leq \epsilon_{cu}$, generate two 1D arrays and concatenate them.

```python linenums="19"
ecy: float = 0.002
ecu: float = 0.0035
fck = 20.0
ec = np.concat((np.linspace(0, ecy, 51), np.linspace(ecy, ecu, 5)))
fc = v_fc(ec, fck)
print(ec.shape, fc.shape)
```
**Note**

1. `np.linspace(0, ecy, 51)` generates `51` equally spaced points from `0` to `ecy`.
2. `np.linspace(ecy, ecu, 5)` generates `5` equally spaced points from `ecy` to `ecu`.
3. `np.concat((np.linspace(0, ecy, 51), np.linspace(ecy, ecu, 5)))` concatenates the two arrays, resulting in a length of `56` elements.

The output should be 
```python
(56,) (56,)
```

The plot can be generated as usual:

```python linenums="25"
fig, ax = plt.subplots()
ax.plot(ec, fc)
ax.set_xlabel(r"$\epsilon_c$")
ax.set_ylabel(r"$f_c$")
ax.set_title("Stress vs Strain for Concrete")
ax.grid()
plt.show()
```
**Note**

1. The $LaTeX$ markup for $\epsilon_c$ is `$epsilon_c$` and for $f_c$ is `$f_c$`.

![Graph of stress vs strain for concrete](/assets/ec_fc.png)

!!! tip "Key technique learnt"
    Converting a scalar function to vector form. Note that atleast one of the arguments to the vectorized function must be an array.

## Understanding Modules and Packages

In the world of software, a **module** is a distinct part of a system that performs a specific function and works together with other parts. In Python, we use modules and packages to organize our code, making it easier to read, test, and reuse.

### What is a Module?

While a single function is "modular," in Python, the term **module** specifically refers to a file containing Python code (ending in `.py`). 

A module usually contains a collection of related functions, variables, or classes that serve a common purpose. By grouping related code into a module, you simplify complex tasks and keep your main program clean.

### What is a Package?

The next level of organization is the **package**. A package is simply a collection of interrelated modules grouped together in a directory (folder). Think of a module as a single file and a package as a folder containing many of those files.

### Where do Modules and Packages come from?

There are three main sources for the tools you will use in your programs:

1. **The Python Standard Library (Built-in)  **
Python comes "batteries included." Many modules and packages are automatically installed when you install Python. These are known as the **Standard Library**.
    * **Examples:** The `math` module for calculations or the `collections` package for advanced data types.
    * **Access:** Since they are already on your system, you can use them immediately.

2. **External Packages (Third-Party)**  
These are created by the global Python community and hosted on services like [PyPI](https://pypi.org/). You must install these before you can use them (usually via a tool like `pip`).
    * **Examples:** `numpy` for scientific computing or `matplotlib` for creating graphs.

3. **Your Own Modules (Custom)**  
As your programs grow, you should collect your own functions and constants into `.py` files. This allows you to:
    *   **Stay Organized:** Keep your main script short and focused.
    *   **Increase Reusability:** Use the same functions in different projects without rewriting them.
    *   **Improve Testing:** Test individual parts of your code independently.

### How to Use Them

Regardless of where the module or package comes from, you bring it into your current program using the `import` keyword. This tells Python to load that specific code so you can use its features.

```python
import math

# Now you can use functions from the math module
print(math.sqrt(16))
```

## Understanding Namespaces

As you start using more modules and packages, you might worry: *"What happens if I name a variable `data`, but a module I imported also has a variable named `data`?"*

Python solves this problem using **Namespaces**.

### What is a Namespace?

A **namespace** is essentially a naming system to ensure that all the names in your program (like variables, functions, and modules) stay organized and don't clash with each other.

Think of a namespace like a **surname (last name)**:  

* In a classroom, there might be two students named **Rajesh**. This is confusing.
* However, if one is **Rajesh Patil** and the other is **Rajesh Kulkarni**, there is no confusion.
* The surnames "Patil" and "Kulkarni" act like namespaces to keep the names distinct.

### Why Namespaces Matter

In Python, namespaces allow you to use the same name for different things, as long as they live in different "folders." For example:

1.  **The Global Namespace:** This contains names defined in your main program.
2.  **The Module Namespace:** This contains names defined inside a specific module (like `math` or `random`).
3.  **The Local Namespace:** This contains names defined inside a specific function.

### A Real-World Example

If you import the `math` module, it has its own namespace. This is why you often see code like this:

```python
import math

# This 'pi' belongs to the math namespace
print(math.pi) 

# You can still create your own 'pi' in your program's namespace
pi = 3
print(pi)
```

By using math.pi, you are telling Python: *"I want the* `pi` *that belongs to the* `math` *namespace, not the one I created myself."* This keeps your code safe and organized!

## Our first module - A module to operate on vectors

Let us create our own module to perform the following operations related to vectors:

1. Create a vector as a one dimensioned list with three components.
2. Add two vectors or subtract one from the other.
3. Obtain the dot product of two vectors.
4. Obtain the cross product of two vectors.
5. Obtain magnitude, and
6. Unit vector along the given vector.

### Theory

Given two vectors $A = A_x \, i + A_y \, j + A_z \, k$ and  $B = B_x \, i + B_y \, j + B_z \, k$, where $i, j, k$ are unit vectors along the $x, y, z$ axes respectively, the different operations are given below:

**1. Addition or Subtraction:** Result of addition or subtraction is a vector and is given by:

$$
  A \pm B = (A_x + B_x) \, i \pm (A_y + B_y) \, j \pm (A_z + B_z) \, k
$$  

**2. Dot Product:**  Dot product results in a scalar and is given by:

$$
A \cdot B = A_x B_x + A_y B_y + A_z B_z
$$

**3. Cross Product:** Cross product is a vector and is given by:

$$
\begin{align*}
A \times B &= \begin{vmatrix}
i & j & k \\
A_x & A_y & A_z \\
B_x & B_y & B_z
\end{vmatrix} \\
&= (A_y B_z - A_z B_y) \, i - (A_x B_z - A_z B_x) \, j + (A_x B_y - A_y B_x) \, k
\end{align*}
$$

**4. Magnitude:** Magnitude is a scalar given by:

$$
| A | = \sqrt{A_x^2 + A_y^2 + A_z^2}
$$

**5. Unit Vector:** Unit vector along a given vector has the same direction as the given vector but has a unit magnitude. It is given by:

$$
\begin{align*}
\hat{A} &= \frac{A}{|A|} = \frac{A_x}{|A|} \, i + \frac{A_y}{|A|} \, j + \frac{A_z}{|A|} \, k \\
|A| &= \sqrt{A_x^2 + A_y^2 + A_z^2}
\end{align*}
$$

### Python module
``` py title="vector.py" linenums="1"
import numpy as np
import matplotlib.pyplot as plt


def vec(ax, ay, az):
    return np.array([ax, ay, az])

def abs(a):
    return np.sqrt(sum(a ** 2))

def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

def dot(a, b):
    return sum(a * b)

def cross(a, b):
    return np.array([
        a[1] * b[2] - a[2] * b[1],
        a[2] * b[0] - a[0] * b[2],
        a[0] * b[1] - a[1] * b[0]
    ])


# Test code
a = vec(2, 3, 4)
b = vec(1, 2, 3)
print(abs(a))
print(abs(b))
print(add(a, b))
print(subtract(a, b))
print(dot(a, b))
print(cross(a, b))
```

Open Python REPL and do the following:
``` pycon
>>> import vector
5.385164807134504
3.7416573867739413
[3 5 7]
[1 1 1]
20
[ 1 -2  1]
```
Alternately, create a file named `main.py` or any name of your choice in a code editor such as VS Code and type the following:
```py title="main.py" linenums="1"
import vector
```
and run the file. You will the same output as above displayed in the terminal.

!!! tip
    To not execute the lines of code meant to test the functions in this file when this file is imported as a **module**, put these lines in a conditional block `#!python if __name__ == "__main__"`. 

``` py title="vector.py" hl_lines="10" linenums="1"
import numpy as np
import matplotlib.pyplot as plt


def vec(ax, ay, az):
    return np.array([ax, ay, az])

# several lines not shown t save space and avoid repetition

if __name__ == "__main__":
    # Test code
    a = vec(2, 3, 4)
    b = vec(1, 2, 3)
    print(abs(a))
    print(abs(b))
    print(add(a, b))
    print(subtract(a, b))
    print(dot(a, b))
    print(cross(a, b))
```

Now, if you run the main.py file, it will produce no output. This is because:

1. **Import Logic:** When a file is imported, Python executes all code in that file once.
2. **Unconditional Execution:** Any code not inside the if __name__ == "__main__": block runs automatically upon import.
3. **Conditional Execution:** Python sets an internal variable named __name__ for every file.
    1. When the file is executed directly, __name__ is set to "__main__". The condition is met, and the test code runs.
    2. When the file is imported, __name__ is set to the module name (e.g., "vector"). The condition is not met, and the test code is skipped.

You can verify this by adding a line `#!python print(__name__)` above the conditional block:
``` py title="vector.py" hl_lines="5" linenums="1"
import numpy as np

# Several lines not shown

print(__name__)

if __name__ == "__main__":
    a = vec(2, 3, 4)
    # Several lines not shown
```

If you execute vector.py directly, you will see __main__. If you execute main.py, you will see vector, and the test results will be hidden.

To use the module functions in main.py, use the module name as a prefix:
``` py title="main.py" hl_lines="3 4 5 6 7 8 9 10" linenums="1"
import vector

a = vector.vec(2, 3, 4)
b = vector.vec(1, 2, 3)
print(vector.abs(a))
print(vector.abs(b))
print(vector.add(a, b))
print(vector.subtract(a, b))
print(vector.dot(a, b))
print(vector.cross(a, b))
```
Executing `main.py` produces the same output as the test code in `vector.py`.

### Creating Packages

While a **module** is a single `.py` file, a **package** is a collection of modules placed within a directory. In **regular packages**, the directory contains a special file named `__init__.py`. This file is often empty; however, if it contains code, that code is executed once when the package is first imported. Since Python 3.3, directories without an `__init__.py` are also recognized as **namespace packages**. The name of the directory defines the name of the package. Any `.py` files in this directory are treated as modules, and sub-directories are treated as sub-packages.

We will look at creating packages at a later point of time.