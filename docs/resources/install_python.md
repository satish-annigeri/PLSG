# Installing Python

## Installing from Python Download Page

**Note: I would recommended this method only if you are unable to install `uv`.**

You can install Python from the [Python download page](https://www.python.org/download). Take care to choose the correct platform (Windows, GNU/Linux or macOS). The download page detects your platform and suggests the correct download file, but it is worth verifying before you proceed. On GNU/Linux and macOS, it is better to use the system package manager rather than downloading the binary from the Python download page.

For Windows, however, it is a good idea to download the installer from the Python download page and, when installing, remember to include the Python Launcher. With the Python Launcher installed, you can list the different versions of Python installed on your machine and choose a specific version when creating a virtual environment. You can download and install as many versions of Python as you need. Here are the help pages for some important commands:
``` doscon
> py help
> py help list
> py help install
```

You can choose a specific Python version installed on your machine when creating a new virtual environment. Once a virtual environment is created, the typical workflow is:

1. Activate the virtual environment (venv) you wish to work in
2. Install, uninstall or update packages in the active venv using the `pip` command
3. Work within the venv using the REPL or IDE
4. Deactivate the venv when you are done working with the project

Remember, the `python` and `pip` commands affect only the currently active venv and have no effect on any other venv. When using this approach, it is important to keep track of which packages your project requires. It is common practice to create a `requirements.txt` file containing the names of the required packages, one per line. This allows `pip` to download and install them all in one go.

Assuming the Python Launcher is installed along with Python 3.14, and you are currently in the project folder within which you wish to create the venv, here is how you can create, activate and deactivate a venv:
``` doscon
> py -3.14 -m venv .venv
> .venv\Scripts\activate
(.venv) > python -V
(.venv) > pip -V
(.venv) > python -m pip install -U pip
(.venv) > pip install marimo
(.venv) > pip install -U marimo
(.venv) > deactivate
>
```

Note the following:

1. You must be within the project folder before creating the venv.
2. The venv is named `.venv` in the above example, which is the convention. You can choose a different name if you wish.
3. Execute the `activate` command as shown above. Once activated, the prompt is prefixed with the name of the venv — `.venv` in this case.
4. The command to update `pip` is only needed if you wish to upgrade it to the most recent version. It can be skipped otherwise.
5. The package `marimo` is used as an example. Replace it with the name of the package you wish to install.
6. Execute the `deactivate` command to deactivate the venv. Once deactivated, the `.venv` prefix disappears from the prompt.

## Installing Python using `uv`

Using [`uv`](https://docs.astral.sh/uv/) is the preferred method of managing a Python project. It brings several operations under a single tool instead of requiring different tools for each individual step. The major tasks in managing a Python project are:

1. Create a virtual environment for the project, isolated from other projects you may be working on.
2. Add, remove and update packages required by your project.
3. Easily recreate the entire project environment on a different machine.
4. Build a package from your code, ready for sharing on [PyPI](https://pypi.org/), and upload it to the repository.

### Installing `uv`

Visit the `uv` [installation documentation page](https://docs.astral.sh/uv/getting-started/installation/) and follow the instructions for your operating system.

=== "Windows"

    1. Open Windows PowerShell
    2. Copy and paste the command from the `uv` download page
    ``` doscon
        PS> powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
    ```
    Close PowerShell and open the Command Prompt.
    
=== "GNU/Linux and macOS"

    1. Open the terminal
    2. Copy and paste the command from the `uv` download page
    ``` bash
        $ curl -LsSf https://astral.sh/uv/install.sh | sh
    ```
    or
    ``` bash
        $ wget -qO- https://astral.sh/uv/install.sh | sh
    ```
    Close the terminal and reopen it.


You can now check if `uv` has been installed successfully by typing the following commands:
``` bash
$ uv -V
$ uv --help
```

If you see the version of `uv` displayed by the first command and the help page displayed by the second, the installation is successful.

### Installing Python

With `uv` installed, you can check the versions of Python available for download with the command:
``` bash
> uv python list
```
In the list displayed, look for output similar to <br>
`cpython-3.14.3-windows-x86_64-none   <download available>`<br>
or<br>
`cpython-3.14.3-windows-x86_64-none   C:\Users\xyz\AppData\Local\Python\binpython3.exe`

The first line indicates that Python 3.14.3 is available for download but is not currently installed on your machine. The second line indicates that it is already installed.

To install an available Python version, type the following commands at the prompt:
``` doscon
> uv python install --help
> uv python install 3.14.3
```
The first command displays the help page for the `python install` sub-command and the second installs Python 3.14.3 if it is available for download.

It is possible to install multiple versions of Python on your machine if different projects require different versions. This situation may arise when a package you wish to use requires a specific version of Python.

While multiple versions of Python may be installed, you need to activate the specific version required by each project. It is equally important to deactivate it when you finish working on the project or wish to switch to another that requires a different version.

In practice, `uv` makes this unnecessary by automatically activating the required version of Python when you use `uv run -- <command>` from within an initialised `uv` project folder, instead of manually activating the venv and typing `<command>` directly. For this to work smoothly, follow these steps:

### Initializing a project

=== "Creating a New Project"

    1. Create a new folder for the project with a suitably chosen short name: `mkdir myprj`
    2. Navigate into the newly created folder: `cd myprj`
    3. Initialise the project with `uv init` (to use the latest version of Python installed on your machine) or `uv init -p 3.14.3` (to use a specific version). If the specified version is not currently installed, it will be installed the next time you add a package or run `uv sync`.
    4. This will create the following files in your project folder:
        * `.python-version` — records the version of Python to be used by the project
        * `pyproject.toml` — the project configuration file that lists the packages installed for your project
    5. Once you add a package, its name will appear in `pyproject.toml` and a file `uv.lock` will be created with the specific version number of the installed package. These files help in reproducing your project environment on a different machine.

=== "Cloning a Project from GitHub/GitLab"

    If you clone a repo from GitHub or GitLab, the `.git` folder will be automatically created and the complete version history will be available in your local repo. Check whether the folder contains `.python-version` and `pyproject.toml`. If they are present, you only need to run `uv sync` to set up the environment.

    If these files are not present, you can initialise the project and add packages as you would for a new project folder.

    If a `requirements.txt` file is present, it typically lists the packages required by the project and you can add them with the command:<br>`> uv pip install -r requirements.txt`

!!! note "What is a project?"

    A project is a folder containing all the files related to one specific program. A typical project has the `.git` folder for source code version control, a `pyproject.toml` file, and if it is a `uv` project, a `.python-version` file and a `uv.lock` file if packages have been added using `uv`. Except for `pyproject.toml`, the others are not strictly necessary but are very useful. The source code is usually kept in a separate sub-folder within the project folder.

### Adding a package to a project

Adding a package to your project requires you to know its name, and sometimes the specific version you need. The `uv` command to add a package is `uv add <package>`. To read the help for this command, type `uv add --help`. To add the package `numpy`, for example, type the following commands:
``` doscon
> uv add numpy
> uv pip list
> type pyproject.toml
```
The first command installs `numpy` in a version compatible with the Python version used by your project (as specified in `.python-version`). The second command lists all packages installed for your project. The third command displays the contents of `pyproject.toml`, where the package should appear as:
``` doscon
dependencies = [
    "numpy>=x.y.z",
]
```
where `x.y.z` is the version of `numpy` that was installed.

!!! note
    The `pyproject.toml` file lists only the packages you have explicitly added, while the list displayed by `uv pip list` is usually longer, because the packages you added may themselves depend on other packages.

### Activating the Virtual Environment

If your project has been correctly initialised and the `.git` folder, `.python-version` file and `pyproject.toml` file are present, there is no need to manually activate the venv — provided you prefix your commands with `uv run --`.

However, if you prefer to manually activate and deactivate the venv and type commands directly at the prompt, here is how to do it:

=== "Windows"
    ``` doscon
        > .venv\Scripts\activate
    ```

=== "GNU/Linux or macOS"
    ``` bash
        $ source .venv/bin/activate
    ```

If the `.venv` is successfully activated, the name of the project enclosed in parentheses will appear to the left of the prompt. To deactivate the `.venv`, type:

=== "Windows"
    ``` doscon
        > deactivate
    ```

=== "GNU/Linux or macOS"
    ``` bash
        $ deactivate
    ```

Deactivating the venv is important to keep project environments isolated from one another.
