# Session 2: Planned Date 2026-03-14 Saturday
#### From 4:00 pm to 6:00 pm
## Agenda

1. Review of previous session
2. Answers to queries asked in person or sent in advance
3. VS Code IDE, its features and use
    * User interface: Main menu,Toolbar, Primary Side Bar, Secondary Side Bar, Panel, Status Bar
    * File explorer, Extensions, Settings, Source Control
    * Installing Microsoft Python extension
4. Writing Python code in VS Code and executing code in a file
5. Purpose of programming computers
6. Principles of designing programs to run on computers
7. Program design paradigms


## Why program computers?
The primary reason of programming computers is to automate repetitive tasks, especially those that take a long time and may contain human errors, errors that occur not because of lack of knowledge but due to oversight, fatigue or monotony. Tasks that do not requirement human judgement are well suited for automation. However, deciding which tasks require human judgement is subjective.

Consider an example. One person may opine that calculating $A_{st}$ and $A_{sc}$ required to resist a bending moment $M_u$, does not require human judgement as it is a straight forward mathematical calculation, whereas deciding the best way to curtail reinforcement bars requires human judgement and it is not a straight forward mathematical task. But another person may opine that rebar curtailment can also be automated, just that it will require more logical cases to be attempted. With the advent of ML, it may well be true. So it is better to take your own decision on this matter based on how much computing effort you wish to put in.

In any case, at the present time, engineers program computers to automate routine tasks that they consider are worth the effort.

## Designing computer programs
The dictionary meaning closest to the word **design** as used by an engineer is "to devise for a specific function or end". The end result of design must be as close as possible to what we had in mind. In that sense, a computer program must also be suject to the process of **design**, so that it performs as we planned it should.

Designing a computer program requires us to understand a few facts:

1. Computer programs have information stored as data structures
2. Computer algorithms act on the data in the data structures to produce intended results

The title of the well known book by Niklaus Wirth, published in 1976 is "[Algorithms + Data Strucures = Programs](https://en.wikipedia.org/wiki/Algorithms_%2B_Data_Structures_%3D_Programs)". It reflects on the fact that computer programs operate on data to produce results. The designer of a computer program must therefore focus attention on:

1. Choosing appropriate data strucutures (data types) to represent the information required to solve the problem
2. Choosing the appropriate procedures (algorithms) to arrive at the correct results starting from the input data

Data structures are required to represent not just the input and the output, but also the intermediate results while moving from input to output.

Data structures are the data types available in a chosen programming language. Irrespective of the programming language, data structures can be classified into three types:

1. **Built-in data types** are intrinsic to a programming language. Most programming languages provide built-in data types to represent boolean, character, string, integer and real numbers.
2. **User defined data types** are created by the programmer to suit a particular information and may consist of any of the built-in data types or the derived data types that will be explained next. The `struct` in **C**, `class` in **C++**, **Python** are examples of user defined types.
3. **Derived data types** are derived from wither built-in or user define data types. Arrays are an example of derived data type. You can have an array of integers, real numbers or even of a user-defined type to represent the information about, say, a student.

## Program design paradigms
When going about designing a program, one can consider different approaches, called programming paradigms. A programming paradigm is a relatively high-level way to conceptualize and structure the implementation of a computer program (See [Wikipedia](https://en.wikipedia.org/wiki/Programming_paradigm)). A programming language may support one or more paradigms.

While the discussion on programming paradigms can be quite involved, for the purpose of designing programs for structural engineering applications, I will keep the list very short:

1. Procedural paradigm
2. Object oriented paradigm

Both the above paradigms fall under the category of **imperative** paradigm, but differ in the way they organise data and algorithms within the program. Programming paradigms are useful both while designing programs and while implementing them using a programming language.

It is possible to design a program without choosing a specific programming language as long as it supports the chosen paradigm. But implementation requires that a specific proramming language be chosen.


### Procedural Paradigm
This approach to designing programs assumes that a given task can be sub-divided into several simpler tasks, and each sub-task may further be divided into more simpler sub-sub-tasks and this sub-division can be continued several more times until you reach a stage when it is not possible to divide a task further or it is simple enough that there is no need to do so.

Typically each task is implemented as a function in a programming language that supports the procedural paradigm. Most programming languages support this paradigm, as does Python.

The next task is to figure out what data is required by each function as input and what data it generates as output. This is the data flow. Within each function is the algorithm that transforms the input into the required output.

Procedural design is a top-down process (going from whole to part) while implementation is a bottom up (part to whole) process. Design requires you to know what the entire program is supposed to achieve before deciding what its individual components are and what each component will achieve.

Typically, higher level components are more complex and abstract as they accomplish several tasks whereas lower level components are simpler and accomplish smaller tasks, sometimes a single task. But remember, the definition of a single task is subjective. One person may say that the component that designs one section in a beam is a single task while another may say that a comonent that designs all sections in a beam is a single task and yet another may say designing all members in a structure is a single task.

Implementation starts with the simplest and the most independent components (functions) of the program and test them before you proceed to implement the higher level components that will use the implemented and tested lower level components.

In the procedural paradigm, the primary focus is on organizing functions (algorithms) and data is considered as flowing into and out of functions until the required output is obtained.

### Object oriented paradigm (OO paradigm)
The primary focus in OO paradigm is on organizing the data to represent the information and algorithms are considered part of the data. Data is transformed from one state to the next by passing messages to the data objects in the correct sequence until the required output is reached.

There are several concepts to be understood before a better description of this paradigm is possible and we will do that at a later point of time.

### Comparison of procedural and OO paradigms
Each paradigm has its advantages and disadvantages and a choice must be made only after studying the problem being solved. Here are some point sthat may help in making that decision:

1. In the OO paradigm, data specific to an object is bundled together as a single package and all the procedures that act on the data within the object are bundled together with that object so that the inter-relationship between the procedures and the data that act on is very clearly defined.
2. In the procedural paradigm, the task performed by each function is clearly defined and which function calls which other function as well as the functions that depend on a given function results in a heirarchy of functions, with the lower level functions being simpler and more independent and higher level functions being complex and highly dependent
3. In the procedural paradigm, it requires some effort to remember which data goes into a given funtion and which output is returned, especially when the program grows quite large
4. Learning the concepts of OO paradigm requires some effort compared to procedural paradigm
5. Effort required to design a procedural program is low compared to designing using OO paradigm
6. OO paradigm is supposed to be more capable when designing, implementing, testing and maintainin (making modifications at a later point of time) compared to the procedural paradigm, but this statement is subjective and can be debated either way

### Illustrative example
Consider the problem of calculating the stress-strain relation of concrete as per the limit state method of design in IS:456.

#### Step 1: Identify the data required to implement this program
From our knowledge of this topic we can identify the data required to solve this problem:

1. $f_{ck}$ the characteristic strength of concrete
2. $\epsilon_{cy}=0.002$ the yield strain of concrete
3. $\epsilon_{cu}=0.0035$ the ultimate strain of concrete

Input data is the given strain $\epsilon_c$ in concrete and the output is the corresponding stress $f_c$ in concrete. From our knowledge of the stress-strain relation for concrete we know that

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
Let us design a function to compute the stress for a given value of strain. Then this is the signature of the function:

1. Name of the function: `get_fc()`
2. Input required by the function: `e_c` the given strain
3. Output returned by the function: `f_c` the corresponding stress

The last part is to design the body of the function, which is the algorithm.

``` python
if e_c < 0 or e_c > e_cu:
    return None
elif e_c >= e_cy:
    return 0.67 * fck / 1.5
else:
    ec_ecy = e_c / e_cy
    return 0.67 * fck / 1.5 * (2 * ec_ecy - ec_ecy ** 2)
```

So here is the full script including the `main()` function to test the `get_fc()` function:
``` python
def get_fc(e_c: float, f_ck: float) -> float:
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
    e_cy = 0.002   # Yield strain
    e_cu = 0.0035  # Ultimate strain
    f_ck = 20.0    # Characteristic strength

    # Tests
    print(get_fc(-0.001, f_ck))  # None
    print(get_fc(0.004, f_ck))   # None
    print(get_fc(0, f_ck))       # 0.0
    print(get_fc(0.001, f_ck))   # 6.7
    print(get_fc(0.002, f_ck))   # 8.933
    print(get_fc(0.003, f_ck))   # 8.933
    print(get_fc(0.0035, f_ck))   # 8.933

if __name__ == "__main__":
    main()
```

1. `main()` is our main function that will test the function `get_fc()`
2. `main()` is called only when the script is called directly and not called when imported by another script as a module

Here are the desired output for different input:


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

1. First identify the **objects** in our program. In this problem, it is obvious there is only one object - Concrete material
2. The next task is to identify its **attributes**, in plain English, its **properties**. The attributes are $\epsilon_{cy}$, $\epsilon_{cu}$, $f_{ck}$.
3. Next we identify the operations we wish to perform on this object. In this case, we wish to calculate the stress $f_c$ for this object for a given strain $\epsilon_c$. This is a **method** in OO terminology. It is a function that is related to the object and a part of it. Because it is a part of the object, it automatically known all its attributes without having to pass them into the method like we do in the case of a function

Without explaining in detail, here is the implementation:

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

1. `#!python m20 = Concrete(20)` is an object created based on the `class Concrete()` (a `class` is a **blueprint** to create objects of a specific type, in this case of type `Concrete`)
2. The object `m20` is initialized with `fck = 20.0`
3. The method `fc()` is a part of the object `m20` and therefore cannot be called independently. It **must** be called on behalf of the object `m20`. That is implied by the `.` separating `m20` and `fc()`
4. The method `fc()` being a part of the object `m20`, can access its attrbute `fck`, it need not be passed into the method as an argument. This is achieved with the help of `self`, the first parameter to the method.
5. `self` is a special attribute that refers to the object on behalf of which the method is called.

This concept can be explained clearly with the following lines of code:
``` python
def main():
    m20 = Concrete(20.0)
    m30 = Concrete(30.0)
    print(m20.fc(0.001))  # 6.7
    print(m30.fc(0.001))  # 10.05
```

1. `m20` in an object of type Concrete with `fck = 20.0`
2. `m30` in an object of type Concrete with `fck = 30.0`
3. On the line `m20.fc(0.001)`, the method `fc()` is the one that belongs to (is a part of) the object `m20` and therefore on this line `self` is the object `m20`
4. On the line `m30.fc(0.001)`, the method `fc()` is the one that belongs to (is a part of) the object `m30` and therefore on this line `self` is the object `m30`
