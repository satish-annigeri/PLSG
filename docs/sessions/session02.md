# Session 2: Planned Date 2026-03-14 Saturday
#### From 4:30 pm to 6:30 pm
## Agenda

1. Review of previous session
2. Answers to queries asked in person or sent in advance
3. Installing Windows Applications
4. Objects and memory locations
5. Logical operations
6. VS Code for Python Prorgamming
7. Writing Python code in VS Code and executing code in a file
8. Program Design

## Installing Windows applications

The important sources of Windows applications, as far as programmers are concerned are:

1. Microsoft Store is installed on Windows 10/11 and can be opened by typing `store` in the search bar and clicking on the **Microsoft Store** application that is pre-installed
2. [WinGet](https://learn.microsoft.com/en-us/windows/package-manager/winget/)
3. [Scoop](https://scoop.sh/)
4. [Chocolatey](https://chocolatey.org/install)

While Microsoft Store hosts FOSS as well as closed-source paid applications, the rest serve the same purpose as `apt` in Debian and Ubuntu GNU/Linux distributions and `brew` in macOS. Essentially, they are a central repository of binary applications that can be searched and you can download, install, update and uninstall applications from these.

See [Windows Applications](../resources/windows_pkg.md) for more.

## Objects and memory locations
Python is said to be easy to learn and use because it keeps complex concepts such as memory addresses, pointers etc. hidden from the prorammer. It automatically allocates and deallocates memory to objects without the programmer having to do this. However, it has a function `id()` that displays memory addresses of objects. Here are a few examples:
``` pycon
>>> a = 10
>>> id(a)
140705796281752
```
**Note:** The memory location is not the same for everyone, and may change if you execute this statement during a different session.

``` pycon
>>> b = 20
>>> id(b)
140705796282072
```
Obviously, this is a different object and therefore has a different memory address. There are several aspects related to this topic that we will take up later. At this point of time, let us note that objects are stored in memory and it is possible to display their memory address.

## Logical operations

The logical operators are: `<`, `>`, `<=`, `>=`, `==`, `!=`, `and`, `or`, `not`. There are only two possible values for a logical operation, either `True` or `False`. Thus, the result of the expression `2 < 3` is `True` while that of `2 > 3` is `False`. Such results can be stored in an object, for example `#!python a = 2 < 3` and the value of `a` if True.
``` pycon
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

It is possible to avoid using complicated operations in some cases. For example, to check if a number `x` is between `0.0` and `1.0`, both values included, this logical expression `#!python 0 <= x <= 1.0` will work instead of `#!python (x >= 0.0) and (x <=1.0)`, which is also valid.

## VS Code for Python prorgamming
VS Code is a popular code editor for Python programming although there are several others. See [Using a Code Editor](../resources/ide.md) for details.

VS Code is lightweight, has a large number of extensions useful to Python (as well as other) programmers and will be used during these sessions. However, you are free to choose a code editor of your choice if you wish to.

As a first step, identify all the important components of the VS Code GUI, especially the vertical toolbar at the left and the status bar at the bottom. For example, when you begin coding in Python, VS Code will try and locate the right venv to use, by searching for virtual environments in the current folder or its parent folders. If it cannot identify a suitable one, it will prompt you to chooce one explicitly.

We will look at the following features of the VS Code GUI:

* **User interface:** Main menu,Toolbar, Primary Side Bar, Secondary Side Bar, Panel, Status Bar
* **Toolbar:** File explorer, Extensions, Settings, Source Control
* **Status bar:** Warnings, Errors, Cursor position, Spaces, File type, Virtual environment
* **Extensions:** Installing Microsoft Python extension customize VS Code for a specific task
* **Workflow:** Working with files, search and replace in one file or all files, search for a file, navigate within a file, working within the terminal, looking at warnings and errors

## Program Design

Engineers design and build things. Just as Civil engineers design and build buildings and infrastructure, Computer science engineers design and build software applications. While one has a physical existence and the other does not. But what is common to both is they are both **designed** to meet requirements that are specified before they come into existence. The dictionary meaning close to the way we use it here is "the way in which something is planned and made".

There are well defined ways in software is designed and it can be a specialized topic in itself. We as *applied computer scientist* will look at it in a way that is useful and meaningful to us in the context of designing and developing programs for structural engineering applications. The methods of designing are intimately related to the way the design will be implemented using a programming language. For exmaple, an object oriented design can be implemented only by using a programming language that supports object orientated programming. Therefore the task of designing cannot be completely detatched from the programming language that will be used to implement it. However, it is possible to design a program keeping it independent of the programming language as long as it is known that the design feature will be available in the chosen programming language. For example, a program design may be in the form of a flow chart, or a hierarchy of functions or a pseudo-code to represent an algorithm.

Learning to design programs is an important skill. While programming languages can change with time, program design methodologies will remain the same. See [Programming Paradigms](../resources/prog_paradigms.md) for a discussion on this topic.

We will begin with the procedural paradigm but soon switch to the object oriented paradigm. For strcutural engineering applications, which mainly work with objects (objects are bundles of **attributes** that represent the properties of a real life object and **methods** which act on attributes and transform them from one state to the next required state).

Structural designing a beam subjected to bending can be *designed* using the procedural paradigm or the object oriented paradigm. Each one has its merits and de-merits and the specific choice is based on whether the merits dominate over the de-dmerits or the other way around.

### Procedural paradigm

1. Design of a beam subjected to bending requires the design of its selected sections, located at specific positions along the length of the beam
2. Design of a chosen section of a beam subjected to bending requires us to calculate the area of tension reinforcement (and compression reinforcement if required)
3. Determining whether the beam requires compression reinforcement requires the calculation of the moment of resistance of a balanced section

and perhaps several other tasks. Here, the given task is sub-divided into smaller tasks. Each task is assigned to one **function**. During implementation, we begin by implementing the simplest and most independent function before moving on to implementing more complex and consequently, dependent functions.

Each function will require a set of input data, the function will operate on that input and return output data. The data output by one function becomes an input for another function an dthis is how the input data eventually gets transformed to the desired output. At every stage of implementation, we must test each function to ensure it is giving the desired output at any intermediate stage.

### Object oriented paradigm
The beam is treated as an object and it has a set of attributes, such as, its dimensions, grade of concrete and steel it uses etc. A beam is made up of several functions and is itself an object. Some of its attributes depend on the attributes of the beam to which it belogs, for example the width and the grade of steel and concrete. But it has some attributes unique to the section, such as its distance from the start of the beam.

Then there are the methods such as calculating the moment of resistance of a section which are specific to an object, in this case, the section and utilizes the properties of that object to carry out these calculations. That is why this method of calculating the moment of resistance is intimately tied to the object and has little meaning when applied to any other object. So are the method that determine the areas of reinforcement.