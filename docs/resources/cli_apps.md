# CLI Applications

Command Line Interface (CLI) applications are applications that take commands and options on the command line to simplify what you want the application to do and any additional information, such as input and output filenames, Following examples may be familiar to you:

`git clone https://github.com/satish-annigeri/rcdesign.git`

* `git` is the CLI application
* `clone` is the command
* `https://github.com/satish-annigeri/rcdesign.git` is the repository to be cloned

## The Mechanism of CLI Applications

When an application is called from the command line (Command Prompt in Windows orterminal in  GNU/Linux and macOS), the operating system shell passes on information about the command and the command line arguments to the application. Within the program, the programming language can access these command line arguments and interpret and act on them based on its own logic.

The built-in module `sys` can access the command line arguments:

```py title="cli_app.py"
import sys

print(type(sys.argv), len(sys.argv))
for i, arg in enumerate(sys.argv):
    print(i, arg)
```

!!! warning "Alert"
    accessing command line arguments requires that the application be called from the command line. This will not work inside the Python REPL.

Run this application from the command line in the following ways and see the output"

=== "Using `uv`"
    ```doscon
    > uv run -- python cli_app.py
    > uv run -- python cli_app.py command
    > uv run -- python cli_app.py command argument
    ```
=== "Using `pip` on Windows"
    ```doscon
    > .venv\Scripts\actvate
    (.venv) > python cli_app.py
    (.venv) > python cli_app.py command
    (.venv) > python cli_app.py command argument
    ```
=== "Using `pip` on GNU/Linux or macOS"
    ```doscon
    > .venv/bin/actvate
    (.venv) > python cli_app.py
    (.venv) > python cli_app.py command
    (.venv) > python cli_app.py command argument
    ```
You should see the following output:

```doscon
> uv run -- python cli_app.py 
<class 'list'> 1
0 cli_app.py
> uv run -- python cli_app.py command
<class 'list'> 2
0 cli_app.py
1 command
> uv run -- python cli_app.py command argument
<class 'list'> 3
0 cli_app.py
1 command
2 argument
```
**Note**

1. `sys.argv` is a `list`
2. The first element at index 0 of `sys.argv` is the name of the application itself, `cli_app.py` in our case
3. The other elements depend on the additional arguments typed on the command line
4. The command line arguments are passed on to the application as they are typed and it is up to the application to make use of them as required

Python has modules specifically to assist in parsing command line arguments and `argparse` is the one of the earliest. However, we will use a module named [`typer`](https://typer.tiangolo.com/) which is simple to use and fairly capable.

## Typer

Typer is a library for building CLI applications and is based on Python type hints. It relies on the parameters of a specified function (usually named `main()` but could be anything else) and their type hints and generates the CLI interface with little to no additional coding on the part of the programmer. Let us begin with a simple example with only arguments (that is, no multiple commands).

```py title="cli_app.py" linenums="1"
import typer

def main(dir: str, pattern: str, recurse: bool=False):
    print(f"{dir=}")
    print(f"{pattern=}")
    print(f"{recurse=}")



if __name__ == "__main__":
    typer.run(main)
```
Let us call this without any arguments:
```doscon
> uv run cli_app.py
Usage: cli_app.py [OPTIONS] DIR PATTERN
Try 'cli_app.py --help' for help.
╭─ Error ──────────────────────────────────────────────────────────────────────╮
│ Missing argument 'DIR'.                                                      │
╰──────────────────────────────────────────────────────────────────────────────╯
> uv run -- python cli_app.py --help
                                                                               
 Usage: cli_app.py [OPTIONS] DIR PATTERN                                        
                                                                                
╭─ Arguments ──────────────────────────────────────────────────────────────────╮
│ *    dir          TEXT  [required]                                           │
│ *    pattern      TEXT  [required]                                           │
╰──────────────────────────────────────────────────────────────────────────────╯
╭─ Options ────────────────────────────────────────────────────────────────────╮
│ --recurse    --no-recurse      [default: no-recurse]                         │
│ --help                         Show this message and exit.                   │
╰──────────────────────────────────────────────────────────────────────────────╯
```

Usage help tells us the following:

1. Arguments `dir` and `pattern` are **required**, and both are of type text
2. Argument `--recurse` is optional and the default value is `no-recurse`
3. Arguement `--help` displays the help page

Let us try with one argument, namely `.`, the current directory:
```doscon
> uv run -- python cli_app.py .
Usage: cli_app.py [OPTIONS] DIR PATTERN
Try 'cli_app.py --help' for help.
╭─ Error ──────────────────────────────────────────────────────────────────────╮
│ Missing argument 'PATTERN'.                                                  │
╰──────────────────────────────────────────────────────────────────────────────╯
```

Let us try with two arguments, `.` fir the directory and `*.py` for pattern:
```doscon
> uv run -- python cli_app.py , "*.py"
dir='.'
pattern='*.py'
recurse=False
```

!!! note
    It may be necessary to enclose `"*.py"` within double quotes to prevent the command shell from interpreting it wrongly.

One last time:
```doscon
> uv run -- python cli_app.py , "*.py" --recurse
dir='.'
pattern='*.py'
recurse=True
> uv run -- python cli_app.py , "*.py" --no-recurse
dir='.'
pattern='*.py'
recurse=False
```

To build CLI applications with multiple commands and a separate set of arguments for each command, study the [Typer documentation](https://typer.tiangolo.com/).

Typer has been used in the [Session 10 `searchdir.py` example](../sessions/session10.md#command-line-interfaces) and in [Snippet 3 CLI application](../snippets/snippet03.md#cli-application).