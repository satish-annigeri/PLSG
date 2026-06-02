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

Let us develop a package named `footing` which is expected to contain modules for the proportioning of different types of footings, and make the module `rect_footing.py` a part of this packgae. The easiest way to get started is to crate a new project folder, and use `uv` to initialize a project to create a **library**. Assuming you are on a Windows machine and your Python projects are in the `C:\Users\username\Projects\` directory, follow these command at the Command Prompt:

```doscon
C:\Users\username\Projects > md footing
C:\Users\username\Projects > cd footing
C:\Users\username\Projects\footing > uv init --lib
Initialized project `footing`
C:\Users\username\Projects\footing > tree /f
C:\Users\username\Projects\footing> tree /f
Folder PATH listing for volume Windows-SSD
Volume serial number is 000000B4 2CED:96CE
C:.
│   .gitignore
│   .python-version
│   pyproject.toml
│   README.md
│
└───src
    └───footing
            py.typed
            __init__.py
```

**Note**

Like any project created with `uv init` (except with `uv init --bare` option) you have the following components created by `uv`:

 1. `.git` directory for source code version management using `git`.
 2. `.gitignore` file, with names of directories and files patterns that are to be ignored by `git`.
 3. `.python-version` file containing the Python version to be used by the project. This file is managed by `uv` and must not be changed by the programmer.
 4. `README.md` file, is the file expected by GitHub and other online `git` web repositories such as GitLab and several others. It is in Markdown format and its contents are displayed on the front page of the repository. It serves as an introduction to the package.
 5. `src` directory containes the source code for the package we intend to develop.
 6. `src\footing` directory contains the source code for the package.
 7. `src\footing\__init__.py` file makes this directory a package.
 8. `py.typed` file tells type checkers (like mypy, pyright, pylance) that your package ships with type hints that should be trusted and enforced. You can ignore it at this point of time.

Check the status of the local Git repository with the command:

```doscon
> git status
git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore
        .python-version
        README.md
        pyproject.toml
        src/

nothing added to commit but untracked files present (use "git add" to track)
```

Let us copy the `rect_footing.py` from our previous application with the name `rectangular.py` into the `src\footing` directory with the command. Let us assume that the `rect_footing.py` file is in a directory named `C:\Users\username\Projects\footing_design` and assume that the destination directory is `C:\Users\username\Projects\footing\src\footing`. (change the command appropriately as needed).

```doscon
> copy C:\Users\username\Projects\footing_design\rect_footing.py C:\Users\username\footing\src\fppting\rectangular.py
```

Alternatively, use Windows File Explorer and make a copy of the file `rect_footing.py` in the original folder, rename it to `rectangular.py` and copy it to the desitnation directory.

Create a directory named `tests` in the project root and copy the `test_rectfooting.py` to that directory.

These are the directory tree and Git status after these changes:

```doscon
> tree /f
C:.
│   .gitignore
│   .python-version
│   pyproject.toml
│   README.md
│
├───src
│   └───footing
│           py.typed
│           rectangular.py
│           __init__.py
│
└───tests
        test_rectfooting.py
> git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore
        .python-version
        README.md
        pyproject.toml
        src/
        tests/

nothing added to commit but untracked files present (use "git add" to track)
```

We can now run the tests using `pytest`:

```doscon
uv run -- pytest tests
================================================= test session starts =================================================
platform win32 -- Python 3.14.0, pytest-9.0.3, pluggy-1.6.0
rootdir: C:\Users\satish\Documents\Python\footing
configfile: pyproject.toml
plugins: cov-7.1.0
collected 2 items

tests\test_rectfooting.py ..                                                                                     [100%]

================================================== 2 passed in 0.06s ==================================================
```

Following points are worth noting:

1. The package we inted to develop is named `footing` and its source code resides in the directory `src\footing` within the project directory.
2. The file `src\footing\__init__.py` must be present for the directory to be considered as a package.
3. At present, the package consists of a single module named `rectangular` and its source code resides in the file `src\footing\rectangular.py`.
4. To import the package into any file within the project directory, it is sufficient to refer to the name of the package `footing`. For example, `RectFooting` class from the module `rectangular` in the package `footing` is imported into the test file `tests\test_rectfooting.py` using the statement `from footing.rectangular import RectFooting`.

### Git Repository for the Package

We took a preliminary llok at Git in [Source Code Management](../resources/git_github.md). We will now create a repository for this package on GitHub. It will serve several purposes:

1. Source coode management: All versions and branches along the entire history of its development
2. Storage on a remote repository: This enables recreating the source code to a local repository on a different machine
3. Distribution of the package to others: This becomes possible because `pip` and by extension `uv` can install packages from GitHub (in addition to their main purpose of installing packages from PyPI).

## Building a Module or a Package for Distribution
If you wish to distribute the module or the package to other users, you must build a package in a way that it can be distributed to other users and they should be able to install it and use it in their applications. A package can be distributed directly from the GitHub repository, assuming one has access to it, or from PyPI [(Python Packaging Index)](https://pypi.org/).

Distributing from GitHub is simple and straightforward as `uv` or `pip` understand how to request, download and install from a Git repository. Distributing via PyPI requires additional steps such as building a distributable package, optionally testing the package on [Test PyPI](https://test.pypi.org/) before uploading to PyPI, following security requirements, a PyPI account and API token etc.

Here are the requirements that must be met:

1. A valid project structure
2. A `pyproject.toml` with PEP 621 metadata
3. A build backend to build a **wheel** (`.whl`) or a **source distribution (sdist)**
4. Build artifacts, **sdist + wheel**
5. A PyPI account and API token
6. A unique module or package name
7. Upload tool

`uv` manages steps 1 to 4, although it requires an external backend build tool such as [`flit``](https://flit.pypa.io/en/stable/). You can install `flit` as a part of the virtual environment, but it is a good idea to install it as a `uv` tool so that a single installation is available to all Python projects and can be updated and managed at one place. The command to install `flit` is as follows:

```doscon
> uv tool install flit
Resolved 10 packages in 1.09s
Prepared 10 packages in 2.78s
Installed 10 packages in 1.63s
 + certifi==2026.5.20
 + charset-normalizer==3.4.7
 + docutils==0.23
 + flit==3.12.0
 + flit-core==3.12.0
 + idna==3.17
 + pip==26.1.2
 + requests==2.34.2
 + tomli-w==1.2.0
 + urllib3==2.7.0
Installed 1 executable: flit
> flit --version
Flit 3.12.0
```
This installs `flit` in an isolated virtual environment of its own and makes it accessible on the command line. Subsequently, it can be updated with the command:
```doscon
> uv tool update flit
```
You don't have to directly use `flit`, `uv` will use it behind the scene to package the code into a distributable module or package.