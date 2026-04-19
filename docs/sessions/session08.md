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

It relies of NumPy for the `ndarray` data structure to store the data and provides the functions to plot a wide variety of graphs. Being one of the earliest data visualization library for Python, it is very popular and widely used. There are several more recent plotting libraries for Python, but Matplotlib remains relevant and popular.

Matplotlib will appear familiar to Matlab users as its traditional approach to generating plots parallel those of Matlab. However, the current style of using Matplotlib uses the object oriented approach and is a little different. While Matplotlib can generate several types of graphs, this introduction will restrict itself primarily to plotting line graphs and perhaps a few other realted graphs.

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

1. Import the `matplotlib.pyplot` subpackage as `plt` once in each script ot program which uses `matplotlib`.
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
```python
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

```python
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

```python
ig, ax = plt.subplots()
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