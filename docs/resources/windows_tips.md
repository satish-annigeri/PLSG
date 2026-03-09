# Tips for Windows Users

Most Windows users are familiar with installing and using GUI applications. But working with any any programming language, including Python, will require some familiarity with the command line and the operating system shell. For most users on GNU/Linux and macOS this is a routine task and they are familiar with installing applications from Internet repositories and typing commands at he command prompt. But for many Windows users new to programming this is a skill they must master.

This page lists some of the topics to help you become comfortable with the keyboard and the command line. Windows offers two choices for working at he command prompt:

1. Windows Command Prompt, the familiar black window which is inherited from the MS-DOS era of Windows
2. Windows PowerShell, which is Microsoft's attempt to emulate the Unix terminal.

While he PowerShell is more powerful, it also has a learning curve. Learning to use the Command Prompt (`cmd.exe`) is sufficient for th purpose of lerning Python. While it is possible to work entirely with GUI applications such as VS Code, tasks are much faster and easier if you use the Command Prompt.

## Useful keyboard shortcuts
1. ++win+e++ Open Windows File Explorer
2. ++win+r++ Open the _Run_ dialog
3. Pres ++win++ to open the search dialog and type the name of the command or application and see the filtered list of matching entries

## Command Prompt
The Microsoft Windows Command Prompt is the equivalent of the terminal on GNU/Linux or macOS. It is an interactive operating system shell that reads commands typed at the prompt and executes them. Following concepts are useful to know when working with the Command Prompt.

There are several ways to open the Command Prompt:

1. Open the _Run_ dialog by pressing ++win+r++ and type the command `cmd` and press `enter`
2. Open the Windows File Explorer by pressing ++win+e++, navigate to the folder within which you wish to open the command prompt, click within the address bar and type `cmd` and press ++enter++
3. On Windows 10 and Windows 11, click in the search bar and type the command `cmd` and press ++enter++

This opens the usually black window and displays the prompt and the blinking cursor. Anything typed at the prompt is treated as a command, which can be of the following types:

1. Built-in commands, such as, `dir` to list contents of a folder, `cd` to navigate the filesystem etc.
2. External commands, usually stored as files with the extension `.com`, `.exe` or `.bat`. If a location has three files with the same name but the above extensions, the order of priority is `.com`, `.exe` and `.bat`. Thus the command `notepad` results in the Command Prompt searching for a file `notepad.com`, `notepad.exe` or `notepad.bat` in the following locations in that order:
    1. Current working directory
    2. A directory on the `PATH` environment variable, which is explained below.

You can check if a command is available at one of these locations with the command `where`. For example, to check if the command `notepad` is available on your machine, type the command
```bash
> where notepad
```
If the command is available, its full path is printed on the next line.

### File system and file paths
Windows filesystem path consists of two portions:

1. the drive, `C:`, `D:` etc
2. the location within the specified drive relative to the root of that drive, for example `C:\Windows` specifies the location `Windows` one step below the root of `C:` drive.

File system path can be one of:

1. **Absolute path:** Path starting with the drive letter
2. **Relative path:** Path not starting with the drive letter, which automatically assumed to be with reefrence to the current working directory. To know the current working directory when working in the Command Prompt, look at the command prompt or type the command `cd` and press ++enter++.

To navigate the filesystem within the Command Prompt, use the `cd` command, which is short for _Change Directory_. The `cd` command without any arguments prints the current working directory. The command `cd Windows` command navigates to the `Windows` folder, provided it exists. Note that the filesystem path is _relative to the current working directory_. The following points will help you navigate the filesystem:

1. The current directory is specified by `.`, a single dot. There is no need to type the path of the current working directory, it is represented by `.`
2. The parent directory of the current working directory is represented by `..`, two dots. To navigate to the parent of the current working directory (go one step up in the filesystem), type `cd ..`. To navigate to the parent of the parent of the current working directory, type the command `cd ..\..`
3. The root directory of the current drive is repesented by `\`, the backslash. to navigate directly to the root of the current drive, type the command `cd \`
4. To change over to another drive, say drive `D:`, type the drive letter `D:` and press ++enter++

You can list the contents of a directory with the `dir` command. To filter the names you can use `*` to match any number of alphanumeric characters and `?` to match exactly one alphanumeric character. The underscore (`_`) and hyphen (`-`) can be considered alphabets. Anything other than a `*` or `?` are matched verbatim, but case is ignored. Thus to search for all files in the current working directory with the extension `.py`, type thhe command `dir *.py`. To do the same for the parent directory, the command is `dir ..\*.py` and for the root of the current drive, the command is `dir \*.py`. This command searches for files with the extension `.py` in the folder `Documents` on the `D:` drive (assuming the folder exists) `dir D:\Documents\*.py`.

### Environment variables and the `PATH` environment variable.
The Command Prompt being an operating system shell, maintains a list of Environment Variables for its use as well as for the use of the commands invoked from the command line. You can view the list of all the environment variables in the Windows Settings by clicking Settings in the Windows start meny and searching for "environment variables". There are two sets of Environment Variables:
1. System Environment Variables: Available to all users of the operating system
2. User Environment Variables: Environment variables specific to a user in addition to the System Environment variables

One important Environment Variable is the `PATH` environment variable. It is a list of filesystem paths, separated by semi-colons. When a user types a command, the shell looks for the executable file (a file with the same name as the command and the extension `.com`, `.exe` or `.bat` in that order, whichever is found first) corresponding to the typed command by looking for an executable in the following locations, in that order:

1. in the current working directory
2. in the paths listed in the `PATH` environment variable

If the executable is not found in either of the above locations, you get a **command not found** error.

