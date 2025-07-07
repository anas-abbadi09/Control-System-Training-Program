## **Why Python?**

From time to time, new programming languages appear. You might wonder: *Should I switch from Python?* The answer is often no. Here’s why **Python is a great first language**:

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


## **Installing Python on Rocky Linux 9.6**

#### Step 1: Check Python Installation
Verify Python is installed and check your version:
```bash
python --version
```
- You should see output like: `Python 3.9.21`
- If you get `command not found`, proceed to Step 2

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
   print("\nHomework complete!")
   ```

4. **Run Script**  
   Execute with:
   ```bash
   python rocky_test.py
   ```
   → Take screenshot showing:
   - Your Python version
   - Success message



## Code Editors & IDEs  

1. **Terminal Editors** (Fast & Lightweight)  
   - `nano`: Simple text editor  
   - `vim`/`neovim`: Powerful keyboard-driven editor 

2. **VS Code** (Recommended)  
   Free, feature-rich, with excellent Python support


3. **PyCharm**
   Dedicated Python IDE with advanced debugging  


4. **Sublime Text** (Lightweight)  
   Fast, customizable editor with Python plugins  


##  String Manipulation 
 
*Strings are immutable sequences of Unicode characters, serving as fundamental building blocks for text processing in Python. In this section, we'll explore their properties and manipulation techniques through practical applications. Remember: every string operation creates a new object rather than modifying the original.*


###  1. String Declaration Techniques 
* Python provides flexible declaration options to handle different textual scenarios. The choice between quotation styles impacts how we manage special characters and multi-line content.*  

```python
# Single quotes for simple text
message = 'Hello World'

# Double quotes when text contains apostrophes
title = "Python's String Handling"

# Triple quotes for multi-line blocks
documentation = """Strings are ordered sequences 
of Unicode characters. They support
indexing, slicing, and rich methods."""
```



###  2. Accessing String Components  
* As sequences, strings support positional access via zero-based indexing. Slicing allows substring extraction using [start:stop:step] notation, while negative indices enable reverse traversal.*  

```python
language = "Python"

# Indexing
first_char = language[0]    # 'P' 
third_char = language[2]    # 't'
last_char = language[-1]    # 'n'

# Slicing [start:stop:step]
first_three = language[0:3]  # 'Pyt' 
even_indices = language[::2] # 'Pto'
reverse = language[::-1]     # 'nohtyP'
```



###  3. Core String Methods  
* String objects provide numerous methods for transformation and analysis. These non-destructive operations always return new strings, preserving the original data.*  

```python
# Case conversion
print("Data Science".lower())      # 'data science'
print("important".upper())         # 'IMPORTANT'

# Search and analysis
print("Mississippi".count("s"))    # 4
print("Python".find("th"))         # 2 (index position)

# Content validation
print("PY101".isupper())           # True
print("2024".isdigit())            # True
```



###  4. String Transformation Techniques  
* Real-world text processing requires restructuring and cleaning capabilities. These methods are essential for data sanitization, format conversion, and content normalization.*  

```python
# Content replacement
code = "print('Hello C++')"
updated_code = code.replace("C++", "Python")

# Whitespace management
user_input = "  data@university.edu  "
clean_email = user_input.strip()  # 'data@university.edu'

# Structural changes
csv_data = "name,id,grade"
fields = csv_data.split(",")                # ['name', 'id', 'grade']
pipe_separated = "|".join(fields)           # 'name|id|grade'
```



###  5. Modern String Formatting  
* Formatting creates dynamic templates by inserting values into placeholders. While concatenation works for simple cases, f-strings provide superior readability and functionality for complex interpolations.*  

```python
student = "Maria"
grade = 92.5

# Concatenation (simple but limited)
print("Student: " + student + ", Grade: " + str(grade))

# .format() method
print("{0}'s score: {1:.1f}%".format(student, grade))

# F-strings (Python 3.6+ - recommended)
print(f"{student.upper()}: {grade} → { 'Pass' if grade >= 70 else 'Fail' }")
# Output: MARIA: 92.5 → Pass
```



###  6. Practical Application: Academic Credential Formatter  
* Let's combine our techniques to solve a common academic need: standardizing researcher credentials. This demonstrates real-world string processing combining multiple operations.*  

```python
# Input: "Dr. Emily Zhang | Computer Science | MIT"
raw_input = input("Enter researcher credentials: ").strip()

# Transformation pipeline
name = raw_input.split("|")[0].replace("Dr.", "").strip().title()
degree = raw_input.split("|")[1].strip().upper()
institution = raw_input.split("|")[2].strip()

# Format using f-string
formatted = f"{name} ({degree}), {institution}"

print(f"Standardized: {formatted}")
# Input "dr. emily zhang | phd | mit" → "Emily Zhang (PHD), MIT"
```



###  7. Exploring String Documentation  
* Python's built-in introspection tools enable autonomous learning. Use dir() for method discovery and help() for detailed documentation—essential skills for professional development.*  

```python
sample_text = "Hello"

# List all available methods
print(dir(sample_text))     

# Full class documentation
print(help(str))            

# Specific method details
print(help(str.upper))      
```


### Homework: Research Paper Formatter  
* Apply ALL string techniques from this section to create `paper_formatter.py` that:*

1. Takes raw research paper data input in this format:  
   `"TITLE|AUTHOR LIST|ABSTRACT|KEYWORDS"`  
   Example:  
   `"Machine Learning Approaches|Chen, L.; Wong, S.|This study explores...|AI,neural networks,classification"`

2. Performs these transformations:  
   a. Convert title to Title Case  
   b. Extract first author's surname and initials (Chen, L.)  
   c. Split keywords into list, capitalize each, and join with semicolons  
   d. Format abstract to 200 characters with ellipsis (...) if longer  
   e. Generate Harvard-style citation:  
      `"[Surname], [Initial]. ([Year]). [Title]. Journal."` (Use 2025 as year)

3. Output structured format using f-string:  
   ```
   Citation: Chen, L. (2024). Machine Learning Approaches.
   Abstract: This study explores... [200 char limit]
   Keywords: Ai; Neural Networks; Classification
   ```

4. Validate using these metrics:  
   - Title length 10-120 characters  
   - At least 2 keywords  
   - Author format matches "Surname, I." pattern  

*Implementation Requirements:*  
- Use minimum 5 different string methods
- Implement slicing/indexing for author processing
- Use f-string for final output formatting 


## Working with Numbers in Python  
*Numeric data forms the foundation of computational logic. In this section, we'll explore Python's numeric types and operations, which enable everything from basic calculations to complex scientific computing. Understanding these concepts is essential for data analysis, algorithm development, and quantitative problem-solving.*



#### **1. Basic Number Types**  
*Python distinguishes between integers (whole numbers) and floats (decimal numbers), each with distinct properties and behaviors. This distinction affects precision, memory usage, and mathematical operations.*  

```python
# Integers (whole numbers)
age = 25
items = 3

# Floats (decimal numbers)
price = 9.99
temperature = 36.6
```



#### **2. Arithmetic Operations**  
*Python provides a comprehensive set of arithmetic operators that follow standard mathematical precedence rules. Understanding these operators and their behaviors with different numeric types is crucial for accurate calculations.*  

```python
# Basic math
print(10 + 3)   # Addition → 13
print(10 - 3)   # Subtraction → 7
print(10 * 3)   # Multiplication → 30
print(10 / 3)   # True division → 3.333... (always returns float)
print(10 // 3)  # Floor division → 3 (integer division)
print(10 % 3)   # Modulus → 1 (remainder after division)
print(10 ** 3)  # Exponentiation → 1000
```



#### **3. Type Conversion**  
*Converting between numeric types is common in Python programming. Explicit type conversions ensure proper handling of values during operations, especially when mixing integers and floats.*  

```python
# Convert between types
num_str = "15"
print(int(num_str) + 5)  # → 20 (string to integer)

# Float to integer (truncates decimals)
print(int(9.99))  # → 9 (loses decimal precision)

# Integer to float
print(float(7))   # → 7.0 (adds decimal component)
```



#### **4. Common Number Methods**  
*Python's built-in numeric methods provide essential mathematical functionality. These methods offer precise control over rounding, absolute values, and numerical properties.*  

```python
# Absolute value (distance from zero)
print(abs(-5))        # → 5

# Rounding (controls decimal precision)
print(round(3.14159))     # → 3 (default: 0 decimals)
print(round(3.14159, 2))  # → 3.14 (specified decimal places)

# Check if float represents whole number
print((1.0).is_integer())   # → True
print((1.5).is_integer())   # → False
```



#### **5. Practical Example: Financial Calculator**  
*Combining numeric operations creates powerful real-world applications. This financial calculator demonstrates how to model compound interest, a fundamental concept in finance and economics.*  

```python
# Compound interest calculator
principal = 1000  # Initial investment
rate = 0.05       # Annual interest rate
years = 10        # Investment period

# Calculate final amount: A = P(1 + r)^t
final_amount = principal * (1 + rate) ** years

# Monthly payment calculation
monthly_payment = final_amount / (years * 12)

# Format currency output
print(f"Initial investment: ${principal}")
print(f"Value after {years} years: ${round(final_amount, 2)}")
print(f"Equivalent monthly value: ${round(monthly_payment, 2)}")
```



#### **6. Exploring Numeric Methods**  
*Python's introspection tools allow deep exploration of numeric capabilities. These techniques help discover available operations and understand their functionality.*  

```python
num = 7.5

# List all available methods
print(dir(num))  # Shows numeric methods

# Detailed documentation
print(help(float))  # Full float class documentation
print(help(int))    # Full integer class documentation
```



### Homework: Scientific Calculator  
*Implement a scientific calculator that performs these operations:*

1. **Temperature Conversion**  
   Convert 212°F to Celsius using: `(F - 32) * 5/9`  
   Convert 37°C to Fahrenheit using: `(C * 9/5) + 32`

2. **Geometric Calculations**  
   Calculate hypotenuse of a triangle with sides 9 and 12  
   Compute volume of a sphere with radius 5: `(4/3) * π * r³`

3. **Financial Projection**  
   Calculate compound interest:  
   - Principal: $5000  
   - Annual rate: 4.5%  
   - Time: 15 years  
   Formula: `A = P(1 + r)^t`

4. **Statistical Operations**  
   Calculate mean of: 88, 92, 79, 93, 85  
   Determine standard deviation using:  
   `σ = √[Σ(xᵢ - μ)² / N]`

5. **Output Formatting**  
   Display results with proper units and precision:  
   ```markdown
   Temperature Conversion:
   212°F = 100.0°C
   37°C = 98.6°F
   
   Geometry:
   Hypotenuse: 15.0
   Sphere Volume: 523.60 cubic units
   
   Finance:
   $5000 @ 4.5% for 15 years → $9823.15
   
   Statistics:
   Mean: 87.4
   Standard Deviation: 5.38
   ```

*Implementation Requirements:*  
- Use minimum 5 different arithmetic operators  
- Implement rounding for decimal results  
- Use type conversions where necessary  
- Include comments explaining each calculation  
- Format output professionally using f-strings

