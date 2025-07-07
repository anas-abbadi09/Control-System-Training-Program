**Why Python?**

Every year, new programming languages appear. You might wonder: *Should I switch from Python?* The answer is often no. Here’s why **Python is a great first language**:

1.  **Easy to Read & Write:** Its clean syntax lets you do more with less code. This makes your programs easier to understand, fix, and improve. As Python's creator, Guido van Rossum, said:
  > *“Python is an experiment in how much freedom programmers need. Too much freedom and nobody can read another’s code; too little and expressiveness is endangered.”*

2.  **Versatile & Powerful:** Python is used everywhere! Build websites, analyze data, create AI tools, solve business problems, make games, and more. It’s essential for many careers.

As Bram Cohen aptly described:

  >*“My favorite language for maintainability is Python. It has simple, clean syntax, object encapsulation, good library support, and optional named parameters.”*

3.  **Amazing Community:** You’re never alone. Python has a huge, friendly global community ready to help when you get stuck. This support is vital for learning quickly, especially as a beginner.

Tim Peters, author of *The Zen of Python*, captured the spirit:
> *“The joy of coding Python should be in seeing short, concise, readable code... not in reams of trivial code that bores the reader.”*

Python combines clear syntax, wide usefulness, and strong support. It's the perfect start for any new programmer.

Want to create a game, design digital art, or even control a robot? Python is your toolkit for turning cool ideas into reality faster than you think.

**Ready to begin your Python journey? Let's go!**

---
### **Installing Python on Rocky Linux 9.6**

#### Step 1: Check Python Installation
Verify Python is installed and check your version:
```bash
python --version
```
- ✅ You should see output like: `Python 3.9.21`
- ❌ If you get `command not found`, proceed to Step 2

#### Step 2: Install Python (If Missing)
```bash
sudo dnf update -y
sudo dnf install python3 -y
```

#### Step 3: Confirm Installation
Verify everything works:
```bash
python --version
python -c "print('Linux setup successful! 🐧')"
```

---

### **Homework: Verify Your Setup**
Complete these tasks to confirm your Python environment:

1. **Version Check**  
   Run: `python --version` → Take screenshot showing your version

2. **Interactive Test**  
   Start Python: `python`  
   Run these commands:
   ```python
   print("Coding on Rocky Linux!")
   15 * 4
   exit()
   ```
   → Take screenshot of output

3. **Create Script**  
   Create `rocky_test.py` with:
   ```python
   # Linux Python Verification
   print("My Python version:")
   !python --version  # Jupyter-style system command
   print("\nHomework complete! 🎉")
   ```

4. **Run Script**  
   Execute with:
   ```bash
   python rocky_test.py
   ```
   → Take screenshot showing:
   - Your Python version
   - Success message

---


### 🛠️ Code Editors & IDEs  

1. **Terminal Editors** (Fast & Lightweight)  
   - `nano`: Simple text editor  
   - `vim`/`neovim`: Powerful keyboard-driven editor 

2. **VS Code** (Recommended)  
   Free, feature-rich, with excellent Python support


3. **PyCharm**
   Dedicated Python IDE with advanced debugging  


4. **Sublime Text** (Lightweight)  
   Fast, customizable editor with Python plugins  
---

### 🔢 Working with Numbers in Python  

#### **1. Basic Number Types**  
```python
# Integers (whole numbers)
age = 25
items = 3

# Floats (decimal numbers)
price = 9.99
temperature = 36.6
```

#### **2. Arithmetic Operations**  
```python
# Basic math
print(10 + 3)   # Addition → 13
print(10 - 3)   # Subtraction → 7
print(10 * 3)   # Multiplication → 30
print(10 / 3)   # True division → 3.333...
print(10 // 3)  # Floor division → 3
print(10 % 3)   # Modulus → 1
print(10 ** 3)  # Exponentiation → 1000
```

#### **3. Type Conversion**  
```python
# Convert between types
num_str = "15"
print(int(num_str) + 5)  # → 20

# Float to integer (truncates decimals)
print(int(9.99))  # → 9

# Integer to float
print(float(7))   # → 7.0
```

#### **4. Common Number Methods**  
```python
# Absolute value
print(abs(-5))        # → 5

# Rounding
print(round(3.14159))     # → 3
print(round(3.14159, 2))  # → 3.14

# Check if float is whole number
print((1.0).is_integer())   # → True
print((1.5).is_integer())   # → False
```

#### **5. Practical Example: Shopping Cart**  
```python
# Calculate total price
item_price = 12.50
quantity = 3
tax_rate = 0.08

subtotal = item_price * quantity
tax = round(subtotal * tax_rate, 2)
total = subtotal + tax

print(f"Subtotal: ${subtotal}")
print(f"Tax (8%): ${tax}")
print(f"Total: ${total}")
```

#### **6. Exploring Numeric Methods**  
Discover available operations:
```python
num = 7
print(dir(num))  # Show all methods
print(help(float))  # Detailed help
```

---

### 🧪 Homework: Temperature Converter  
Create `temperature.py` that:
1. Converts 78°F to Celsius using: `(F - 32) * 5/9`
2. Calculates the hypotenuse of a triangle with sides 6 and 8
3. Prints both results formatted as:
   ```
   78°F = 25.56°C
   Hypotenuse: 10.0
   ```

---

