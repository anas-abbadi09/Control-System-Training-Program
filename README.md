Linux Command Line

1. Introduction to the Linux Command Line
   Welcome to the Linux command line (shell, terminal, or console)—a powerful text-based interface. While GUIs are user-friendly, the CLI offers unmatched power, flexibility, and speed, making it essential for developers, sysadmins, and power users.

**Why the Command Line Matters:**

* **Automation & Scripting:** Automate repetitive tasks with shell scripts to save time and reduce errors.
* **Power & Flexibility:** Perform advanced configuration and troubleshooting not available in GUIs.
* **Efficiency:** One well-crafted command can replace dozens of GUI clicks.
* **Remote Access:** Manage servers over SSH.
* **Lightweight:** Uses far fewer resources than a full desktop—key on servers.
* **Consistency:** Core tools and syntax remain the same across distributions.

2. Structure of a Command

```
command [options] [arguments]
```

* **command:** program name (e.g., `ls`, `cp`)
* **options:** modify behavior (e.g., `-l`, `--recursive`)
* **arguments:** targets (files, directories, patterns)

**Example:**

```bash
grep -rin "TODO" ~/projects
```

3. Opening a Terminal & The Prompt

**Terminal vs. Console: What's the Difference?**
While often used interchangeably, here’s a quick distinction:

* A **console** was historically a physical, direct interface to a computer—think of it as the raw, built-in access point.
* A **terminal** (or more accurately, a **terminal emulator**) is the software application you use today. It simulates that physical console experience within your graphical desktop. When you open “Terminal” on your Linux machine, you’re launching a terminal emulator.

Popular examples include:

* **Terminal** (often the default in GNOME-based distributions)
* **Konsole** (common in KDE environments)
* **xterm** (a classic and lightweight option)

Essentially, a terminal emulator is your window to the command line, allowing you to type commands and see their output in a text-based environment.

――――――――――――――――――――

**The Command Prompt Format**
When you open a terminal emulator, you’ll see a prompt indicating the system is ready for your input. It usually looks like this:

```
user@hostname:~/current/path$
```

Here’s what each part means:

* **user:** Your current username.
* **hostname:** The name of your computer.
* **\~:** A shortcut for your home directory (e.g., `/home/yourusername`).
* **/current/path:** Your current working directory. If you’re in your home directory, this will just be `~`.
* **\$:** Indicates you’re a regular user. If it were `#`, you’d be the root (administrative) user.

You can customize this prompt’s appearance and information by editing the `PS1` variable in your `~/.bashrc` file.

4. Getting Help

* `man <command>`: detailed manual
* `<command> --help`: quick usage summary
* `info <command>`: hyperlinked docs
* `apropos <keyword>`: search man-page descriptions
* `whatis <command>`: one-line summary

**⚡ Bonus Tool: tldr (Too Long; Didn’t Read)**

* `tldr <command>`: For quick, practical examples and common use cases, tldr provides simplified, community-contributed “man pages.” It’s excellent for when you just need to remember how to perform a specific task without sifting through all the details. *Note: tldr is a separate tool and might need to be installed on your system if it’s not available by default.*

Here’s the concise version of the “Package Management with DNF” section:

――――――――――――――――――――

5. Package Management with DNF
   Rocky Linux, like other Red Hat-based distributions, uses a robust system for managing software called the RPM Ecosystem. Understanding its core components is essential:

* **RPM (Red Hat Package Manager):** The low-level package format. An RPM file (`.rpm`) is a self-contained archive that includes the software, metadata about its version, dependencies, and the correct file locations on the system.
* **DNF (Dandified YUM):** The next-generation package manager you’ll primarily interact with. DNF serves as a smart interface to RPM packages and has replaced the older YUM command.
* **Repositories:** Centralized online servers (or local directories) that store collections of RPM packages. When you use DNF to install software, it automatically fetches the package (and its dependencies) from these repositories.

DNF is the default package manager for Rocky Linux. It handles software installation, updates, and removal while managing dependencies automatically. Most DNF commands require `sudo`. When you install software, DNF resolves and installs all required dependencies to ensure the software functions correctly.

**Essential DNF Commands**

* **Install:**

  ```bash
  sudo dnf install <package_name(s)>
  ```

  *Example:* `sudo dnf install htop alacritty`
* **Remove:**

  ```bash
  sudo dnf remove <package_name(s)>
  ```

  *Example:* `sudo dnf remove htop ulauncher`
* **Search:**

  ```bash
  dnf search <keyword>
  ```

  (No `sudo` needed.) *Example:* `dnf search apache` (Often `httpd` for web server)
* **List Installed:**

  ```bash
  dnf list installed
  ```

  (No `sudo` needed.)
* **Upgrade All (System Update):**

  ```bash
  sudo dnf upgrade
  ```

  Crucial for security; run regularly. (`sudo dnf update` works too.)
* **Upgrade Specific:**

  ```bash
  sudo dnf upgrade <package_name>
  ```

  *Example:* `sudo dnf upgrade firefox`
* **Reinstall:**

  ```bash
  sudo dnf reinstall <package_name>
  ```
* **Remove Unused Dependencies:**

  ```bash
  sudo dnf autoremove
  ```
* **Clean Caches:**

  ```bash
  sudo dnf clean all
  ```

――――――――――――――――――――

5. Basic Navigation & File Management

```bash
# Show current directory
pwd

# List files
ls -lhSr              # long, human-readable, sorted by size (reverse)

# Change directory
cd /path/to/dir
cd ..                 # parent
cd -                  # previous directory
cd                    # home

# Make directories
mkdir -p parent/child # nested in one shot

# Create/update file timestamp
touch file.txt

# Copy
cp -a src/ dest/      # archive mode: preserves perms, timestamps, symlinks

# Move/rename
mv file.txt ../other/

# Remove
rm -i file.txt        # interactive, safer delete
rmdir empty-dir
rm -rf dir-to-delete  # DANGER: no undo
```

**⚡ Bonus Tool: Ranger (Terminal File Manager)**
For a visual and interactive way to navigate and manage files directly within your terminal, `ranger` is an excellent tool. It provides a two-pane or three-pane interface similar to graphical file managers, allowing you to browse directories, preview files, and perform common file operations with keyboard shortcuts. *To use Ranger, you’ll likely need to install it first if it’s not present on your system. Once installed, simply type `ranger` in your terminal to launch it.*

6. Working with File Content

```bash
# View entire file
cat file.txt

# Page through long files
less /var/log/messages

# Head & tail
head -n5 file.txt
tail -n20 file.txt
tail -f /var/log/messages

# Search text
grep -Rin "error" ~/projects
```

Consider faster alternatives like `ripgrep` (`rg`) for large codebases.

――――――――――――――――――――

7. Permissions & Ownership
   Permissions and ownership are fundamental to Linux security and access control. They define who can perform actions on files and directories.

**Viewing Permissions**
Use `ls -l` to see the permission string (e.g., `drwxr-xr--`) along with other file details.

* **First Character:**

  * `d`: Directory
  * `-`: File
  * `l`: Symbolic Link
* **Next Nine Characters (Permissions):** Divided into three groups of three:

  * **User (Owner):** Permissions for the file’s owner.
  * **Group:** Permissions for the file’s owning group.
  * **Others (World):** Permissions for everyone else.

Each character in these groups represents:

* `r`: Read (view file content / list directory content)
* `w`: Write (modify/delete file / create/delete files in directory)
* `x`: Execute (run file as program / enter directory)
* `-`: Permission not granted

*Example* `drwxr-xr--`: It’s a directory. Owner has read, write, execute. Group has read, execute. Others have only read.

――――――――――――――――――――

**Changing Permissions (`chmod`)**
The `chmod` command modifies permissions.

1. **Symbolic Mode (Easier to read)**
   Uses `who` + `+`/`-`/`=` permission syntax.

   * **Who:** `u` (user), `g` (group), `o` (others), `a` (all)
   * **Action:** `+` (add), `-` (remove), `=` (set exactly)
   * **Permissions:** `r` (read), `w` (write), `x` (execute)

   *Examples:*

   ```bash
   chmod u+x script.sh        # Add execute for owner
   chmod go-w secret.txt      # Remove write for group and others
   ```

2. **Numeric (Octal) Mode (More concise)**
   Uses a three-digit number (`chmod XXX file`). Each digit represents User, Group, Others respectively. Sum the values for desired permissions:

   | Sum | Permissions |
   | :-- | :---------- |
   | 0   | ---         |
   | 1   | --x         |
   | 2   | -w-         |
   | 3   | -wx         |
   | 4   | r--         |
   | 5   | r-x         |
   | 6   | rw-         |
   | 7   | rwx         |

   *Examples:*

   ```bash
   chmod 755 script.sh         # rwxr-xr-x (Common for scripts/directories)
   chmod 644 config.yaml       # rw-r--r-- (Common for config files)
   chmod -R 770 my_project/    # Recursively set rwxrwx--- for project and its contents
   ```

――――――――――――――――――――

**Changing Ownership (`chown`)**
The `chown` command changes the user and/or group owner. Requires `sudo`.

* `sudo chown <new_owner> <file/dir>`: Change user owner.
* `sudo chown :<new_group> <file/dir>`: Change group owner.
* `sudo chown <new_owner>:<new_group> <file/dir>`: Change both.

  * Tip: `<new_owner>:` (without group) defaults group to the new owner’s primary group.
* `-R`: Recursive (for directories and their contents).

*Examples:*

```bash
sudo chown alice:developers project/       # Change project/ owner to alice and group to developers
sudo chown -R bob: project_data/           # Recursively change owner to bob for project_data/ and all contents; group defaults to bob’s primary group
```

*I understand. I’ll simplify the “Process Management” section, keeping only the most essential information and commands for a beginner in a university Linux basics course.*

――――――――――――――――――――

8. Process Management
   Process management involves monitoring and controlling the programs and tasks running on your Linux system. Understanding processes is crucial for troubleshooting simple issues and seeing what your computer is doing.

**The `ps` Command: Viewing Processes**
The `ps` (process status) command shows you what’s currently running.

* **Basic `ps` Output (Processes in your current terminal)**
  When you run `ps` without any options, it shows only the processes linked to your current terminal window:

  ```bash
  ps
  # Example Output:
  #    PID TTY          TIME CMD
  #   2925 pts/0    00:00:00 bash
  #  12968 pts/0    00:00:00 ps
  ```

  **What the Columns Mean:**

  * **PID:** Process ID. A unique number for each running program.
  * **TTY:** Terminal. The terminal where the process is running. A `?` means it’s not tied to a specific terminal.
  * **TIME:** CPU Time. How much CPU time the process has used, not how long it’s been running.
  * **CMD:** Command. The actual command that started the process.

* **Viewing All Your Processes (`ps x`)**
  To see all processes started by your user account, even those not tied to your current terminal:

  ```bash
  ps x
  ```

  This output will likely show more processes, including programs like web browsers or graphical applications you’ve launched. You might also see a new column:

  * **STAT** (Process Status): Shows the current state of the process (e.g., `S` for sleeping, `R` for running).

* **Viewing All Processes on the System (`ps aux`)**
  This is one of the most common and useful ways to use `ps`. It displays all processes running on the entire system, regardless of who started them or which terminal they’re associated with.

  ```bash
  ps aux
  ```

  **Why `ps aux` Is So Useful (New Columns):**

  * **USER:** The name of the user who owns the process. Easier to read than a numerical user ID.
  * **%CPU:** The percentage of your computer’s CPU that the process is currently using. High numbers can indicate a busy or stuck program.
  * **%MEM:** The percentage of your computer’s memory (RAM) that the process is using. High numbers can indicate a memory-hungry application.
  * **START:** The time or date when the process began. Useful for seeing if a program has unexpectedly restarted.

Think of `ps aux` as your primary tool for a quick overview of system activity.

――――――――――――――――――――

**Beyond `ps` (Basic Process Control for Beginners)**
While `ps` helps you see processes, sometimes you need to manage them.

* **top:** An interactive command that shows processes in real time, sorted by CPU usage. It’s like a live task manager in your terminal. Press `q` to exit `top`.
* **kill <PID>:** If a program is frozen or misbehaving, you can often stop it using the `kill` command with its PID.

  * **How to use:** First, find the PID of the problematic process using `ps aux` or `top`. Then, run `kill <PID>`.
  * *Example:* If a process with PID `12345` is frozen: `kill 12345`

**⚡ Bonus Tool: htop (Interactive Process Viewer)**
`htop` is an enhanced and more user-friendly alternative to `top`. It provides a colorful, interactive display of processes, resource usage meters, and allows for easier sorting and killing of processes with keyboard shortcuts.

* Not installed by default. Install with:

  ```bash
  sudo dnf install htop
  ```
* Launch with:

  ```bash
  htop
  ```

10. Useful Utilities

```bash
find . -type f -name "*.log" -exec gzip {} \;
tar -cJvf archive.tar.xz /path/to/dir
tar -xzvf archive.tar.xz
sudo <command>
sudo -i                # interactive root shell
```

**Vim (Text Editor)**
Vim is a powerful, terminal-based text editor that’s widely used in Linux environments. It’s fast, efficient, and available by default on almost all Unix-like systems.

**Basic Vim Workflow:**

1. **Start Vim:**

   ```bash
   vim filename.txt
   ```
2. **Modes in Vim:**

   * **Normal Mode** (Default): Navigate, delete, copy, paste.
   * **Insert Mode:** Type text. Press `i` to enter insert mode.
   * **Command Mode:** Save, quit, and more. Press `:` to enter command mode.
3. **Essential Commands:**

   * `i` → Enter insert mode to start typing.
   * `Esc` → Return to normal mode.
   * `:w` → Save (write) the file.
   * `:q` → Quit.
   * `:wq` → Save and quit.
   * `:q!` → Quit without saving.
   * `dd` → Delete (cut) the current line.
   * `yy` → Copy the current line.
   * `p` → Paste after the current line.
   * `/word` → Search for “word” in the file.
   * `n` → Jump to the next search result.
4. **Exit Vim:**
   Press `Esc` → Type `:wq` → Press Enter (save and quit).

*Quick Tip:*
If you accidentally open Vim and don’t know how to exit:

```
Esc  
:q! [Enter]  
```

This will force quit without saving.

――――――――――――――――――――

11. Basic Networking Commands

**SSH (Secure Shell): Remote Server Management**
SSH is the standard and secure way to connect to and manage Linux servers remotely. It allows you to execute commands on a distant server just as if you were sitting in front of it.

* **Basic Connection:**

  ```bash
  ssh user@remote-host
  ```

  *Example:* `ssh j@192.168.1.100`

  * **user:** Your username on the remote server.
  * **remote-host:** The IP address or domain name of the server.
  * **First-Time Connection:** SSH will ask you to confirm its authenticity. Type `yes` and press Enter.
  * **Password Prompt:** You’ll be prompted for your password on the remote server.
  * **Default Username:** If your username on the remote server is the same as your local username, you can omit `user@`:

    ```bash
    ssh remote-host
    ```

* **Specify a Different Port:**
  By default, SSH uses port 22. If the remote server’s SSH service is listening on a different port (e.g., 2222), use the `-p` option:

  ```bash
  ssh -p <port_number> user@remote-host
  ```

  *Example:* `ssh -p 2222 j@192.168.1.100`

* **Exiting an SSH Session:**
  To disconnect and return to your local terminal, type:

  ```bash
  exit
  ```

**Other Network Commands**

* **Test Connectivity (`ping`):**

  ```bash
  ping -c 4 example.com
  ```
* **Secure Copy (`scp`):**

  ```bash
  scp file.txt user@remote-host:/path/to/dest     # Copy local file to remote
  scp -r mydir/ user@remote-host:/backup/        # Recursively copy local directory to remote
  ```
* **Network Statistics (`netstat` / `ss`):**

  * `netstat` is an older command.
  * `ss` is a modern, faster alternative.

  ```bash
  netstat -tuln       # List listening TCP/UDP ports (numeric)
  ss -tulwn           # Modern alternative: numeric, verbose
  ```

<!-- end list -->  

――――――――――――――――――――

12. Hands-On Exercises

――――――――――――――――――――

1. **Prompt Customization**

   * **Task:** Add `export PS1="\u@\h [\t] \$ "` to your `~/.bashrc`, then `source ~/.bashrc`.
   * **Validate:**

     ```bash
     echo $PS1 | grep -q '\\u@\\h \\[\\t\\] \\$' && echo "Prompt OK"
     ```

2. **Getting Help**

   * **Task:**

     1. `man ls | head -n2 > help_ls.txt`
     2. `ls --help | head -n2 > help_ls2.txt`
     3. `sudo dnf install -y tldr && tldr tar | head -n5 > help_tldr_tar.txt`
   * **Validate:**

     ```bash
     wc -l help_ls.txt help_ls2.txt help_tldr_tar.txt  
     # Expect 2, 2, 5
     ```

3. **Package Management (DNF)**

   * **Task:**

     1. `dnf search nano`
     2. `sudo dnf install -y nano git`
     3. `dnf list installed | grep -E 'nano|git' > pkg_list.txt`
     4. `sudo dnf remove -y nano`
   * **Validate:**

     ```bash
     grep -q git pkg_list.txt && echo "git OK"  
     grep -q nano pkg_list.txt && echo "nano installed"  
     dnf list installed | grep -q nano || echo "nano removed"
     ```

4. **Basic Navigation & File Ops**

   * **Task:**

     ```bash
     mkdir -p project/{src,docs,tests}
     cd project
     touch README.md
     cp README.md docs/
     mv docs/README.md docs/INTRO.md
     rm docs/INTRO.md
     ```
   * **Validate:**

     ```bash
     tree project  # only src/ docs/ tests/
     ```

5. **Vim Practice**

   * **Task:**

     ```bash
     touch vim_practice.txt
     vim vim_practice.txt
     ```

     In Vim:

     * `i` → type three lines
     * `Esc` then `dd` on line 2
     * `:%s/Vim/VIM/g`
     * `:wq`
   * **Validate:**

     ```bash
     grep -q 'Line one: Hello VIM!' vim_practice.txt && echo "Vim OK"
     ```

6. **Working with File Content**

   * **Task:**

     ```bash
     cd project/src
     for i in {1..5}; do echo "Line $i" >> sample.txt; done
     head -n3 sample.txt
     tail -n2 sample.txt
     grep -n "Line 3" sample.txt
     ```
   * **Validate:**

     ```bash
     grep -q '^3:Line 3' sample.txt && echo "Content OK"
     ```

7. **Permissions & Ownership**

   * **Task:**

     ```bash
     echo 'echo Hello' > project/src/run.sh
     ls -l project/src/run.sh
     chmod u+x,go-rwx project/src/run.sh
     ```
   * **Validate:**

     ```bash
     ls -l project/src/run.sh | grep -q '^-.rwx' && echo "Perms OK"
     ```

8. **Process Management**

   * **Task:**

     ```bash
     sleep 120 & echo $! > sleep.pid
     ps x | grep '[s]leep'
     ps aux | grep '[s]leep'
     kill "$(cat sleep.pid)"
     ```
   * **Validate:**

     ```bash
     ps aux | grep sleep | grep -v grep || echo "Process gone"
     ```

9. **Useful Utilities: `find` & `tar`**

   * **Task:**

     ```bash
     mkdir -p project/tests
     touch project/tests/{a.log,b.log,c.log}
     find project/tests -name '*.log' > logs.txt
     tar -czf project/tests/logs.tar.gz -C project/tests *.log
     mkdir project/tests/extracted
     tar -xzf project/tests/logs.tar.gz -C project/tests/extracted
     ```
   * **Validate:**

     ```bash
     test -f project/tests/logs.tar.gz && echo "Archive OK"
     ls project/tests/extracted | grep -q 'a.log' && echo "Extract OK"
     ```

10. **Basic Networking**

    * **Task:**

      ```bash
      ping -c1 google.com
      ssh localhost exit
      scp project/src/sample.txt project/src/sample_copy.txt
      ```
    * **Validate:**

      ```bash
      test -f project/src/sample_copy.txt && echo "SCP OK"
      ```

11. **Shell Scripting**

    * **Task:**

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
    * **Validate:**

      ```bash
      project/run_all.sh | grep -q Hello && echo "Script OK"
      ```

**Task 1:**
**Objective:** Install EPICS Base on your Linux system. This will require independent research to identify the correct commands and procedures for your specific Linux distribution.

**Steps:**

1. **Research Prerequisites:**

   * Research the necessary system packages and development tools required to compile EPICS Base (e.g., C/C++ compilers, `make`, Perl, and development libraries such as readline).
   * Install these dependencies using your distribution’s package manager (`dnf` for Rocky/RHEL-based systems, `apt` for Debian/Ubuntu systems). Use `sudo` where necessary.
2. **Obtain EPICS Base Source Code:**

   * Find the official source code repository or download link for EPICS Base.
   * Download or clone the source code into a suitable directory in your home folder (e.g., `~/EPICS`).
3. **Build EPICS Base:**

   * Navigate into the downloaded EPICS Base directory.
   * Initiate the build process (likely using `make`, possibly with specific options).
   * Troubleshoot any errors—this may involve installing additional dependencies or adjusting configuration files.
4. **Configure Environment Variables:**

   * After a successful build, set environment variables (`EPICS_BASE`, `EPICS_HOST_ARCH`) and add EPICS executables to your `PATH`.
   * Permanently add these to your shell environment by editing `~/.bashrc` or `~/.profile`.
   * Apply changes without logging out using `source`.
5. **Test the Installation:**

   * Run `softIoc` from your terminal. A successful run shows an `epics>` prompt.
   * Exit the prompt (usually `Ctrl+C` or `exit`).

**Evaluation:**

* Can you run `softIoc` from any terminal after setting up your environment variables?
* Are all necessary files and directories created by the build process present in your EPICS installation path?
