# Answer 1

#### Answers to: [Assignment 1](assignment01.md)


1. What does **REPL** stand for? Can you name other programming languages/environments that offer a REPL?
<br>**Answer**<br>
REPL stands for **R**ead, **E**valuate, **P**rint **L**oop. It is a programming environment with its own memory space and can evaluate single or multiple lines of code and produce output. It is an interactive environment where the programmer can try out lines of code one at a time and examine the results before proceeding. One disadvantage of REPL is that it does not save the code in a file for subsequent use, although it can read and execute code that is already written in a file. But that takes away the interactive nature of a REPL and a code editor is much better suited to execute code in a file.<br><br>Other programming languages that offer a REPL are Matlab, Julia, Javascript (Node JS) and many more.
2. Having assigned the value `10` to the object `a`, what are the two ways to display the value of the object `a`?<br>**Answer**<br>
In the REPL, value of an object can be displayed by typing the name of the object and pressing ++enter++ or by using the `print()` function.<br>
```pycon
>>> a = 10
>>> a
10
>>> print(a)
10
```
In a script, the only way to display the value of an object is to print it using `#!python print(a)`.
3. Given the list `#!python a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]`
    1. Determine the number of elements in the list
    ```pycon
    >>> len(a)
    10
    ```
    2. Use negative indexing operation to obtain the **last but one element** of the list (in this example, the element with value `9`).
    ```pycon
    >>> a[-2]
    9
    ```
    3. What are the slice `start`, `stop` and `step` values to produce the list [9, 6, 3]. Remember the slice notation `#!python a[start:stop:step]`.
    ```pycon
    >>> a[-2::-3]
    [9, 6, 3]
    ```
4. You can create an empty `list` with `#!python a = []`. Creating an empty `tuple` is similar `#!python b = ()`. But how do you create a `tuple` with exactly one element? Does `#!python b = (10)` work? Why not? What is the correct way to create a tuple with exactly one element. Search the net for the answer.
**Answer**<br>
```pycon
>>> b = ()
>>> print(type(b), len(b))
<class 'tuple'> 0
>>> b = (10)
>>> print(type(b))
<class 'int'>
>>> b = (10,)
>>> print(type(b), len(b))
<class 'tuple'> 1
```
`#!python b = (10)` creates an `int`. The comma (`,`) after the only value (`#!python (10,)` in this case) is critical and indicates that it is a tuple with a single element.
5. The `set` data structure is a container, similar to `list` and `tuple`, but its elements are not indexed. Further, its elements are unique, there can only be one occurrence of an element in a set. Search for the official Python documentation for `set` and find the operations that can be performed on it. Can you add a new element? Can you remove an existing element? Can you check if a certain value is present in a `set`? Can you find the intersection of two sets? Are there other operations that can be performed?
**Answer**<br>
```pycon
>>> basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
>>> basket
{'pear', 'banana', 'orange', 'apple'}
>>> len(basket)
4
>>> 'apple' in basket
True
>>> basket[0]
Traceback (most recent call last):
  File "<python-input-15>", line 1, in <module>
    basket[0]
    ~~~~~~^^^
TypeError: 'set' object is not subscriptable
>>> c = basket.union(b2)
>>> c
{'pear', 'banana', 'grapes', 'apple', 'orange'}
>>> basket - b2
{'pear', 'banana', 'orange'}
>>> b2 - basket
{'grapes'}
>>> basket + b2
Traceback (most recent call last):
  File "<python-input-23>", line 1, in <module>
    basket + b2
    ~~~~~~~^~~~
TypeError: unsupported operand type(s) for +: 'set' and 'set'
>>> d = {"apple", "Apple"}
>>> d
{'Apple', 'apple'}
```
**Note**<br>
    1. Order of the elements may not be in the same order as in the defnition of the set
    2. Elements of a set cannot be accessed by indexing
    3. It is possible to check if a value is contained in the set using the `in` operator
    4. Union of two sets can be obtained using the method `#!python set.union(aother_set)`. Using the `+` operator to find the union of two sets results in an error
    5. Difference between two sets is obtained using the `-` operator `#!python set1 - set2` returns the values of `set1` that are not present in `set2`
    6. Elements in a set are case-sensitive when deciding whether an element is unique
6. Given the list `#!python a = [10, 20, 30, 40, 50]`, what does `#!python a[1:4]` return?<br>i) `[30, 40, 50]` ii) `[10, 20, 30]` iii) `[20, 30, 40, 50]` iv) `[20, 30, 40]`
**Answer**<br>
```
>>> a = [10, 20, 30, 40, 50]
>>> a[1:4]
[20, 30, 40]
```
The correct answer is (iv), The slice is defined by start index = 1, stop index = 4 (but 4 not included) with step size = 1. Thus the indices are `#!python 1, 2, 3` and the elements are `#!python a[1], a[2], a[3]`, anmely `#!python [20, 30, 40]`
7. Which of the following operations is NOT allowed on tuples?<br>i) Item assignment ii) Slicing iii) Indexing iv) Concatenation
**Answer**<br>
The answer is (i). The operation **Item assignment** is not allowed because `tuple` is immutable.
```pycon
>>> a = (1, 2, 3)
>>> a[0] = 10
Traceback (most recent call last):
  File "<python-input-32>", line 1, in <module>
    a[0] = 10
    ~^^^
TypeError: 'tuple' object does not support item assignment
>>> a[::2]
(1, 3)
>>> a[2]
3
>>> b = (4, 5)
>>> c = a + b
>>> c
(1, 2, 3, 4, 5)
```