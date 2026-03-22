# Answer 1

#### Answers to: [Assignment 1](assignment01.md)


**Q1.** What does **REPL** stand for? Can you name other programming languages/environments that offer a REPL?

??? success "Answer"
    REPL stands for **R**ead, **E**valuate, **P**rint **L**oop. It is a programming environment with its own memory space and can evaluate single or multiple lines of code and produce output. It is an interactive environment where the programmer can try out lines of code one at a time and examine the results before proceeding. One disadvantage of REPL is that it does not save the code in a file for subsequent use, although it can read and execute code that is already written in a file. But that takes away the interactive nature of a REPL and a code editor is much better suited to execute code in a file.<br><br>Other programming languages that offer a REPL are Matlab, Julia, Javascript (Node JS) and many more.
**Q2.** Having assigned the value `10` to the object `a`, what are the two ways to display the value of the object `a`?

??? success "Answer"
    In the REPL, value of an object can be displayed by typing the name of the object and pressing ++enter++ or by using the `print()` function.<br>
    ```pycon
    >>> a = 10
    >>> a
    10
    >>> print(a)
    10
    ```
    In a script, the only way to display the value of an object is to print it using `#!python print(a)`.
**Q3.** Given the list `#!python a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]`

**3.1** Determine the number of elements in the list
??? success "Answer"
    ```pycon
    >>> len(a)
    10
    ```
**3.2** Use negative indexing operation to obtain the **last but one element** of the list (in this example, the element with value `9`).
??? success "Answer"
    ```pycon
    >>> a[-2]
    9
    ```
**3.3** What are the slice `start`, `stop` and `step` values to produce the list [9, 6, 3]. Remember the slice notation `#!python a[start:stop:step]`.
??? success "Answer"
    ```pycon
    >>> a[-2::-3]
    [9, 6, 3]
    ```
**Q4.** You can create an empty `list` with `#!python a = []`. Creating an empty `tuple` is similar `#!python b = ()`. But how do you create a `tuple` with exactly one element? Does `#!python b = (10)` work? Why not? What is the correct way to create a tuple with exactly one element. Search the net for the answer.
??? success "Answer"
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
**Q5.** The `set` data structure is a container, similar to `list` and `tuple`, but its elements are not indexed. Further, its elements are unique, there can only be one occurrence of an element in a set. Search for the official Python documentation for `set` and find the operations that can be performed on it. Can you add a new element? Can you remove an existing element? Can you check if a certain value is present in a `set`? Can you find the intersection of two sets? Are there other operations that can be performed?
??? success "Answer"
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
    **Note**

    1. Order of the elements may not be in the same order as in the defnition of the set
    2. Elements of a set cannot be accessed by indexing
    3. It is possible to check if a value is contained in the set using the `in` operator
    4. Union of two sets can be obtained using the method `#!python set.union(aother_set)`. Using the `+` operator to find the union of two sets results in an error
    5. Difference between two sets is obtained using the `-` operator `#!python set1 - set2` returns the values of `set1` that are not present in `set2`
**Q6.** Elements in a set are case-sensitive when deciding whether an element is unique
1. Given the list `#!python a = [10, 20, 30, 40, 50]`, what does `#!python a[1:4]` return?<br>i) `[30, 40, 50]` ii) `[10, 20, 30]` iii) `[20, 30, 40, 50]` iv) `[20, 30, 40]`
??? success "Answer"
    ```
    >>> a = [10, 20, 30, 40, 50]
    >>> a[1:4]
    [20, 30, 40]
    ```
    The correct answer is (iv), The slice is defined by start index = 1, stop index = 4 (but 4 not included) with step size = 1. Thus the indices are `#!python 1, 2, 3` and the elements are `#!python a[1], a[2], a[3]`, anmely `#!python [20, 30, 40]`
**Q7.** Which of the following operations is NOT allowed on tuples?<br>i) Item assignment ii) Slicing iii) Indexing iv) Concatenation
??? success "Answer"
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
**Q8.** What is the output of `#!python len((1, 2, (3, 4)))`?<br>i) `3` ii) `4` iii) `2` iv) Error
??? success "Answer"
    ```pycon
    >>> len((1, 2, (3, 4)))
    3
    ```
    Element at index `2` is a tuple with two elements inside it, is counted as one element.
**Q9.** Which of the following data type is mutable?<br>i) `int` ii) `str` iii) `tuple` iv) `list`
??? success "Answer"
    Only `list` is mutable, the rest are immutable. Here is an exercise that wil clarify how an `int` is immutable.
    ```pycon
    >>> x = 10
    >>> id(x)
    93827280581664
    >>> id(10)
    93827280581664
    >>> y = x
    >>> id(y)
    93827280581664
    >>> x = 20
    >>> id(x)
    93827280581984
    >>> id(20)
    93827280581984
    >>> id(y)
    93827280581664
    >>> z = 20
    >>> id(z)
    93827280581984
    ```

    1. Like the variable (object) `x`, an integer constant such as `10` also has a memory address
    2. `#!python y = x` makes `y` an alternate name for `x` and have the same memory address as the integer 10
    3. `#!python x = 20` creates a new integer `20` at a new memory adress and that address is assigned to `x`. But the memory address of `y` remains unchanged to the memory address of `10`.
    4. `#!python z = 20` creates a new variable `z` and is assigned the memory address that already contains the value `20`
    5. Integers `10` and `20` are **immutable**, once created their value stored in a specific memory address does not change
**Q10.** What is the result of `#!python ('a', 'b') + ('c',)`?<br>i) Error ii) `#!python ['a', 'b', 'c']` iii) `#!python ('a', 'b', 'c')` iv) `#!python ('a', 'b')`

??? success "Answer"
    ```pycon
    >>> ('a', 'b') + ('c',)
    ('a', 'b', 'c')`
    ```

    `#!python ('c',)` is a `tuple` containing a single element and when added to the `tuple` with two elements `#!python ('a', 'b')` returns a new `tuple` with three elements. If the comma (`,`) after `c` is missed, `#!python ('`')` is not a `tuple` and the operation would result in an error.

    ```pycon
    >>> ('a', 'b') + ('c')
    Traceback (most recent call last):
    File "<python-input-12>", line 1, in <module>
        ('a', 'b') + ('c')
        ~~~~~~~~~~~^~~~~~~
    TypeError: can only concatenate tuple (not "str") to tupl
    ```
## Answer True or False

**Q1.** The REPL manages its own memory to store the objects created by you, as well as the modules and packages imported by you
??? success "Answer"
    **True**

    REPL is a complete Python environment with the built-in Python interpreter, memory space and memory manager. As you type in each command, REPL will interpret your *commands* and if valid, carry them out. Carrying out a command may involve creating objects in memory, importing modules from an external source and store in memory for later use, compile a function and store it in memory and make it available for subsequent use.

    ```pycon
    >>> import math
    >>> math
    <module 'math' (built-in)>
    id(math)
    140734448557632
    >>> def dbl(x):
    ...     return 2 * x
    ...     
    >>> dbl
    <function dbl at 0x7fff4ad09220>
    >>> id(dbl)
    140734448570912
    ```

**Q2.** In a REPL, you can display the value of an object without having to use the `print()` function whereas it is necessary to use the `print()` function to display the value of an object in a script (code written in a file and executed from the terminal).
??? success "Answer"
    **True**

    REPL has a built-in interpreter and has it logic for interpreting the commands typed atthe prompt. When the user types the name of an object, the interpreter is programmed to print the corresponding value of the object.
    
    But when the name of an object apperas all by itself in script, becuase it is not assigned to any other object or not used in any other way, that line does not result in any output. In a script, one must use the `#!python print()` function to display values.

**Q3.** Data type `str` is immutable.
??? success "Answer"
    **True**

**Q4.** Immutable means the value assigned to the object cannot be changed once assigned.
??? success "Answer"
    **True**

**Q5.** Immutability only prevents replacing an element with a new value, but does not stop you from assigning an entirely new value to the object. That is, `#!python a = (1, 2, 3); a[0] = 10` is not permitted, but `#!python a = (1, 2, 3); a = (10, 20, 30)` is permitted.
??? success "Answer"
    **True**

**Q6.** Data type `list` is immutable.
??? success "Answer"
    **False**

**Q7.** You can embed an apostrophe (`'`) inside a string constant delimited by apostrophes, provided it is escaped using the backslash `\'`. That is, this is a valid string: `'This isn\'t difficult'`.
??? success "Answer"
    **True**

    ```pycon
    >>> 'This isn\'t difficult'
    "This isn't difficult"
    >>> print('This isn\'t difficult')
    This isn't difficult
    ```

    Note that the REPL normally delimits the string by single quotes (`'`) when you type the object or the name of an object. But when the string contains single quotes within it, it delimits the string by double quotes (`"`).

    When the string is displayed using the `print()` function, no quotes are shown in the REPL.

**Q8.** When you carry out an index or slice operation on a list, tuple or a string, the operation returns a **new object** with the values copied from the original object.
??? success "Answer"
    **True**

    Using the index of an element returns a single object of the same type as that of the returned object.

    Using the slicing operation returns a list with the objects as defined in the slice.

    ```pycon
    >>> a = [1, 2, 3, 4, 5]
    >>> type(a[0]), a[0]
    (<class 'int'>, 1)
    >>> type(a[::2]), a[::2]
    (<class 'list'>, [1, 3, 5])
    ```

    If you observe, you will notice that typing more than one object in the REPL command promt, separated commas returns a `tuple` with the values of the objects typed at the command prompt.

**Q9.**  Create a `dict` object to represent the name. age and phone number of a person.

1. Obtain the **keys** and **values** of the object.
1. Obtain the value for the name of the person
2. Increase the age of the person by 1 year

??? success "Answer"

    ```pycon
    >>> a = {"name": "John Doe", "age": 25, "phone": "+91 6xyzx abcde"}
    >>> type(a), a
    (<class 'dict'>, {'name': 'John Doe', 'age': 25, 'phone': '+91 6xyzx abcde'})
    >>> a.keys()
    dict_keys(['name', 'age', 'phone'])
    >>> a.values()
    dict_values(['John Doe', 25, '+91 6xyzx abcde'])
    >>> a["age"] += 1
    >>> a
    >>> a["age"] += 1
    >>> a
    {'name': 'John Doe', 'age': 26, 'phone': '+91 6xyzx abcde'}
    ```

**Q10.** When you assign a previously created list to a new object, the new object is an exact copy of the values of the original list, and not the same values as the original list. Another way to ask the same question is, `#!python a = [1, 2, 3]; b = a; a is b` returns False.<br>**Note:** This topic has not been discussed in any of the previous sessions. But I encourage you to try out the following lines of code in the REPL to find the answer. More importanly, can you explain what is happening?

``` pycon
>>> a = [1, 2, 3]
>>> b = a
>>> a is b
???
>>> id(a)
???
>>> id(b)
???
>>> c = a[:]
>>> a is c
???
>>> id(c)
???
>>> a == c
???
>>> b[0] = 100
>>> a
???
```
??? success "Answer"

    **False**. It returns `True`

    ``` pycon
    >>> a = [1, 2, 3]
    >>> b = a
    >>> a is b
    True
    >>> id(a)
    140734448672256
    >>> id(b)
    140734448672256
    >>> c = a[:]
    >>> a is c
    False
    >>> id(c)
    140734448672896
    >>> a == c
    True
    >>> b[0] = 100
    >>> a
    [100, 2, 3]
    >>> c
    [1, 2, 3]
    ```
