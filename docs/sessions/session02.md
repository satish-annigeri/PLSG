# Session 2: Working with Python, Objects and Memory Location

**Date: 2026-03-14  4:30 pm to 6:30 pm**

## Agenda

1. Review of previous session
2. Answers to queries asked in person or sent in advance
3. Installing Windows Applications
4. Objects and memory locations
5. Logical operations
6. VS Code for Python Prorgamming
7. Writing Python code in VS Code and executing code in a file
8. Program Design

## Installing Windows Applications

The important sources of Windows applications, especially for programmers, are:

### 1. Microsoft Store
Microsoft Store is pre-installed on Windows 10/11.  
You can open it by typing `store` in the search bar and selecting the **Microsoft Store** app.

- Hosts both free and open-source (FOSS) and paid applications  
- Provides a graphical interface for installation  

---

### 2. WinGet
WinGet is Microsoft's official command-line package manager.

- Install applications via terminal  
- Example: `winget install git`  
- Similar to package managers in Linux  

---

### 3. Scoop
Scoop is a lightweight, developer-focused package manager.

- Installs applications in user space (often no admin required)  
- Ideal for CLI tools and developer utilities  

---

### 4. Chocolatey
Chocolatey is a popular Windows package manager.

- Large repository of software  
- Typically requires admin privileges  
- Example: `choco install nodejs`  

---

### Key Idea

Except for Microsoft Store, these tools function similarly to:

- `apt` on Debian/Ubuntu  
- `brew` on macOS  

They act as centralized repositories of precompiled applications, allowing you to:

- Search for software  
- Install and uninstall programs  
- Keep applications updated  

---

See [Windows Applications](../resources/windows_pkg.md) for more.

## Objects and Memory Locations

Python is considered easy to learn and use because it hides complex concepts such as memory addresses and pointers from the programmer. It automatically handles memory allocation and deallocation for objects.

However, Python provides a built-in function `id()` that returns the memory address (identity) of an object. Here are a few examples:

```pycon
>>> a = 10
>>> id(a)
140705796281752
```

**Note:** The memory location will differ across systems and may change between sessions.

```pycon
>>> b = 20
>>> id(b)
140705796282072
```

Since `a` and `b` are different objects, they have different memory addresses.

At this stage, it is enough to understand that:

- Objects are stored in memory
- Each object has a unique identity (accessible using `id()`)

---

## Logical Operations

Python supports the following logical (comparison and boolean) operators:

- Comparison: `<`, `>`, `<=`, `>=`, `==`, `!=`
- Boolean: `and`, `or`, `not`

A logical expression always evaluates to either `True` or `False`.

Examples:

```pycon
>>> a = 2 < 3
>>> a
True

>>> b = 2 > 3
>>> b
False

>>> 2 < 3 and 5 > 2
True

>>> x = 10; y = 20
>>> x, y
(10, 20)

>>> (x < y) and (x >= 0)
True
```

### Chained Comparisons

Python allows chaining comparisons for cleaner expressions.

For example, to check if a number `x` lies between `0.0` and `1.0` (inclusive):

```python
0 <= x <= 1.0
```

This is equivalent to:

```python
(x >= 0.0) and (x <= 1.0)
```

Chained comparisons are more concise and often easier to read.

## VS Code for Python Programming

VS Code is a popular code editor for Python programming, although there are several others. See [Using a Code Editor](../resources/ide.md) for details.

VS Code is lightweight, has a large number of extensions useful to Python (as well as other) programmers, and will be used during these sessions. However, you are free to choose a code editor of your choice if you wish to.

As a first step, identify all the important components of the VS Code GUI, especially the vertical toolbar on the left and the status bar at the bottom. For example, when you begin coding in Python, VS Code will try to locate the appropriate virtual environment (venv) by searching in the current folder or its parent folders. If it cannot identify a suitable one, it will prompt you to choose one explicitly.

We will look at the following features of the VS Code GUI:

- **User interface:** Main menu, Toolbar, Primary Side Bar, Secondary Side Bar, Panel, Status Bar  
- **Toolbar:** File Explorer, Extensions, Settings, Source Control  
- **Status bar:** Warnings, Errors, Cursor position, Spaces, File type, Virtual environment  
- **Extensions:** Installing the Microsoft Python extension to customize VS Code for Python development  
- **Workflow:** Working with files, search and replace (in a single file or across files), searching for files, navigating within a file, using the terminal, and handling warnings and errors  

## Program Design

Engineers design and build things. Just as civil engineers design and build buildings and infrastructure, computer science engineers design and build software applications. While one has a physical existence and the other does not, what is common to both is that they are **designed** to meet requirements specified before they come into existence. The dictionary meaning closest to how we use it here is: "the way in which something is planned and made."

There are well-defined ways in which software is designed, and it can be a specialized topic in itself. As *applied computer scientists*, we will approach it in a way that is useful and meaningful in the context of designing and developing programs for structural engineering applications.

The methods of design are closely related to how the design will be implemented using a programming language. For example, an object-oriented design can only be implemented using a programming language that supports object-oriented programming. Therefore, the task of designing cannot be completely detached from the programming language used for implementation.

However, it is possible to design a program in a way that is largely independent of the programming language, as long as the required design features are supported by the chosen language. For example, a program design may be represented using:

- Flowcharts  
- A hierarchy of functions  
- Pseudocode to describe an algorithm  

Learning to design programs is an important skill. While programming languages may change over time, program design methodologies tend to remain relevant. See [Programming Paradigms](../resources/prog_paradigms.md) for more on this topic.

We will begin with the procedural paradigm and later transition to the object-oriented paradigm. Structural engineering applications often deal with objects—where objects are bundles of **attributes** (representing properties of real-world entities) and **methods** (which operate on those attributes and transform them from one state to another).

For example, designing a program for analyzing a beam subjected to bending can be approached using either the procedural paradigm or the object-oriented paradigm. Each approach has its own merits and demerits, and the choice depends on which advantages are more relevant for the problem at hand.

### Procedural Paradigm

1. Designing a beam subjected to bending requires designing selected sections located at specific positions along the length of the beam.  
2. Designing a chosen section of a beam subjected to bending requires calculating the area of tension reinforcement (and compression reinforcement, if required).  
3. Determining whether the beam requires compression reinforcement requires calculating the moment of resistance of a balanced section.  

There may be several additional tasks involved. In this approach, the overall problem is subdivided into smaller tasks. Each task is assigned to a **function**.

During implementation, we begin by writing the simplest and most independent functions, and then move on to more complex and dependent ones.

Each function:

- Takes a set of input data  
- Performs operations on that input  
- Returns output data  

The output of one function becomes the input to another. In this way, the initial input data is gradually transformed into the desired final output.

At every stage of implementation, each function must be tested to ensure it produces the expected results, even at intermediate stages.

### Object-Oriented Paradigm

In the object-oriented paradigm, a beam is treated as an object. It has a set of attributes such as its dimensions, grade of concrete, and grade of steel.

A beam consists of several sections, and each section can also be treated as an object. Some attributes of a section depend on the attributes of the beam to which it belongs (for example, width, and grades of steel and concrete). However, a section also has attributes unique to itself, such as its distance from the start of the beam.

Objects also have **methods**, which are functions associated with them. For example, calculating the moment of resistance of a section is a method specific to that section. This method uses the properties (attributes) of the section object to perform the calculation.

Such methods are closely tied to the object they belong to and have little meaning when applied outside that context. Similarly, methods used to determine the areas of reinforcement are specific to the section object and operate on its attributes.