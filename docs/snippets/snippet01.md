# Functions as Arguments

Just as `int`, `float`, or `list` objects can be passed as arguments to a function, functions themselves can be passed as arguments. This is possible because, in Python, functions are **first-class objects**.

When passing a function as an argument, a challenge arises: how does the receiving function know which arguments to pass to the function it just received? If all functions passed to the receiver share the same **signature** (the same number and types of parameters), the solution is trivial: the receiver simply accepts those parameters and passes them along.

### Example 1: Functions with Identical Signatures

In this example, `evalfunc` is a higher-order function that accepts any function `f`, provided `f` accepts four specific arguments.

```python
from typing import Callable

def f1(x: float, a: float, b: float, c: float) -> float:
    print(f"f1 inputs: {x}, {a}, {b}, {c}")
    return a * x**2 + b * x + c

def f2(x: float, a: float, b: float, c: float) -> float:
    print(f"f2 inputs: {x}, {a}, {b}, {c}")
    return a * x + b - c

def evalfunc(f: Callable[[float, float, float, float], float], x: float, a: float, b: float, c: float) -> float:
    """Executes function 'f' with the provided arguments."""
    return f(x, a, b, c)

print("f1 result:", evalfunc(f1, 1, 2, 3, 4))
print("f2 result:", evalfunc(f2, 1, 2, 3, 4))
```

**Output:**
```text
f1 inputs: 1, 2, 3, 4
f1 result: 9
f2 inputs: 1, 2, 3, 4
f2 result: 1
```

!!! note
    In the `typing` module, `Callable` is used to hint that an object can be called like a function.

---

### Handling Variable Signatures with `*args` and `**kwargs`

The previous approach fails if the functions being passed have different numbers of arguments or different parameter names. To make a higher-order function truly generic, we use **argument unpacking** with `*args` (positional arguments) and `**kwargs` (keyword arguments).

### Example 2: A Generic Wrapper

Here, `evalfunc2` is designed to be agnostic of the signature of the function it receives.

```python
from typing import Callable, Any

def f3(x: float, a: float, b: float, c: float) -> float:
    print(f"f3 inputs: {x}, {a}, {b}, {c}")
    return a * x**2 + b * x + c

def f4(x: float, a0: float, a1: float) -> float:
    print(f"f4 inputs: {x}, {a0}, {a1}")
    return a0 * x + a1

def evalfunc2(f: Callable[..., Any], x: float, *args, **kwargs) -> Any:
    """A generic wrapper that passes 'x' followed by any other arguments."""
    print(f"Wrapper received: x={x}, args={args}, kwargs={kwargs}")
    return f(x, *args, **kwargs)

print("f3 call:")
print("Result:", evalfunc2(f3, 1, 2, 3, 4))

print("\nf4 call:")
print("Result:", evalfunc2(f4, 1, 2, 3))
```

**Output:**
```text
f3 call:
Wrapper received: x=1, args=(2, 3, 4), kwargs={}
f3 inputs: 1, 2, 3, 4
Result: 9

f4 call:
Wrapper received: x=1, args=(2, 3), kwargs={}
f4 inputs: 1, 2, 3
Result: 5
```

### Key Takeaways

1.  **Flexibility:** Using `*args` allows `evalfunc2` to accept any number of positional arguments, making it compatible with functions like `f3` and `f4` regardless of their parameter count.
2.  **Decoupling:** By using `*args` and `**kwargs`, the wrapper function is "decoupled" from the specific requirements of the function being passed. It doesn't need to know the internal structure of `f` to execute it.
3.  **Robustness:** This pattern allows for the creation of decorators and middleware that can wrap any function, regardless of its complexity or signature.