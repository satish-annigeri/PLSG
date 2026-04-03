# Assignment 4

#### Corresponds to: [Session 4](../sessions/session04.md)

## Quiz: Python f-String Formatting (5 Questions)

Below are five multiple‑choice questions covering f‑string formatting for integers, floats, and strings.

**1. Which f‑string correctly formats an integer variable `count` inside a message?**

A. `f"Count: {count:d}"`  
B. `f"Count: {count:f}"`  
C. `f"Count: {count:s}"`  
D. `f"Count: {count:2f}"`  

??? success "Answer"
    **Correct answer:** A  
    **Explanation:** `:d` is the correct integer format specifier.

**2. Which f‑string prints a float `value` with exactly two decimal places?**  
A. `f"{value:.02}"`  
B. `f"{value:2f}"`  
C. `f"{value:.2f}"`  
D. `f"{value:0.2}"`  

??? success "Answer"
    **Correct answer:** C  
    **Explanation:** `:.2f` formats a float to two decimal places.

**3. Given `name = "Alice"`, which f‑string correctly embeds the string?**  
A. `f"User: {name:s}"`  
B. `f"User: {name}"`  
C. `f"User: {name:str}"`  
D. `f"User: {name:txt}"`  

??? success "Answer"
    **Correct answer:** B  
    **Explanation:** Strings can be inserted directly without a format specifier.

**4. Which f‑string right‑aligns an integer `n` in a field of width 5?**  
A. `f"{n:>5d}"`  
B. `f"{n:<5d}"`  
C. `f"{n:^5d}"`  
D. `f"{n:5>}"`  

??? success "Answer"
    **Correct answer:** A  
    **Explanation:** `>5d` means right‑aligned integer in a field of width 5.

**5. Which f‑string formats a float `pi` in a field of width 8 with 3 digits after the decimal?**  
A. `f"{pi:8.3}"`  
B. `f"{pi:8.3f}"`  
C. `f"{pi:.3f8}"`  
D. `f"{pi:3.8f}"`  

??? success "Answer"
    **Correct answer:** B  
    **Explanation:** `8.3f` means width 8, precision 3, float formatting.


## Quiz: Python Functions (10 Questions)

Below are ten multiple‑choice questions covering function signatures, parameters vs. arguments, calling conventions, and type annotations.

**1. What is the correct way to define a function in Python that takes two parameters, x and y?**  
A. `function my_func(x, y):`  
B. `def my_func(x, y):`  
C. `define my_func(x, y):`  
D. `func my_func(x, y):`  

??? success "Answer"
    **Correct answer:** B  
    **Explanation:** Python uses the keyword `def` to define a function.

**2. Which term refers to the values passed into a function when it is called?**  
A. Signatures  
B. Annotations  
C. Arguments  
D. Parameters  

??? success "Answer"
    **Correct answer:** C  
    **Explanation:** Arguments are the actual values supplied during a function call.

**3. What does the following function signature indicate? `def scale(value: float) -> float:`**  
A. The function takes any type and returns any type  
B. The function takes a float and returns a float  
C. The function must return an integer  
D. The function takes no parameters  

??? success "Answer"
    **Correct answer:** B  
    **Explanation:** The annotation indicates a float input and a float return value.

**4. Given the function `def add(a, b): return a + b`, which call correctly matches the parameters?**  
A. `add(a=3)`  
B. `add(3, 4, 5)`  
C. `add()`  
D. `add(3, 4)`  

??? success "Answer"
    **Correct answer:** D  
    **Explanation:** The function expects exactly two arguments.

**5. What is the purpose of a function signature?**  
A. To describe the function name, parameters, and return type  
B. To automatically generate documentation  
C. To specify the indentation level of the function  
D. To list all variables used inside the function  

??? success "Answer"
    **Correct answer:** A  
    **Explanation:** A function signature defines how the function should be called.

**6. Which of the following is a valid Python function signature with type annotations for two integer inputs and a float return value?**  
A. `def compute(int a, int b): float`  
B. `def compute(a: int, b: int) -> float:`  
C. `compute def(a: int, b: int) -> float:`  
D. `function compute(int a, int b): float`  

??? success "Answer"
    **Correct answer:** B  
    **Explanation:** Python uses `def` and the `name: type -> return_type` annotation style.

**7. What happens if you call a function with fewer arguments than the number of parameters it defines (and no defaults exist)?**  
A. Python automatically fills missing values with zero  
B. The function runs but missing parameters become `None`  
C. Python converts the function into a lambda  
D. A `TypeError` is raised  

??? success "Answer"
    **Correct answer:** D  
    **Explanation:** Python requires all parameters to be supplied unless

**8. Which statement correctly describes parameters in a function definition?**  
A. They are the values passed during a function call  
B. They must always be integers  
C. They must always include type annotations  
D. They are placeholders listed in the function definition  

??? success "Answer"
    **Correct answer:** D  
    **Explanation:** Parameters are the named placeholders inside the function signature.

**9. Given the function `def area(length: float, width: float) -> float:`, which call is valid?**  
A. `area(length=5.0, 3.0)`  
B. `area(length=5.0, width=3.0, unit="m")`  
C. `area()`  
D. `area(5.0, width=3.0)`  

??? success "Answer"
    **Correct answer:** D  
    **Explanation:** Positional arguments may come first, followed by keyword arguments.

**10. What does the return type annotation in a function signature represent?**  
A. The type of the function name  
B. The type of all intermediate variables  
C. The type the function is expected to return  
D. The type of the last parameter  

??? success "Answer"
    **Correct answer:** C  
    **Explanation:** The annotation after `->` indicates the expected return type.

## Designing, Developing, and Testing Python Functions — Applied Engineering Problems

Below are three application‑driven problems requiring you to design Python functions. Each problem includes a unit‑test template to guide verification. When run, these test functions must pass the test.

------
**Note:** These exercises require you to write `pytest` test files and install and run `pytest`. For these details see [Unit-testing using `pytest`](../sessions/session04.md#unit-testing-using-pytest) section of Session 4.

------

**1. Beam Deflection Under a Point Load (Mechanics of Materials)**  
A simply supported beam of length $L$ carries a point load $P$ at mid‑span.  
The maximum deflection is:

$$
\delta_{\max} = \frac{P L^3}{48 E I}
$$

**Task:**  
Design a Python function with appropriate parameters and type annotations that computes the maximum deflection.  
The function must:

- Accept $P$, $L$, $E$, and $I$  
- Validate that all inputs are positive  
- Return the deflection as a float  

**Unit‑test template:**
```python
import pytest

def test_deflection_realistic():
    # Example: P=500 N, L=2 m, E=200e9 Pa, I=8e-6 m^4
    from beam import max_deflection
    result = max_deflection(500, 2.0, 200e9, 8e-6)
    assert result > 0
    assert pytest.approx(result, rel=1e-6) == result  # sanity check

def test_deflection_invalid_input():
    from beam import max_deflection
    with pytest.raises(ValueError):
        max_deflection(-10, 2.0, 200e9, 8e-6)
```

??? success "Answer"

    ```python title="File: beam.py"
    def max_deflection(P: float, L: float, E: float, I: float) -> float:
    """
    Returns maximum deflection due to a point load P applied at mid-span.

    Parameters
    ----------
    P : float
        Point load applied at mid-span in N.
    L : float
        Span in m.
    E : float
        Modulus of elasticity of material in N / m^2.
    I : float
        Second-moment of area of cross section about neutral axis, in m^4.

    Raises
    ------
    ValueError
        Each of P, L, E and I must be greater than or equal to zero.

    Returns
    -------
    float
        Maximum deflection in m, at mid-span due to a point load P applied at midspan.

    """
    if (P < 0) or (L < 0) or (E < 0) or (I < 0):
        raise ValueError(f"All {P=}, {L=}, {E=}, {I=} must be non-negative")
    return (P * L**3) / (E * I)
    ```

    Run `pytest` under `uv`

    ```doscon
    > uv run -- pytest test_beam.py
    ```
    or `.venv`
    ```doscon
    (.venv) > pytest test_beam.py
    ```

    Verify that all tests pass.
    ```doscon
    ============================= test session starts ==============================
    platform linux -- Python 3.13.9, pytest-9.0.2, pluggy-1.6.0
    rootdir: /home/satish/python/sci
    configfile: pyproject.toml
    plugins: anyio-4.12.1
    collected 2 items                                                              

    test_beam.py ..                                                          [100%]

    ============================== 2 passed in 0.03s ===============================
    ```

**2. Resultant of Two Forces (Engineering Mechanics)**


Two forces $F_1$ and $F_2$ act at an angle $\theta$. The magnitude of the resultant is:
$$R = F_1^2 + F_2^2 + 2 \cdot F_1 F_2 \cos ⁡\theta$$

**Task:**

Write a function that:

- Accepts $F_1$, $F_2$, and $\theta$ (in degrees)
- Converts $\theta$ from degrees to radians internally
- Computes and returns the resultant force $R$ as a float
- Raises ValueError if any force is negative

**Unit-test template**

```python
import pytest

def test_resultant_zero_angle():
    from forces import resultant
    assert resultant(10.0, 20.0, 0.0) == pytest.approx(30.0)

def test_resultant_opposite_direction():
    from forces import resultant
    assert resultant(20.0, 10.0, 180.0) == pytest.approx(10.0)

def test_resultant_one_force_zero():
    from forces import resultant
    assert resultant(0.0, 15.0, 45.0) == pytest.approx(15.0)

def test_resultant_negative_force_raises():
    from forces import resultant
    with pytest.raises(ValueError):
        resultant(-5.0, 10.0, 30.0)
```


??? success "Answer"

    ```python title="File: forces.py"
    import math


    radians = math.radians


    def resultant(F1: float, F2: float, theta: float) -> float:
    """
    Returns the resultant of two forces F1 and F2 acting at an angle theta (degrees)

    Parameters
    ----------
    F1 : float
        Magnitude of F1 in same the units as that of F2.
    F2 : float
        Magnitude of F2 in the same units as that of F1.
    theta : float
        Angle measured from F1 to F2 in degrees, positive when measured counter-clockwise.

    Raises
    ------
    ValueError
        Both F1 and F2 must not be negative.

    Returns
    -------
    float
        Magnitude of resultant of F1 and F2.

    """
    if (F1 < 0) or (F2 < 0):
        raise ValueError(f"Both {F1=} and {F2=} must be non-negative")
    if (theta < 0) or (theta > 180):
        raise ValueError(f"Angle {theta=} must be between 0 and 180 degrees")
    return math.sqrt(F1 ** 2 + F2 ** 2 + 2 * F1 * F2 * math.cos(radians(theta)))
    ```

    Run `pytest` under `uv`

    ```doscon
    > uv run -- pytest test_forces.py
    ```
    or `.venv`
    ```doscon
    (.venv) > pytest test_forces.py
    ```

    Verify that all tests pass.
    ```doscon
    ============================= test session starts ==============================
    platform linux -- Python 3.13.9, pytest-9.0.2, pluggy-1.6.0
    rootdir: /home/satish/python/sci
    configfile: pyproject.toml
    plugins: anyio-4.12.1
    collected 4 items                                                              

    test_forces.py ....                                                      [100%]

    ============================== 4 passed in 0.03s ===============================
    ```

**Suggestion 1**

The angle in radians from the first force $F_1$ to the resultant is given by:

$$
\alpha = \tan^{-1} \left( \frac{F_2 \sin \theta}{F_1 + F_2 \cos \theta} \right)
$$

where $\theta$ is the angle in radians measured from $F_1$ to $F_2$. Modify the function to return both the magnitude of the resultant and its direction in terms of the angle, in degrees, measured from $F_`$.

**Suggestion 2**

The better approach to calculate the resultant, especially when the number of forces is more than two, is to resolve the forces into components along orthogonal directions, summing the components and combining them into a resultant.

**3. Soil Grading Check (Basic Geotechnical Concepts)**

A soil sample is classified as well‑graded sand if:

$$
C_u = \frac{D_{60}}{D_{10}}, \qquad C_c = \frac{(D_{30})^2}{D_{10} D_{60}}
$$

Criteria for well‑graded sand:

- $C_u > 6$
- $1 < C_c < 3$

**Task**

Design a function that:

- Accepts the diameters $D_{10}$, $D_{30}$, and $D_{60}$
- Computes $C_u$ and $C_c$
- Returns a boolean indicating whether the soil is well‑graded
- Raises ValueError if any diameter is non‑positive

**Unit-test template**

```python
import pytest

def test_well_graded_sample():
    from soil import is_well_graded
    assert is_well_graded(0.1, 0.3, 0.8) is True

def test_poorly_graded_sample():
    from soil import is_well_graded
    assert is_well_graded(0.2, 0.25, 0.3) is False

def test_invalid_input_raises():
    from soil import is_well_graded
    with pytest.raises(ValueError):
        is_well_graded(0.0, 0.3, 0.8)
    with pytest.raises(ValueError):
        is_well_graded(-0.1, 0.3, 0.8)
```

??? success "Answer"

    ```python title="File: soil.py"
    def is_well_graded(d10: float, d30: float, d60: float) -> bool:
    """
    Returns True if the soil is well graded, False otherwise.

    Parameters
    ----------
    d10 : float
        Diameter D10.
    d30 : float
        Diameter D30.
    d60 : float
        Diameter D60.

    Raises
    ------
    ValueError
        Each of D10, D30 and D60 must be greater than zero.

    Returns
    -------
    bool
        True if soil is well-graded.

    """
    if (d10 <= 0) or (d30 <= 0) or (d60 <= 0):
        raise ValueError(f"Each of D10={d10}, D30={d30} and D60={d60} must be non-negative")
    Cu = d60 / d10
    Cc = d30 ** 2 / (d10 * d60)
    return (Cu > 6) and (1 < Cc < 3)
    ```

    Run `pytest` under `uv`

    ```doscon
    > uv run -- pytest test_forces.py
    ```
    or `.venv`
    ```doscon
    (.venv) > pytest test_forces.py
    ```

    Verify that all tests pass.
    ```doscon
    ============================= test session starts ==============================
    platform linux -- Python 3.13.9, pytest-9.0.2, pluggy-1.6.0
    rootdir: /home/satish/python/sci
    configfile: pyproject.toml
    plugins: anyio-4.12.1
    collected 3 items                                                              

    test_soil.py ...                                                         [100%]

    ============================== 3 passed in 0.03s ===============================
    ```
