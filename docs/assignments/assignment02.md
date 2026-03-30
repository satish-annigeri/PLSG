# Assignment 2

#### Corresponds to: [Session 2](../sessions/session02.md)

#### Answers: [Answer 2](answer02.md)

## Questions

**1.** Given three lists `#!python a = [1, 2, 3]`, `#!python b = a` and `c = a[:]`, which of the following logical expresions are `True`? Explain why the results are what they are.
A. `#!python a == b`  
B. `#!python a is b`  
C. `#!python a == c`  
D. `#!python a is c`  

??? success "Answer"
    A. `#!python a == b` -> **True**. Both the lists `a` and `b` contain the same elements.   
    B. `#!python a is b` -> **True**.List object `b` refers to the same list object as `a`, so they share the same memory address.  
    C. `#!python a == c` -> **True**. List `c` is an element-wise copy of the list `a`, and both contain the same elements.  
    D. `#!python a is c` -> **False**. List `c` is a new object created by slicing, so it has a different memory address.  

**2.** A quadratic equation is repesented as $a x^2 + bx + c = 0$, where $a \neq 0$. The roots are real numbers if $b^2 - 4 ac \geq 0$. Given the coefficients `a`, `b` and `c`, write the logical expression to check that they represent a quadratic equation with real roots. **Note:** You must check for the conditions that $a \neq 0$ and also $b^2 - 4 ac \geq 0$.
??? success "Answer"
    ```python
    if (a != 0) and (b*b - 4*a*c >= 0)
    ```

**3.** Why is it important to design a program before implementing it as code?
??? success "Answer"
    1. It provides confidence that the final program meets the requirements defined at the start.  
    2. It reduces time spent during implementation by clarifying structure and decisions early.

**4.** When designing a program using the procedural paradigm, how do you decide when to stop sub-dividing a task?
??? success "Answer"
    One useful guideline is to stop sub‑dividing a task when one of the following conditions is met:

    1. The task **cannot** be divided further.  
    2. The task is simple enough that further division is **not worthwhile**.

**5.** The two important components of a program are the data (the information required to repesent the problem being solved) and the algorithm (the procedure used to transform the input data to the required output data). What is the primary focus of the procedural paradigm - data or algorithm? Justify your answer.
??? success "Answer"
    The procedural paradigm primarily focuses on the procedure required to accomplish the task. Functions form the core of this paradigm, and programs are built as hierarchies of functions. More abstract, higher‑level functions call simpler, lower‑level functions. Data flows through these functions and is transformed step by step until the desired output is produced. The emphasis is on designing clear, well‑structured procedures, while data is shaped and refined as it moves through the sequence of operations.


## Quiz

**1.** What does the function `id(x)` return?

A. The data type of `x`  
B. The memory address (identity) of `x`  
C. The size of `x` in bytes  
D. The value `x`  

??? success "Answer"
    **Correct answer:** B

    A. The data type of `x` is returned by `type(x)`  
    B. The memory address (identity) of `x`  
    C. The size of `x` is returned by the function `getsizeof()` from the built-in module `sys`.  

    ```pycon
    >>> import sys
    >>> x = 10
    >>> sys.getsizeof(x)
    28
    ```  

    D. The value of `x` is returned by using its name `x` in a statement  

**2.** Which operator checks whether two variables refer to the same object?

A. `!=`  
B. `is`  
C. `==`  
D. `in`  

??? success "Answer"
    **Correct answer:** B

    A. `!=` checks if a value *is not equal to* another value  
    B. **`is`** checks if one object has the same identity (memory address) as another object  
    C. `==` checks if one value is equal to another value  
    D. `in` checks if one value is contained in a given container object  

**3.** If `#!python a = [1, 2]` and `#!python b = [1, 2]`, what is the result of `#!python a == b`?

A. Depends on Python version  
B. `True`  
C. Error  
D `False`  

??? success "Answer"
    **Correct answer:** B

    A. The answer is the same in all versions of Python  
    B. **True** -> Both objects have the same values. **Note:** `1 == 1.0` where the first value is an `int` and the second is a `float`  
    C. No error is reported when comparing `a == b`  
    D. Not **false** -> Both `a` and `b` have the same values  


**4.** If `#!python a = [1, 2]` and `#!python b = [1, 2]`, what is the result of `a is b`?

A. `False`  
B. Error  
C. `True`  
D. Depends on indentation  

??? success "Answer"
    **Correct answer:** C

    A. Even though they both have the same values, they have different identities (memory address)  
    B. Not an error. `a is b` is not an error, it is a valid statement  
    C. Not **true** -> They do not have the same identity, therefore not `True`  
    D. Does not depend on indentation  

**5.** Which logical operator returns `#!python True` only if both conditions are true?

A. `xor`  
B. `and`  
C. `not`  
D. `or`  

??? success "Answer"
    **Correct answer:** B
    
**6.** What is the result of `#!python True or False`?

A. `False`  
B. Error  
C. `True`  
D. `None`  

??? success "Answer"
    **Correct answer:** C

    An `or` condition is `True` if one of the two operands is `True`. It is `False` only when both are `False`.

**7.** What does the `not` operator do?

A. Checks identity  
B. Reverses a `bool` value  
C. Creates a new variable  
D. Compares two values  

??? success "Answer"
    **Correct answer:** B

    The `not` operator inverts the value of a `bool` value. Thus `not True` return `False` and `not False` returns `True`.

**8.** Which of the following is a valid logical expression?

A. `#!python 5 multiply 10`  
B. `#!python 5 equals 10`  
C. `#!python 5 plus 10`  
D. `#!python 5 and 10`  

??? success "Answer"
    **Correct answer:** D

    None among `multiply`, `equals` and `plus` is a valid Python operator. `#!python 5 and 10` returns `10`, the second operator. This is how Python logical `and` expressions are evaluated:

    1. If the left operand is *falsy* (`0`, `""`, `None`, `False` or `[]`) the logical expression returns the first operand, without evaluating the second operand. In this example, the first operand `5` is not `False`.
    2. If the left operand is not *falsy*, the expression returns the second operand, which in this example is `10`..

    Thus `#!python 5 and 20` will return `20` and `#!python 5 and False` will return `False` and `#!python 0 and 10` will return `0`.

**9.** In VS Code, where do you typically see error messages and program output?

A.  The Activity bar  
B.  The Explorer panel  
C.  The Extension panel  
D.  The Terminal panel  

??? success "Answer"
    **Correct answer:** D

    The **Terminal panel** lets the user type commands and display results of executing programs

**10.** Which VS Code panel shows your files and folders?

A. Extension
B. Source Control
C. Explorer
D. Run and Debug

??? success "Answer"
    **Correct answer:** C

    The **Explorer** lets the user navigate the filesystem with the directory open in VS Code as the root dirctory. User can traverse downward from this root but not upwards.

**11.** What is the purpose of the VS Code Command Palette?

A. To display errors
B. To manage Git branches
C. To run commands quickly
D. To store code snippets

??? success "Answer"
    **Correct answer:** C

    The Command Palette is VS Code’s universal command launcher. Instead of hunting through menus, you can open it and fuzzy‑search for any action VS Code can perform — built‑in commands, extension commands, settings, navigation tools, and more.

**12.** True or False: The `is` operator checks whether two objects have equal values.

 A. False
 B. True
 C. Sometimes True
 D. Only for integers

??? success "Answer"
    **Correct answer:** A

    The `is` operator check whether two objects have the same identity (memory address) not whether they have equal values.

**13.** Which logical operator would make this expression True: False ___ True?

A. `and`
B. `not`
C. `is`
D. `or`

??? success "Answer"
    **Correct answer:** D

    A. `and` -> `#!python False and True` is `False`  
    B. `not` -> `#!python False not True` is an error  
    C. `is` -> `#!python False is True` is `False` because they have different identities (memory address)  
    D. `or` -> `#!python False or True` is `True` as the left operand is `True`  

**14.** If `#!python a = 5` and `#!python b = 10`, `#!python c = -3` and `#!python d = a`, what are the results of the following logical operations?

A. `#!python 0 <= c <= a`  
B. `#!python c <= a <= b`  
C. `#!python a != c`  
D. `#!python not (a >= c)`  
E. `#!python a is d`  
F. `#!python c is not d`  

??? success "Answer"
    A. `#!python 0 <= c <= a` -> `False` because this is equivalent to `#!python (0 <= -3) and (c <= 5)` and `#!python 0 <= -3` is `False` and one `False` results in the `and` expression to evaluate to `False`  
    B. `#!python c <= a <= b` -> `True` because `#!python (-3 <= 5) and (5 <= 10` is `True`   
    C. `#!python a != c` -> `True` because `#!python 5 != -3` is `True`  
    D. `#!python not (a >= c)` -> `True` because `#!python 5 >= -3` is `True`  
    E. `#!python a is d` -> `True` because in Python they both have the same memory address, which is the memory address of the immutable integer value `5`  
    F. `#!python c is not d` -> `True` because `c` and `d` are integers with different vlues and therefore have different memory addresses. Thus `c` and `d` do not have the same memory address, which is true.  