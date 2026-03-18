# Assignment 3

#### Corresponds to: [Session 3](../sessions/session03.md)

## Quiz

### Instructions
Choose the correct option for each question.

---

1. What will be the type of `x` after execution?

```python
x = 10
x = "hello"
```

A. `int`  
B. `str`  
C. `float`  
D. Error  

---

2. Which of the following statements about Python lists is **true**?

A. Lists are immutable  
B. Lists can contain elements of different data types  
C. Lists cannot contain other lists  
D. Lists have fixed size  

---

3. What will be the output?

```python
a = [1, 2, 3]
a.append([4, 5])
print(len(a))
```

A. 3  
B. 4  
C. 5  
D. Error  

---

4. What does `range(2, 10, 3)` generate?

A. 2, 5, 8  
B. 2, 5, 8, 11  
C. 3, 6, 9  
D. 2, 3, 4, 5  

---

5. What will be the output?

```python
for i in range(3):
    print(i, end=" ")
```

A. 1 2 3  
B. 0 1 2  
C. 0 1 2 3  
D. Error  

---

6. Which statement about `while` loops is correct?

A. They always execute at least once  
B. They execute only a fixed number of times  
C. They execute while a condition is `True`  
D. They cannot be nested  

---

7. What will happen when the following code is executed?

```python
a = [10, 0, 5]
for x in a:
    print(10 / x)
```

A. Prints all values successfully  
B. Raises `TypeError`  
C. Raises `ZeroDivisionError`  
D. Infinite loop  

---

8. What is the purpose of the `continue` statement?

A. Exit the loop completely  
B. Skip the current iteration and continue with the next  
C. Restart the loop  
D. Pause execution  

---

9. What will be the output?

```python
x = "abc"
print(x.center(5, "-"))
```

A. `--abc`  
B. `abc--`  
C. `-abc-`  
D. `abc`  

---

10. Which of the following is a valid function definition?

A.
```python
def func:
    pass
```

B.
```python
def func():
    pass
```

C.
```python
function func():
    pass
```

D.
```python
def func[]
    pass
```

---

11. What will be the output?

```python
def f(a):
    return a, a * 2

x = f(3)
print(type(x))
```

A. `<class 'int'>`  
B. `<class 'list'>`  
C. `<class 'tuple'>`  
D. Error  

---

12. Which statement about function parameters is correct?

A. Parameter names must match argument names  
B. Parameters must always have type annotations  
C. Parameters act as placeholders for arguments  
D. Functions must have at least one parameter  

---

13. What will be the output?

```python
a = [1, 2, 3]
b = a
a[0] = 10
print(b)
```

A. `[1, 2, 3]`  
B. `[10, 2, 3]`  
C. Error  
D. `[10]`  

---

14. Which of the following is **not** a sequence type?

A. `list`  
B. `tuple`  
C. `range`  
D. `set`  

---

15. What is the output?

```python
print(3 in range(1, 5))
```

A. `True`  
B. `False`  
C. Error  
D. None  