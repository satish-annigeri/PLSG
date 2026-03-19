# Using `git`

When working with source code, it is important to maintain older versions of the code as changes are made. This makes it possible to roll back to a previous version if needed. You can thus maintain a record of different milestones and branches of your source code as it evolves. Software that helps with source code management is essential in software development, and the current most widely used tool for this is `git`.

## `git` Concepts
When working with `git`, you must know the following concepts:

1. **Local repository** is the source code on your filesystem on the machine you are working on.
2. **Remote repository** is the source code stored on a remote server, such as [GitHub](https://github.com).

For brevity, a **repository** may also be referred to as a **repo**.

The typical workflow is as follows:

1. Create an empty repo on GitHub.
2. Clone the empty remote repo to a local repo on the machine you are working on.
3. Add, delete, and modify source code in the local repo, committing changes as frequently as you find useful.
4. At the end of the work session, `push` the local repo to the remote repo.

This way, if you continue your work on a different machine, you first `clone` the remote repo to the new machine (which must have `git` installed), make changes to the source code, commit the changes, and `push` them to the remote repo at the end of the session. After pushing the code to the remote repo, you can even delete the local repo.

It is also possible to first write the source code in a local folder, convert it into a Git repo using `git init`, and then push it to a remote repo (after having created a new empty remote repo on GitHub).

## Installing `git`

On Microsoft Windows, `git` can be installed by downloading it from [Git for Windows](https://gitforwindows.org/). Alternatively, it can be installed using either [WinGet](windows_pkg.md#installing-winget) or [Scoop](windows_pkg.md#installing-scoop):
``` doscon
> winget install git
```
or
``` doscon
> scoop install git
```

On GNU/Linux and macOS, `git` is usually pre-installed. If it is not, use the package manager on your operating system to install it.

## Configuring `git`

It is necessary to configure `git` once before you start using it. At a minimum, you must set your username and email address, as `git` attaches this information to every commit you make. To do this, type the following commands at the prompt, replacing the name and email address with your own:
```doscon
> git config --global user.name "Your Name"
> git config --global user.email "your_email@example.com"
```

The `--global` flag means these settings apply to all Git repos on your machine. You can verify your configuration at any time with:
```doscon
> git config --list
```

## Using `git`

The `git` command has many sub-commands. To see the full list along with a brief description of each, type the following at the prompt:
```bash
> git --help
```

The most commonly used sub-commands are:

1. `git status` displays the status of the local repo and shows which files are being tracked and whether they have been modified but not yet committed.
2. `git add *.py` stages all files matching the pattern `*.py` for the next `commit`.
3. `git commit -m "A useful commit message"` commits all staged changes.
4. `git push` pushes all commits to the remote repo.
5. `git clone https://github.com/satish-annigeri/plsg.git` creates a new local repo from the remote repo at the specified URL. This creates a new folder named `plsg` in the current working directory and copies the source code from the remote repo into it.
6. `git fetch` fetches any changes made to the remote repo without updating the source code in the local repo.
7. `git pull` fetches any changes made to the remote repo and updates the source code in the local repo.

`git` determines whether the current working directory is a valid Git repo by looking for a folder named `.git` and verifying its contents. If this `.git` folder does not exist, the directory is not a valid Git repo.