## Importing Modules and Exploring the Standard Library  

*Modules are Python files containing reusable code (functions, variables, classes). The standard library is a rich collection of pre-built modules included with Python, offering solutions for common tasks like math operations, date handling, and OS interactions.*



#### **1. Basic Module Import**  
*Import entire modules with `import module_name`. All top-level code executes upon import.*  

```python
# my_module.py
test = "Test string"
def find_index(to_search, target):
    """Finds index of target in sequence"""
    for i, value in enumerate(to_search):
        if value == target:
            return i
    return -1

# main.py
import my_module
courses = ["Math", "Art", "Physics"]
index = my_module.find_index(courses, "Art")
print(index)  # Output: 1
```



#### **2. Import Techniques**  
*Control what gets imported using aliases and selective imports. Avoid `import *` for clarity.*  

```python
import my_module as mm  # Alias
idx = mm.find_index(courses, "Physics")  # 2

from my_module import find_index  # Import specific function
idx = find_index(courses, "Math")  # 0

from my_module import find_index as fi, test  # Import with aliases
print(fi(courses, "History"))  # -1
```



#### **3. Module Search Path (sys.path)**  
*Python searches for modules in directories listed in `sys.path` (in order):*  
1. Current script's directory  
2. `PYTHONPATH` environment variable directories  
3. Standard library paths  
4. `site-packages` for third-party packages  

```python
import sys
print(sys.path)  # View search paths

# Manually add a module directory
sys.path.append("/Users/me/Desktop/my_modules")
```



#### **4. Setting PYTHONPATH**  
*Add custom directories to module search path:*  

- **Mac/Linux**:  
  ```bash
  # ~/.bash_profile
  export PYTHONPATH="/path/to/directory:$PYTHONPATH"
  ```
- **Windows**:  
  `System Properties → Environment Variables → New (PYTHONPATH)`  
  


#### **5. Standard Library Modules**  
*Key modules and their uses:*  

- **random**: Random selections  
  ```python
  import random
  print(random.choice(["Heads", "Tails"]))  # Heads/Tails
  ```

- **math**: Mathematical operations  
  ```python
  import math
  print(math.radians(180))  # 3.14159 (π radians)
  print(math.sin(math.pi/2))  # 1.0
  ```

- **datetime & calendar**: Date/time handling  
  ```python
  from datetime import date
  import calendar
  print(date.today())  # 2023-09-15
  print(calendar.isleap(2024))  # True
  ```

- **os**: OS interactions  
  ```python
  import os
  print(os.getcwd())  # /current/working/directory
  ```


#### **6. Inspecting Modules**  
*Locate module source files using `.__file__`*  

```python
import os
print(os.__file__)  
# Output: /path/to/python/lib/os.py (actual path varies)
```

 


### Homework: Module Explorer  
*Create `module_demo.py` that:*  

1. **Uses Standard Library Modules**  
   ```python
   import math, datetime, os, random
   ```

2. **Implement Functionality**  
   - Calculate circle area (`math.pi`)  
   - Print today's weekday (`datetime.date.today().strftime("%A")`)  
   - List first 3 items of shuffled list (`random.shuffle()`)  
   - Check if a directory exists (`os.path.isdir()`)

3. **Test Cases**  
   ```python
   # Circle radius=5 → ~78.54
   # Weekday name (e.g., "Friday")
   # Shuffled [1,2,3] → [3,1,2] (example)
   # Check if /tmp exists → True/False
   ```




## OS Module: Interacting with the Operating System  
*The `os` module provides a portable way to interact with the operating system, allowing Python scripts to perform file system operations, environment management, and path manipulations across different platforms.*


#### **1. Directory Navigation**  
*Get and change working directories to navigate the file system.*  

```python
import os

# Get current working directory
print(os.getcwd())  # Output: /current/path

# Change directory
os.chdir('/Users/me/Desktop')
print(os.getcwd())  # Output: /Users/me/Desktop
```


#### **2. File & Directory Operations**  
*Create, remove, and list directory contents with proper recursive handling.*  

```python
# List directory contents
print(os.listdir())  # Output: ['file1.txt', 'folder1', ...]

# Create directories (single vs recursive)
os.mkdir('new_folder')             # Single directory
os.makedirs('parent/child/grandchild')  # Nested directories

# Remove directories
os.rmdir('empty_folder')              # Remove empty directory
os.removedirs('parent/child/grandchild')  # Remove nested empty directories

# Rename files
os.rename('old.txt', 'new.txt')
```



#### **3. File Information & Metadata**  
*Access file statistics and convert timestamps to readable formats.*  

```python
file_stats = os.stat('demo.txt')
print(f"Size: {file_stats.st_size} bytes")  # File size
print(f"Modified: {file_stats.st_mtime}")   # Timestamp

# Convert to readable datetime
from datetime import datetime
mod_time = datetime.fromtimestamp(file_stats.st_mtime)
print(f"Last modified: {mod_time}")
```


#### **4. Directory Tree Traversal**  
*Use `os.walk()` to recursively explore directory structures.*  

```python
for dirpath, dirnames, filenames in os.walk(os.getcwd()):
    print(f"Current Path: {dirpath}")
    print(f"Subdirectories: {dirnames}")
    print(f"Files: {filenames}")
    print("-" * 50)
```



#### **5. Environment Variables**  
*Access and utilize system environment variables.*  

```python
# Get home directory
home_dir = os.environ.get('HOME')
print(f"Home directory: {home_dir}")

# Create file path in home directory
file_path = os.path.join(home_dir, 'test.txt')
print(f"Full path: {file_path}")  # Output: /Users/me/test.txt
```



#### **6. Path Manipulation with `os.path`**  
*Safely handle path operations across different OS platforms.*  

```python
# Combine paths safely
full_path = os.path.join(home_dir, 'Documents', 'file.txt')

# Path components
print(os.path.basename(full_path))   # file.txt
print(os.path.dirname(full_path))    # /Users/me/Documents
print(os.path.split(full_path))      # ('/Users/me/Documents', 'file.txt')

# File properties
print(os.path.exists(full_path))     # True/False
print(os.path.isfile(full_path))     # True if file
print(os.path.isdir(full_path))      # True if directory

# File extensions
root, ext = os.path.splitext('document.pdf')
print(f"Root: {root}, Extension: {ext}")  # Root: document, Extension: .pdf
```



### 💎 Key Insights  
1. **Cross-Platform Compatibility**: Write once, run anywhere  
2. **Safe Path Handling**: Always use `os.path.join()` instead of string concatenation  
3. **Recursive Operations**: `makedirs()`/`removedirs()` handle nested directories  
4. **Metadata Access**: Get rich file information beyond basic attributes  
5. **Environment Awareness**: Adapt scripts to user's system configuration  


### Homework: File System Analyzer  
*Create `analyzer.py` that:*  

1. **Accepts a directory path as input**  
2. **Generates a report containing**:  
   - Total files and folders  
   - File type distribution (by extension)  
   - Largest file size  
   - Last modified timestamp  
   - Directory tree structure  

3. **Required OS Module Features**:  
   ```python
   os.walk()          # Traverse directories
   os.path.getsize()  # Get file size
   os.path.splitext() # Split file extension
   os.stat()          # Get file metadata
   os.path.join()     # Build paths safely
   ```

4. **Sample Output**:  
   ```text
   Analyzed: /Users/me/Documents
   Total Files: 42
   Total Folders: 7
   File Types: 
     .pdf: 12 files
     .txt: 8 files
     .jpg: 15 files
   Largest File: report.pdf (4.2 MB)
   Last Modified: 2023-10-15 14:30:00
   ```
   
