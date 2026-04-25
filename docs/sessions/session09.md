# Session 9

### Planned date: 02-05-2026 4:00 pm to 6:00 pm

## Agenda

1. Review of previous sessions
2. Answers to queries
3. Object Oriented Programming in Python

Here is the corrected and improved version of your tutorial content. I have removed the repeated sections, fixed the typos and grammatical errors, and simplified the language for a beginner audience.

---

# Programming Paradigms and Classes

## Programming Paradigms

A programming paradigm is an approach or "style" of designing and implementing software. While you can design a program's logic independently of a specific language, actually building (implementing) it requires a language that supports your chosen paradigm.

### Procedural vs. Object-Oriented Programming

The **procedural paradigm** focuses on **algorithms** (procedures) as the core of program design.

*   **Design:** It starts with a main task and breaks it down into smaller, simpler sub-tasks. This is represented as a hierarchy of functions. Each function achieves a well-defined result; higher-level functions depend on lower-level ones to work.
*   **Implementation:** Development begins with the lowest-level functions and progresses toward the "top" until the `main` function is complete.

The **object-oriented paradigm (OOP)** puts **objects** at the center of design and implementation (See [OOP](../resources/prog_paradigms.md#object-oriented-paradigm-oo-paradigm)).

*   **Design:** It identifies the objects within a problem statement. For each object, it defines its **attributes** (data) and the **operations** (logic) needed to transform input into the desired output. This design is often visualized using class diagrams and state diagrams.
*   **Implementation:** Development starts with the most independent classes and moves toward dependent ones. Once the classes are built, the `main` function creates (**instantiates**) the objects and calls their methods to produce the final result.

---

## Classes

In his 1976 book, *Algorithms + Data Structures = Programs*, Niklaus Wirth explained that algorithms and data structures are inherently related. 

In traditional procedural programming, functions organize logic, but there is no formal way to "bind" that logic to specific data. Programmers have to manually keep track of which function belongs to which data through naming conventions or documentation.

**Classes** are user-defined types designed to unify logic and data into a single entity. (See [Allen B. Downey, Think Python, 3ed.](https://allendowney.github.io/ThinkPython/chap14.html#classes-and-functions)). A class consists of:

*   **Attributes:** Data fields that represent the characteristics or "state" of an entity.
*   **Methods:** Functions defined within the class that operate specifically on its attributes.

By grouping these together, classes use **encapsulation** to make the relationship between data and logic explicit. This makes the program's intent clearer and easier to maintain, as the data and the tools used to change it are housed in the same "blueprint."

### Blueprints and Instances

While a class is a **blueprint**, the objects created from it are **instances**. Think of a class as an empty registration form that defines what information is required. An instance is the actual filled-out form, containing unique data for a specific person.

### Modeling the Real World

Classes allow us to model real-world entities through **abstraction**. By identifying the essential qualities of an object and the actions it performs, we create a digital version of it. 

#### Example 1: Structural Engineering
Consider a program designed to model a structural beam:

*   **Attributes:** Span, cross-section shape, size and location, and design forces at cross-sections.
*   **Operations (Methods):** Calculating the required reinforcement or determining how to detail the steel between sections.

#### Example 2: Library Management
Consider a program for a library. While the library has many parts (users, shelves, etc.), let's look at the **Book** object:

*   **Attributes:** Title, authors, publisher, and ISBN.
*   **Operations (Methods):** Lending the book to a user, returning it to the shelf, or displaying its bibliographic information.

In practice, a Python program defines the classes needed for a specific problem and creates instances of them. It then triggers methods to transform the data within those instances or to help different objects interact—using data from one object to generate new information for another.