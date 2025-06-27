# Git Version Control

## 1. Introduction to Git

Git is a distributed version control system (DVCS). Each developer has a full local copy of the entire project history, so you don't rely on a single central server. Git tracks changes over time, showing who made each change and allowing you to revert to previous versions if needed.

* **Tracking changes:** Git saves snapshots of your project, so you can compare versions and undo changes if something breaks.
* **Collaboration:** Multiple people can work on the same project concurrently. Git helps merge everyone's changes without conflict.
* **Branching:** You can create branches to develop features or fixes in isolation. Merging branches back keeps the main codebase stable.
* **Experimentation:** Try new ideas safely. If an experimental branch doesn’t work out, you can discard it without affecting the stable code.
* **Industry standard:** Git is the most commonly used version control system in software development. Learning Git is essential for any developer.


## 2. Centralized vs. Distributed Version Control

Version control systems manage project history. **Centralized** systems (like SVN) use a single server for all files and history. Developers check out files, make changes, and check them back in. **Distributed** systems (like Git) give every developer a full repository copy on their machine.

* **Centralized (SVN):** Pros: simpler to understand. Cons: if the server goes down, work halts; slower since many commands need the server.
* **Distributed (Git):** Pros: faster local operations, works offline, very robust (any clone has full history). Cons: more complex initially.

Git's distributed model means you can work and commit offline and then sync when you're online. Your clone even serves as a backup of the whole project.


## 3. Installing and Configuring Git


**Recap**: Git is a distributed version control system that tracks project changes, enables collaborative development through branching/merging, and preserves historical versions for safety.  

## Homework (Rocky Linux):  
1. **Install Git**  
```bash
sudo dnf install git -y
```  

2. **Verify Installation**  
```bash
git --version
```  

3. **Configure Identity**  
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```  

4. **Create Test Repository**  
```bash
mkdir ~/git-lab && cd ~/git-lab
git init
echo "# Git Test Project" > README.md
git add .
git commit -m "Initial commit"
```  

**Email submission**:  
- **Subject**: `HW1 – Git Installation – [Your Name]`  
- **Body**:  
  1. Git version from `git --version`  
  2. Your configured name/email  
  3. Output of `git log --oneline` in ~/git-lab 

## 4. Initializing a Repository and File States

To start tracking a project with Git, navigate to your project’s folder and run:

```
git init
```

This creates a `.git` directory and starts a new Git repository. Now Git will track changes to files in this folder.

There are three important "states" for files in Git:

* **Working Directory (Untracked):** Your actual project files. New files are **untracked** until you tell Git about them.
* **Staging Area (Staged):** When you run `git add <file>`, you move changes from the working directory to the staging area, preparing them for a commit.
* **Repository (Committed):** When you run `git commit`, Git takes everything in the staging area and saves it as a snapshot in the repository.

  ![deepseek_mermaid_20250626_25d0bc](https://github.com/user-attachments/assets/decd4238-37b1-48e1-92a0-e8115daf10c3)


Use `git status` to see which files are untracked, modified, or staged. It’s very helpful to see what’s going on.

## Homework:  
1. Create repository and file:  
```bash  
mkdir ~/rocky-git-lab && cd ~/rocky-git-lab  
git init  
echo "1. Learn Git states" > tasks.txt  
```  

2. Verify file state:  
```bash  
git status  
```  

**Email submission**:  
- **Subject**: `HW2 – Initializing a Repository and File States – [Your Name]`  
- **Body**:  
  a) Full output of `git status`  
  b) Why `tasks.txt` appears as untracked  
  c) Command to transition it to staged state


## 5. Ignoring Files with .gitignore

Some files should not be tracked by Git (for example, compiled binaries, log files, or personal notes). Create a file named `.gitignore` in the root of your project to list patterns for files Git should ignore.

Common patterns:

* `*.log` to ignore all `.log` files.
* `build/` to ignore a directory named `build`.
* `secret.txt` to ignore a specific file.

Add and commit the `.gitignore` file to share it with others. After adding patterns, `git status` will no longer list those ignored files.

## Homework:  
1. **Create files to ignore**:  
```bash  
cd ~/rocky-git-lab  
echo "Personal notes" > notes.txt  
touch cache.tmp output.tmp  
```  

2. **Create .gitignore with Vim**:  
```bash  
vim .gitignore  
```  
*Follow these steps in Vim*:  
```text  
i                  # Enter Insert Mode  
*.tmp<Enter>       # Pattern 1  
notes.txt<Enter>   # Pattern 2  
build/<Esc>        # Pattern 3, then Normal Mode  
:wq<Enter>         # Write and quit  
```  

3. **Verify exclusion**:  
```bash  
git status --ignored  
```  

**Email submission**:  
- **Subject**: `HW5 – .gitignore – [Your Name]`  
- **Body**:  
  a) Output of `cat .gitignore`  
  b) `git status --ignored` output  
  c) Vim commands used to create the file 


## 6. Staging and Committing Changes

To include changes in your next snapshot, you first add them to the staging area with `git add`. For example:

```
git add <filename>
git add .       # stage all changes in current directory
```

After staging, create a commit with a message:

```
git commit -m "Describe the changes"
```

This saves the staged changes in the repository as a new snapshot.

**Commit message tips:**

* Keep it short but descriptive (e.g., "Fix login bug").
* Use present tense (e.g., "Add feature" instead of "Added feature").
* For longer explanations, omit `-m` and write a multi-line message (the first line is a summary).

 
**Recap**: Use `git add` to stage changes and `git commit` to save snapshots. Vim is essential for creating and modifying files before committing.  

## Homework:  
1. **Create file with Vim**:  
```bash  
cd ~/rocky-git-lab  
vim plan.md  
```  
*Vim steps*:  
```text  
i                     # Insert mode  
# Project Plan<Enter>  
1. Research Git workflows<Esc>  
:wq                   # Save and quit  
```  

2. **Stage and commit**:  
```bash  
git add plan.md  
git commit -m "Add initial project plan"  
```  

3. **Verify commit**:  
```bash  
git log --oneline  
```  

**Email submission**:  
- **Subject**: `HW6 – Git Commit – [Your Name]`  
- **Body**:  
  a) `plan.md` content  
  b) `git log --oneline` output  
  c) Vim commands used to create file



## 7. Cloning and Adding Remotes

To get a local copy of an existing repository, use:

```
git clone <repository_url>
```

This creates a new directory with the project name, downloads the entire `.git` directory (all history), and checks out the latest version. It also sets up a remote named `origin` pointing to that URL.

To see your remotes, use:

```
git remote -v
```

This lists names and URLs of remotes (usually `origin`). If you created a new local repo with `git init` and want to connect it to a remote, use:

```
git remote add <name> <repository_url>
```

A common convention is `name = origin`, as in:

```
git remote add origin https://github.com/username/my-project.git
```

  
**Recap**: Use `git clone` to copy remote repositories locally, and `git remote add` to connect local repositories to remote servers.  

## Homework:  
1. **Clone a public repository**:  
```bash  
git clone https://github.com/example/example // explore GitHub and choose something interesting.  
```  

2. **Navigate and verify**:  
```bash  
cd example  
git log --oneline | head -3  
```  

3. **Add remote to your repo**:  
```bash  
cd ~/rocky-git-lab  
git remote add origin https://github.com/yourusername/rocky-git-lab.git  
```  

4. **Verify remotes**:  
```bash  
git remote -v  
```  

**Email submission**:  
- **Subject**: `HW7 – Git Remotes – [Your Name]`  
- **Body**:  
  a) First 3 commits from Linux repository  
  b) `git remote -v` output from your repo  
  c) Purpose of `origin` in Git workflows  


## 8. Synchronizing with Remote (Fetch, Pull, Push)

When collaborating, you often need to sync with a central repository.

* **Fetch:** `git fetch origin` downloads new commits, branches, and tags from `origin` but does **not** merge them into your local branches. It updates your local view of the remote branch (e.g., `origin/main`).
* **Pull:** `git pull origin main` is shorthand for `git fetch` followed by `git merge origin/main`. It fetches changes from the remote and then merges them into your current branch.
* **Push:** `git push origin main` sends your local commits from `main` to the `main` branch on the remote `origin`. If it’s the first time you push a new branch, use `git push -u origin <branch>` to set the upstream.

It's good practice to pull frequently to integrate others' changes and reduce merge conflicts.


**Recap**: Use `git fetch` to download remote changes, `git pull` to fetch + merge changes, and `git push` to upload your commits to a shared repository.  

## Homework:  
1. **Create analog repository**:  
```bash  
mkdir ~/sync-lab && cd ~/sync-lab  
git init  
echo "Version 1" > file.txt  
git add . && git commit -m "Initial commit"  
```  

2. **Simulate remote collaboration**:  
```bash  
# Simulate teammate's change  
mkdir ~/teammate-copy && cp -r ~/sync-lab/. ~/teammate-copy  
cd ~/teammate-copy  
echo "Version 2" > file.txt  
git commit -am "Teammate update"  
```  

3. **Practice sync commands**:  
```bash  
cd ~/sync-lab  
git fetch ~/teammate-copy/.git  # Fetch changes  
git diff HEAD @{u}              # See incoming changes  
git merge                       # Merge changes  
```  

**Email submission**:  
- **Subject**: `HW8 – Sync Simulation – [Your Name]`  
- **Body**:  
  1. `git diff` output before merge  
  2. Final content of `file.txt`  
  3. Your analogy: "Fetch is like ______, while pull is like ______"  





## Project 1: Collaborative Story Writing

*Objective:* Practice branching, merging, and resolving conflicts collaboratively (even in a non-code context).

* **Setup:** One person creates a new public GitHub repository named `git-story-project` and adds an initial `story.txt` with a sentence like "Once upon a time...". Invite one or two collaborators to the repository.
* **Branching and Writing:** Each collaborator clones the repository locally. Each person creates a branch (for example, `alice-chapter1` or `bob-adds-dragon`). On that branch, they add a paragraph or a few sentences to `story.txt`. Commit often with descriptive messages about the changes.
* **Pull Requests and Merging:** Push each branch to GitHub and open a Pull Request (PR) for it. Collaborators review the PRs. Then merge each branch into `main` via the GitHub interface or command line. If multiple people edit the same part of `story.txt`, resolve merge conflicts as needed (edit the conflict markers and commit).
* **Syncing Branches:** After a PR is merged into `main`, collaborators should pull the updated `main` into their local branches (or rebase onto `main`) before continuing work, to stay up-to-date.
* **Optional:** One person can create a branch to add a table of contents or chapter headings to `story.txt`. When the story is at a point (like first draft complete), create an annotated tag (e.g., `v1.0-draft`) on `main` with `git tag -a v1.0-draft -m "First draft complete"` and push it (`git push origin --tags`).

*Skills Practiced:* Cloning repos, branching (`git branch`, `git checkout -b`), committing changes, pushing branches (`git push`), creating and merging PRs, resolving merge conflicts, and using tags.

## Project 2: Personal Portfolio Website (Static)

*Objective:* Build a simple multi-page static website and manage its development using Git (including deploying with GitHub Pages).

* **Setup:** On GitHub, create a repository named `<yourusername>.github.io` (for default GitHub Pages). Clone it locally or initialize a new repo in a local folder (e.g., `my-portfolio`). Add this repo as `origin`.
* **Initial Commit:** On `main`, create `index.html` (homepage), `about.html`, and `projects.html`. Add basic HTML structure and a linked CSS file `css/style.css`. Commit and push these files.
* **Homepage Content:** Create a branch `feature/homepage`. Add introduction content and an image to `index.html`. Update `style.css` to style the homepage. Commit and merge this branch into `main` when done.
* **About Page:** Create a branch `feature/about-page`. Add your background/skills content to `about.html`, and any needed CSS. Commit and merge into `main`.
* **Projects Page:** Create a branch `feature/projects-page`. List several projects (real or mock) in `projects.html`. Style as needed. Commit and merge.
* **Refactoring:** (Optional) Create a branch `refactor/css`. Maybe split the CSS into multiple files (e.g., `layout.css`, `colors.css`) and update the HTML to link them. Commit and merge.
* **Contact Form:** Create a branch `feature/contact-form`. Add a simple contact form in a new `contact.html` or on one of the existing pages. Style it in CSS. Commit and merge.
* **.gitignore:** If you use build tools (like Sass/SCSS compilers or editor backups), add those outputs or temp files to `.gitignore`.
* **GitHub Pages:** If using `<username>.github.io` repo, your site is automatically deployed from `main`. Otherwise, enable GitHub Pages in repo settings and choose the `main` branch. Visit `https://yourusername.github.io` (or provided URL) to see your live site.
* **Deployment Update:** Make a small change (like updating a project description) on `main`, commit and push, and verify the live site reflects it.
* **Reverting a Mistake:** (Simulation) On a new branch `feature/bad-change`, make a change that breaks the site (e.g., bad CSS). Commit and merge it. Then use `git revert <commit>` on `main` to undo it and push, restoring the site. (Alternatively, use `git reset --hard` on your local `main` and force-push, but this rewrites history and is discouraged on shared branches.)

*Skills Practiced:* Full Git workflow (initializing, cloning, branching, merging), committing and pushing to GitHub, using GitHub Pages, `.gitignore` usage, and undoing changes with `git revert`.
