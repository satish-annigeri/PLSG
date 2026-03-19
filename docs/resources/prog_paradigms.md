# Programming Paradigms

Here are some theoretical concepts to ponder before embarking on programming:

1. Purpose of programming computers
2. Principles of designing programs to run on computers
3. Program design paradigms


## Why program computers?
The primary reason for programming computers is to automate repetitive tasks, especially those that take a long time or are prone to human error — errors that occur not due to lack of knowledge but due to oversight, fatigue or monotony. Tasks that do not require human judgement are well suited for automation. However, deciding which tasks require human judgement is subjective.

Consider an example. One person may argue that calculating $A_{st}$ and $A_{sc}$ required to resist a bending moment $M_u$ does not require human judgement, as it is a straightforward mathematical calculation, whereas deciding how best to curtail reinforcement bars does require human judgement. Another person may argue that rebar curtailment can also be automated — it would simply require more logical cases to be handled. With the advent of machine learning, this may well be true. It is therefore best to make your own judgement on this matter based on how much computing effort you are willing to invest.

In any case, at the present time, engineers program computers to automate routine tasks that they consider worth the effort.

## Designing computer programs
The dictionary meaning of **design** closest to its use in engineering is "to devise for a specific function or end". The end result of design must be as close as possible to what was intended. In that sense, a computer program must also be subject to the process of **design**, so that it performs as planned.

Designing a computer program requires us to understand a few key facts:

1. Computer programs store information as data structures
2. Computer algorithms act on the data in those data structures to produce the intended results

The title of the well known book by Niklaus Wirth, published in 1976, is "[Algorithms + Data Structures = Programs](https://en.wikipedia.org/wiki/Algorithms_%2B_Data_Structures_%3D_Programs)". It reflects the fact that computer programs operate on data to produce results. The designer of a computer program must therefore focus on:

1. Choosing appropriate data structures (data types) to represent the information required to solve the problem
2. Choosing appropriate algorithms to arrive at the correct results from the input data

Data structures are needed to represent not just the input and output, but also intermediate results along the way.

Data structures are the data types available in the chosen programming language. Regardless of the programming language, data structures can be classified into three types:

1. **Built-in data types** are intrinsic to a programming language. Most programming languages provide built-in types to represent booleans, characters, strings, integers and real numbers.
2. **User defined data types** are created by the programmer to suit a particular need and may be composed of built-in or derived data types. The `struct` in **C** and `class` in **C++** and **Python** are examples of user defined types.
3. **Derived data types** are derived from either built-in or user defined data types. Arrays are an example — you can have an array of integers, real numbers or even of a user defined type, such as one representing information about a student.

## Program design paradigms
When designing a program, different approaches can be taken. These approaches are called programming paradigms. A programming paradigm is a relatively high-level way to conceptualise and structure the implementation of a computer program (see [Wikipedia](https://en.wikipedia.org/wiki/Programming_paradigm)). A programming language may support one or more paradigms.

While the discussion on programming paradigms can be quite involved, for the purpose of designing programs for structural engineering applications, the focus here will be kept to two paradigms:

1. Procedural paradigm
2. Object oriented paradigm

Both fall under the category of the **imperative** paradigm, but differ in the way they organise data and algorithms. Programming paradigms are useful both while designing programs and while implementing them in a programming language.

It is possible to design a program without choosing a specific programming language, as long as it supports the chosen paradigm. Implementation, however, requires a specific programming language to be chosen.


### Procedural Paradigm
This approach assumes that a given task can be subdivided into several simpler sub-tasks, each of which may be further divided into even simpler sub-sub-tasks. This subdivision can continue until a point is reached where further division is either not possible or not necessary.

Each task is typically implemented as a function in a programming language that supports the procedural paradigm. Most programming languages support this paradigm, as does Python.

The next step is to determine what data each function requires as input and what it produces as output. This is the data flow. Within each function is the algorithm that transforms the input into the required output.

Procedural design is a top-down process — moving from the whole to its parts — while implementation is a bottom-up process, moving from parts to the whole. Design requires knowing what the entire program is supposed to achieve before deciding what its individual components are and what each component will do.

Higher level components tend to be more complex and abstract, accomplishing several tasks, while lower level components are simpler and accomplish smaller tasks, sometimes just one. The definition of a single task is, of course, subjective.

Implementation begins with the simplest and most independent components (functions), which are tested before moving on to the higher level components that will use them.

In the procedural paradigm, the primary focus is on organising functions (algorithms). Data is considered as flowing into and out of functions until the required output is obtained.

<hr style="height:2px; background:black;">

<span style="color:red"><b>You can safely ignore the discussion on object oriented programming until we learn more about Python and OO programming in Python.</b></span>

<hr style="height:2px; background:black;">

### Object oriented paradigm (OO paradigm)
The primary focus in the OO paradigm is on organising data to represent information, with algorithms considered part of the data. Data is transformed from one state to the next by passing messages to the data objects in the correct sequence until the required output is reached.

There are several concepts to understand before a fuller description of this paradigm is possible. These will be covered at a later stage.

### Comparison of procedural and OO paradigms
Each paradigm has its advantages and disadvantages, and the choice should be made after studying the problem at hand. Here are some points that may help in making that decision:

1. In the OO paradigm, data specific to an object is bundled together as a single package along with all the procedures that act on it, making the relationship between data and procedures very clearly defined.
2. In the procedural paradigm, the task performed by each function is clearly defined and the call hierarchy — which function calls which, and which functions depend on the results of others — is explicit, with lower level functions being simpler and more independent and higher level functions being more complex and dependent.
3. In the procedural paradigm, it can require some effort to keep track of which data goes into a given function and what output it returns, especially as the program grows large.
4. Learning the concepts of the OO paradigm requires more effort compared to the procedural paradigm.
5. The effort required to design a procedural program is generally lower than designing with the OO paradigm.
6. The OO paradigm is often considered more capable when it comes to designing, implementing, testing and maintaining programs over time, but this is subjective and can be debated either way.

### Illustrative example
Consider the problem of calculating the stress-strain relation of concrete as per the limit state method of design in IS:456.

#### Step 1: Identify the data required to implement this program
From our knowledge of this topic we can identify the data required to solve this problem:

1. $f_{ck}$ the characteristic strength of concrete
2. $\epsilon_{cy}=0.002$ the yield strain of concrete
3. $\epsilon_{cu}=0.0035$ the ultimate strain of concrete

Input data is the given strain $\epsilon_c$ in concrete and the output is the corresponding stress $f_c$ in concrete. From our knowledge of the stress-strain relation for concrete we know that:

$$
\begin{align*}
f_c &=
\begin{cases}
  \frac{0.67 f_{ck}}{1.5} \left[ 2 \left( \frac{\epsilon_c}{\epsilon_{cy}} \right) - \left( \frac{\epsilon_c}{\epsilon_{cy}} \right)^2 \right] & 0 \leq \epsilon_c \leq \epsilon_{cy} \\
  \frac{0.67 f_{ck}}{1.5} & \epsilon_{cy} < \epsilon_c \leq \epsilon_{cu} \\
  0 & \epsilon_c < 0 \text{ or } \epsilon_c > \epsilon_{cu}
\end{cases}
\end{align*}
$$

#### Procedural paradigm
Let us design a function to compute the stress for a given value of strain. The signature of the function is:

1. Name of the function: `get_fc()`
2. Input required by the function: `e_c` the given strain
3. Output returned by the function: `f_c` the corresponding stress

The last part is to design the body of the function, which is the algorithm:
``` python
if e_c < 0 or e_c > e_cu:
    return None
elif e_c >= e_cy:
    return 0.67 * fck / 1.5
else:
    ec_ecy = e_c / e_cy
    return 0.67 * fck / 1.5 * (2 * ec_ecy - ec_ecy ** 2)
```

Here is the full script, including the global constants and the `main()` function to test `get_fc()`:
``` python
e_cy = 0.002   # Yield strain
e_cu = 0.0035  # Ultimate strain

def get_fc(e_c: float, fck: float) -> float:
    # Function returns the stress for a given strain e_c
    # Returns None for invalid values of e_c

    if e_c < 0 or e_c > e_cu:
        return None
    elif e_c >= e_cy:
        return 0.67 * fck / 1.5
    else:
        ec_ecy = e_c / e_cy
        return 0.67 * fck / 1.5 * (2 * ec_ecy - ec_ecy ** 2)


def main():
    # Test function
    fck = 20.0    # Characteristic strength

    # Tests
    print(get_fc(-0.001, fck))  # None
    print(get_fc(0.004, fck))   # None
    print(get_fc(0, fck))       # 0.0
    print(get_fc(0.001, fck))   # 6.7
    print(get_fc(0.002, fck))   # 8.933
    print(get_fc(0.003, fck))   # 8.933
    print(get_fc(0.0035, fck))  # 8.933

if __name__ == "__main__":
    main()
```

1. `main()` is the function that tests `get_fc()`
2. `main()` is called only when the script is run directly and not when it is imported as a module by another script

Here are the expected outputs for different inputs:

|  $\epsilon_c$   |   $f_c$    |
|---------------:|-----------:|
| -0.001         |  None      |
|  0.004         |  None      |
|  0.000         |  0.0       |
|  0.001         |  6.700     |
|  0.002         |  8.933     |
|  0.003         |  8.933     |
|  0.0035        |  8.933     |

#### Object oriented paradigm
Here are the steps in OO design:

1. First identify the **objects** in the program. In this problem, there is clearly one object — the concrete material.
2. Next identify its **attributes** — in plain English, its **properties**. The attributes are $\epsilon_{cy}$, $\epsilon_{cu}$ and $f_{ck}$.
3. Finally, identify the operations to be performed on this object. In this case, we wish to calculate the stress $f_c$ for a given strain $\epsilon_c$. This is a **method** in OO terminology — a function that belongs to the object. Because it is part of the object, it automatically has access to all its attributes without needing them to be passed in as arguments, as would be the case with a standalone function.

Without going into full detail at this stage, here is the implementation:
``` python
class Concrete:
    e_cy: float = 0.002
    e_cu: float = 0.0035

    def __init__(self, fck: float):
        self.fck = fck

    def fc(self, e_c: float) -> float:
        if e_c < 0 or e_c > self.e_cu:
            return None
        elif e_c >= self.e_cy:
            return 0.67 * self.fck / 1.5
        else:
            ec_ecy = e_c / self.e_cy
            return 0.67 * self.fck / 1.5 * (2 * ec_ecy - ec_ecy ** 2)

def main():
    m20 = Concrete(20.0)
    print(m20.fc(-0.001))
    print(m20.fc(0.004))
    print(m20.fc(0.0))
    print(m20.fc(0.001))
    print(m20.fc(0.002))
    print(m20.fc(0.003))
    print(m20.fc(0.0035))
```

Here are some points to note:

1. `#!python m20 = Concrete(20)` creates an object based on the `class Concrete` (a `class` is a **blueprint** for creating objects of a specific type — in this case, of type `Concrete`)
2. The object `m20` is initialised with `fck = 20.0`
3. The method `fc()` is part of the object `m20` and therefore cannot be called independently — it **must** be called on behalf of the object `m20`, as implied by the `.` separating `m20` and `fc()`
4. Because `fc()` is part of `m20`, it can access its attribute `fck` directly without it being passed as an argument. This is achieved through `self`, the first parameter of the method.
5. `self` is a special parameter that refers to the object on whose behalf the method is called.

This concept can be illustrated clearly with the following lines of code:
``` python
def main():
    m20 = Concrete(20.0)
    m30 = Concrete(30.0)
    print(m20.fc(0.001))  # 6.7
    print(m30.fc(0.001))  # 10.05
```

1. `m20` is an object of type `Concrete` with `fck = 20.0`
2. `m30` is an object of type `Concrete` with `fck = 30.0`
3. On the line `m20.fc(0.001)`, the method `fc()` belongs to the object `m20`, and therefore `self` on this line refers to `m20`
4. On the line `m30.fc(0.001)`, the method `fc()` belongs to the object `m30`, and therefore `self` on this line refers to `m30`