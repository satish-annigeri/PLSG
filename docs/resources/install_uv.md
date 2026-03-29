# Installing `uv`

Creating an isolated virtual environment (venv) for each project is good practice, as it keeps the Python version and packages used by one project separate from those used by others. But what about tools that are needed across all projects — should they be installed in each one individually? Common examples of such tools include `uv` and `poetry` for project management, and various linters that check the syntax of your code. These are better installed at the system level, and `uv` is one such tool.

Assuming either WinGet or Scoop is installed, here are the instructions to install `uv`. If you need to install them first, see the instructions for [WinGet](windows_pkg.md#installing-winget) and [Scoop](windows_pkg.md#installing-scoop).

## Installing using WinGet
With WinGet installed, here are the commands to search for and install `uv`:
```doscon
> winget search --id astral-sh.uv
Name Id           Version Source
---------------------------------
uv   astral-sh.uv 0.10.8  winget
> winget install astral-sh.uv
```

To subsequently update `uv`:
```doscon
> winget upgrade astral-sh.uv
```

## Installing using Scoop
With Scoop installed, here are the commands to search for and install `uv`:
```doscon
> scoop search uv
Results from local buckets...

Name Version Source Binaries
---- ------- ------ --------
uv   0.10.9  main
> scoop install uv
```

To subsequently update `uv`:
```doscon
> scoop update uv
```

## Installing `pipx`

`pipx` can download and install Python applications in separate environments and make them available system-wide. It can also list applications installed using `pipx`, update them, and uninstall them when they are no longer needed. You can install `pipx` using Python already installed on your system:
```doscon
> py -m pip install --user pipx
```
or using Scoop:
```doscon
> scoop install pipx
```

After installing `pipx`, execute the following command:
```doscon
> pipx ensurepath
```

To install `uv` using `pipx`:
```doscon
> pipx install uv
```

To subsequently update `uv`:
```doscon
> pipx upgrade uv
```