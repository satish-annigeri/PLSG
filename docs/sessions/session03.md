# Session 3

#### Planned Schedule: 21-03-2026 4:00 pm to 6:00 pm

## Agenda

1. Review of previous sessions
2. Answers to queries
3. `range()` to generate a sequence of integers
4. Program flow control: `for` loop, `if -then - elif - else`
5. Function signatures
6. Designing functions

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