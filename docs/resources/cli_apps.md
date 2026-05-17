# CLI Applications

Command Line Interface (CLI) applications are applications that take command line arguments to pass in information to the application so as to avoid interacting with the application to input information. Command line arguments include information such as input and output filenames, switches to say yes or no. Following examples may be familiar to you:

1. `copy file1.csv file2.csv`
    * `copy` is the CLI application. This application takes only command line arguments and does not have subcommands.
    * `file1.csv` is the first argument and is assumed to be the source file that is to be copied
    * `file2.csv` is the second command line argument and is assumed to be the name of the copy of the source file.
2. `git clone https://github.com/satish-annigeri/rcdesign.git`
    * `git` is the CLI application. This application has several subcommands which can be displayed with the `git --help` command.
    * `clone` is the subcommand
    * `https://github.com/satish-annigeri/rcdesign.git` is the argument to the subcommand and is assumed to be the repository to be cloned

## Catching Command Line Arguments with `sys.argv`

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
    # You can write other lines here to do what this function is required to do


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

Let us test one last time:
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

An alternative to Typer is the package [Click](https://click.palletsprojects.com/en/stable/). In fact, Typer depends on Click. While requiring a slightly steeper learning curve, Click is versatle and capable compared to Typer. 

### Example with only command line arguments and no subcommands

Let us build a dummy `main()` functions as examples.

A Python script **secprop_cli.py** takes the name of a input file as the first argument and an optional second argument representing the name of an output file.

```py title="secprop_cli.py" linenums="1"
import typer

# Any functions that may be required by main() go here

def main(input: str, output: str | None=None):
    # This is only to demonstrate the use of command line arguments. delete later
    print(f"{input=}, {output=}")

    # Here you can call any functions required to accomplish the given task


if __name__ == "__main__":
    typer.run(main)
```
Execute the application from the command line and ask for the help page.
```doscon
> uv run -- python secprop_cli.app --help
Usage: secprop_cli.py [OPTIONS] INPUT                                          
                                                                                
╭─ Arguments ──────────────────────────────────────────────────────────────────╮
│ *    input      TEXT  [required]                                             │
╰──────────────────────────────────────────────────────────────────────────────╯
╭─ Options ────────────────────────────────────────────────────────────────────╮
│ --output        TEXT                                                         │
│ --help                Show this message and exit.                            │
╰──────────────────────────────────────────────────────────────────────────────╯
> uv run -- python secprop_cli.py sections.csv
input='sections.csv', output=None
> uv run -- python sections,csv --output sections_geomprop.csv
uv run -- python secprop_cli.py sections.csv --output sections_prop.csv
input='sections.csv', output='sections_prop.csv'
```

### Example with subcommands

This example is copied from [Typer documentation](https://typer.tiangolo.com/#an-example-with-two-subcommands), with one change (`Ms. ` from `goodbye()` is deleted).

```py title="greet.py" linenums="1"
import typer

app = typer.Typer()


@app.command()
def hello(name: str):
    print(f"Hello {name}")


@app.command()
def goodbye(name: str, formal: bool = False):
    if formal:
        print(f"Goodbye {name}. Have a good day.")
    else:
        print(f"Bye {name}!")


if __name__ == "__main__":
    app()
```

**Note**

1. The name of the application is `greet.py`
2. Th `greet.py` CLI application has two subcommands, `hello` and `goodbye`
3. Subcommand `hello` takes one argument:
    * Required argument `name`
4. Subcommand `goodbye` takes two arguments:
    * Required argument `name`
    * Optional boolean argument `formal`, which defaults to `False` if not given.

Let us try out this CLI application:

```doscon
> uv run -- python greet.py --help
Usage: greet.py [OPTIONS] COMMAND [ARGS]...                                    
                                                                                
╭─ Options ────────────────────────────────────────────────────────────────────╮
│ --install-completion          Install completion for the current shell.      │
│ --show-completion             Show completion for the current shell, to copy │
│                               it or customize the installation.              │
│ --help                        Show this message and exit.                    │
╰──────────────────────────────────────────────────────────────────────────────╯
╭─ Commands ───────────────────────────────────────────────────────────────────╮
│ hello                                                                        │
│ goodbye                                                                      │
╰──────────────────────────────────────────────────────────────────────────────╯
> uv run -- python greet.py hello Raj
Hello Raj
> uv run -- python greet.py goodbye Raj
Bye Raj!
> uv run -- python greet.py goodbye Raj --formal
Goodbye Raj. Have a good day.
```