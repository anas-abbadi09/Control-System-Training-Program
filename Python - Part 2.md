## Dictionaries in Python  
*Dictionaries store data as key-value pairs, providing efficient lookup and management of related data. They are mutable, unordered collections ideal for representing real-world entities like users, products, or configurations.*


#### **1. Creating Dictionaries**  
*Use curly braces `{}` with `key: value` pairs separated by commas. Keys must be immutable types (strings, numbers, tuples).*  

```python
# Student dictionary example
student = {
    'name': 'John',      # String key
    'age': 25,           # Integer key
    'courses': ['Math', 'CompSci']  # List value
}

print(student)  # {'name': 'John', 'age': 25, 'courses': ['Math', 'CompSci']}
```



#### **2. Accessing Values**  
*Retrieve values using square bracket notation `[]` or the safer `get()` method.*  

```python
print(student['name'])          # 'John' (direct access)
print(student.get('age'))       # 25 

# Handling missing keys
print(student.get('phone'))     # None (no error)
print(student.get('phone', 'Not Found'))  # 'Not Found' (custom default)
```



#### **3. Modifying Dictionaries**  
*Add/update values using assignment or the `update()` method for multiple changes.*  

```python
# Add new key-value pair
student['phone'] = '555-1234'

# Update existing key
student['name'] = 'Jane'

# Update multiple keys at once
student.update({
    'name': 'Emily',
    'age': 26,
    'email': 'emily@university.edu'
})
```


#### **4. Removing Items**  
*Use `del` for permanent deletion or `pop()` to remove and return the value.*  

```python
del student['age']  # Permanently remove 'age'

# Remove and capture value
email = student.pop('email')  
print(email)  # 'emily@university.edu'
```



#### **5. Dictionary Methods**  
*Key methods for inspection and iteration:*

```python
# Get keys/values/items
print(student.keys())    # dict_keys(['name', 'courses', 'phone'])
print(student.values())  # dict_values(['Emily', ['Math', 'CompSci'], '555-1234'])
print(student.items())   # dict_items([('name', 'Emily'), ...])

# Check existence
print('phone' in student)  # True

# Length of dictionary
print(len(student))  # 3
```



## Conditionals and Booleans in Python  
*Conditionals control program flow using boolean logic. Mastering `if/elif/else` structures and truth value evaluation is essential for decision-making in code.*



#### **1. Boolean Basics**  
*Python has two boolean values: `True` and `False`. Comparisons and operations return these values.*

```python
# Simple comparisons
print(10 > 9)   # True
print(10 == 10) # True
print(10 < 5)   # False
```



#### **2. `if` Statements**  
*Execute code blocks only when conditions evaluate to `True`.*

```python
# Basic if statement
language = "Python"
if language == "Python":
    print("Language is Python")  # Executes

# Using variables
is_admin = True
if is_admin:
    print("Admin privileges granted")
```



#### **3. Comparison Operators**  
*Test relationships between values.*

| Operator | Meaning          | Example          |
|----------|------------------|------------------|
| `==`     | Equal to         | `x == 10`       |
| `!=`     | Not equal to     | `y != "no"`     |
| `>`      | Greater than     | `score > 90`    |
| `<`      | Less than        | `age < 18`      |
| `>=`     | Greater/equal    | `balance >= 0`  |
| `<=`     | Less/equal       | `items <= 5`    |

```python
# Practical comparison
age = 25
if age >= 18:
    print("You can vote!")
```



#### **4. `elif` and `else` Clauses**  
*Handle multiple conditions and default cases.*

```python
# Multi-branch logic
score = 85

if score >= 90:
    print("Grade: A")
elif score >= 80:
    print("Grade: B")  # Executes
elif score >= 70:
    print("Grade: C")
else:
    print("Grade: F")
```



#### **5. Boolean Operators**  
*Combine conditions with `and`, `or`, `not`.*

```python
# Combining conditions
is_premium = True
has_license = False

if is_premium and has_license:
    print("Full access")
elif is_premium or has_license:
    print("Partial access")  # Executes
elif not has_license:
    print("License required") 
```



#### **6. Truth Value Testing**  
*Certain values evaluate to `False` (falsy), others to `True` (truthy).*

**Falsy Values:**  
- `False`
- `None`
- Zero: `0`, `0.0`
- Empty sequences: `""`, `[]`, `()`, `{}`

```python
# Truthy/Falsy examples
values = [False, None, 0, "", [], 1, "Hello", [1,2]]

for val in values:
    if val:
        print(f"{repr(val)} is truthy")
    else:
        print(f"{repr(val)} is falsy")
```



#### **7. Identity vs Equality**  
*`is` checks object identity, `==` checks value equality.*

```python
a = [1, 2, 3]
b = [1, 2, 3]
c = a

print(a == b)  # True (same values)
print(a is b)  # False (different objects)
print(a is c)  # True (same object)
```


### Homework: Authentication System  
*Implement a program that:*  

1. **Validates user credentials**  
   ```python
   username = "admin"
   password = "secure123"
   is_active = True
   ```

2. **Checks multiple conditions**  
   - Verify username/password match  
   - Check account active status  
   - Validate password length > 8 characters  
   - Handle empty inputs  

3. **Provide detailed responses**  
   ```markdown
   Access Report:
   - Username: admin
   - Password: *******
   - Active: Yes
   - Password Strength: Strong
   - Result: ACCESS GRANTED
   ```

*Requirements:*  
- Use `if/elif/else` chain
- Implement at least 3 boolean operators
- Check for falsy values (empty strings)
- Include identity check (`is` operator)
- Test cases:  
  ```python
  # Test 1: Correct credentials (ACCESS GRANTED)
  # Test 2: Correct user, wrong password (DENIED)
  # Test 3: Empty username (INVALID INPUT)
  # Test 4: Correct credentials, inactive (ACCOUNT DISABLED)
  ```

```python
# Starter template
username = input("Username: ")
password = input("Password: ")
is_active = True

# Your conditional logic here
if ...:
    print("ACCESS GRANTED")
elif ...:
    print("ACCOUNT DISABLED")
else:
    print("ACCESS DENIED")
```



### Homework: Employee Database  
*Create `employee_manager.py` that:*  

1. **Initialize a dictionary** for an employee:  
   ```python
   employee = {
       'id': 10247,
       'name': 'Maria Garcia',
       'department': 'Engineering',
       'skills': ['Python', 'SQL', 'Cloud'],
       'start_date': '2021-03-15'
   }
   ```

2. **Implement operations**:  
   - Add `'salary': 85000`  
   - Update department to 'Data Science'  
   - Add skill 'Machine Learning' to the skills list  
   - Remove start_date and store it in a variable  

3. **Create functions**:  
   ```python
   def print_employee(emp):
       # Print formatted employee record
       pass
   
   def add_certification(emp, cert):
       # Add cert to skills if not present
       pass
   ```

4. **Handle edge cases**:  
   - Prevent duplicate skills  
   - Validate department from allowed list: ['Engineering', 'Data Science', 'HR']  
   - Ensure salary is integer  

5. **Final output**:  
   ```
   Employee ID: 10247
   Name: Maria Garcia
   Department: Data Science
   Skills: Python, SQL, Cloud, Machine Learning
   Salary: $85,000
   Certifications: AWS Certified (if added)
   ```

*Requirements:*  
- Use all dictionary operations: get(), update(), pop(), items()  
- Implement loops for skill management  
- Include error handling for invalid keys  
- Format output using f-strings  

## Loops and Iterations in Python  
*Loops automate repetitive tasks by executing code blocks multiple times. Python offers two primary loop types: `for` loops for iterating over sequences and `while` loops for conditional repetition.*

---

#### **1. For Loops**  
*Ideal for iterating over sequences (lists, strings, tuples, etc.). The loop variable takes each value in the sequence sequentially.*  

```python
# Basic list iteration
fruits = ['apple', 'banana', 'cherry']
for fruit in fruits:
    print(fruit.upper())
# Output: APPLE, BANANA, CHERRY

# String iteration
for char in "Python":
    print(char, end='-')  
# Output: P-y-t-h-o-n-
```

#### **2. Loop Control: Break & Continue**  
*Modify loop behavior with these keywords:*
- `break`: Exit loop immediately  
- `continue`: Skip to next iteration  

```python
# Break example
for num in range(1, 6):
    if num == 3:
        print("Found 3!")
        break
    print(num)
# Output: 1, 2, Found 3!

# Continue example
for num in range(1, 6):
    if num == 3:
        print("Skipping 3")
        continue
    print(num)
# Output: 1, 2, Skipping 3, 4, 5
```


#### **3. Nested Loops**  
*Loops within loops create combinations. Use cautiously as complexity grows exponentially.*  

```python
# Matrix iteration
matrix = [[1, 2], [3, 4], [5, 6]]
for row in matrix:
    for num in row:
        print(num * 2, end=' ')
    print()  # New line per row
# Output: 
# 2 4 
# 6 8 
# 10 12
```


#### **4. The range() Function**  
*Generate number sequences for controlled iterations. Syntax: `range(start, stop, step)`.*  

```python
# Basic range
for i in range(5):        # 0-4
    print(i, end=' ')     # 0 1 2 3 4

# Custom range
for i in range(2, 11, 2): # Start=2, Stop=11, Step=2
    print(i, end=' ')     # 2 4 6 8 10
```


#### **5. While Loops**  
*Execute until condition becomes False. Essential for unknown iteration counts.*  

```python
# Basic counter
count = 0
while count < 3:
    print(f"Count: {count}")
    count += 1
# Output: Count:0, Count:1, Count:2

# Controlled infinite loop
x = 0
while True:
    print(x, end=' ')
    x += 1
    if x >= 5:
        break  # Critical exit condition!
# Output: 0 1 2 3 4
```


#### **6. Loop Techniques**  
*Advanced patterns for efficient iteration:*

```python
# Enumerate for indexes
for index, fruit in enumerate(fruits, start=1):
    print(f"{index}. {fruit}")

# Zip for parallel iteration
names = ['Alice', 'Bob', 'Charlie']
ages = [24, 30, 28]
for name, age in zip(names, ages):
    print(f"{name} is {age} years old")
```


### 💎 Key Loop Characteristics  
| Loop Type | Use Case | Risk |  
|-----------|----------|------|  
| `for` | Known iterations, sequence processing | Off-by-one errors |  
| `while` | Unknown iterations, condition-based | Infinite loops |  


### Homework: Data Analyzer  
*Create `data_processor.py` that:*  

1. **Process a dataset**  
   ```python
   data = [12, 45, 'N/A', 32, 89, 'missing', 55, 0, 31, 'N/A']
   ```

2. **Implement logic**  
   - Convert valid numbers to Fahrenheit: `F = C * 9/5 + 32`  
   - Skip non-numeric values with `continue`  
   - Stop processing if value is 0 (use `break`)  
   - Track processed count with `enumerate`  

3. **Generate report**  
   ```
   Processing 10 records...
   1: 12°C → 53.6°F
   2: 45°C → 113.0°F
   Skipping non-numeric: N/A
   4: 32°C → 89.6°F
   5: 89°C → 192.2°F
   Skipping non-numeric: missing
   7: 55°C → 131.0°F
   Stopped at 0 value
   Processed 8/10 records
   Valid conversions: 6
   ```

*Requirements:*  
- Use both `for` and `while` loops  
- Implement `break`, `continue`, and `enumerate`  
- Handle type errors gracefully  
- Format temperatures to 1 decimal place


## Functions in Python  
*Functions encapsulate reusable code blocks that perform specific tasks. They promote modularity, reduce redundancy, and enhance code maintainability by centralizing logic. Functions follow the DRY principle: Don't Repeat Yourself.*



#### **1. Function Definition & Execution**  
*Define functions with `def` and execute them using parentheses `()`. Functions without explicit `return` statements yield `None`.*  

```python
# Basic function definition
def greet():
    print("Hello, function!")

# Function execution
greet()  # Output: Hello, function!

# Function object reference (without execution)
print(greet)  # Output: <function greet at 0x...>
```



#### **2. Parameters & Arguments**  
*Parameters receive data; arguments supply data. Required arguments must precede default-valued parameters.*  

```python
def personalized_greet(greeting, name="User"):
    return f"{greeting}, {name}!"

print(personalized_greet("Hi"))          # Hi, User!
print(personalized_greet("Hello", "Aya")) # Hello, Aya!
```



#### **3. Return Values**  
*Functions process inputs and return results using `return`. Return values can be directly used or assigned.*  

```python
def celsius_to_fahrenheit(c):
    return c * 9/5 + 32

temp_f = celsius_to_fahrenheit(25)
print(f"25°C = {temp_f}°F")  # 25°C = 77.0°F
```



#### **4. Advanced Argument Handling**  
*`*args` collects positional arguments into a tuple; `**kwargs` collects keyword arguments into a dictionary.*  

```python
def student_info(*courses, **details):
    print(f"Courses: {courses}")
    print(f"Details: {details}")

student_info("Math", "Art", name="Lina", age=21)
# Output: 
# Courses: ('Math', 'Art')
# Details: {'name': 'Lina', 'age': 21}
```



#### **5. Argument Unpacking**  
*Unpack sequences/dictionaries into function arguments using `*` and `**`.*  

```python
courses = ["Physics", "CS"]
info = {"name": "Omar", "id": "S12345"}

student_info(*courses, **info)
# Output:
# Courses: ('Physics', 'CS')
# Details: {'name': 'Omar', 'id': 'S12345'}
```



#### **6. Documentation Strings (Docstrings)**  
*Docstrings describe function purpose and usage, accessible via `help()` or `.__doc__`.*  

```python
def is_leap(year):
    """
    Determines if a year is a leap year.
    
    Args:
        year (int): Year to check
        
    Returns:
        bool: True if leap year, False otherwise
    """
    return year % 4 == 0 and (year % 100 != 0 or year % 400 == 0)

print(help(is_leap))  # Displays docstring
```



#### **7. Practical Example: Date Validation**  
*Combining functions for complex logic. Note: `month_days[0]` is unused (January = index 1).*  

```python
month_days = [0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]

def days_in_month(year, month):
    """Returns days in month considering leap years"""
    if not 1 <= month <= 12:
        return "Invalid month"
        
    if month == 2 and is_leap(year):
        return 29
        
    return month_days[month]

print(days_in_month(2023, 2))  # 28 (non-leap)
print(days_in_month(2024, 2))  # 29 (leap)
```



### Function Features  
1. **Modularity**: Isolate logic into reusable units  
2. **Parameterization**: Accept inputs via parameters  
3. **Return Values**: Output processed results  
4. **Scope**: Variables inside functions are local  
5. **Documentation**: Docstrings provide usage guidance  



### Homework: Scientific Calculator  
*Create `calculator.py` implementing:*

1. **Core Functions**  
   ```python
   def quadratic(a, b, c):
       # Returns roots of ax² + bx + c = 0
       pass
   
   def bmi(weight, height):
       # Calculates BMI: weight(kg) / height(m)²
       pass
   
   def investment(principal, rate, years):
       # Calculates compound interest: P(1 + r)^t
       pass
   ```

2. **Requirements**  
   - Each function must have descriptive docstrings  
   - Handle edge cases (division by zero, invalid inputs)  
   - Use default arguments where appropriate  
   - Implement *args/**kwargs in at least one function  

3. **Test Cases**  
   ```python
   print(quadratic(1, -3, 2))    # Roots of x²-3x+2 → (1.0, 2.0)
   print(bmi(70, 1.75))           # ≈22.86
   print(investment(1000, 0.05, 10))  # ≈1628.89
   ```

4. **Advanced Feature**  
   Create `calculate()` function that:
   - Accepts operation name and parameters  
   - Uses function dictionary mapping:  
     ```python
     operations = {
         'quadratic': quadratic,
         'bmi': bmi,
         'investment': investment
     }
     ```

