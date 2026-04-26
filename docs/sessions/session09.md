# Session 9

### Planned date: 02-05-2026 4:00 pm to 6:00 pm

## Agenda

1. Review of previous sessions
2. Answers to queries
3. Object Oriented Programming in Python


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

## Example: A Line Counting Program

The task is to write a program to scan a specified directory for filenames with a specified pattern (such as `*.txt`) and, if found, to print the name of the file and the number of lines contained in the file.

### Design

The program has one main object: the starting directory from where to begin the search. Its attributes are:

1. Directory name
2. File pattern
3. Flag to recursively search sub-directories

The operations to perform on the directory are:

1. Search the directory and make a list of matching filenames
2. Process each file by counting the number of lines contained in the file
3. Display the filename and number of lines

Python is said to be "batteries included" because it provides a large number of built-in and third-party packages to efficiently accomplish tasks without us having to write our own code from scratch. Searching directories for matching filename patterns is one such task. The built-in package [`pathlib`](https://docs.python.org/3/library/pathlib.html) is well-suited for this task, and we will make use of it.

Having prepared a list of matching filenames, counting the number of lines is a process known to us from [Session 6](https://plsg.netlify.app/sessions/session06/#reading-and-writing-files).

### Implementation

Before we begin implementing the class, let us learn the basics of `pathlib` by trying it out in the Python REPL:

```pycon
>>> from pathlib import Path
>>> p = Path(".")
>>> p.absolute()
PosixPath('/home/satish/Python/sci')
>>> p.exists()
True
>>> p.is_dir()
True
>>> p.is_file()
False
>>> flist = p.glob("*.py")
>>> type(flist)
<class 'map'>
>>> for f in flist:
...     print(f.name)
...     
vector.py
main.py
vector2.py
searchdir.py
```

**Note**

1. `Path` is the path object imported from the `pathlib` package.
2. A `Path` object has methods such as `absolute()` that returns the absolute path of a directory, `exists()` that returns `True` if a file or a directory with the specified path exists, `is_dir()` that returns `True` if the path is a directory, and `is_file()` that returns `True` if the path is a file.
3. The method `glob()` returns a collection of paths that match a given pattern, such as `"*.py"`. If there are files with matching names, we can loop over them and process them one at a time. Note that `glob()` returns a generator which can be directly iterated over without having to first convert it to a list.

Let us begin by naming the class `SearchDir`. Python convention is to name classes starting with a capital letter and using capital letters for each word in the name (PascalCase). This is in contrast to the `snake_case` style used for functions or in other languages. Here is the code to define our class:

```python linenums="1" title="searchdir.py"
from pathlib import Path


class SearchDir:
    def __init__(self, dirpath: str, pattern: str, recurse: bool=False):
        p = Path(dirpath).absolute()
        if p.is_dir():
            self.path = Path(dirpath)
            self.pattern = pattern
            self.recurse = recurse
        else:
            raise ValueError(f"Path {dirpath} must be a directory")

    def __str__(self) -> str:
        return f"SearchDir({self.path.absolute()}, {self.pattern}, {self.recurse})"


if __name__ == "__main__":
    dir = SearchDir(".", "*.py")
    print(dir)
```

!!! tip
    `self` is the variable that represents an instance of the class. While it could be assigned a different name, Python convention is to name this variable `self`. It represents, at the time of defining a class, the specific instance of the object that will be created later. Since the object to be created later may have a name chosen at runtime, `self` acts as a placeholder for that name within the class definition.

!!! note
    Methods with names beginning and ending with double underscore characters (`__`) are called **dunder** (Double UNDERscore) methods. They have special meanings in the Python language and must not be used as names for regular user-defined functions or methods. We will learn more dunder methods later on.

**Note**

1. `__init__()` is a special method which is used to initialize an object when it is first created. It merely copies the values from the arguments into the data field of the object. This calss has three data fields, namely `self.dirpath`, `self.pattern` and `self.recurse`.
2. The last, `self.recurse` defaults to `False` if not specified at the time of creating the instance.
3. `__str__()` is a dunder method that is expected to return a string representation of the object.

The output of the test run must produce the following output:

```pycon
> uv run python searchdir.py
SearchDir(/home/satish/Python/sci, *.py, True)
```
**Note:**

1. `pathlib` is cross-platform and understands how filesystems are repersented on Windows, GNU/Linux, macOS and any other on which it runs.
2. It correctly reerpsents the path separator as the forward slah (`/`) on GNU/Linux and macOS and the backslash (`\\`). The backslash is hsown as two backslashes becuase the backslash is used as the escape sequence, such as in representing a newline (`\n`) and the backslash itself is repersented as two backslashes.
3. The above code was run on GNU/Linux. The output will differ slightly in Windows. For example, it would be similar to `C:\\Users\\satish\\Documents\\Python\\sci` on Windows.

Let us add the functionality to count the number of lines in the file and print the name of the file and the number of lines.

```python linenums="13" hl_lines="5 6 7 8 13" title="serachdir.py"
    # Previous lines not shown
    def __str__(self) -> str:
        return f"SearchDir({self.dirpath}, {self.pattern}, {self.recurse})"

    def linecount(self, fname):
        with open(fname) as f:
            lines = f.readlines()
        return len(lines)

if __name__ == "__main__":
    dir = SearchDir(".", "*.py")
    print(dir)
    print(dir.linecount("searchdir.py"))
```

We can now add the facility to search for filenames matching a pattern and print their names along with the number of lines in the file using the method `linecount()`:

```python linenums="16" title="searchdir.py" hl_lines="7-19 24"
    # Previous lines not shown
    def linecount(self, fname):
        with open(fname) as f:
            lines = f.readlines()
        return len(lines)

    def search_print(self):
        flist = self.path.rglob(self.pattern) if self.recurse else self.path.glob(self.pattern)
        flist = list(flist)
        if len(flist) == 0:
            print(f"No files matching {self.pattern} found")
            return

        total_lines = 0
        for i, f in enumerate(sorted(flist), 1):
            num_lines = self.linecount(f)
            total_lines += num_lines
            print(f"{f} ({num_lines})")
        print(f"Files: {i}, Total lines: {total_lines}")

if __name__ == "__main__":
    dir = SearchDir(".", "*.py")
    print(dir, "\n")
    dir.search_print()
```
The output may look similar to the following:
```pycon
SearchDir(/home/satish/Python/sci, *.py, False)

main.py (10)
searchdir.py (34)
vector.py (37)
vector2.py (41)
Files: 4, Total lines: 122
```

!!! note
    The list of files returned by `glob()` or `rglob()` are not in alphabetical order, and may need the use of `sorted()` in case they are to be listed in alphabetical order.

!!! tip
    If there are no filenames matching the specified pattern, it is best to convert `flist`, which is a `map` to a `list` and check if the length of the list is `0`, and print an appropriate message if that is true.

### Command Line Interfaces

Type the following code in a code editor (not in the Python REPL):
```python title="app.py"
import sys

print(sys.argv)
```

and run it from the command line:
```doscon
> uv run python app.py
['app.py']
> uv run python app.py one, two three
['app.py', 'one', 'two', 'three']
```

**Note**

1. `sys` is a built-in module and gives access to several system information.
2. `sys.argv` returns a list of command line arguments typed at the command line when executing the application.
3. The first argument is the name of the application, in this case, `app.py`
4. All items in the `sys.argv` list are of type `str`. Arguments starting from index `1` can be treated as arguments to the application and interpreted as appropriate.

Let us use `sys.argv` and assume that the arguments have the following meaning:

1. `sys.argv[1]` represents the path to be searched, and is a required argument.
2. `sys.argv[2]` represents the filename pattern to be searched, and is a required argument.
3. `sys.argv[3]` represents whether to search the path recursively, and is an optional argument, defaulting to "false". User must type true to indicate the search to be recursive.

```python
import sys


def argparse(argv):
    if len(argv) < 3:
        sys.exit("Usage: python app.py path pattern [false]")


    if (len(argv) > 3) and argv[3].lower() == 'true':
            recurse = True
    else:
        recurse = False

    return argv[1], argv[2], recurse


if __name__ == "__main__":
    print(sys.argv)
    path, pattern, recurse = argparse(sys.argv)
    print(f"Path: {path}, Pattern: {pattern}, Recursive search: {recurse}")
```

**Note**

1. Filename pattern such as `*.py` must be enclosed within single or double quotes. Otherwise the command shell expands it to a list of filenames **before** calling the application.
2. The third argument is case-insensitive becaue we convert it to lowercase before checking its value.
3. Any value other than **true** is treated as **false** when evaluating the third command line argument.

Test this with different number of command line arguments:
```doscon
> uv run python app.py
Usage: python app.py path pattern [false]
> uv run python app.py .
Usage: python app.py path pattern [false]
> uv run python app.py . "*.py"
Path: ., Pattern: .py, Recursive search: False
> uv run python app.py . "*.py" true
Path: ., Pattern: .py, Recursive search: True
```

You can now integrate this with the program, but let us import it as a module and modify `app.py`.
```python title="app.py"
import sys
from searchdir import SearchDir


def argparse(argv):
    if len(argv) < 3:
        sys.exit("Usage: python app.py path pattern [false]")


    if (len(argv) > 3) and argv[3].lower() == 'true':
            recurse = True
    else:
        recurse = False

    return argv[1], argv[2], recurse


if __name__ == "__main__":
    path, pattern, recurse = argparse(sys.argv)
    dir = SearchDir(path, pattern, recurse)
    dir.search_print()
```

Execute this application as follows:
```doscon
> uv run python app.py . "*.py"
app.py (22)
main.py (10)
searchdir.py (46)
vector.py (37)
vector2.py (41)
Files: 5, Total lines: 156
```

Python has several libraries for argument parsing, `argparse` being one of the oldest and very comprehensive but come with a learning curve. There are more recent and simpler packages such as [Typer](https://typer.tiangolo.com/) that simplify this process. The following code does the same as the previous version of the program. Study the Typer documentation to learn more, the code below is presented without any explanation.

Remember to install Typer with
```doscon
> uv add typer
```

Here is the code:
```python linenums="1" title="app.py"
import typer
from searchdir import SearchDir, main


if __name__ == "__main__":
    typer.run(main)
```
Execute the application from the command line:
```doscon
> uv run python app.py
                                                                                
 Usage: app.py [OPTIONS] PATH PATTERN                                           
                                                                                
╭─ Arguments ──────────────────────────────────────────────────────────────────╮
│ *    path         TEXT  [required]                                           │
│ *    pattern      TEXT  [required]                                           │
╰──────────────────────────────────────────────────────────────────────────────╯
╭─ Options ────────────────────────────────────────────────────────────────────╮
│ --recurse    --no-recurse      [default: no-recurse]                         │
│ --help                         Show this message and exit.                   │
╰──────────────────────────────────────────────────────────────────────────────╯
> uv run python app.py
Usage: app.py [OPTIONS] PATH PATTERN
Try 'app.py --help' for help.
╭─ Error ──────────────────────────────────────────────────────────────────────╮
│ Missing argument 'PATH'.                                                     │
╰──────────────────────────────────────────────────────────────────────────────╯
> uv run python app.py .
Usage: app.py [OPTIONS] PATH PATTERN
Try 'app.py --help' for help.
╭─ Error ──────────────────────────────────────────────────────────────────────╮
│ Missing argument 'PATTERN'.                                                  │
╰──────────────────────────────────────────────────────────────────────────────╯
> uv run python app.py . "*.py"
SearchDir(/home/satish/Python/sci, *.py, False) 

app.py (12)
app_v1.py (22)
main.py (10)
searchdir.py (46)
vector.py (37)
vector2.py (41)
Files: 6, Total lines: 168
> uv run python app.py . "*.py" --recurse
SearchDir(/home/satish/Python/sci, *.py, False) 

...
app.py (12)
app_v1.py (22)
main.py (10)
searchdir.py (46)
vector.py (37)
vector2.py (41)
Files: 1759, Total lines: 830435
```
!!! warning
    Recursive listing lists the `.py` files in `.venv` and its subdirectories.

