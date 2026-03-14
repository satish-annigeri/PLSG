# Session 3

#### Planned Schedule: 21-03-2026 4:00 pm to 6:00 pm

## Agenda

1. Review of previous sessions
2. Answers to queries
3. Function signatures

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

The data types defined for the parameters are for the guidance of the programmer and are ignored by the Python interpreter. Some linters, such as Pylance and Ruff, which are used inside code editors such as VS Code will indicate a warning if the parameters do not match the data type of the parameters, but that is only to warn the programmer.