# Session 3

#### Planned Schedule: 21-03-2026 4:00 pm to 6:00 pm

## Agenda

1. Review of previous sessions
2. Answers to queries
3. Some operations on `list`
4. Some operations on `str`
5. `range()` to generate a sequence of integers
6. Program flow control: `for` loop, `if -then - elif - else`
7. Function signatures
8. Designing functions

## Some operations on `list`

The `list` data type is mutable and is a container data type, that is, it is a container for other elements. The elements of a list can be of any valid type, including built-in types as well as user defined types. In fact, an element of a list can itself be another list. Unlike an array, elements of a list can be of different types. This leads to the concept of multi-dimensioned lists, that is two-dimensioned (consisting of rows and columns) or three-dimensioned (consisting of cards each of which consists of rows and columns) etc. However, unlike an array, the number of columns in the rows need not be the same.

Here is an example of a list containing elements of different data types:
``` pycon
>>> a = [10, 2.5, 'Hello, world", [1, 2.0]]
>>> len(a)
4
>>> type(a[0])
<class int>
>>> type(a[1])
<class float>
>>> type(a[2])
<class str>
>>> type(a[3])
<class list>
>>> len(a[3])
2
>>> type(a[3][0])
<class int>
>>> type(a[3][1])
<class float>
```

Note the following points:

1. The elements of the list `a` are of different types, as shown with the output of the `type()` function
2. Element `a[3]` is itself a list with two elements
3. The elements within `a[3]` can be accessed using index of the element within as shown: `a[3][0]` for element with index `0` of element `a[3]` and `a[3][1]` for the element with index `1` of `a[3]`.
4. If we consider the list as being two dimensioned (because one of its elements is itself a list), all the rows except row with index `3` have only one column and row `a[3]` has two columns.

A list being mutable, you can change its elements:
``` pycon
>>> a[0] = 20
>>> a
[20, 2.5, 'Hello, world", [1, 2.0]]
>>> a[3][0] = 10
>>> a
[20, 2.5, 'Hello, world", [10, 2.0]]
```

Other than changing values of the elements of list, there are several operations we can perform on a list:
``` pycon
>>> a.append(50)
>>> a
[20, 2.5, 'Hello, world', [10, 2.0], 50]
>>> len(a)
5
>>> a[4]
50
>>> a.append((10, 20, 30))
>>> a
[20, 2.5, 'Hello, world', [10, 2.0], 50, (10, 20, 30)]
>>> len(a)
6
>>> len(a[5])
3
```
This is what we did:

1. We appended the element `50`, which is an integer to the list `a`. This increased the length of the list to `5`
2. Subsequently, we appended a tuple `(10, 20, 30)` to the list and increased its length to `6`.

We can insert an element (say the integer `100`) at any chosen index (say `1`):
``` pycon
>>> a.insert(1, 100)
>>> a
[20, 100, 2.5, 'Hello, world', [10, 2.0], 50, (10, 20, 30)]
```

Note the following points about `list.insert(i, element)`:

1. If `i = 0`, the element is inserted at the start of the list
2. If `i = len(a)`, the element is appended to the list, same as `a.append(element)`
3. If `i > len(a)`, the element is appended to the list, same as `a.append(element)`. No error is raised and the list is not expanded to the specified length
4. If `i < 0`, then it is converted to a non-negative insertion position `i = max(0, len(a) + i)`. For example, if `len(a)` is 10, `a.insert(-1, 500)` inserts the element `500` at index $i = max(0, 10 - 1) = 9$, which turns out to be the lremove(x)    | ast but oneRemove the first item in the list whose value is equal to `x` |position after inserting the element tresulting in a length of `11` elements.

Other operations on lists are shown in the table below:

|  Method | Action |
|:------------------|:----------------------------------------------|
|`list.pop([i])`                 |Repme the item at the position in the list, and return it. If `i` is not specified, the last item is popped. |
|`list.clear()`                  |Remove all items from the list. Equivalent to `del a[:]` |
|`list.remove(x)`                |Remove the first item in the list whose value is equal to `x` |
|`list.count(x)`                 |Return the number of times `x` appears in the list  |
|`list.index(x[, start[, end]])` |Return zero-based index in the list of the first item whose value is `x`. Raises a ValueError if there is no such item. |
|`list.count(x)`                 |Return the number of times `x` appears in the list |
|`list.sort(*, key=None, reverse=False)` |Sort the items of the list in place. `key` specifies a function of one argument that is used to extract a comparison key from each element in iterable (for example, key=str.lower). The default value is None (compare the elements directly). `reverse` is a boolean value. If set to True, then the list elements are sorted as if each comparison were reversed. |
|`list.reverse()`  |Reverse the elements of the list in place  |
|`list.copy()`     |Return a shallow copy of the list. Equivalent to a[:]  |

**Note:** The square brackets `[ ]` around `i` in the method signature `list.pop([i])` denote that the parameter is **optional**, not that you should type square brackets in that position. So is the case with `start` and `end` in the method `index(x[, start[, end]])`. When they are not provided, default values defined in the method definition are used.

For more information, refer the Python documentation page: [More on lists](https://docs.python.org/3.10/tutorial/datastructures.html#more-on-lists).

## Some operations on `str`
A Python `str` has a number of very useful methods which you will find useful when you have to process text.

|  Method | Action |
|:------------------|:----------------------------------------------|
|`str.capitalise()` |Return a copy of the string with the first character capitalized and the rest lowercased |
|`str.casefold()`   |Return a casefolded copy of the string. Casefolding is similar to lowercasing but is more aggressive, specifically with non-English language characters |
|`str.center(width[, fillchar])` |Return centered in a string of length width. Padding is done using the specified fillchar (default is an ASCII space). The original string is returned if width is less than or equal to len(s) |
|`str.count(sub[, start[, end]])` |Return the number of non-overlapping occurrences of substring sub in the range [start, end]. Optional arguments start and end are interpreted as in slice notation.<br> If sub is empty, returns the number of empty strings between characters which is the length of the string plus one. |
|`str.endswith(suffix[, start[, end]])` |Return True if the string ends with the specified suffix, otherwise return False. suffix can also be a tuple of suffixes to look for. With optional start, test beginning at that position. With optional end, stop comparing at that position. |
|`str.find(sub[, start[, end]])` |Return the lowest index in the string where substring sub is found within the slice s[start:end]. Optional arguments start and end are interpreted as in slice notation. Return -1 if sub is not found. |
|`str.lower()` |Return a copy of the string with all the cased characters 4 converted to lowercase |
|`str.upper()` |eturn a copy of the string with all the cased characters 4 converted to uppercase |

There are many more and you should study all of them from the Python documentation page: [Text Sequence Type - `str`](https://docs.python.org/3.10/library/stdtypes.html?highlight=str#text-sequence-type-str)

## `range()` to generate a sequence of integers
Let us try this in the Python REPL before we attempt to understand `range()` and what it does:
``` pycon
>>> range(5)
range(0, 5)
>>> range(1, 6)
range(1, 6)
>>> range(1, 10, 2)
range(1, 10, 2)
>>> r = range(5)
>>> print(r.start, r.stop, r.step)
0 5 1
```

## Program flow control

## Function Signatures

A function has the following attributes:

1. A unique name: The name must uniquely identify this function. If two functions have the same name, the most recent definition of the function erases the previous definition.
2. Zero or more input parameters: Input parameters are enclosed within parentheses in fron t of the function name. Defining the type for the parameters is encouraged, but not required.
3. zero or more output parameters: The `return` statement returns the output parameters. If no parameters are defined in the `return` statement, the value `None` is returned.
4. Body of the function: Zero or more statements indented with reference to the first line of the function constitute the body of the function.

Function definition requires the keyword `def` follwed by the name of the function and a pair of parentheses. Parentheses are required even when there are no input parameters. The line defining the function ends with the colon (`:`). The body of the function must be indented by a fixed number of spaces (4 by convention). To mark the end of the function, the subsequent lines must be unindented.

Here is a illustrative example that takes two real numbers as input and returns their product. Type the following code in the Python REPL:

``` pycon
>>> def product(a: float, b: float) -> float:
...     return a * b
...
>>> type(product)
<class function>
>>> product
<function product at 0x7fff36029010>
```
The parameters `a` and `b` are **parameters** and are placeholders for objects that will take their place (called **arguments**), when the function is called.

Having defined the function, you can call it:
``` pycon
>>> product(2, 3)
6
>>> product(2.5, 3)
7.5
```
The arguments in the first call to the function are `#!python a = 2` and `#!python b = 3`. The second time, the arguments are `#!python a = 2.5` and `#!python b = 3`.

!!! note
    The data types of the input and output parameters in the function definition are for the guidance of the programmer and are ignored by the Python interpreter. This is called type hints, and some code editors display the function signature when the mouse hovers over the name of the function. Type hints remind the programmer's intent and help avoid errors.


Defining a function that returns more than one value is easy and straigh forward.
``` pycon
>>> def stats(a: list[float]) -> tuple[int, float, float]:
...     n = len(a)
...     s = sum(a)
...     mean = s / n
...     return n, s, mean
...
>>> 
```
When this function is called, it returns three values. Therefore we must provide three objects on the left hand side of the function call to store these returned values for subsequenty use.
``` pycon
>>> num, total, avg = stats([1, 2, 3, 4, 5])
>>> print(num, total, avg)
5 15 3.0
```

!!! note
    The names of the parameters in the function definition and the names of the arguments at the time of function call need not be the same, although they can be. The very aim of modularity is to have this flexibility. If were forced to use the same names it would place an additiional burden on the programmer to keep track of all the names of parameters. Now the programmer need only remember the number and data type of the parameters.

## Designing functions

Designing a function requires the following steps:

1. Write a clear and complete definition of what the function is expected to do
2. Based on what the function is expected to do, determine the input data required to accomplish the defined task and the output data to be produced by the function
3. Identify the procedure to transform the input data into the required output data. This will require knowing some theory, possibly some mathematics and an algorithm
4. Define the function signature:
   1. Name of the function: It must be unique, cryptic (not too lengthy or verbose), and reflect the task it accomplishes
   2. Number, data type and names of input parameters
   3. Number, data type and names of output parameters
5. Represent the algorithm in pseudo-code or flow chart
6. Prepare test input and output to test the function once it is written

With that, the design is complete and the implementation can begin. At the stage of defining the algorithm, if it is found to be overly complex, it may be a good idea to sub-divide the task of the required function into sub-tasks, and proceed with the design of the functions to implement the sub-tasks. You may work backwards until the required task is accomplished.

It may not always be clear when you start implementing the function that it is too complex to implement. In such a case, it is best to stop, think about sub-dividing the task, completing the functions for the sub-tasks before proceeding with the required function.

## Example of designing a function