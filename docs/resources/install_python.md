# Installing Python

## Installing from Python Download Page

**Note: This method is recommended only when you are unable to install `uv`.**

You can install Python from the [Python download page](https://www.python.org/download). Take care to choose the correct platform (Windows, GNU/Linux distribution or macOS). The download page detects your platform and chooses the correct download file for you, but you can verify it is correct before you download. On GNU/Linux distributions and macOS, it is a better to use the package manager instead of downloading and installing the binary from the Python download page.

However, for Windows it is a good idea to download the install file from the Python download page and when installing, remeber to install the Python Launcher. With Python Launcher installed, you can list the different versions of Python installed and choose a specific version at the time of creating a virtual environment. You can download and install as many versions of Python as you need. Here are the help pages for some important commands.

``` doscon
> py help
> py help list
> py help install
```

You can choose a specific Python version that is installed on your machine at the time of creating a new virtual environment. Once a virtual environment is created, this is the workflow:

1. Activate the virtual environment (venv) you wish to work in
2. Install, uninstall or update a package into the active venv using the `pip` command
3. Work within the venv using the REPL or IDE
4. Deactivate the venv when you are done working with the project

Remember, `python` and `pip` commands affect only the currently active venv and has no effect on any other venv. When using this approach, it is important to remember which packages are required by your project. It is command practice to create a `requirements.txt` file containg the names of the required packages, one package name per line. This helps `pip` command to download and install them in one go.

Assuming Python Launcher is installed along with Python version 3.14, an dyou are currently in the project folder inside which you wish to create the venv, this is how you can create, activate and deactivate a venv:

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

1. You must be within the project folder before creating the venv
2. The venv is named `.venv` in this above example, but that is the convention. You can choose a different name if you wish
3. Execute the `activate` command as shown in the above example and once activated, the prompt is prefixed with the name of the venv, `.venv` in this case
4. The command to update the version of `pip` is required only if you wish to upgrade the installed `pip` to the most recent version. It can be skipped if you do not wish to upgrade `pip`.
5. The package `marimo` is used as an example. Replace marimo with the name of the package you wish to install
6. Execute the `deactivate` command to deactivate the venv, and when you do so, the prompt changes and the prefix `.venv` disappears

## Installing Python using `uv`

Using [`uv`](https://docs.astral.sh/uv/) is the preferred method of managing a Python project. It brings several operations under a single tool instead of using different tools for the individual steps. The major tasks in managing a Python projec are:

1. Create a Virtual Environment for the project, isolated from the rest of the projects you may be working on at the same time
2. Add, remove and update packages required by your project
3. Easily recreate the entire environment required by the project on a different machine
4. Build a package from your code ready for sharing it with others on [PyPI](https://pypi.org/), the Python repository of packages and upload it to the repository


### Installing `uv`

Visit the `uv` [installation documentation page](https://docs.astral.sh/uv/getting-started/installation/) and read the instructions specific to your operating system.

=== "Windows"

    1. Open Windows PowerShell
    2. Copy and paste the command from the `uv` download page

    ``` bash
    PS> powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
    ```
    Close the PowerShell and open the Command Prompt. Then check if `uv` has been installed successfully by typing the following commands
    ``` bash
    > uv -V
    > uv --help
    ```
    If your see the version of `uv` displayed by the first command and the help page displayed by the second command, the installation is successful.
    
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
    Close the PowerShell and open the Command Prompt. Then check if `uv` has been installed successfully by typing the following commands
    ``` bash
    $ uv -V
    $ uv --help
    ```
    If your see the version of `uv` displayed by the first command and the help page displayed by the second command, the installation is successful.

### Installing Python

With `uv` installed, you can check the versions of Python available for download with the command
``` bash
> uv python list
```
In the list displayed, look for output similar to <br>
`cpython-3.14.3-windows-x86_64-none   <download available>`<br>
or<br>
`cpython-3.14.3-windows-x86_64-none   C:\Users\xyz\AppData\Local\Python\binpython3.exe`.

The first line indicates that Python 3.14.3 is available for download but is not currently installed on your machine. The second line indicates that Python 3.14.3 is installed on your machine.

To install an available Python version, type the following command atthe prompt
``` doscon
> uv python install --help
> uv python install 3.14.3
```
The first command displays the help page corresponding the the sub-command `python install` and the second command installs Python 3.14.3 if it is available for download.

It is possible to download and install multiple versions of Python on your machine if different projects you are working on require this. This situation may arise because a package you wish to use requires a specific version of Python.

While multiple versions of Python may be installed on your machine, it is necessary to activate the specific version you wish to use for a specific project. This is accomplished by activating the required version required by the project. Correspondingly, it is a good idea to deactivate the selected version of Python when you finish working on a project or wish to switch to another project that requires a different version of Python.

In fact, `uv` makes it unnecessary by automatically activating the required version of Python if you use the `uv run -- <command>` from within an initialized `uv` project folder instead of first activating the virtual environment (venv) and typing `<command>`. For this to work smoothly, follow these steps:

### Initializing a project

=== "Creating a New Project"

    1. Create a new folder for the project with a suitably selected short name `mkdir myprj`
    2. Navigate into the newly created folder `cd myprj`
    3. Initialize the project `uv init` (if you wish to use the latest version of Python installed on your machine) or `uv init -p 3.14.3` (if you wish to use a specific version of Python. if the specified version of Python is not currently installed on your machine, it will be installed the next time you add a package to your project or `sync` the project with `uv sync`)
    4. This will create the following files in your project folder:
        * `.python-version` with the version of Python to be used by the project
        * `pyproject.toml` the project configuration file that will list the packages installed for your project
    5. Once you add a package, the name of the added package will be listed in the `pyproject.toml` file and a file `uv.lock` with the specific version number of the installed package is created. These files help in porting your project to a different machine.

=== "Cloning a Project from GitHub/GitLab"

    If you clone a repo from GitHub or GitLab, the `.git` folder will be automatically created and complete version history becomes available in your local repo. You can then check to see if the folder contains `.python-version` and `pyproject.toml` are present. If they are present, you only have to `sync` the project with the command `uv sync`.

    If these files are not available, then you can initialize the project and add the packages similar to when working with a new project folder.

    If a file with the name `requirements.txt` is available, it usually lists the packages required by the project and you can add them to your project with the command<br>`> uv pip install -r requirements.txt`

!!! note "What is a project?"

    A project is a folder containing the files related to one specific task. A typical project has the `,git` folder for source code version control, a `pyproject.toml` file and if it is a `uv` project, then the `.python-version` file and `uv.lock` file if packages are added to the project using `uv`. Except for `pyproject.toml`, the others are not necessary but are useful. Usually the source code is in a separate sub-folder within the project folder.

### Adding a package to a project

Adding a package required by your project requires you to know the name of the package, and sometimes, the specific version of the package you wish to install. The `uv` command to add a package is `uv add <package>`. To read the help for this command, type `uv add --help`. Thus, to add the package `numpy`, type the following command
``` doscon
> uv add numpy
> uv pip list
> type pyproject.toml
```
The first command installs the package `numpy` compatible with the version of Python used by your project (as indicated by the `.python-version` file). The second command lists all packages installed for your prject. The third command displays the contents of `pyproject.toml` file and the name of the package must show up as
``` doscon
dependencies = [
    "numpy>=x.y.z",
]
```
where `x.y.z` is the version of `numpy` that was installed.

!!! note
    The `pyproject.toml` file lists only those packages added by you while the list of packages displayed by `uv pip list` is usually longer, because the packages added by you may depend on other required packages.

### Activating the Virtual Environment

If your project has been correctly initialized and the `.git` folder, `.python-version` file and `pyproject.toml` file are present, there is no need to activate the project, but the commands must be typed as `uv run -- <command>`.

However, if you insist on manually activating and deactivating the venv, and wish to directly type the command at the prompt as `<command>`, then this is how you do it:

=== "Windows"

    ``` doscon
    > .venv\Script\activate
    ```

=== "GNU/Linux or macOS"

    ``` bash
    $ source .venv/bin/activate
    ```

If the `.venv` is successfully activated, the name of the project enclosed within parantheses will appear to the left of the prompt. You can deactivate the `.venv` by typing the command"
=== "Windows"

    ``` doscon
    > deactivate
    ```

=== "GNU/Linux or macOS"

    ``` bash
    $ deactivate
    ```

Deactivating the venv is important to keep them isolated from one another.

