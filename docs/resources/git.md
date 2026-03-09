# Using `git`

When working with source code, it is important to maintain older versions of the code as we make changes. This enables rolling back to a previous version if we wish to do so for any reason. You can thus maintain a record of different milestones and branches of your source code as it evolves. Software which help in source code management are essential in software deelopment, and the current popular program to do this is `git`.

## `git` Concepts
When working with `git`, you must know the following concepts:

1. **Local repository** is the source code on your filesystem on the machine you are working on
2. **Remote repository** is the source code stored on a remote server, such as [GitHub](https://github.com)

Now on, I may refer to a **repository** in short as a **repo**.

The typical workflow is as follows:

1. Create an empty repo on GitHub
2. Clone the empty remote repo to a local repo on the machine you are working on
3. Add, delete, modify source code on the local repo, and commit the code as frequently as you feel is useful and necessary
4. At the end of the work session, `push` the local repo to the remote repo

This way, if you continue your work on a different machine, you have to first `clone` the remote repo to the new machine (which must have `git` available on it), make changes to the source code, commit the changes and `push` the changes to the remote repo at the end of the session. After pushing the code to the remote repo, you can even delete the local repo.

It is possible to first write the source code in a local folder, convert it into a Git repo (`git init`) and then push it to a remote repo (after having created a new empty remote repo)

## Installing `git`

On Microsoft Windows, `git` can be installed by downloading it from [Git for Windows](https://gitforwindows.org/). You can also install it using Windows package managers such as WinGet or scoop if you have them installed and know how to use them. Alternately, Git can be installed on Windows using either [WinGet](windows_pkg.md#installing-winget) or [Scoop](windows_pkg.md#installing-scoop).
``` doscon
> winget install git
```
or
``` doscon
> scoop install git
```

On GNU/Linux and macOS, they are usually pre-installed, and if not installed, use the package manager on your operating system to download and install it.

## Configuring `git`

It is necessary to configure `git` once before you start using it.

## Using `git`

The `git` command is fairly complex and has many sub-commands. To learn all the sub-commands, what they do and the corresponding switches, type the following at the prompt
```bash
> git --help
```
This prints the list of sub-commands and their switches.

The most commonly used sub-commands are:

1. `git status` displays the status of the local repo and shows the list of files that are being tracked and whether they have been modified but not commited etc.
2. `git add *.py` stages all files matching the pattern `*.py`  for the next `commit` command
3. `git commit -m "A useful commit message"` commits all staged changes
4. `git push` pushes all commits to the remote repo
5. `git clone https://github.com/satish-annigeri/plsg.git` clones (creates a new local repo) from the remote repo at the specified URL to the local machine. This creates a new folder named plsg in the current working directory and clones the source code from the remote repo to the local repo
6. `git fetch` fetches any changes made to the remote repo to the local repo without updating the source code in the local repo
7. `git pull` fetches  any changes made to the remote repo to the local repo and updates the source code in the local repo

The way `git` knows whether the current working directory is a valid Git repo is by looking for a folder named `.git` and checking its contents to verify that it is indeed a Git repo. If this `.git`  folder does not exist, then it is not a valid Git repo.