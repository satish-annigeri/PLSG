# Session 13: Modules and Packages

**Planned Date: 06-06-2026 4:00 pm to 6:00 pm**

## Agenda

1. Review of previous sessions
2. Answers to queries
3. Distributing Python Code
4. Modules
5. Packages
6. Building Packages

## Distributing Python Code

Python is an interpreted programming language. Python source code can be distributed and consumed in two different ways:

1. **Module** is an individual Python file containing functions, classes, constants, and if necessary, executable statements. Name of the Python file is he name of the module. A module can be imported into another Python program with the `import` keyword. Typically a module is stored in the same directory as the program it is imported into although Python can import modules from other standard directories.
2. **Package** is a directory containing a special file named `__init__.py` and other Python files. Name of the directory containing the `__init__.py` file is the name of the package. A package can contain any number of modules and sub-directories within it. A sub-directory must contain a `__init__.py` file for it to be teated as a sub-package. If a sub-directory does not contain the `__init__.py` file, but contains Python modules in it, they are accessible to code within the package but can be called from outside the package.

### Module

A Python module is a:

1. A valid Python file containing Python code, consisting of functions, classes, variables, and optionally, executable statements. (Note: This code is executed only once, the first time the module is imported).
2. Its contents can be imported into another Python program with the import module or from module import xyz statements.
3. Name of the file, without the `.py`, is the name of the module.
4. When an import module statement is executed, Python runs the module code to create a module object, and binds that module's name to the current scope.
5. When from module import xyz is executed, the specific attribute xyz is imported directly into the current scope, allowing it to be used without the module. prefix.
6. An application looks for modules in the same directory as the application and, if not found, looks for them in a set of predefined directories described later.

### Package

A Python package is a:

1. A directory with the file `__init__.py`, which may be an empty file or optionally contain Python code.
2. A sub-directory containing a `__init__.py` file within a directory that is a Python package (that itself contains a `__init__.py` file) is a sub-package of the said package. However, with Python 3.3 onwards, Python supports **implicit Namespace Packages** that allow one to create a package across multiple directories without an `__init__.py` file.
3. A package or a subpackage may contain modules.
4. Contents of a package can be imported with the `import package` statement. Similarly, a subpackage can be imported, usually with an alternate name as `import package.subpackage as alternatename`. For example `import matplotlib.pyplot as plt`.
5. Name of the directory is the name of the package.
6. Executing `import package` in an application creates the namespace `package`.
7. An application looks for packages in the same directory as the application and if not found, looks for them in a set of predefined directories described later.

!!! note "Where does an application look for modules and packages?"
    Python looks for a module (file with `.py` extension) or a package (a directory) in the same directory as the Python application being executed.

    If a matching file or directory is not found, the application looks for them in the predefined locations. These predefined locations are stored in `sys.path` and can be viewed with the following lines of code in the Python REPL or a Python script:

    ```pycon
    >>> import sys
    >>> for p in sys.path:
    ...     print(p)
    C:\Users\username\AppData\Local\Python\pythoncore-3.14-64\python314.zip
    C:\Users\username\AppData\Local\Python\pythoncore-3.14-64\DLLs
    C:\Users\username\AppData\Local\Python\pythoncore-3.14-64\Lib
    C:\Users\username\AppData\Local\Python\pythoncore-3.14-64
    C:\Projects\Python\ProjectName\.venv
    C:\Projects\Python\ProjectName\.venv\Lib\site-packages
    ```

    1. `username` is the name of the user on a Windows machine, and `C:\Users` is the typical location for user home directories. It is similar on GNU/Linux and macOS machines.
    2. `C:\Projects\Python\ProjectName` is the location where the Python project is located and is a choice of the programmer.


## Example Module

Let us write a module with two functions to calculate the the nearest multiplt of a specified number for a given input number, either on the higher side (ceiling) or the lower side (floor). Let us call the module file `utils.py` so that the name of the module is `utils`.

```py title="utils.py" linenums="1"
import math


def ceiling(x: float, m: float) -> float:
    return m * math.ceil(x / m)


def floor(x: float, m: float) -> float:
    return m * math.floor(x / m)


if __name__ == "__main__":
    print(ceiling(1.12, 0.25))  # Result 1.2
    print(floor(1.12, 0.15))  # Result 1.05
```
Place it in the same directory as the main program `main.py`, which imports the module.

```py title="main.py" linenums="1"
import utils

print(utils.ceiling(1.12, 0.25))  # Result 1.2
print(utils.floor(1.12, 0.15))  # Result 1.05
```

## Example Package

Let us develop a package named `footing` which is expected to contain modules for the proportioning of different types of footings, starting with the simplest, namely isolated rectangular footing.

The directory structure of the package within the project directory is as follows:
```doscon
|---- Project
   |     main.py
   |---- footing
             rectangular.py
```