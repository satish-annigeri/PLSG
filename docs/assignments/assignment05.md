# Assignment 5

#### Corresponds to: [Session 5](../sessions/session05.md)

### Quiz: Python List Comprehensions (5 Questions)

**1. What is the output of the list comprehension `[x*x for x in range(3)]`?**

A. [0, 1, 2]  
B. [1, 4, 9]  
C. [2, 4, 6]  
D. [0, 1, 4]

??? success "Answer"
    **Correct answer:** D  
    **Explanation:** `: `range(3)` gives 0, 1, 2 and squaring them yields 0, 1, 4.

**2. Which list comprehension correctly filters even numbers from a list `nums`?**

A. `[x for nums in x if x % 2 == 0]`  
B. `[x % 2 == 0 for x in nums]`  
C. `[x if x % 2 == 0 for x in nums]`  
D. `[x for x in nums if x % 2 == 0]`

??? success "Answer"
    **Correct answer:** D  
    **Explanation:** The correct syntax is `expression for item in iterable if condition`.

**3. What is the output of `[x if x > 0 else -x for x in [-2, 0, 3]]`?**  
A. [2, -0, -3]  
B. [-2, 0, 3]  
C. [2, 0, 3]  
D. [2, 0, -3]

??? success "Answer"
    **Correct answer:** C  
    **Explanation:** Negative numbers become positive; zero stays zero; positive stays positive.

**4. Which of the following is equivalent to the list comprehension `[x*2 for x in data if x > 5]`?**  
A. A loop that filters values less than 5  
B. A loop that doubles all values in data  
C. A loop that halves values greater than 5  
D. A loop that doubles only values greater than 5  

??? success "Answer"
    **Correct answer:** D  
    **Explanation:** The comprehension filters values > 5 and then multiplies them by 2.

**5. What is the output of `[x%3 if x%2==0 else x%5 for x in [2,3,4]]`?**  
A. [2, 3, 4]  
B. [2, 3, 4]  
C. [2, 3, 1]  
D. [2, 3, 1]

??? success "Answer"
    **Correct answer:** C  
    **Explanation:**  
    - 2 is even → 2 % 3 = 2  
    - 3 is odd → 3 % 5 = 3  
    - 4 is even → 4 % 3 = 1  

### Quiz: Python Unpacking Rules (5 Questions)

**1. What is the result of the assignment `a, b = [10, 20]`?**  
A. `a = 10, b = [20]`  
B. `a = 10, b = 20`  
C. `a = [10], b = 20`  
D. `a = [10, 20], b = []`  

??? success "Answer"
    **Answer:** B  
    **Explanation:** The number of variables on the left side is equal to the number of elements in the list on the right side. Therefore, the elements are unpacked sequentially into the corresponding variables on the left side.

**2. Which statement about starred expressions in unpacking is correct?**  
A. Starred targets are only allowed inside functions.  
B. You can use multiple starred targets if they unpack evenly.  
C. Only one starred target is allowed in an assignment.  
D. Starred targets can only appear at the end.  

??? success "Answer"
    **Answer:** C  
    **Explanation:** Multiple starred targets on the left side makes it impossible to decide how the unpacking is to be carried out, or there are a multitude of ways of unpacking possible with multiple starred targets on the left side.

**3. What is the value of `rest` after executing `x, *rest = (5, 6, 7, 8)`?**  
A. `(6, 7, 8)`  
B. `[6, 7, 8]`  
C. `[5, 6, 7]`  
D. `(5, 6, 7)`  

??? success "Answer"
    **Answer:** B  
    **Explanation:** The result of unpacking multiple elements into a starred target is a list, not a tuple. This makes it possible to alter the values if necessary.

**4. Which unpacking operation will raise a `ValueError`?**  
A. `a, b = (1, 2)`  
B. `a, *b = [1]`  
C. `a, b = [1, 2, 3]`  
D. `a, b, c = [1, 2, 3]`  

??? success "Answer"
    **Answer:** C  
    **Explanation:** When the tarhets on the left side cannot unpack all elements on the right side, an exception is raised.

**5. What does the expression `*a, b, c = range(5)` assign to `a`?**  
A. `(0, 1, 2, 3)`  
B. `(0, 1, 2)`  
C. `[0, 1, 2, 3]`  
D. `[0, 1, 2]`  

   **Answer:** D

### Quiz: Positional, Keyword, and Default Parameters in Python (10 questions)

**1. Which of the following is a valid function definition using default parameters?**  
A. `def f(a=1, b): pass`  
B. `def f(a, b=1): pass`  
C. `def f(a=1, b=2, c): pass`  
D. `def f(a, b, c=): pass`  
??? success "Answer"
    **Answer:** B  
    **Explanation:**  
    A. SyntaxError: parameter without a default follows parameter with a default.  
    B. Parameter with a default follows a parameter without a default.  
    C. SyntaxError: parameter without a default follows parameter with a default.  
    D. SyntaxError: expected default value expression. Parameter is followed by `=` but no default value is specified.  

**2. What happens when calling `func(10, c=30)` for the function `def func(a, b=20, c=40): ...`?**  
A. `a=10, b=20, c=40`  
B. `a=10, b=30, c=40`  
C. `a=10, b=20, c=30`  
D. Error: positional argument after keyword  
??? success "Answer"
    **Answer:** C

**3. Which call is invalid for the function `def f(x, y, z): ...`?**  
A. `f(1, 2, 3)`  
B. `f(x=1, y=2, z=3)`  
C. `f(1, y=2, 3)`  
D. `f(1, z=3, y=2)`  
??? success "Answer"
    **Answer:** C

**4. What is the correct order of parameters in a Python function definition?**  
A. keyword-only → positional → default  
B. positional → default → keyword-only  
C. default → positional → keyword-only  
D. positional → keyword-only → default  
??? success "Answer"
    **Answer:** B

**5. Given `def f(a, b=5, c=10): ...`, which call overrides only `c`?**  
A. `f(c=20)`  
B. `f(1, c=20)`  
C. `f(1, 2, 20)`  
D. Both B and C  
??? success "Answer"
    **Answer:** B

**6. What is the result of calling `g(1, y=2)` for `def g(x, y, z=3): ...`?**  
A. `x=1, y=2, z=3`  
B. `x=1, y=2, z=None`  
C. Error: missing positional argument  
D. Error: multiple values for y  
??? success "Answer"
    **Answer:** A

**7. Which statement about keyword arguments is true?**  
A. They must appear before positional arguments in a call.  
B. They can appear in any order as long as names match.  
C. They cannot be mixed with positional arguments.  
D. They must match the order of parameters.  
??? success "Answer"
    **Answer:** B

**8. What happens when calling `h(1, 2, x=3)` for `def h(x, y, z): ...`?**  
A. `x=1, y=2, z=3`  
B. Error: multiple values for x  
C. `x=3, y=2, z=None`  
D. Error: missing argument z  
??? success "Answer"
    **Answer:** B

**9. Which of the following defines a function with keyword‑only parameters?**  
A. `def f(a, b, c): ...`  
B. `def f(a, b, *, c): ...`  
C. `def f(*, a, b, c): ...`  
D. Both B and C  
??? success "Answer"
    **Answer:** D

**10. Given `def f(a, b=2, *, c=3): ...`, which call is valid?**  
A. `f(1, 2, 3)`  
B. `f(1, c=10)`  
C. `f(a=1, 2, c=10)`  
D. `f(1, b=2, 3)`  
??? success "Answer"
    **Answer:** B