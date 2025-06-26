
# Linux Command Line

## 1. Introduction to the Linux Command Line

Welcome to the Linux command line (shell/terminal/console)—a powerful text-based interface. While GUIs are user-friendly, the CLI offers unmatched power, flexibility, and speed, making it essential for developers, sysadmins, and power users.

**Why the Command Line Matters:**

* **Automation & Scripting:** Automate repetitive tasks with shell scripts to save time and reduce errors.
* **Power & Flexibility:** Perform advanced configuration and troubleshooting not available in GUIs.
* **Efficiency:** One well-crafted command can replace dozens of GUI clicks.
* **Remote Access:** Manage servers over SSH.
* **Lightweight:** Uses far fewer resources than a full desktop, which is key on servers.
* **Consistency:** Core tools and syntax remain the same across distributions.

## 2. Structure of a Command

The basic syntax of a command is:

```
command [options] [arguments]
```

* **command:** Program name (e.g., `ls`, `cp`).
* **options:** Modify behavior (e.g., `-l`, `--recursive`).
* **arguments:** Targets (files, directories, patterns).

**Example:**

```bash
grep -rin "TODO" ~/projects
```

This command searches recursively (`-r`) for the string "TODO" (case-insensitive, `-i`) in the `~/projects` directory, showing line numbers (`-n`).

### Homework:

1. Examine the following command and list which part is the command name, which are the options, and which are the arguments:

`tar -czvf site_backup.tar.gz /var/www/site`

2. Write a single shell command that copies all `.txt` files from a directory named `reports/` into a directory named `old_reports/`, shows each filename as it copies, and preserves file timestamps.


## 3. Opening a Terminal and the Prompt

A *terminal emulator* (often just called “Terminal”) is the software you use today to access the CLI. It simulates a physical console. Common terminal emulators include **Terminal** (GNOME), **Konsole** (KDE), and **xterm** (lightweight).

When you open a terminal emulator, you’ll see a *prompt* indicating the system is ready for your input. It usually looks like:

```
user@hostname:~/current/path$
```

* **user:** Your current username.
* **hostname:** The name of your computer.
* **\~:** A shortcut for your home directory (e.g., `/home/yourusername`).
* **/current/path:** Your current working directory. If you’re in your home directory, this will just be `~`.
* **\$:** Indicates you’re a regular user. If it were `#`, you’d be the root (administrative) user.

You can customize this prompt’s appearance and information by editing the `PS1` variable in your `~/.bashrc` file.

## 4. Getting Help

When you need help with a command, the CLI provides several tools:

* `man <command>`: Detailed manual (full documentation).
* `<command> --help`: Quick usage summary (common options).
* `info <command>`: Hyperlinked documentation pages (often more detailed than `man`).
* `apropos <keyword>`: Search man-page descriptions for a keyword.
* `whatis <command>`: One-line summary of what a command does.

**⚡ Bonus Tool: tldr (Too Long; Didn't Read)** – A simplified help resource.

* `tldr <command>`: Practical examples and common use cases for a command. (Note: `tldr` is a separate tool and might need installation.)


### Homework:

**Investigate `curl`.**

Run `curl --help`, `man curl` (just the first two lines), and `info curl` (just the first two entries in its menu). For each tool, note what type of information it gives you.

**Find an alternative to `grep`.**

Use `apropos "search text"` to discover a command other than `grep` that can search inside files. Then run `whatis` on the suggestion and record its one-line description.

## 5. Package Management with DNF

Rocky Linux (a Red Hat-based distribution) uses the RPM package ecosystem. The core components are:

* **RPM (Red Hat Package Manager):** The low-level package format (`.rpm` files) containing software and metadata.
* **DNF (Dandified YUM):** The next-generation package manager you’ll interact with. It replaced the older `yum`.
* **Repositories:** Online servers (or local directories) that store collections of RPM packages. DNF automatically fetches packages and their dependencies from repos.

DNF handles software installation, updates, and removal while resolving dependencies automatically. Most DNF commands require `sudo`. When you install software, DNF ensures all required dependencies are also installed.

**Essential DNF Commands:**

* **Install:** `sudo dnf install <package_name(s)>`
  Example: `sudo dnf install htop alacritty`.
* **Remove:** `sudo dnf remove <package_name(s)>`
  Example: `sudo dnf remove htop ulauncher`.
* **Search:** `dnf search <keyword>` (No sudo needed.)
  Example: `dnf search apache` (often `httpd` for the Apache web server).
* **List Installed:** `dnf list installed` (No sudo needed.)
* **Upgrade All (System Update):** `sudo dnf upgrade`
  *Crucial for security; run regularly.* (You can also use `sudo dnf update`.)
* **Upgrade Specific:** `sudo dnf upgrade <package_name>`
  Example: `sudo dnf upgrade firefox`.
* **Reinstall:** `sudo dnf reinstall <package_name>`.
* **Remove Unused Dependencies:** `sudo dnf autoremove`.
* **Clean Caches:** `sudo dnf clean all`.

### Homework:

**Simulate installing and listing.**

Without actually installing, write the sequence of commands you would use to install two packages—vlc and ncdu—and then list all installed packages whose names start with “n”.

**Clean up and verify.**

Write the commands to remove a package named tinymembench, automatically remove any now-unused dependencies, clean all cached data, and finally confirm that tinymembench is no longer installed.

## 6. Basic Navigation and File Management

Use the following commands to move around and manage files/directories:

```bash
# Show current directory
pwd
# List files (long format, human-readable sizes, sort by size reverse)
ls -lhSr

# Change directory
cd /path/to/dir
cd ..      # go to parent directory
cd -       # go to previous directory
cd        # go to home directory

# Make directories
mkdir -p parent/child   # nested directories in one command

# Create/update file timestamp (or create an empty file)
touch file.txt

# Copy files/directories
cp -a src/ dest/        # archive mode: preserves perms, timestamps, symlinks

# Move or rename
mv file.txt ../other/

# Remove files/directories
rm -i file.txt          # interactive (safer delete, prompts for confirmation)
rmdir empty-dir        # remove empty directory
rm -rf dir-to-delete    # DANGER: force remove directory and contents (no undo)
```

* ⚡ **Bonus Tool: Ranger (Terminal File Manager):** Use `ranger` for a visual, two- or three-pane interface in the terminal. It lets you browse directories and preview files with keyboard shortcuts, similar to a GUI file manager. (Install it first with `sudo dnf install ranger` on Rocky Linux, then run `ranger`.)

### Homework:

**Explore and Inspect**

* List the **full pathname** of your current home directory.
* Display **all files** in `~/logs` in **long format**, sorted by **modification time (newest first)**.
* Change into the **parent directory** of `~/logs`.

**Create, Copy, Rename, and Remove**

Within your working directory (`~/projects`):

* Create nested folders: `archive/2025_June`.
* Inside `archive/2025_June`, create an empty file named `notes.md`.
* Copy all **`.conf` files** from `~/config` into `archive/2025_June`, **preserving metadata**.
* Rename one of the copied files to **append `.bak`**.
* **Interactively delete** an existing empty directory called `temp_test`.


## 7. Working with File Content

View and search file contents with these commands:

```bash
# View entire file
cat file.txt

# Page through long files
less /var/log/messages

# View first/last lines
head -n5 file.txt      # first 5 lines
tail -n20 file.txt     # last 20 lines

# Follow a file (e.g., live log)
tail -f /var/log/messages

# Search text
grep -Rin "error" ~/projects
```

### Homework:

**Task: Create a Command Script**

In a script named `hw7_commands.sh`, write commands to:

1. Display the first 7 lines of `/home/student/debug.log`.
2. Page through the rest of that same file.
3. Show the last 15 lines of `/home/student/debug.log`.
4. Recursively search for the string "ALERT" (case-insensitive) in all `.conf` files under `/etc/myservice`.
5. Monitor `/home/student/debug.log` for new entries until you interrupt it.

**Submission: Email**

- **Subject**: HW7 – File Content
- **Attach**: `hw7_commands.sh`
- **In the body**:
  - Paste the output you saw for the `grep` search.
  - Write one sentence summarizing what happened when you ran `tail -f`.

## 8. Permissions and Ownership

Permissions and ownership control access to files and directories.

**Viewing Permissions:** Use `ls -l` to see permissions. Example output:

```
drwxr-xr--  2 alice developers 4096 Mar  5 10:00 mydir
```

* The first character shows the file type: `d` (directory), `-` (file), `l` (symbolic link).
* The next nine characters are permissions, divided into three groups of three: **user/owner**, **group**, and **others**.

  * `r` (read), `w` (write), `x` (execute). A `-` means the permission is not granted.

For example, `drwxr-xr--` means: it's a directory (`d`); owner has read/write/execute (`rwx`); group has read/execute (`r-x`); others have only read (`r--`).

### Changing Permissions (`chmod`)

Modify permissions with `chmod`:

* **Symbolic Mode:** Use `u`, `g`, `o`, `a` (user, group, others, all) with `+` (add), `-` (remove), or `=` (set exactly).

  * Example: `chmod u+x script.sh` (add execute for owner).
  * Example: `chmod go-w secret.txt` (remove write for group and others).

* **Numeric (Octal) Mode:** Use three octal digits (`chmod XYZ file`), each digit 0–7: read=4, write=2, execute=1. Add values for each class.

| Sum | Permissions |
| :-: | ----------- |
|  0  | ---         |
|  1  | --x         |
|  2  | -w-         |
|  3  | -wx         |
|  4  | r--         |
|  5  | r-x         |
|  6  | rw-         |
|  7  | rwx         |

* Example: `chmod 755 script.sh` sets `rwxr-xr-x`. (Common for scripts/directories.)
* Example: `chmod 644 config.yaml` sets `rw-r--r--`. (Common for config files.)
* Example: `chmod -R 770 my_project/` sets `rwxrwx---` for the project directory and all its contents (recursive).

### Changing Ownership (`chown`)

Change file/directory owner with `chown` (requires `sudo`):

* `sudo chown <new_owner> <file/dir>`: Change the user owner only.
* `sudo chown :<new_group> <file/dir>`: Change the group owner only.
* `sudo chown <new_owner>:<new_group> <file/dir>`: Change both owner and group.

  * Tip: If you use `sudo chown new_owner:`, the group will default to the new owner's primary group.
* Use `-R` to apply recursively to directories and their contents.

Examples:

```bash
sudo chown alice:developers project/   # owner=alice, group=developers
sudo chown -R bob: project_data/       # owner=bob for project_data/ and all inside; group=bob's group
```


## Homework

### Interpret permissions

Imagine you run `ls -l` and see:
`-rwxr--r-- 1 carol analysts 2048 Jul 10 09:15 secret_notes.txt`

**Task 1:** In an email, state the file type, and list exactly what permissions Carol (the owner), the group, and others have.

---

### Change permissions and ownership

**Task 2:** Create a script named `hw8_commands.sh` that:

* Sets `project_alpha/` and everything inside to be **readable and writable** by **owner and group**, but **inaccessible** to others.
* Makes the file `project_alpha/config.yml` **executable by owner only**.
* Changes the **owner** of `project_alpha/` and its contents to **user `dave`** and **group `qa`**.

---

### Email Submission

**Subject:** HW8 – Permissions & Ownership

**Attach:** `hw8_commands.sh`

**Email Body:**

* For **task 1**, provide a **one-sentence answer** describing the permissions.
* For **task 2**, write a **two-sentence summary** of what each command in your script does.



## 9. Process Management

Process management involves monitoring and controlling programs running on your Linux system. Understanding processes is crucial for troubleshooting and seeing what your computer is doing.

### The `ps` Command: Viewing Processes

Use `ps` (process status) to see running processes.

```bash
ps
# Example Output:
#    PID TTY          TIME CMD
#   2925 pts/0    00:00:00 bash
#  12968 pts/0    00:00:00 ps
```

* **PID:** Process ID (unique number for each running program).
* **TTY:** Terminal; `?` means not tied to a specific terminal.
* **TIME:** CPU time used by the process (not wall-clock time).
* **CMD:** The command that started the process.

#### Viewing All Your Processes

To see all processes started by your user (even those not tied to the current terminal):

```bash
ps x
```

This shows more processes (e.g., graphical apps). You might see a `STAT` column, indicating the process state (e.g., `S` = sleeping, `R` = running).

#### Viewing All Processes on the System

For all processes on the system (regardless of user):

```bash
ps aux
```

* **USER:** Owner of the process (name, easier than numeric UID).
* **%CPU:** Percent of CPU used by the process.
* **%MEM:** Percent of memory (RAM) used by the process.
* **START:** Time or date when the process began.

Think of `ps aux` as your primary tool for a quick overview of system activity.

### Beyond `ps` (Basic Process Control for Beginners)

* **`top`:** An interactive, real-time process viewer (like a terminal task manager). Displays processes sorted by CPU usage. Press `q` to exit `top`.
* **`kill <PID>`:** Stop a frozen or misbehaving process by its PID. First find the PID (with `ps aux` or `top`), then:

  ```bash
  kill 12345
  ```

  Example: To stop a process with PID 12345, run `kill 12345`.

⚡ **Bonus Tool: htop (Interactive Process Viewer)**
`htop` is an enhanced, user-friendly alternative to `top`. It shows a colorful display of processes and resource meters, with easy keyboard shortcuts to sort or kill processes. Install it on Rocky Linux with:

```bash
sudo dnf install htop
```

Then run `htop`.


## Homework

### Process listing and control

In a script named `hw9_commands.sh`, write commands to:

* Save a full system process snapshot to `all_procs.txt`.
* Show only your user's processes.
* Launch a background `sleep 200` process.
* Find and kill that `sleep` process by its PID.

---

### Email submission

**Subject:** HW9 – Process Management

**Attach:**
* `hw9_commands.sh` (your script)
* `all_procs.txt` (the snapshot from step 1)

**In the body:**
State the PID you identified and killed.




## 10. Useful Utilities

Here are some handy commands and utilities:

```bash
find . -type f -name "*.log" -exec gzip {} \;
tar -cJvf archive.tar.xz /path/to/dir
tar -xzvf archive.tar.xz
sudo <command>
sudo -i                # interactive root shell
```

### Vim (Text Editor)

Vim is a powerful terminal-based text editor, available by default on most Unix-like systems.

**Basic Vim Workflow:**

1. **Start Vim:**

   ```bash
   vim filename.txt
   ```

2. **Vim Modes:**

   * **Normal Mode (default):** Navigate, delete, copy, paste.
   * **Insert Mode:** Type text. Press `i` to enter insert mode.
   * **Command Mode:** Save, quit, and more. Press `:` to enter command mode.

3. **Essential Commands (in Normal Mode):**

   * `i` → Enter insert mode (to start typing).
   * `<Esc>` → Return to normal mode.
   * `:w` → Save (write) the file.
   * `:q` → Quit Vim.
   * `:wq` → Save and quit.
   * `:q!` → Quit without saving.
   * `dd` → Delete (cut) the current line.
   * `yy` → Copy (yank) the current line.
   * `p` → Paste after the current line.
   * `/word` → Search for “word” in the file.
   * `n` → Jump to the next search result.

4. **Exit Vim:** Press `<Esc>`, type `:wq`, and press Enter (save and quit).

**Quick Tip:** If you accidentally open Vim and don’t know how to exit: press `<Esc>`, then type `:q!` and press Enter (force quit without saving).


## Homework

### Archive and compress

Create a script named `hw10_archive.sh` that:

* Finds every `.tmp` file under `~/workdir` and compresses it in place with `gzip`.
* Creates an XZ-compressed tarball `~/backups/workdir_backup.tar.xz` containing the entire `~/workdir` directory.

### Quick Vim edit

In a file at `~/workdir/notes.txt`, insert the line `# Workdir Backup Completed` at the very top, then save and exit Vim, using only Normal, Insert, and Command modes (no mouse).

---

### Email submission

**Subject:** HW10 – Utilities & Vim

**Attach:**
* `hw10_archive.sh`
* A plain text file `vim_steps.txt` listing the exact keystrokes you used in Vim.

**In the body:**
* Paste the output line from `tar -tjf ~/backups/workdir_backup.tar.xz | head -1`.
* One sentence confirming that the first line of `notes.txt` now reads your header.



## 11. Basic Networking Commands

### SSH (Secure Shell): Remote Server Management

SSH is a secure way to connect to and manage Linux servers remotely. You can execute commands on a distant server as if you were sitting in front of it.

* **Basic Connection:** Connect by specifying your username and the server’s address:

  ```bash
  ssh user@remote-host
  ```

  * `user`: Your username on the remote server.
  * `remote-host`: The server’s IP address or domain name.
* **First-Time Connection:** The first time you connect, SSH will ask you to confirm the server’s authenticity. Type `yes` and press Enter.
* **Password Prompt:** After confirming, you’ll be prompted for the remote user’s password.
* **Default Username:** If your local username matches your remote username, you can omit `user@`:

  ```bash
  ssh remote-host  # if local_user == remote_user
  ```
* **Specify a Different Port:** If the server uses a non-standard SSH port (not 22), use `-p`:

  ```bash
  ssh -p 2222 user@remote-host
  ```
* **Exiting an SSH Session:** To disconnect, type:

  ```bash
  exit
  ```

### Other Network Commands

* **Test Connectivity (`ping`):** Check if a host is reachable. Example:

  ```bash
  ping -c 4 example.com  # send 4 packets to example.com
  ```
* **Secure Copy (`scp`):** Copy files between local and remote hosts using SSH. Examples:

  ```bash
  scp file.txt user@remote-host:/path/to/dest   # copy local to remote
  scp -r mydir/ user@remote-host:/backup/      # recursively copy directory
  ```
* **Network Statistics (`netstat` / `ss`):** List active connections and ports. `netstat` is older; `ss` is a modern, faster alternative. Examples:

  ```bash
  netstat -tuln   # list listening TCP/UDP ports (numeric)
  ss -tulwn       # same, more verbose
  ```



## Homework

### Compose a networking script

Create `hw11_commands.sh` containing commands to:

* SSH into `devops@myserver.example.com` on port `2223` and print the remote hostname.
* Ping `example.org` exactly 4 times, saving the output to `ping_output.txt`.
* Securely copy the local file `/var/log/custom.log` to `devops@myserver.example.com:~/remote_logs/`.
* List all listening TCP ports numerically using `ss`.

---

### Email submission

**Subject:** HW11 – Networking Commands

**Attach:**
* `hw11_commands.sh`
* `ping_output.txt`

**In the body:**
* Paste the first line of `ping_output.txt`.
* One sentence describing what you saw when you ran `ss -tln`.




###  Hands-On Exercises

---

 **Getting Help**
   **Objective:** Compare different help systems (man pages, built-in `--help`, and community-driven tldr) to understand their output formats and uses.
   *Description:* Capture the first lines of documentation from three sources for comparison.

   **Task:**

   ```bash
   man ls        | head -n2 > help_ls.txt
   ls --help     | head -n2 > help_ls2.txt
   sudo dnf install -y tldr && tldr tar | head -n5 > help_tldr_tar.txt
   ```

   **Validate:**

   ```bash
   wc -l help_ls.txt help_ls2.txt help_tldr_tar.txt
   # Expect: 2  2  5
   ```

 **Package Management (DNF)**
   **Objective:** Gain hands-on experience searching for, installing, listing, and removing RPM packages via DNF, and learn how to verify package state.
   *Description:* Install and remove `nano`, install `git`, capture the installed-package list, then confirm each package’s status.

   **Task:**

   ```bash
   dnf search nano
   sudo dnf install -y nano git
   dnf list installed | grep -E 'nano|git' > pkg_list.txt
   sudo dnf remove -y nano
   ```

   **Validate:**

   ```bash
   grep -q git pkg_list.txt && echo "git OK"
   grep -q nano pkg_list.txt && echo "nano installed"
   dnf list installed | grep -q nano || echo "nano removed"
   ```

 **Basic Navigation & File Operations**
   **Objective:** Practice creating nested directories, and using copy, move, and remove operations to manipulate files in a project scaffold.
   *Description:* Build a standard project structure and move a README through copy, rename, and deletion steps.

   **Task:**

   ```bash
   mkdir -p project/{src,docs,tests}
   cd project
   touch README.md
   cp README.md docs/
   mv docs/README.md docs/INTRO.md
   rm docs/INTRO.md
   ```

   **Validate:**

   ```bash
   tree project  # Should show only src/ docs/ tests/
   ```

 **Vim Practice**
   **Objective:** Familiarize yourself with basic Vim modes: insert, normal, deletion, find-and-replace, and saving/exiting.
   *Description:* Use Vim to insert text, delete a line, globally replace a word, then save and quit.

   **Task:**

   ```bash
   touch vim_practice.txt
   vim vim_practice.txt
   # In Vim:
   #  1) Press i, type three lines
   #  2) Press <Esc>, move to line 2, type dd
   #  3) Enter :%s/Vim/VIM/g, then :wq
   ```

   **Validate:**

   ```bash
   grep -q 'Line one: Hello VIM!' vim_practice.txt && echo "Vim OK"
   ```

 **Working with File Content**
   **Objective:** Generate sample text data, practice viewing subsets with `head`/`tail`, and locate a specific line with `grep -n`.
   *Description:* Create a 5-line file, inspect its beginning and end, and confirm you can pinpoint “Line 3.”

   **Task:**

   ```bash
   cd project/src
   for i in {1..5}; do echo "Line $i" >> sample.txt; done
   head -n3 sample.txt
   tail -n2 sample.txt
   grep -n "Line 3" sample.txt
   ```

   **Validate:**

   ```bash
   grep -q '^3:Line 3' sample.txt && echo "Content OK"
   ```

 **Permissions & Ownership**
   **Objective:** Understand Unix file permissions by making a script executable only by its owner, and verify the permission bits.
   *Description:* Create a `run.sh` script, inspect its default permissions, tighten them, and check the result.

   **Task:**

   ```bash
   echo 'echo Hello' > project/src/run.sh
   ls -l project/src/run.sh
   chmod u+x,go-rwx project/src/run.sh
   ```

   **Validate:**

   ```bash
   ls -l project/src/run.sh | grep -q '^-.rwx' && echo "Perms OK"
   ```

 **Process Management**
   **Objective:** Launch background jobs, capture and inspect their PIDs, and learn how to terminate them cleanly.
   *Description:* Run `sleep` in the background, confirm it’s alive via `ps`, then kill it using its PID.

   **Task:**

   ```bash
   sleep 120 & echo $! > sleep.pid
   ps x | grep '[s]leep'
   ps aux | grep '[s]leep'
   kill "$(cat sleep.pid)"
   ```

   **Validate:**

   ```bash
   ps aux | grep sleep | grep -v grep || echo "Process gone"
   ```

 **Useful Utilities: find & tar**
   **Objective:** Combine `find` with `tar` to archive and extract sets of files, reinforcing directory-and-path handling.
   *Description:* Locate all `.log` files, archive them into a compressed tarball, then unpack them into a new folder.

   **Task:**

   ```bash
   mkdir -p project/tests
   touch project/tests/{a.log,b.log,c.log}
   find project/tests -name '*.log' > logs.txt
   tar -czf project/tests/logs.tar.gz -C project/tests *.log
   mkdir project/tests/extracted
   tar -xzf project/tests/logs.tar.gz -C project/tests/extracted
   ```

   **Validate:**

   ```bash
   test -f project/tests/logs.tar.gz && echo "Archive OK"
   ls project/tests/extracted | grep -q 'a.log' && echo "Extract OK"
   ```

 **Basic Networking**
    **Objective:** Verify basic network connectivity, practice SSH to localhost (loopback), and use SCP for secure file copy.
    *Description:* Ping an external host, open/close an SSH session on localhost, then transfer a file via SCP.

    **Task:**

    ```bash
    ping -c1 google.com
    ssh localhost exit
    scp project/src/sample.txt project/src/sample_copy.txt .
    ```

    **Validate:**

    ```bash
    test -f project/src/sample_copy.txt && echo "SCP OK"
    ```

 **Shell Scripting**
    **Objective:** Build a reusable Bash script that orchestrates multiple commands, then execute it to observe end-to-end flow.
    *Description:* Write `run_all.sh` to call your `run.sh` test script, make it executable, and run it.

    **Task:**

    ```bash
    cat > project/run_all.sh << 'EOF'
    #!/bin/bash
    echo "Starting Tests"
    cd project/src && bash run.sh
    echo "Done"
    EOF
    chmod +x project/run_all.sh
    project/run_all.sh
    ```

    **Validate:**

    ```bash
    project/run_all.sh | grep -q Hello && echo "Script OK"
    ```

---



## Task : Install EPICS Base on your Linux system

**Objective:** Install EPICS Base on your Linux system. This requires researching the correct commands and procedures for your specific Linux distribution.

**Steps:**

1. **Research Prerequisites:**

   * Identify the system packages and development tools needed to compile EPICS Base. These typically include C/C++ compilers, `make`, `perl`, and specific development libraries (e.g., `readline`).
   * Install these dependencies using your distribution’s package manager (`dnf` for Rocky Linux/RHEL-based systems, `apt` for Debian/Ubuntu). Use `sudo` as needed.
2. **Obtain EPICS Base Source Code:**

   * Find the official EPICS Base source repository or download link.
   * Download or clone the source code into a suitable directory in your home folder (e.g., `~/EPICS`).
3. **Build EPICS Base:**

   * Navigate into the EPICS Base directory you downloaded.
   * Start the build process (usually by running `make` or `gnumake`, possibly with certain options). For example:

     ```bash
     make
     ```
   * Watch for error messages. If there are missing dependencies or configuration issues, install additional packages or adjust settings as needed.
4. **Configure Environment Variables:**

   * After building successfully, set environment variables: `EPICS_BASE`, `EPICS_HOST_ARCH`, and add the EPICS `bin` directory to your `PATH`.
   * Learn how to make these changes permanent (for example, by editing `~/.bashrc` or `~/.profile` so that the variables are set each time you open a terminal).
   * Apply the changes immediately in your current session with the `source` command (e.g., `source ~/.bashrc`).
5. **Test the Installation:**

   * Run the `softIoc` command, which is a basic EPICS I/O controller.
   * If EPICS is installed correctly, you should see an `epics>` prompt.
   * Exit the `softIoc` prompt (usually by pressing `Ctrl+C` or typing `exit`).

**Evaluation:**

* Can you successfully run `softIoc` from any terminal after setting up your environment variables?
* Are all necessary files and directories created by the build process present in your EPICS installation path?
