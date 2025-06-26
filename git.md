Great! I’ll now organize the Git training material into a beginner-friendly guide. Each section will have a clear title, a brief recap, and a practical homework assignment with email submission instructions and model answer outlines. I’ll also keep the large projects at the end as requested.

I’ll get started and let you know when the formatted guide is ready.


# Git Version Control Course for Beginners

## 1. Introduction to Git

Git is a distributed version control system (DVCS). Each developer has a full local copy of the entire project history, so you don't rely on a single central server. Git tracks changes over time, showing who made each change and allowing you to revert to previous versions if needed.

* **Tracking changes:** Git saves snapshots of your project, so you can compare versions and undo changes if something breaks.
* **Collaboration:** Multiple people can work on the same project concurrently. Git helps merge everyone's changes without conflict.
* **Branching:** You can create branches to develop features or fixes in isolation. Merging branches back keeps the main codebase stable.
* **Experimentation:** Try new ideas safely. If an experimental branch doesn’t work out, you can discard it without affecting the stable code.
* **Industry standard:** Git is the most commonly used version control system in software development. Learning Git is essential for any developer.

**Recap:** Git is a distributed version control tool that helps you save project snapshots, collaborate with others, and experiment safely with branches.

**Homework:** Install Git on your computer and verify it’s working. In your terminal or command prompt, run `git --version`. Take a screenshot or copy the output and email it.

* **Subject:** HW1 - Git Installation
* **Include:** A file or image showing the output of `git --version`.
* **Message:** Explain that this shows your Git installation and version.

**Model answer outline:**

* **Expected output:** Something like `git version 2.x.x`.
* **Key steps:** Ran `git --version` in the terminal to verify installation.
* **Sample subject:** "HW1 - Git Installation".
* **Sample body:** The student explains they have Git installed and shows the version output in the attached screenshot or file.

## 2. Centralized vs. Distributed Version Control

Version control systems manage project history. **Centralized** systems (like SVN) use a single server for all files and history. Developers check out files, make changes, and check them back in. **Distributed** systems (like Git) give every developer a full repository copy on their machine.

* **Centralized (SVN):** Pros: simpler to understand. Cons: if the server goes down, work halts; slower since many commands need the server.
* **Distributed (Git):** Pros: faster local operations, works offline, very robust (any clone has full history). Cons: more complex initially.

Git's distributed model means you can work and commit offline and then sync when you're online. Your clone even serves as a backup of the whole project.

**Recap:** Centralized VCS has a single server; distributed VCS like Git gives every user a complete copy of the repository for faster, more flexible work.

**Homework:** In an email, explain one advantage of distributed VCS over centralized VCS. Use Git or SVN examples to illustrate your point.

* **Subject:** HW2 - Version Control Models
* **Include:** No attachment needed.
* **Message:** Provide a brief explanation (1-2 sentences) comparing distributed and centralized models.

**Model answer outline:**

* **Key point:** The advantage might be offline work or no single failure point.
* **Example:** “In Git (distributed), you can commit changes locally even if the server is down.”
* **Sample subject:** "HW2 - Version Control Models".
* **Sample body:** The student explains the chosen advantage and gives an example using Git or SVN.

## 3. Installing and Configuring Git

First, install Git from [git-scm.com](https://git-scm.com/downloads) for your operating system. After installation, open a terminal or command prompt and run `git --version` to confirm it’s installed correctly.

Next, configure your identity with Git. In your terminal, run:

```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

These settings will tag all your future commits with your name and email. You can check your configuration with:

```
git config --list
```

Look for `user.name` and `user.email` in the output to ensure they are correct.

If you ever need help with a Git command, you can use:

```
git help <command>
```

or

```
git <command> --help
```

This will display documentation for that command in your terminal.

**Recap:** Install Git, then set your global username and email so your commits are properly attributed. Use `git config --list` to confirm your settings.

**Homework:** Configure Git on your computer with your own name and email. Then email me a screenshot or text file of `git config --list` showing your user.name and user.email.

* **Subject:** HW3 - Git Configuration
* **Include:** A screenshot or text file of `git config --list` showing your name and email.
* **Message:** Confirm that Git is configured with your name and email.

**Model answer outline:**

* **Key output:** Lines showing `user.name=Your Name` and `user.email=your@example.com`.
* **Key steps:** Used `git config --global user.name` and `git config --global user.email` and then ran `git config --list`.
* **Sample subject:** "HW3 - Git Configuration".
* **Sample body:** The student states they configured Git with their name and email and attached the command output.

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

Use `git status` to see which files are untracked, modified, or staged. It’s very helpful to see what’s going on.

**Recap:** Use `git init` to create a repository. Files can be untracked, staged, or committed. Use `git status` to check file states.

**Homework:** Create a new folder (for example, `project-demo`), run `git init` inside it, then create a new text file named `tasks.txt` with some content. Run `git status`. Email a screenshot or text of the `git status` output showing your untracked file.

* **Subject:** HW4 - Git Init and Status
* **Include:** An image or text of the `git status` output showing `tasks.txt` as an untracked file.
* **Message:** Explain that you initialized a Git repository and have an untracked file.

**Model answer outline:**

* **Output:** `git status` shows `tasks.txt` under "Untracked files".
* **Key steps:** Created folder, ran `git init`, created `tasks.txt`, ran `git status`.
* **Sample subject:** "HW4 - Git Init and Status".
* **Sample body:** The student says they initialized the repo and shows the status output with the untracked file.

## 5. Ignoring Files with .gitignore

Some files should not be tracked by Git (for example, compiled binaries, log files, or personal notes). Create a file named `.gitignore` in the root of your project to list patterns for files Git should ignore.

Common patterns:

* `*.log` to ignore all `.log` files.
* `build/` to ignore a directory named `build`.
* `secret.txt` to ignore a specific file.

Add and commit the `.gitignore` file to share it with others. After adding patterns, `git status` will no longer list those ignored files.

**Recap:** Use a `.gitignore` file to tell Git which files or patterns to ignore (like logs, temporary files, or personal notes). This keeps unwanted files out of your commits.

**Homework:** In your repository, create two new files: `notes.txt` and `temp.tmp`, then create a `.gitignore` that ignores all `*.tmp` files and the specific file `notes.txt`. Run `git status` again. Email the `.gitignore` file (attached or copied) and a screenshot or text of `git status` showing that these files are ignored.

* **Subject:** HW5 - .gitignore File
* **Include:** The `.gitignore` file and `git status` output (e.g., as a screenshot or text).
* **Message:** Explain that `notes.txt` and `temp.tmp` are now ignored by Git.

**Model answer outline:**

* **.gitignore content:** Lines like `*.tmp` and `notes.txt`.
* **Output:** `git status` should not list `notes.txt` or `temp.tmp` as untracked.
* **Key steps:** Created `notes.txt` and `temp.tmp`, added ignore patterns, ran `git status`.
* **Sample subject:** "HW5 - .gitignore File".
* **Sample body:** The student says they added the patterns and shows the status confirming those files are ignored.

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

**Recap:** Use `git add` to stage changes and `git commit -m "message"` to record a snapshot of those changes in your repository. Good commit messages explain what changed and why.

**Homework:** Create a new file `plan.md` in your repository and write a sentence in it. Stage and commit this file with an appropriate commit message. Email a screenshot or text of the `git log --oneline` output showing your new commit.

* **Subject:** HW6 - Git Add and Commit
* **Include:** Output of `git log --oneline` showing your commit message (screenshot or text).
* **Message:** State that you added `plan.md` and committed it with a message.

**Model answer outline:**

* **Output:** A line from `git log --oneline` showing the commit with the message (e.g., "Add initial plan file").
* **Key steps:** Created `plan.md`, ran `git add plan.md`, then `git commit -m "..."`.
* **Sample subject:** "HW6 - Git Add and Commit".
* **Sample body:** The student explains they created and committed `plan.md` and included the log output.

## 7. Viewing History and Differences

To review past commits, use:

```
git log
```

This shows each commit's unique hash, author, date, and message. Use `git log --oneline` for a compact view, and `git log --graph` to see branching.

To see changes you’ve made, use:

```
git diff
```

This shows unstaged changes in your working directory. Use `git diff --staged` to see what is staged for the next commit, and `git diff <commit>` to compare with an old commit. You can even diff between two commits:

```
git diff <hash1> <hash2>
```

**Recap:** `git log` shows the commit history, and `git diff` shows the specific changes between commits or between your working files and a commit.

**Homework:** Append a new line to `plan.md` (for example, add "Testing diff feature."). Run `git diff` and capture the output. Email the diff output (as text) along with the result of `git log --oneline` to show your commit history.

* **Subject:** HW7 - Git Log and Diff
* **Include:** The text output of `git diff` and `git log --oneline`.
* **Message:** Mention that you made a change to `plan.md` and are showing the diff and log.

**Model answer outline:**

* **Diff output:** Shows the added line in `plan.md` (with a `+` prefix).
* **Log output:** Includes your previous commit (with your message).
* **Key steps:** Edited `plan.md`, saved it, ran `git diff` and `git log --oneline`.
* **Sample subject:** "HW7 - Git Log and Diff".
* **Sample body:** The student notes they changed `plan.md` and attached the diff and log output.

## 8. Unstaging and Discarding Changes

If you accidentally stage a file, you can remove it from the staging area (but keep your changes) with:

```
git reset HEAD <filename>
```

This moves the changes back to unstaged in your working directory. To undo changes in a file entirely (discard local edits), you can use:

```
git checkout -- <filename>
```

**Warning:** `git checkout -- <file>` will erase your unsaved changes in that file, reverting it to the last committed state.

**Recap:** Use `git reset HEAD <file>` to unstage a file you added. Use `git checkout -- <file>` to discard changes and revert to the last commit (be careful, this loses unsaved edits).

**Homework:** In your repository, stage one of your files (e.g., `tasks.txt`) with `git add` and then unstage it using `git reset HEAD <filename>`. Run `git status` and email a screenshot or text of the output showing that the file is back to unstaged.

* **Subject:** HW8 - Git Unstage Changes
* **Include:** The `git status` output after unstaging (screenshot or text).
* **Message:** Describe that you staged a file and then unstaged it.

**Model answer outline:**

* **Output:** `git status` shows the file as modified (not staged) again.
* **Key steps:** Ran `git add tasks.txt`, then `git reset HEAD tasks.txt`, and then `git status`.
* **Sample subject:** "HW8 - Git Unstage Changes".
* **Sample body:** The student notes they unstaged the file and attached the status output.

## 9. Cloning and Adding Remotes

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

**Recap:** `git clone <url>` downloads a repo and sets `origin`. Use `git remote -v` to view remotes. For a new repo, use `git remote add` to link to a remote server.

**Homework:** In your repository, add a new remote named `origin` using a URL of your choice (you can use a dummy URL). Run `git remote -v` and email the output.

* **Subject:** HW9 - Git Remotes
* **Include:** Output of `git remote -v` (screenshot or text).
* **Message:** Explain that you added a remote named `origin`.

**Model answer outline:**

* **Output:** Shows `origin    https://github.com/username/my-project.git` (or the dummy URL).
* **Key steps:** Ran `git remote add origin <url>`, then `git remote -v`.
* **Sample subject:** "HW9 - Git Remotes".
* **Sample body:** The student notes they added `origin` and shows the `git remote -v` output.

## 10. Synchronizing with Remote (Fetch, Pull, Push)

When collaborating, you often need to sync with a central repository.

* **Fetch:** `git fetch origin` downloads new commits, branches, and tags from `origin` but does **not** merge them into your local branches. It updates your local view of the remote branch (e.g., `origin/main`).
* **Pull:** `git pull origin main` is shorthand for `git fetch` followed by `git merge origin/main`. It fetches changes from the remote and then merges them into your current branch.
* **Push:** `git push origin main` sends your local commits from `main` to the `main` branch on the remote `origin`. If it’s the first time you push a new branch, use `git push -u origin <branch>` to set the upstream.

It's good practice to pull frequently to integrate others' changes and reduce merge conflicts.

**Recap:** `git fetch` downloads changes without merging; `git pull` fetches and merges; `git push` uploads your commits to the remote repository.

**Homework:** Write a brief email explaining the difference between `git fetch` and `git pull`. Use simple language or an example if needed.

* **Subject:** HW10 - Fetch vs Pull
* **Include:** No attachment needed.
* **Message:** Provide a short comparison of what each command does.

**Model answer outline:**

* **Key point:** Fetch only downloads, pull downloads and merges.
* **Example:** “`git fetch` gets updates from the server, and `git pull` gets updates and merges them into my branch.”
* **Sample subject:** "HW10 - Fetch vs Pull".
* **Sample body:** The student explains the difference in their own words.

## 11. Branching and Merging

Branches are separate lines of development. Use branches to work on features without affecting the main code.

* **Listing branches:** `git branch` (local branches), `git branch -r` (remote branches), `git branch -a` (all).
* **Creating a branch:** `git branch new-feature` makes a new branch.
* **Switching branches:** `git checkout new-feature` moves to that branch.
* **Shortcut:** `git checkout -b new-feature` creates and switches in one step.
* **Merging:** To combine changes, first switch to the target branch (e.g., `main`), then `git merge new-feature`. If the main branch hasn’t changed, Git does a fast-forward merge. If both have new commits, Git makes a new merge commit.

Using branches helps keep development organized and safe. After merging, you can delete the branch if it's no longer needed (`git branch -d new-feature`).

**Recap:** Use `git branch` and `git checkout` to create and switch branches. Use `git merge` to combine a branch back into the main branch.

**Homework:** Create a new branch named `test-branch`. Switch to it and create a file `hello.txt` containing "Hello, Git!" (or similar text). Commit this change on `test-branch`. Switch back to `main` and merge `test-branch` into it. Run `git log --oneline --graph` and email the output showing the branch merge.

* **Subject:** HW11 - Git Branching and Merging
* **Include:** Output of `git log --oneline --graph` showing the merge (screenshot or text).
* **Message:** State that you created and merged `test-branch`.

**Model answer outline:**

* **Output:** The graph shows `test-branch` merged into `main`.
* **Key steps:** Created and switched to `test-branch`, added `hello.txt`, committed, switched to `main`, merged, and viewed log.
* **Sample subject:** "HW11 - Git Branching and Merging".
* **Sample body:** The student explains they merged the branch and attached the log graph.

## 12. Resolving Merge Conflicts

When you merge branches, Git will try to combine the changes. If both branches have changes on the same lines, a **merge conflict** occurs. Git will pause the merge and mark the conflict in the file using special markers:

```
<<<<<<< HEAD
// code from your current branch
=======
// code from the branch being merged
>>>>>>> feature-branch
```

To resolve it, open the file, decide which parts to keep (or combine them), remove the markers, and save. Then run:

```
git add <file>
git commit
```

to complete the merge. If you want to stop the merge process, use `git merge --abort` (before committing) to go back to the state before the merge.

**Recap:** Merge conflicts happen when changes overlap. Git marks the conflicts in the files, and you must edit and remove the markers to resolve the conflict before committing.

**Homework:** Describe in a short email how you would recognize and resolve a merge conflict in Git.

* **Subject:** HW12 - Merge Conflicts
* **Include:** No attachment needed.
* **Message:** Explain the process of resolving a merge conflict and what the conflict markers mean.

**Model answer outline:**

* **Key points:** The conflict markers `<<<<<<<`, `=======`, `>>>>>>>` show differences.
* **Resolution:** Edit the file to keep the desired code and remove markers, then `git add` and `git commit`.
* **Sample subject:** "HW12 - Merge Conflicts".
* **Sample body:** The student explains the conflict markers and how they merge the code manually.

## 13. Deleting Branches

Once a feature branch has been merged, you can delete it. Locally, use:

```
git branch -d <branch_name>
```

This safely deletes the branch (Git will warn if it hasn’t been merged). To force-delete an unmerged branch (be careful), use `-D`. To delete a remote branch:

```
git push origin --delete <branch_name>
```

**Recap:** After merging, delete feature branches with `git branch -d` locally and `git push origin --delete` remotely to keep the repository clean.

**Homework:** Delete the `test-branch` you created earlier by running `git branch -d test-branch`. Run `git branch` and email the output showing the branch has been removed.

* **Subject:** HW13 - Delete Branch
* **Include:** Output of `git branch` (screenshot or text) after deletion.
* **Message:** Confirm that `test-branch` has been deleted locally.

**Model answer outline:**

* **Output:** `git branch` no longer lists `test-branch`.
* **Key steps:** Ran `git branch -d test-branch`, then `git branch`.
* **Sample subject:** "HW13 - Delete Branch".
* **Sample body:** The student notes they deleted the branch and shows the branch list.

## 14. Git Workflows (Feature Branch and GitHub Flow)

**Feature Branch Workflow:** Start by updating the main branch (`git pull origin main`). Create a new branch for your feature (`git checkout -b feature-x`) and work on it. Commit your changes regularly on that branch. Push the branch to the remote (`git push -u origin feature-x`). Once your feature is done, you can merge it back into main:

* *Option A:* Merge locally: switch to `main`, pull latest, then `git merge feature-x`, and push `main`.
* *Option B:* Open a Pull Request on GitHub, review, then merge via the web interface (common in teams).

After merging, delete the feature branch (`git branch -d feature-x` and `git push origin --delete feature-x`).

**GitHub Flow (simplified):** Always create a branch for a new change, commit, open a Pull Request for review, and merge into `main` once approved. Each change is deployed from a branch or `main`, ensuring everything is reviewed and tested before going live.

**Recap:** Use branches to develop features. Merge features into `main` after review. Open Pull Requests on platforms like GitHub to integrate changes collaboratively and safely.

**Homework:** In your own words, write a brief outline of the feature-branch workflow steps you would follow when adding a new feature.

* **Subject:** HW14 - Git Workflow
* **Include:** No attachment needed.
* **Message:** List the main steps of the feature-branch workflow (e.g., branch from main, work, push, pull request, merge).

**Model answer outline:**

* **Steps:** Update main, create feature branch, commit changes, push branch, open PR (or merge to main), delete branch.
* **Sample subject:** "HW14 - Git Workflow".
* **Sample body:** The student lists the steps for using branches and merging features into main.

## 15. Advanced Git Topics

Git has many more powerful commands. Here are a few:

* **git rebase:** Reapply your commits on top of another branch. This can create a linear history by moving feature-branch commits to the tip of `main`. *Caution:* Don’t rebase public/shared history.
* **git stash:** Temporarily save (stash) changes that are not ready to commit. Use `git stash` to save and clear your working directory, and `git stash pop` to reapply them later.
* **git tag:** Mark a specific commit as an important milestone, such as a release. For example, `git tag v1.0` or `git tag -a v1.0 -m "Release 1.0"`. Push tags with `git push origin --tags`.
* **git reset --hard <commit>:** **Warning:** Resets your current branch to a specific commit, discarding all later commits and changes. Use with extreme caution (it rewrites history).
* **git revert <commit>:** Create a new commit that undoes the changes introduced by a previous commit. This is a safer way to undo changes on a shared branch as it doesn’t rewrite history.

These features are useful for advanced workflows, but beginners should learn them gradually.

**Recap:** Git includes advanced tools like rebasing, stashing, and tagging. Each has special uses (e.g., cleaning up history, saving unfinished work, marking releases). Use them carefully.

**Homework:** Pick one advanced Git feature (rebase, stash, tag, reset, or revert) and in an email briefly describe a scenario where it would be useful.

* **Subject:** HW15 - Advanced Git
* **Include:** No attachment needed.
* **Message:** Explain the chosen feature and give a use-case scenario.

**Model answer outline:**

* **Example:** For `git stash`, a student might say: "Stash lets me save my uncommitted changes if I need to switch branches quickly without losing work."
* **Sample subject:** "HW15 - Advanced Git".
* **Sample body:** The student explains one advanced command and how it solves a problem.

## 16. Project 1: Collaborative Story Writing

*Objective:* Practice branching, merging, and resolving conflicts collaboratively (even in a non-code context).

* **Setup:** One person creates a new public GitHub repository named `git-story-project` and adds an initial `story.txt` with a sentence like "Once upon a time...". Invite one or two collaborators to the repository.
* **Branching and Writing:** Each collaborator clones the repository locally. Each person creates a branch (for example, `alice-chapter1` or `bob-adds-dragon`). On that branch, they add a paragraph or a few sentences to `story.txt`. Commit often with descriptive messages about the changes.
* **Pull Requests and Merging:** Push each branch to GitHub and open a Pull Request (PR) for it. Collaborators review the PRs. Then merge each branch into `main` via the GitHub interface or command line. If multiple people edit the same part of `story.txt`, resolve merge conflicts as needed (edit the conflict markers and commit).
* **Syncing Branches:** After a PR is merged into `main`, collaborators should pull the updated `main` into their local branches (or rebase onto `main`) before continuing work, to stay up-to-date.
* **Optional:** One person can create a branch to add a table of contents or chapter headings to `story.txt`. When the story is at a point (like first draft complete), create an annotated tag (e.g., `v1.0-draft`) on `main` with `git tag -a v1.0-draft -m "First draft complete"` and push it (`git push origin --tags`).

*Skills Practiced:* Cloning repos, branching (`git branch`, `git checkout -b`), committing changes, pushing branches (`git push`), creating and merging PRs, resolving merge conflicts, and using tags.

## 17. Project 2: Personal Portfolio Website (Static)

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
