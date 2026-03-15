# Assignment 1

#### Corresponds to: [Session 1](../sessions/session01.md)

#### Answers: [Answer 1](answer01.md)

## Questions

1. What does **REPL** stand for? Can you name other programming languages/environments that offer a REPL?
2. Having assigned the value `10` to the object `a`, what are the two ways to display the value of the object `a`?
3. Given the list `#!python a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]`
    1. Determine the number of elements in the list
    2. Use negative indexing operation to obtain the **last but one element** of the list (in this example, the element with value `9`).
    3. What are the slice `start`, `stop` and `step` values to produce the list [9, 6, 3]. Remember the slice notation `#!python a[start:stop:step]`.
 4. You can create an empty `list` with `#!python a = []`. Creating an empty `tuple` is similar `#!python b = ()`. But how do you create a `tuple` with exactly one element? Does `#!python b = (10)` work? Why not? What is the correct way to create a tuple with exactly one element. Search the net for the answer.
 5. The `set` data structure is a container, similar to `list` and `tuple`, but its elements are not indexed. Further, its elements are unique, there can only be one occurrence of an element in a set. Search for the official Python documentation for `set` and find the operations that can be performed on it. Can you add a new element? Can you remove an existing element? Can you check if a certain value is present in a `set`? Can you find the intersection of two sets? Are there other operations that can be performed?

## Answer True or False

1. The REPL manages its own memory to store the objects created by you, as well as the modules and packages imported by you
2. In a REPL, you can display the value of an object without having to use the `print()` function whereas it is necessary to use the `print()` function to display the value of an object in a script (code written in a file and executed from the terminal).
3. Data type `str` is immutable.
4. Immutable means the value assigned to the object cannot be changed once assigned.
5. Immutability only prevents replacing an element with a new value, but does not stop you from assigning an entirely new value to the object. That is, `#!python a = (1, 2, 3); a[0] = 10` is not permitted, but `#!python a = (1, 2, 3); a = (10, 20, 30)` is permitted.
6. Data type `list` is immutable.
7. You can embed an apostrophe (`'`) inside a string constant delimited by apostrophes, provided it is escaped using the backslash `\'`. That is, this is a valid string: `'This isn\'t difficult'`.
8. When you carry out an index or slice operation on a list, tuple or a string, the operation returns a **new object** with the values copied from the original object.
9. Create a `dict` object to represent the name. age and phone number of a person.
    1. Obtain the **keys** and **values** of the object.
    2. Obtain the value for the name of the person
    3. Increase the age of the person by 1 year
10. When you assign a previously created list to a new object, the new object is an exact copy of the values of the original list, and not the same values as the original list. Another way to ask the same question is, `#!python a = [1, 2, 3]; b = a; a is b` returns False. **Note:** This topic has not been discussed in any of the previous sessions. But I encourage you to try out the following lines of code in the REPL to find the answer. More importanly, can you explain what is happening?
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
