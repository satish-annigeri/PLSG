# Tips for Windows Users

Most Windows users are familiar with installing and using GUI applications. However, working with any programming language, including Python, requires some familiarity with the command line and the operating system shell. For users on GNU/Linux and macOS this tends to be a routine task, but for many Windows users who are new to programming it is a skill that needs to be picked up along the way.

This page covers some topics to help you get comfortable with the keyboard and the command line. Windows offers two choices for working at the command prompt:

1. Windows Command Prompt, the familiar black window that has been part of Windows since the MS-DOS era
2. Windows PowerShell, which is Microsoft's attempt to emulate the Unix terminal

While PowerShell is more powerful, it also has a steeper learning curve. Learning to use the Command Prompt (`cmd.exe`) is sufficient for the purpose of learning Python. You can open it by searching for **Command Prompt** in the Start menu. While it is possible to work entirely with GUI applications such as VS Code, many tasks are faster and easier from the Command Prompt.

## Useful keyboard shortcuts
1. ++win+e++ Open Windows File Explorer
2. ++win+r++ Open the _Run_ dialog
3. Press ++win++ to open the search dialog and type the name of the command or application to see a filtered list of matching entries

## Command Prompt
The Microsoft Windows Command Prompt is the equivalent of the terminal on GNU/Linux or macOS. It is an interactive operating system shell that reads commands typed at the prompt and executes them. The following concepts are useful to know when working with the Command Prompt.

There are several ways to open the Command Prompt:

1. Open the _Run_ dialog by pressing ++win+r++ and type the command `cmd` and press `enter`
2. Open the Windows File Explorer by pressing ++win+e++, navigate to the folder within which you wish to open the command prompt, click within the address bar and type `cmd` and press ++enter++
3. On Windows 10 and Windows 11, click in the search bar and type the command `cmd` and press ++enter++

This opens the usually black window and displays the prompt and the blinking cursor. Anything typed at the prompt is treated as a command, which can be of the following types:

1. Built-in commands, such as, `dir` to list contents of a folder, `cd` to navigate the filesystem etc.
2. External commands, usually stored as files with the extension `.com`, `.exe` or `.bat`. If a folder contains three files with the same name but these different extensions, the order of priority is `.com`, `.exe` and `.bat`. Thus the command `notepad` results in the Command Prompt searching for a file `notepad.com`, `notepad.exe` or `notepad.bat` in the following locations in that order:
    1. Current working directory
    2. A directory on the `PATH` environment variable, which is explained below.

You can check if a command is available at one of these locations with the command `where`. For example, to check if the command `notepad` is available on your machine, type:
```bash
> where notepad
```
If the command is found, its full path is printed on the next line. If it is not found, an error message is displayed instead.

### File system and file paths
A Windows filesystem path consists of two portions:

1. the drive, `C:`, `D:` etc.
2. the location within the specified drive relative to the root of that drive — for example `C:\Windows` specifies the location `Windows` one step below the root of the `C:` drive.

A filesystem path can be one of:

1. **Absolute path:** A path starting with the drive letter.
2. **Relative path:** A path not starting with the drive letter, which is automatically assumed to be relative to the current working directory. To know the current working directory when working in the Command Prompt, look at the command prompt or type the command `cd` and press ++enter++.

To navigate the filesystem within the Command Prompt, use the `cd` command, which is short for _Change Directory_. The `cd` command without any arguments prints the current working directory. The command `cd Windows` navigates to the `Windows` folder, provided it exists. Note that the filesystem path is _relative to the current working directory_. The following points will help you navigate the filesystem:

1. The current directory is represented by `.`, a single dot. There is no need to type the full path of the current working directory — it is simply `.`
2. The parent directory of the current working directory is represented by `..`, two dots. To navigate to the parent of the current working directory (go one step up in the filesystem), type `cd ..`. To navigate two levels up, type `cd ..\..`
3. The root directory of the current drive is represented by `\`, the backslash. To navigate directly to the root of the current drive, type `cd \`
4. To switch to another drive, say drive `D:`, type the drive letter `D:` and press ++enter++

You can list the contents of a directory with the `dir` command. To filter results, you can use `*` to match any sequence of characters and `?` to match exactly one character. Anything other than a `*` or `?` is matched verbatim, but case is ignored. For example, to list all files in the current working directory with the extension `.py`, type `dir *.py`. To do the same for the parent directory, the command is `dir ..\*.py`, and for the root of the current drive, `dir \*.py`. To search for files with the extension `.py` in the folder `Documents` on the `D:` drive (assuming the folder exists), the command is `dir D:\Documents\*.py`.

### Environment variables and the `PATH` environment variable
The Command Prompt, being an operating system shell, maintains a list of environment variables for its own use as well as for the use of commands invoked from the command line. You can view all environment variables in Windows Settings by opening the Start menu and searching for "environment variables". There are two sets of environment variables:

1. **System environment variables:** Available to all users of the operating system.
2. **User environment variables:** Specific to a particular user, in addition to the system environment variables.

!!! note
    One important environment variable is `PATH`. It is a list of filesystem paths separated by semicolons. When a user types a command, the shell searches for an executable file (a file with the same name as the command and the extension `.com`, `.exe` or `.bat`, in that order) in the following locations:

    1. The current working directory
    2. Each path listed in the `PATH` environment variable, in order

    If the executable is not found in any of these locations, you get a **command not found** error.

