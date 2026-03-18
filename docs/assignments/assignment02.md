# Assignment 2

#### Corresponds to: [Session 2](../sessions/session02.md)

#### Answers: [Answer 2](answer02.md)

## Questions

1. Given three lists `#!python a = [1, 2, 3]`, `#!python b = a` and `c = a[:]`, which of the following logical expresions are `True`? Explain why the results are what they are.
    1. `#!python a == b`
    2. `#!python a is b`
    3. `#!python a == c`
    4. `#!python a is c`
2. A quadratic equation is repesented as $a x^2 + bx + c = 0$, where $a \neq 0$. The roots are real numbers if $b^2 - 4 ac \geq 0$. Given the coefficients `a`, `b` and `c`, write the logical expression to check that they represent a quadratic equation with real roots. **Note:** You must check for the conditions that $a \neq 0$ and also $b^2 - 4 ac \geq 0$.
3. Why is it important to design a program before implementing it as code?
4. When designing a program using the procedural paradigm, how do you decide when to stop sub-dividing a task?
5. The two important components of a program are the data (the information required to repesent the problem being solved) and the algorithm (the procedure used to transform the input data to the required output data). What is the primary focus of the procedural paradigm - data or algorithm? Justify your answer.

## Quiz

1. What does the function `id(x)` return?
    1. The data type of `x`
    2. The memory address (identity) of `x`
    3. The size of `x` in bytes
    4. The value `x`
2. Which operator checks whether two variables refer to the same object?
    1. `!=`
    2. `is`
    3. `==`
    4. `in`
3. If `#!python a = [1, 2]` and `#!python b = [1, 2]`, what is the result of `#!python a == b`?
    1. Depends on Python version
    2. `True`
    3. Error
    4. `False`
4. If `#!python a = [1, 2]` and `#!python b = [1, 2]`, what is the result of `a is b`?
    1. `False`
    2. Error
    3. `True`
    4. Depends on indentation
5. Which logical operator returns `#!python True` only if both conditions are true?
    1. `xor`
    2. `and`
    3. `not`
    4. `or`
6. What is the result of `#!python True or False`?
    1. `False`
    2. Error
    3. `True`
    4. `None`
7. What does the `not` operator do?
    1. Checks identity
    2. Reverses a `bool` value
    3. Creates a new variable
    4. Compares two values
8. Which of the following is a valid logical expression?
    1. `#!python 5 multiply 10`
    2. `#!python 5 equals 10`
    3. `#!python 5 plus 10`
    4. `#!python 5 and 10`
9. In VS Code, where do you typically see error messages and program output?
    1.  The Activity bar
    2.  The Explorer panel
    3.  The Extension panel
    4.  The Terminal panel
10. Which VS Code panel shows your files and folders?
    1. Extension
    2. Source Control
    3. Explorer
    4. Run and Debug
11. What is the purpose of the VS Code Command Palette?
    1. To display errors
    2. To manage Git branches
    3. To run commands quickly
    4. To store code snippets
12. True or False: The `is` operator checks whether two objects have equal values.
    1. False
    2. True
    3. Sometimes True
    4. Only for integers
13. Which logical operator would make this expression True: False ___ True?
    1. `and`
    2. `not`
    3. `is`
    4. `or`
14. If `#!python a = 5` and `#!python b = 10`, `#!python c = -3` and `#!python d = a`, what are the results of the following logical operations?
    1. `#!python 0 <= c <= a`
    2. `#!python c <= a <= b`
    3. `#!python a != c`
    4. `#!python not (a >= c)`
    5. `#!python a is d`
    6. `#!python c is not d`
