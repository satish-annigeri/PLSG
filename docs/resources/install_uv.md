# Installing `uv`

Creating an isolated  (venv) for each project is a good idea as it isolates the version of Python and the packages it uses from those used by other projects. But what if there is a tool that is required by all projects? Should that tool be installed in each project? There are several examples of such tools that are required by all projects, `uv` and `poetry` which are used to manage projects, a host of linters that check the syntax of your code etc.

Assuming either WinGet or Scoop is installed, here are the instructions to install `uv`. Here are instructions to install [WinGet](windows_pkg.md#installing-winget) and [Scoop](windows_pkg.md#installing-scoop).

## Installing using WinGet
With WinGet installed, here are the commands to search for and install `uv`:
``` doscon
> winget search --id astral-sh.uv
Name Id           Version Source
---------------------------------
uv   astral-sh.uv 0.10.8  winget
> winget install astral-sh.uv
```

## Installing using Scoop
Assuming Scoop is installed, here are the commands to search and install `uv` using scoop:
``` doscon
> scoop search uv
Results from local buckets...

Name Version Source Binaries
---- ------- ------ --------
uv   0.10.9  main
> scoop install uv
```

## Installing `pipx`

`pipx` can download and install Python applications in separate environments and make them available system-wise. It can also list applications installed using `pipx`, update them and uninstall them when not required any longer. You can install `pipx` using Python downloaded from the Python download page already installed on your system:
``` dosco
> py -m pip install --user pipx
```
or using Scoop:
``` doscon
> scoop install pipx
```

After installing `pipx` execute the following command:
``` doscon
> pipx ensurepath
```

To install `uv` using `pipx`, follow these instructions:
``` doscon
> pipx install uv
```

To subsequently update `uv`, use the command:
``` doscon
> pipx update uv
```
