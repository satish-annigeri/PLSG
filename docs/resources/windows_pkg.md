# Windows Applications

GNU/Linux and macOS have the concept of a central repository of applications and  package managers that can search these repositories, download and install applications from the repository an dupdate installed applications when new versions become available and uninstalling applications when you don't need an application anymore. Debian, Ubuntu and their numerous derivatives use `apt`. macOS uses `brew`. Windows has Microsoft Store. But Microsoft Store has a limited collection of applications and not many of them are Free and Open Source. Note that you can install Python from the Microsoft Store.

There are several tools similar to `apt` and `brew` for Windows and the popular ones are [WinGet](https://learn.microsoft.com/en-us/windows/package-manager/winget/) and [Scoop](https://scoop.sh/). Once one of these is installed, you can search for and install apllications in a way similar to GNU/Linux and macOS. There is a GUI application name [`UniGetUI`](https://www.marticliment.com/unigetui/) that makes it easy to use both `winget` and scoop.

Beginners would find UniGetUI easy to use as it is a GUI application, can access applications from multiple repositories (winget, scoop, chocolatey and many more) and is available for download from [Microsoft Store](https://apps.microsoft.com/detail/XPFFTQ032PTPHF?hl=en-IN&gl=IN&ocid=pdpshare).

This discussion addresses the issue of installing applications for Windows and specifically that of installing `uv`. Following are the tools that can address this issue:

1. [UniGetUI](https://www.marticliment.com/unigetui/) which uses winget, scoop, chocolatey, pip, npm, PowerShell and a few more. Each of these is a package manager that can be used individually. UniGetUI only provides a GUI on top of these individual tools
2. [`pipx`](https://pipx.pypa.io/latest/) can install and run Python applications in isolated environments so that they are available for use like any other executable

The individual package managers, such as scoop, winget, chocolatey have their respective repsitories. Some applications may be available on  more than one source. For UniGetUI to choose applications from multiple sources, these package managers must first be installed.

## Installing PowerShell

The current version is PowerShell 7. Please check which version of PowerShell is installed and update to the current version of PowerShell. You can download and install PowerShell 7 from [Microsoft website](https://learn.microsoft.com/en-us/powershell/scripting/install/install-powershell-on-windows?view=powershell-7.5#msi).

## Installing `winget`
This requires you to use PowerShell, so please ensure you have installed the current version of PowerShell.

[Installation instructions](https://learn.microsoft.com/en-us/windows/package-manager/winget/) to install WinGet. 

You can read the help page of WinGet for some of its important commands:
``` doscon
> winget help
> winget search --help
> winget install --help
> winget list --help
> winget uninstall --help
```
Here are the commands to search for and install `uv`:
``` doscon
> winget search --id astral-sh.uv
Name Id           Version Source
---------------------------------
uv   astral-sh.uv 0.10.8  winget
> winget install astral-sh.uv
```

## Installing scoop
This requires you to use PowerShell, so please ensure you have installed the current version of PowerShell.

Excute the following commands after opeining PowerShell:
``` doscon
> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
> Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
```

You can learn to use scoop with the following commands:
``` doscon
> scoop help
> scoop search
```

Here are the commands to search and install `uv` using scoop:
``` doscon
> scoop search uv
Results from local buckets...

Name Version Source Binaries
---- ------- ------ --------
uv   0.10.9  main
> scoop install uv
```
