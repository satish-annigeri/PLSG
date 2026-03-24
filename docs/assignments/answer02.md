# Answer 2

#### Answers to: [Assignment 2](assignment02.md)


The answers will be added on 28-03-2026

## Questions

**Q1.** Given three lists `#!python a = [1, 2, 3]`, `#!python b = a` and `c = a[:]`, which of the following logical expressions are `True`? Explain why the results are what they are.

1. `#!python a == b` **Ans: True** because both lists contain the same elements.  
2. `#!python a is b` **Ans: True** because `b` refers to the same list object as `a`, so they share the same memory address.  
3. `#!python a == c` **Ans: True** because `c` is a shallow copy of `a`, and both contain the same elements.  
4. `#!python a is c` **Ans: False** because `c` is a new list created by slicing, so it has a different memory address.

**Q2.** A quadratic equation is represented as \(a x^2 + bx + c = 0\), where \(a \neq 0\). The roots are real numbers if \(b^2 - 4ac \geq 0\). Given the coefficients `a`, `b` and `c`, write the logical expression to check that they represent a quadratic equation with real roots. **Note:** You must check both \(a \neq 0\) and \(b^2 - 4ac \geq 0\).

??? success "Answer"
    ```python
    if (a != 0) and (b*b - 4*a*c >= 0)
    ```

**Q3.** Why is it important to design a program before implementing it as code?

??? success "Answer"
    1. It provides confidence that the final program meets the requirements defined at the start.  
    2. It reduces time spent during implementation by clarifying structure and decisions early.

**Q4.** When designing a program using the procedural paradigm, how do you decide when to stop sub‑dividing a task?

??? success "Answer"
    One useful guideline is to stop sub‑dividing a task when one of the following conditions is met:

    1. The task **cannot** be divided further.  
    2. The task is simple enough that further division is **not worthwhile**.

**Q5.** The two important components of a program are the data (the information required to represent the problem being solved) and the algorithm (the procedure used to transform the input data into the required output). What is the primary focus of the procedural paradigm—data or algorithm? Justify your answer.

??? success "Answer"
    The procedural paradigm primarily focuses on the procedure required to accomplish the task. Functions form the core of this paradigm, and programs are built as hierarchies of functions. More abstract, higher‑level functions call simpler, lower‑level functions. Data flows through these functions and is transformed step by step until the desired output is produced. The emphasis is on designing clear, well‑structured procedures, while data is shaped and refined as it moves through the sequence of operations.


## Quiz

Q1. What does the function `id(x)` return?

1. The data type of `x`
2. :lucide-circle-check: **The memory address (identity) of `x`**
3. The size of `x` in bytes
4. The value `x`

??? success "Answer"

    1. The data type of `x` is returned by `type(x)`

    2. The memory address (identity) of `x`

    3. The size of `x` is returned by the function `getsizeof()` from the built-in module `sys`.
    ```pycon
    >>> import sys
    >>> x = 10
    >>> sys.getsizeof(x)
    28
    ```

    4. The value of `x` is returned by using its name `x` in a statement

Q2. Which operator checks whether two variables refer to the same object?

1. `!=`
2. :lucide-circle-check: **`is`**
3. `==`
4. `in`

??? success "Answer"

    1. `!=` checks if a value *is not equal to* another value
    2. **`is`** checks if one object has the same identity (memory address) as another object
    3. `==` checks if one value is equal to another value
    4. `in` checks if one value is contained in a given container object

Q3. If `#!python a = [1, 2]` and `#!python b = [1, 2]`, what is the result of `#!python a == b`?

1. Depends on Python version
2.  :lucide-circle-check: **`True`**
3. Error
4. `False`
??? success "Answer"
    1. Depends on Python version -> **False**. The answer is the same in all versions of Python
    2. `True` -> **Correct** because both objects have the same values. **Note:** `1 == 1.0` where the first value is an `int` and the second is a `float`
    3. Error -> No error is reported when comparing `a == b`
    4. `False` --> Incorrect, because `a` and `b` both have the same values

Q4. If `#!python a = [1, 2]` and `#!python b = [1, 2]`, what is the result of `a is b`?

1. :lucide-circle-check: **`False`**
2. Error
3. `True`
4. Depends on indentation
??? success "Answer"
    1. **`False`** -> Even though they both have the same values, they have different identities (memory address)
    2. Error -> `a is b` is not an error, it is a valid statement
    3. `True` -> They do not have the same identity, therefore not `True`
    4. Depends on indentation -> Not correct

Q5. Which logical operator returns `#!python True` only if both conditions are true?

1. `xor`
2. :lucide-circle-check: **`and`**
3. `not`
4. `or`
??? success "Answer"
    
Q6. What is the result of `#!python True or False`?

1. `False`
2. Error
3. :lucide-circle-check: **`True`**
4. `None`
??? success "Answer"
    For `or` to be `True`, it is enough if one of the two is `True`. It is `False` only when both are `False`.

Q7. What does the `not` operator do?

1. Checks identity
2. :lucide-circle-check: **Reverses a `bool` value**
3. Creates a new variable
4. Compares two values
??? success "Answer"
    The `not` operator inverts the value of a `bool` value. Thus `not True` return `False` and `not False` returns `True`.

Q8. Which of the following is a valid logical expression?

1. `#!python 5 multiply 10`
2. `#!python 5 equals 10`
3. `#!python 5 plus 10`
4. :lucide-circle-check: **`#!python 5 and 10`**
??? success "Answer"
    None among `multiply`, `equals` and `plus` is a valid Python operator. `#!python 5 and 10` returns `10`, the second operator. This is how Python logical `and` expressions are evaluated:
    1. If the left operand is *falsy* (`0`, `""`, `None`, `False` or `[]`) the logical expression returns the first operand, without evaluating the second operand. In this example, the first operand `5` is not `False`.
    2. If the left operand is not *falsy*, the expression returns the second operand, which in this example is `10`..

    Thus `#!python 5 and 20` will return `20` and `#!python 5 and False` will return `False` and `#!python 0 and 10` will return `0`.

Q9. In VS Code, where do you typically see error messages and program output?

1.  The Activity bar
2.  The Explorer panel
3.  The Extension panel
4.  :lucide-circle-check: **The Terminal panel**
    
Q10. Which VS Code panel shows your files and folders?

1. Extension
2. Source Control
3. :lucide-circle-check: **Explorer**
4. Run and Debug
    
Q11. What is the purpose of the VS Code Command Palette?

1. To display errors
2. To manage Git branches
3. :lucide-circle-check: **To run commands quickly**
4. To store code snippets
    
Q12. True or False: The `is` operator checks whether two objects have equal values.

1. :lucide-circle-check: **False**
2. True
3. Sometimes True
4. Only for integers
??? success "Answer"
    The `is` operator check whether two objects have the same identity (memory address) not whether they have equal values.

Q13. Which logical operator would make this expression True: False ___ True?

1. `and`
2. `not`
3. `is`
4. :lucide-circle-check: **`or`**
??? success "Answer"
    1. `and` -> `#!python False and True` is `False`
    2. `not` -> `#!python False not True` is an error
    3. `is` -> `#!python False is True` is `False` because they have different identities (memory address)
    4. `or` -> `#!python False or True` is `True` as the left operand is `True`

Q14. If `#!python a = 5` and `#!python b = 10`, `#!python c = -3` and `#!python d = a`, what are the results of the following logical operations?

1. `#!python 0 <= c <= a`
2. `#!python c <= a <= b`
3. `#!python a != c`
4. `#!python not (a >= c)`
5. `#!python a is d`
6. `#!python c is not d`
??? success "Answer"
    1. `#!python 0 <= c <= a` -> `False` because this is equivalent to `#!python (0 <= -3) and (c <= 5)` and `#!python 0 <= -3` is `False` and one `False` results in the `and` expression to evaluate to `False`
    2. `#!python c <= a <= b` -> `True` because `#!python (-3 <= 5) and (5 <= 10` is `True` 
    3. `#!python a != c` -> `True` because `#!python 5 != -3` is `True`
    4. `#!python not (a >= c)` -> `True` because `#!python 5 >= -3` is `True`
    5. `#!python a is d` -> `True` because in Python they both have the same memory address, which is the memory address of the immutable integer value `5`
    6. `#!python c is not d` -> `True` because `c` and `d` are integers with different vlues and therefore have different memory addresses. Thus `c` and `d` do not have the same memory address, which is true.
