# Source Code Management

Software undergoes rapid evolution. Occasionally, a planned improvement may inadvertently break existing functionality, creating a need to roll back to a previous, stable version. This is where Source Code Management (SCM) tools become essential.

An SCM tool allows you to save the current state of your program as a **snapshot**. If future changes cause errors, you can instantly revert the project to a previous working snapshot, abandoning any problematic changes. This capability becomes even more critical when an application is developed by a team, as it ensures the stability of the shared codebase.

## Git

[Git](https://git-scm.com/) is the industry-standard SCM tool. It is a distributed version control system developed by [Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds), the creator of the Linux kernel (which powers the GNU/Linux operating system and Android). Git is designed for speed, data integrity, and support for non-linear workflows, allowing thousands of parallel branches to run simultaneously across different machines.

Because Git is distributed, every contributor maintains their own local version of the software. Developers can make changes to their assigned components and, once finished, **push** those changes to a central **repository**. If multiple developers modify the same file, Git flags these "conflicts" and provides tools to resolve them. This workflow allows submissions to be reviewed, approved, and integrated seamlessly.

While Git is indispensable for teamwork, it is equally valuable for individual developers. A central repository acts as a remote source of truth and a reliable backup, allowing a development environment to be quickly replicated on a new machine if necessary.

## GitHub

While Git is the engine that handles version control, [GitHub](https://github.com) is the platform where that engine lives. Think of GitHub as a cloud-based host for your Git repositories. It provides a central location to store your code online, making it accessible from any computer and easy to share with others.

Beyond simple storage, GitHub acts as a complete project management hub. It offers a suite of collaborative tools, including bug tracking, task management, and "wikis" for documentation. This allows teams to not only manage their code but also manage the entire lifecycle of a project—from the first feature request to the final deployment. While anyone can browse and learn from public repositories, GitHub also provides private spaces for secure, professional development.


## Git Tutorial

### A. The Local Workflow

You do not need a team or even an internet connection to benefit from Git. Even as a solo developer, Git serves as your personal safety net. It allows you to experiment fearlessly, knowing that you can always view your progress or travel back to a version of your code that actually worked.

This workflow focuses on managing your project locally on your own machine.

#### 1. Starting Your Project: The Initialization
Before you can track changes, you have to tell Git to start watching your folder.

* **The Setup (`git init`)**  
  Open your terminal in your project folder and run `git init`. This command transforms a standard folder into a **Local Repository**. From this moment forward, Git is silently watching every file in that folder, ready to take snapshots.

#### 2. The Recording Cycle: Creating Snapshots
To create a version of your work, you follow a two-step process: preparing the changes and then recording them.

* **Step 1: The Compass (`git status`)**  
  As you write code, run `git status` frequently. It is your most important tool; it tells you which files you have modified and whether those changes are currently "staged" or "unstaged."
  
* **Step 2: The Loading Dock (`git add`)**  
  When you reach a small milestone (like finishing a single function), move your changes to the **Staging Area** using `git add <filename>`. This is like placing items in a shipping box, ready to be sealed.

* **Step 3: The Snapshot (`git commit`)**  
  Once your changes are staged, seal the box by running `git commit -m "A descriptive message"`. This creates a permanent snapshot in your local history. You now have a "checkpoint" you can return to at any time.

#### 3. Using the Time Machine: History and Rollbacks
This is where the power of SCM becomes real. If you realize you’ve made a mistake, you don't have to manually undo your typing; you can simply navigate through your history.

* **Viewing Your History (`git log`)**  
  To see all the snapshots you have ever taken, run `git log`. This will display a list of your commits, showing the author, the date, your descriptive message, and a unique ID (a long string of numbers and letters called a **Hash**). This Hash is the "address" of that specific moment in time.

* **Traveling Back in Time (`git checkout`)**  
  If your current code is broken and you want to see how it looked three commits ago, you can "travel" to that version using `git checkout <commit-hash>`. 
  
  *Note: When you do this, your files will physically change on your screen to match that past version. This is a powerful way to inspect old code or recover a specific function you accidentally deleted. To return to the present, simply run `git checkout main` (or the name of your primary branch).*

#### 4. The Next Level: Moving to the Cloud
Once you are comfortable managing your own history and moving through time locally, you are ready to move from a **Local Repository** to a **Remote Repository**.

This is the stage where you create an account on a platform like **GitHub**, create a "Remote Repository" there, and use the `git push` command to upload your local snapshots to the cloud. This provides you with a secondary backup and prepares you for the eventual step of collaborating with others.

#### Summary Cheat Sheet (Local Workflow)
| Command | Purpose | Analogy |
| :--- | :--- | :--- |
| `git init` | Turn a folder into a Git repo | Building the time machine |
| `git status` | See what has changed | Checking your coordinates |
| `git add` | Prepare changes for a snapshot | Placing items in the shipping box |
| `git commit` | Permanently save a snapshot | Sealing and labeling the box |
| `git log` | View the list of all snapshots | Reading the history book |
| `git checkout` | Travel to a previous snapshot | Stepping into the time machine |

Since authentication is often the most frustrating "roadblock" for new developers (because Git will reject your normal GitHub password), it is best placed in the **"Moving to the Cloud"** section, right at the moment they attempt their first `git push`.

Here is the updated **Moving to the Cloud** section, including the "Digital Handshake" (authentication) requirement.

***

### B. Moving to the Cloud: Remote Repositories & GitHub

Up until now, your "time machine" has existed only on your own computer. This is great for experimenting, but it carries two major risks:
1.  **The Hardware Risk:** If your laptop is lost, stolen, or suffers a hard drive failure, your entire project history vanishes with it.
2.  **The Portability Problem:** If you move to a new computer, you have to manually move all your files via USB or email, which is slow and error-prone.

To solve this, we use a **Remote Repository**. By "pushing" your code to a platform like GitHub, you create a cloud-based backup and a "master version" that can be instantly downloaded to any machine.

#### 1. Setting up your GitHub Account
If you don't have one yet, head to [GitHub.com](https://github.com) and sign up for a free account. Once you're in, you have access to a secure place to host your work and a global community of developers.

#### 2. Connecting your Local Project to GitHub
Connecting your existing local project to GitHub is a three-step process. **Crucial Tip:** For the sake of organization, ensure the name you give your repository on GitHub matches the name of your project folder on your computer.

##### Step A: Create the "Empty Shell" on GitHub
Once logged in, click the **"+"** icon in the top right and select **"New repository."**

*   **Repository Name:** Enter your project name (e.g., `my-first-project`).
*   **Public/Private:** Choose "Private" if you want to keep your code hidden.
*   **IMPORTANT:** Do **NOT** check the boxes for "Add a README file," "Add .gitignore," or "Choose a license." We want a completely empty repository to avoid conflicts with your local history.

##### Step B: The "Handshake" (Linking Local to Remote)
Now, go back to your terminal in your local project folder. You need to tell your local Git the "address" of your new GitHub repository. Copy the URL provided on your GitHub repository page and run:

`git remote add origin <PASTE_YOUR_URL_HERE>`

##### Step C: The First Upload (`git push`)
Now that the link is established, attempt to send your snapshots to the cloud:

`git push -u origin main`

#### 3. The Digital Handshake: Authenticating your Terminal
When you run that first `git push`, you will hit a security gate. GitHub will ask you to prove that you are actually the owner of the account.

**Important: For security reasons, GitHub no longer accepts your standard account password when you are using the Terminal.** 

Instead, you must use a **Personal Access Token (PAT)**. Think of this as a long, highly secure password designed specifically for your computer to use.

1.  **Generate the Token:** On GitHub, go to your **Settings** $\rightarrow$ **Developer Settings** $\rightarrow$ **Personal Access Tokens** $\rightarrow$ **Tokens (classic)**. 
2.  **Create New Token:** Click "Generate new token," give it a name (like "My Laptop"), and select the checkbox for `repo` (this gives the token permission to manage your code).
3.  **Copy the Token:** GitHub will show you a long string of characters. **Copy this immediately and save it somewhere safe.** You will never see it again once you leave that page.
4.  **Use the Token:** When your terminal asks for your "Password," **paste the token instead of your actual password.** 

*(Note: When pasting in the terminal, you won't see any characters moving—this is a security feature. Just paste it and hit Enter.)*

#### 4. The "New Machine" Workflow: Cloning
Now that your code is safely on GitHub, imagine you just bought a brand-new computer. You don't need to move files manually. You simply "Clone" the environment.

On your new machine, open a terminal and run:

`git clone <URL_OF_YOUR_GITHUB_REPO>`

In seconds, Git will reach out to GitHub, download your entire project, and—most importantly—**restore your entire history of snapshots.** You are instantly caught up and ready to work exactly where you left off.

#### Summary of the Remote Workflow
| Scenario | Action | Command |
| :--- | :--- | :--- |
| **First time connecting** | Tell local Git where GitHub is | `git remote add origin <URL>` |
| **First time uploading** | Send all local history to GitHub | `git push -u origin main` |
| **Daily work** | Send new snapshots to GitHub | `git push` |
| **New computer** | Download everything from GitHub | `git clone <URL>` |

### C. Best Practices & Pro-Tips

As you begin your journey with Git, keep these practical tips in mind to avoid common pitfalls and streamline your workflow.

#### 1. Watch for Automatic Initialization
If you are using modern Python tools like `uv` to manage your projects, you might find that Git is already running. When you run `uv init`, the tool typically initializes a Git repository for you automatically. If you see a `.git` folder in your directory, there is no need to run `git init` again.

#### 2. Leverage Your Code Editor (GUI)
While learning the command line is essential, you don't always have to type. Most professional code editors, such as **VS Code**, have built-in Git integration. They can visually show you which lines have changed and provide buttons for `add`, `commit`, `push`, and `pull`. Using a Graphical User Interface (GUI) is a great way to "see" your changes visually before you commit them.

#### 3. The Golden Rule of Committing: "Logical Milestones"
A common question is: *"How often should I commit?"* 

Avoid committing every single time you type a line of code, but also avoid waiting until the end of the day. Instead, **commit when you reach a logical milestone.** A milestone is a point where your code is in a stable state—for example, after you have successfully finished a new function or fixed a specific bug. If you feel, *"If I break this next part, I'll want to be able to go back to exactly how it looks right now,"*—**that is your cue to commit.**

#### 4. Syncing Across Machines
Remember that a `commit` only saves your work to your **local** machine. If you work on a project at your office and then move to your home computer, your changes will not be there unless you have **pushed** them to GitHub. Always make it a habit to `push` your work at the end of a session to ensure your cloud backup is up to date.

#### 5. Write Meaningful Messages
A commit without a good message is a gift to your "future self" that you will eventually regret. If you find yourself typing vague messages like `git commit -m "update"` or `git commit -m "fix"`, stop. It means you haven't reached a clear milestone yet. Wait until you can clearly describe **what** was changed and **why**.

#### 6. Pro-Tip: Viewing a Clean History
If you want to quickly scan your history without the clutter of long metadata, use this command in your terminal:

`git log --pretty="%H %s"`

This will show you a concise list of the unique Commit Hash (the ID) followed by your commit message. 

*(Note: When typing this command, ensure there are no spaces around the `=` sign, or the command will fail.)*

#### 7. The Golden Rule of Security: Never Push Secrets
This is the most important rule in modern development. **Never, ever commit sensitive information to a public repository.** This includes API keys, database passwords, or private credentials. 

* **The Risk:** There are automated bots constantly scanning GitHub for these strings. If you push a password to a public repo, it is considered compromised within seconds. 
* **The Solution:** Use "Environment Variables" or `.env` files to store secrets, and ensure those files are listed in your `.gitignore` so they are never tracked by Git.

#### 8. Use a `.gitignore` File (Your Repository Filter)
As you work, your computer creates many "junk" files that aren't actually part of your source code—things like temporary cache files (`__pycache__`), local virtual environments (`.venv`), or system files (`.DS_Store`). 

* **The Solution:** Create a file named `.gitignore` in your project folder. Inside this file, list the names of files or folders you want Git to ignore. This keeps your repository "clean" and ensures that only your actual code is being tracked and shared.

#### 9. Don't Panic During a Merge Conflict
If you see a message saying a "Merge Conflict" has occurred, do not panic. This is not a sign that you have broken the software; it is simply Git saying, *"I see two different versions of this line, and I don't want to guess which one is right."*

* **The Mindset:** A conflict is just a request for human intervention. Git has paused the process to let you look at the code, decide which version to keep (or how to combine them), and then move forward. It is a safety feature, not an error.

#### 10. Git is for Code, Not Big Data
Git is designed to track changes in text files (source code). It is remarkably efficient at this. However, it is **not** designed to version-control massive datasets, large CSV files, or high-resolution images. 

* **The Problem:** If you try to commit a 500MB dataset, your repository will become incredibly slow, and pushing/pulling will become a nightmare. For large data files, consider using dedicated data management tools or cloud storage rather than Git.