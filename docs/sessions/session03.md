# Session 3: 21-03-2026 4:00 pm to 6:00 pm

## Agenda

1. Review of previous sessions
2. Answers to queries
3. Python has a dynamic type system
4. Some operations on `list`
5. Some operations on `str`
6. `range()` to generate a sequence of integers
7. Program flow control - `for` loop
8. Program flow control - `while` loop
9. Program flow control - `if - elif - else`
10. Function signatures
11. Designing functions

## Python has a dynamic type system

Programming languages can be classified as **statically typed** or **dynamically typed**.

- In a **statically typed** language, the data type of a variable must be specified when it is created and cannot change during program execution.
- In a **dynamically typed** language, the type of a variable is determined automatically and can change during execution.

Python is a **dynamically typed** language. You do not need to declare the type of a variable explicitly. Instead, the type is **inferred** from the value assigned to it. If a new value of a different type is assigned later, the variable’s type changes accordingly.

### Example
```pycon
>>> a = [10, 2.5, "Hello", 2 > 3]
>>> a
[10, 2.5, 'Hello', False]

>>> x = a[0]
>>> print(x, type(x))
10 <class 'int'>

>>> x = a[1]
>>> print(x, type(x))
2.5 <class 'float'>

>>> x = a[2]
>>> print(x, type(x))
Hello <class 'str'>
```

!!! note
    1. Data type of `x` is determined by the values assigned to it
    2. Data type of `x` is not static. It changes when the type of the value assigned to it is different.

Dynamic typing makes Python flexible and easy to use, since types do not need to be declared explicitly. However, in larger programs, it requires care to ensure that values have the expected types.

To address this, Python supports optional type annotations. These allow developers to specify expected types (especially for function parameters), helping editors and tools detect potential issues. However, the Python interpreter does not enforce type annotations at runtime.

## Some operations on `list`

A `list` in Python is:

- **Mutable** (its elements can be changed)
- A **container** (it can store multiple elements)

List elements:

- Can be of different types  
- Can include built-in or user-defined types  
- Can include other lists (nested lists)  

Unlike arrays in some languages, Python lists:

- Do not require elements to be of the same type  
- Do not require uniform structure (nested lists can vary in size)  

### Example: mixed data types
```pycon
>>> a = [10, 2.5, 'Hello, world', [1, 2.0]]
>>> len(a)
4

>>> type(a[0])
<class 'int'>
>>> type(a[1])
<class 'float'>
>>> type(a[2])
<class 'str'>
>>> type(a[3])
<class 'list'>

>>> len(a[3])
2
>>> type(a[3][0])
<class 'int'>
>>> type(a[3][1])
<class 'float'>
```

### Notes
1. Elements of `a` have different types  
2. `a[3]` is itself a list  
3. Nested elements can be accessed using indices (e.g., `a[3][0]`)  
4. Nested lists can be viewed as multi-dimensional, but they do not need to be uniform  

---

### Modifying list elements

Since lists are mutable, their elements can be changed:

```pycon
>>> a[0] = 20
>>> a
[20, 2.5, 'Hello, world', [1, 2.0]]

>>> a[3][0] = 10
>>> a
[20, 2.5, 'Hello, world', [10, 2.0]]
```

---

### Appending elements

```pycon
>>> a.append(50)
>>> a
[20, 2.5, 'Hello, world', [10, 2.0], 50]

>>> a.append((10, 20, 30))
>>> a
[20, 2.5, 'Hello, world', [10, 2.0], 50, (10, 20, 30)]
```

### Notes
1. `append()` adds an element to the end of the list  
2. The list can store values of any type, including tuples  

---

### Inserting elements

```pycon
>>> a.insert(1, 100)
>>> a
[20, 100, 2.5, 'Hello, world', [10, 2.0], 50, (10, 20, 30)]
```

### Behavior of `list.insert(i, element)`

- If `i = 0` → insert at the beginning  
- If `i = len(a)` → equivalent to `append()`  
- If `i > len(a)` → element is appended  
- If `i < 0` → position is adjusted using:
  ```
  i = max(0, len(a) + i)
  ```

---

### List methods

| Method | Description |
|:------|:------------|
| `list.pop([i])` | Remove and return element at index `i` (default: last element) |
| `list.clear()` | Remove all elements |
| `list.remove(x)` | Remove first occurrence of `x` |
| `list.count(x)` | Count occurrences of `x` |
| `list.index(x[, start[, end]])` | Return index of first occurrence of `x` |
| `list.sort(*, key=None, reverse=False)` | Sort list in place |
| `list.reverse()` | Reverse list in place |
| `list.copy()` | Return a shallow copy |

!!! note
    Square brackets in method signatures (e.g., `pop([i])`) indicate **optional arguments**, not literal syntax.

For more information, see:  
[More on lists](https://docs.python.org/3.10/tutorial/datastructures.html#more-on-lists)

---

### Examples: removing elements

```pycon
>>> a = [1, 2, 3, 4, 5]

>>> a.pop(0)
1
>>> a
[2, 3, 4, 5]

>>> a.pop()
5
>>> a
[2, 3, 4]

>>> a.pop(10)
IndexError: pop index out of range

>>> a.clear()
>>> a
[]
```

### Notes
1. `pop()` returns the removed value  
2. Invalid indices raise `IndexError`  

---

### More examples

```pycon
>>> a = [1, 2, 3, 4, 5, 4]

>>> a.remove(4)
>>> a
[1, 2, 3, 5, 4]

>>> a.append(5)
>>> a
[1, 2, 3, 5, 4, 5]

>>> a.count(2)
1
>>> a.count(5)
2

>>> a.index(5)
3
>>> a.index(5, 4)
5

>>> a.index(6)
ValueError: list.index(x): x not in list
```

### Notes
1. `remove()` deletes only the first occurrence  
2. `index()` raises `ValueError` if the element is not found  
3. The returned index is always relative to the full list  

---

### Sorting and copying

```pycon
>>> a = [10, 7, 2, 4, 6, 7]

>>> a.sort()
>>> a
[2, 4, 6, 7, 7, 10]

>>> a.reverse()
>>> a
[10, 7, 7, 6, 4, 2]

>>> x = [1, 2, 3]
>>> y = x
>>> z = x.copy()

>>> x is y
True
>>> x is z
False
```

### Notes
1. `sort()` modifies the list in place  
2. `reverse()` modifies the list in place  
3. `y = x` creates a reference to the same object  
4. `copy()` creates a new list with the same elements

## Some operations on `str`

A Python `str` provides many useful methods for processing text.

### Common string methods

| Method | Description |
|:------|:------------|
| `str.capitalize()` | Return a copy of the string with the first character capitalized and the rest lowercased |
| `str.casefold()` | Return a casefolded copy of the string (more aggressive than `lower()`, especially for non-English characters) |
| `str.center(width[, fillchar])` | Return the string centered in a field of given width, padded with `fillchar` (default: space) |
| `str.count(sub[, start[, end]])` | Return the number of non-overlapping occurrences of `sub` |
| `str.endswith(suffix[, start[, end]])` | Return `True` if the string ends with the specified suffix |
| `str.find(sub[, start[, end]])` | Return the lowest index where `sub` is found, or `-1` if not found |
| `str.lower()` | Return a lowercase copy of the string |
| `str.upper()` | Return an uppercase copy of the string |

For a complete list, see:  
[Text Sequence Type - `str`](https://docs.python.org/3.10/library/stdtypes.html#text-sequence-type-str)

---

### Examples

```pycon
>>> a = 'abracadabra'
>>> b = a.capitalize()
>>> b
'Abracadabra'

>>> c = b.upper()
>>> c
'ABRACADABRA'

>>> c.lower()
'abracadabra'

>>> a = "this is a sentence with several words"
>>> a.title()
'This Is A Sentence With Several Words'

>>> a.center(60)
'           this is a sentence with several words            '

>>> a.center(60, '-')
'-----------this is a sentence with several words------------'

>>> a.startswith('thi')
True

>>> a.endswith("words")
True

>>> a.replace(" ", "_")
'this_is_a_sentence_with_several_words'

>>> x = "  hello, world  "
>>> x.strip()
'hello, world'

>>> x.lstrip()
'hello, world  '

>>> x.rstrip()
'  hello, world'

>>> y = "This is just the beginning."
>>> y.rstrip(".")
'This is just the beginning'
```

---

### Joining strings

```pycon
>>> a = ["apple", "orange", "banana", "grapes"]

>>> " ".join(a)
'apple orange banana grapes'

>>> ", ".join(a)
'apple, orange, banana, grapes'
```

### Notes

- `join()` combines elements of an iterable into a single string  
- The string on which `join()` is called is used as the separator  

---

There are many more `str` methods, and they are very useful for text processing. Refer to the Python documentation for a complete list.

## `range()` to generate a sequence of integers

Let us explore `range()` using the Python REPL.

```pycon
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

The `range()` function returns an object of type `<class 'range'>`.

```pycon
>>> type(range(5))
<class 'range'>

>>> print(range(5))
range(0, 5)

>>> print(range(1, 10, 2))
range(1, 10, 2)

>>> r = range(1, 10, 2)
>>> print(r.start, r.stop, r.step)
1 10 2

>>> list(r)
[1, 3, 5, 7, 9]
```

### Notes

1. A `range` object has three attributes: `start`, `stop`, and `step`  
2. It generates values one at a time, rather than storing all values in memory  
3. You can convert it to a `list` or `tuple` to generate all values at once  
4. `range` is a *sequence type*, so it supports indexing and slicing  

---

### Examples

```pycon
>>> len(range(5))
5

>>> len(range(1, 10, 2))
5

>>> 3 in range(5)
True

>>> 4 in range(1, 10, 2)
False

>>> range(1, 6)[3]
4

>>> range(1, 6)[-1]
5
```

## Program flow control - `for` loop

The `for` loop iterates over elements of an *iterable*, such as a list, tuple, or string.

```pycon
>>> lst = ["one", "two", "three"]

>>> for item in lst:  # Pythonic
...     print(item)
...
one
two
three

>>> for i in range(len(lst)):  # Less Pythonic
...     print(lst[i])
...
one
two
three

>>> for i in range(len(lst)):
...     print(i)
...
0
1
2

>>> for i in range(1, 10, 2):
...     print(i, end=" ")
...
1 3 5 7 9 >>>

>>> for i in range(10, 1, -2):
...     print(i, end=", ")
...
10, 8, 6, 4, 2, >>>
```

### Handling conditions inside loops

```pycon
>>> a = [10, 20, 0, 5]

>>> for x in a:
...     print(100 / x)
...
10.0
5.0
Traceback (most recent call last):
  File "<python-input-91>", line 2, in <module>
    print(100 / x)
ZeroDivisionError: division by zero

>>> for x in a:
...     if x == 0:
...         continue
...     print(100 / x)
...
10.0
5.0
20.0
```

### Notes

- The `for` loop works directly with elements of an iterable  
- Using `for item in lst` is generally more readable than indexing with `range(len(lst))`  
- The `continue` statement skips the remaining part of the current iteration and proceeds to the next one  
- `continue` is typically used with a conditional statement


## Program flow control - `while` loop

The `while` loop repeatedly executes a block of code as long as a given condition evaluates to `True`. The loop stops when the condition becomes `False`.

A `while` loop has two important requirements:

1. Variables used in the condition must be initialized before the loop starts  
2. These variables must be updated inside the loop so that the condition eventually becomes `False`  

If these conditions are not met:

- The loop may never execute  
- The loop may run indefinitely (infinite loop)  

The block of code executed in each iteration is defined by indentation.

---

### Example

The following example simulates a `for i in range(5)` loop:

```pycon
>>> i = 0
>>> while i < 5:
...     print(i)
...     i += 1
...
0
1
2
3
4
```

Using a `while` loop in place of a `for` loop in such cases is generally less efficient and less readable. A `while` loop is more appropriate when:

- The number of iterations is not known in advance  
- The stopping condition is complex  

---

### Example: Iterative computation

```pycon
>>> maxiter = 10
>>> x = 5
>>> i = 0
>>> guess = x / 2

>>> while (abs(guess * guess - x) > 0.0001) and (i < maxiter):
...     guess = (guess + x / guess) / 2
...     i += 1
...
>>> print(i, guess)
3 2.2360679779158037
```

### Notes

- The loop continues while the condition  
  `abs(guess * guess - x) > 0.0001 and i < maxiter`  
  remains `True`  

- The number of iterations depends on:
  - the value of `x`  
  - the chosen tolerance (`0.0001`)  

- Variables initialized before the loop:
  - `maxiter = 10`  
  - `i = 0`  
  - `guess = x / 2`  

- The goal of the loop is to approximate the square root of `x`

## Program flow control - `if - elif - else`

Conditional branching in Python is performed using the `if - elif - else` construct.

- The `if` clause is required  
- The `elif` and `else` clauses are optional  

---

### Dual branching (`if - else`)

```pycon
>>> x = 0

>>> if x < 0:
...     print("Negative")
... else:
...     print("Non-negative")
...
Non-negative
```

---

### Notes

1. A colon (`:`) is required at the end of each `if`, `elif`, and `else` statement  
2. The condition can be a simple or complex logical expression  
3. Indentation is mandatory and must be consistent throughout the code  

---

### Multiple branching (`if - elif - else`)

```pycon
>>> x = 0

>>> if x < 0:
...     print("Negative")
... elif x > 0:
...     print("Positive")
... else:
...     print("Zero")
...
Zero
```

