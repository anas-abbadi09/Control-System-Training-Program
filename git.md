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
- **Subject**: `HW3 – Git Installation – [Your Name]`  
- **Body**:  
  1. Git version from `git --version`  
  2. Your configured name/email  
  3. Output of `git log --oneline` in ~/git-lab 

## 4. Initializing a Repository and File States  

To start tracking a project with Git, navigate to your project’s folder and run:  

```bash
git init
```  

This creates a hidden `.git` directory, initializing a new Git repository. Git will now track changes to files in this folder.  

Files in Git exist in one of three main states:  

* **Working Directory (Untracked/Modified):**  
  Your active project files. New files are **untracked** by default. Existing tracked files become **modified** when changed but not staged.  
* **Staging Area (Staged):**  
  When you run `git add <file>`, changes move from the working directory to the staging area, preparing them for a commit.  
* **Repository (Committed):**  
  Running `git commit` permanently saves the staged snapshot to the repository.  

![Git File States Diagram](https://github.com/user-attachments/assets/decd4238-37b1-48e1-92a0-e8115daf10c3)  

### Core Concepts Made Simple  
- **Repository:** Project folder tracked by Git  
- **Commit:** Saved snapshot (like a game save point)  
- **Branch:** Parallel development line for experiments  
- **Remote:** Cloud-hosted copy (e.g., GitHub/GitLab)  

### Local vs. Remote Repositories  
- **Local Repository:**  
  Lives on your computer (created by `git init`). This is your private workspace where you make changes and commit snapshots.  
- **Remote Repository:**  
  Hosted on a server (e.g., GitHub/GitLab). Acts as a shared central hub for collaboration.  
  - Sync with `git push` (upload local → remote)  
  - Update with `git pull` (download remote → local)  

Use `git status` to see file states (untracked, modified, or staged). This command is essential for understanding your current workflow status.


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
- **Subject**: `HW4 – Initializing a Repository and File States – [Your Name]`  
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


## Your First Git Project

```bash
# 1. Create repository
mkdir climate-research && cd climate-research
git init

# 2. Create README
vim README.md
#   Type: "# Global Warming Study"
git add README.md
git commit -m "Initial commit"

# 3. Create and work on feature branch
git checkout -b temperature-models
vim sources.txt
git add sources.txt
git commit -m "Add data sources"

# 4. Merge changes to main
git checkout main
git merge temperature-models

# 5. Configure and push to remote
git remote add origin https://github.com/your-username/climate-research.git
git push -u origin main
```
## 9. Branching and Merging**

Branches are independent lines of development. Use them to work on new features without affecting the main code:

* **List branches**

  * Local:

    ```bash
    git branch
    ```
  * Remote:

    ```bash
    git branch -r
    ```
  * All:

    ```bash
    git branch -a
    ```

* **Create a branch**

  ```bash
  git branch new-feature
  ```

* **Switch branches**

  ```bash
  git checkout new-feature
  ```

  **Shortcut:**

  ```bash
  git checkout -b new-feature
  ```

  (creates **and** switches)

* **Merge a branch**

  1. Switch to the target branch (e.g., `main`):

     ```bash
     git checkout main
     ```
  2. Merge in your feature branch:

     ```bash
     git merge new-feature
     ```

  * If `main` has no new commits, Git will perform a *fast-forward* merge.
  * If both branches have new commits, Git will create a new **merge commit**.

* **Clean up**
  After merging, you can delete the feature branch if you no longer need it:

  ```bash
  git branch -d new-feature
  ```

## 9. Resolving Merge Conflicts**

When you merge two branches, Git attempts to auto-combine changes. If both branches modify the same lines, a **merge conflict** occurs. Git will:

1. **Pause the merge**

2. **Insert conflict markers** into the affected file(s):

   ```diff
   <<<<<<< HEAD
   // code from your current branch
   =======
   // code from the branch being merged
   >>>>>>> feature-branch
   ```

3. **Resolve the conflict**:

   * Open the file and decide which code to keep (you can also combine both).
   * Remove the `<<<<<<<`, `=======`, and `>>>>>>>` lines.
   * Save the file.

4. **Finalize the merge**:

   ```bash
   git add <file>
   git commit
   ```

5. **Abort the merge** (if you change your mind before committing):

   ```bash
   git merge --abort
   ```

## 10. Deleting Branches**

Once a feature branch has been merged, you can safely remove it to keep your repository tidy:

* **Delete locally**

  ```bash
  git branch -d <branch_name>
  ```

  Git will refuse to delete if the branch hasn’t been merged.

* **Force-delete locally** (use with caution):

  ```bash
  git branch -D <branch_name>
  ```

* **Delete on the remote**

  ```bash
  git push origin --delete <branch_name>
  ```


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




temppppppppp




### Project 1: Collaborative Story Generator (Final Version)

**Objective**: Practice Git workflows with guaranteed conflict resolution using Python story generation.

#### Python Scripts
**1. story_generator.py**:
```python
import random

beginnings = [
    "Once upon a time",
    "In a distant galaxy",
    "Long ago in a magical kingdom"
]

characters = [
    "a curious programmer",
    "a robotic cat",
    "a wise old owl"
]

actions = [
    "discovered Git magic",
    "solved a coding mystery",
    "learned Python spells"
]

print(f"{random.choice(beginnings)}, {random.choice(characters)} {random.choice(actions)}.")
```

**2. story_combiner.py** (Fixed):
```python
import sys
import os

output_filename = "master_story.txt"

if len(sys.argv) < 2:
    print(f"Usage: python {sys.argv[0]} file1.txt file2.txt ...")
    exit(1)

combined = ""
for filename in sys.argv[1:]:
    if os.path.basename(filename) == output_filename:
        print(f"Skipping '{filename}'...")
        continue
    
    try:
        with open(filename, 'r') as f:
            combined += f.read().strip() + "\n\n"
    except FileNotFoundError:
        print(f"Warning: {filename} not found")

with open(output_filename, 'w') as out:
    out.write(combined)

print(f"Stories combined into {output_filename}")
```

#### Git Workflow
```bash
# 1. Setup
git clone https://github.com/yourusername/story-generator.git
cd story-generator
echo -e '#!/bin/bash\npython story_generator.py > "$1.txt"' > generate_story
chmod +x generate_story
git add . && git commit -m "Initial commit"

# 2. Create conflicting branches
git checkout -b add-dragon
sed -i '/characters = \[/a\    "a friendly dragon",' story_generator.py
git commit -am "Add dragon character"

git checkout main
git checkout -b add-ninja
sed -i '/characters = \[/a\    "a stealthy ninja",' story_generator.py
git commit -am "Add ninja character"

# 3. Create conflict
git checkout main
git merge add-dragon
git merge add-ninja  # CONFLICT!

# 4. Resolve conflict
# Edit story_generator.py to keep BOTH characters
nano story_generator.py  # Manual edit
git add story_generator.py
git commit -m "Resolve conflict: keep both characters"

# 5. Generate stories
./generate_story chapter1
./generate_story chapter2
python story_combiner.py chapter*.txt

# 6. Finalize
git add .
git commit -m "Add story chapters"
git tag v1.0-story
git push --tags
```

#### Verification
```bash
# Check conflict resolution
git diff HEAD~2 HEAD~1  # Should show dragon addition
git diff HEAD~1 HEAD    # Should show ninja addition

# Test combiner
python story_combiner.py chapter1.txt chapter2.txt
cat master_story.txt
```

---

### Project 2: Template-Based Portfolio (Final Version)

**Objective**: Build portfolio using Python templates with validation and safe deployment.

#### Project Structure
```
.
├── templates/
│   └── base.html
├── content/
│   ├── index.md
│   ├── about.md
│   └── projects.md
├── builder.py
├── validator.py
└── style.css
```

#### Core Files
**1. templates/base.html**:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{{title}} | My Portfolio</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <nav>
        <a href="index.html">Home</a> |
        <a href="about.html">About</a> |
        <a href="projects.html">Projects</a>
    </nav>
    <h1>{{title}}</h1>
    <div>{{content}}</div>
</body>
</html>
```

**2. builder.py** (Fixed):
```python
import os
import markdown  # pip install markdown

def build_site():
    for page in os.listdir('content'):
        if page.endswith('.md'):
            name = page[:-3]
            with open(f'content/{page}') as f:
                content = markdown.markdown(f.read())
            
            with open('templates/base.html') as f:
                html = f.read()
            
            html = html.replace('{{title}}', name.capitalize())
            html = html.replace('{{content}}', content)
            
            with open(f'{name}.html', 'w') as f:
                f.write(html)
    print("Site built successfully")

if __name__ == '__main__':
    build_site()
```

**3. validator.py**:
```python
import sys

def validate_html(file):
    with open(file) as f:
        content = f.read()
        if '</body>' not in content or '</html>' not in content:
            return False
    return True

if __name__ == '__main__':
    if not validate_html(sys.argv[1]):
        print(f"ERROR: {sys.argv[1]} has invalid HTML structure")
        exit(1)
    print("Validation successful")
```

#### Workflow
```bash
# 1. Setup
git clone https://github.com/yourusername/portfolio.git
cd portfolio
python -m pip install markdown
echo "__pycache__/" > .gitignore
git add . && git commit -m "Initial commit"
python builder.py

# 2. Add contact page
git checkout -b contact-page
echo "## Contact\nEmail: me@example.com" > content/contact.md
python builder.py
git add .
git commit -m "Add contact page"

# 3. Merge changes
git checkout main
git merge contact-page

# 4. Create and revert bad update
git checkout -b bad-update
sed -i 's/<\/body>/<!-- /g' templates/base.html  # Break HTML
python builder.py
python validator.py index.html || echo "Validation failed (expected)"
git commit -am "Bad template update"

git checkout main
git merge bad-update
git revert HEAD -m 1 --no-edit

# 5. Fix and verify
python builder.py
python validator.py index.html && echo "Validation passed"

# 6. Deploy
git add *.html
git commit -m "Rebuild site"
git push origin main
```

#### Verification Commands
```bash
# Check HTML structure
grep -c '</body>' *.html

# Test validation
python validator.py index.html

# Check deployment
curl -s https://yourusername.github.io | grep -q "My Portfolio" && echo "Live"
```

---

### Key Improvements:

**Project 1**:
1. Added `generate_story` script for consistent file naming
2. Fixed newline escaping in Python combiner
3. Added error handling for missing files
4. Simplified conflict creation with `sed`
5. Added verification commands

**Project 2**:
1. Added Markdown support for content
2. Fixed template variable replacement
3. Added proper HTML validation
4. Simplified bad update creation
5. Added dependency installation step
6. Improved verification commands

**Both Projects**:
1. Added explicit error handling
2. Included verification steps
3. Simplified conflict creation
4. Fixed all syntax issues
5. Added post-operation checks
6. Ensured compatibility with Rocky Linux
