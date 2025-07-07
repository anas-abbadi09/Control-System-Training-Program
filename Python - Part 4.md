##  Working with Dates and Times in Python  
*The datetime module provides comprehensive tools for handling dates, times, and timezones. Understanding naive vs aware datetime objects and timedeltas is crucial for accurate temporal operations in applications.*



#### **1. Naive vs Aware Datetimes**  
*Naive objects lack timezone context, while aware objects include timezone information for precise time calculations.*  

```python
import datetime
import pytz

# Naive datetime (no timezone)
naive_dt = datetime.datetime(2023, 7, 26, 12, 30)
print(naive_dt.tzinfo)  # None

# Aware datetime (UTC timezone)
aware_dt = datetime.datetime.now(pytz.UTC)
print(aware_dt.tzinfo)  # UTC
```


#### **2. Working with Dates (date class)**  
*Handles calendar dates (year, month, day) without time information.*  

```python
# Creating dates
d = datetime.date(2023, 7, 24)  # No leading zeros
print(d)  # 2023-07-24

# Current date
today = datetime.date.today()
print(f"Year: {today.year}, Month: {today.month}, Day: {today.day}")

# Weekday calculations
print(today.weekday())     # Monday=0, Sunday=6
print(today.isoweekday())  # Monday=1, Sunday=7
```



#### **3. Working with Times (time class)**  
*Stores time components (hour, minute, second, microsecond) independently.*  

```python
t = datetime.time(12, 30, 45, 100000)
print(f"{t.hour}:{t.minute}")  # 12:30
```



#### **4. Combined Datetimes (datetime class)**  
*Represents full date + time objects for comprehensive time operations.*  

```python
dt = datetime.datetime(2023, 7, 26, 12, 30, 45)
print(dt.date())  # Get date component
print(dt.time())  # Get time component

# Current datetime methods
print(datetime.datetime.now())   # Local naive
print(datetime.datetime.utcnow()) # UTC naive
```



#### **5. Timedeltas: Time Arithmetic**  
*Represents time differences and enables date calculations.*  

```python
# Creating durations
week = datetime.timedelta(days=7)
hour = datetime.timedelta(hours=12)

# Date arithmetic
next_week = datetime.date.today() + week
last_week = datetime.date.today() - week
future_time = dt + hour  # Adds 12 hours

# Difference between dates
bday = datetime.date(2023, 9, 24)
days_until = (bday - today).days
```



#### **6. Timezone Handling (pytz)**  
*Manages timezone conversions and daylight saving time.*  

```python
# UTC aware datetime
utc_dt = datetime.datetime.now(pytz.UTC)

# Timezone conversion
ny_tz = pytz.timezone('America/New_York')
ny_time = utc_dt.astimezone(ny_tz)

# Localizing naive datetimes
local_dt = ny_tz.localize(datetime.datetime(2023, 7, 26, 12, 30))
```



#### **7. Formatting & Parsing**  
*Converts between datetime objects and strings.*  

```python
# Datetime → String
formatted = dt.strftime("%B %d, %Y at %I:%M %p")  # July 26, 2023 at 12:30 PM

# String → Datetime
parsed = datetime.datetime.strptime("July 26, 2023", "%B %d, %Y")
```



### 💎 Key Concepts Summary  
| Feature          | Naive | Aware | Timedelta |
|------------------|-------|-------|-----------|
| Timezone Support | ❌    | ✅    | N/A       |
| Daylight Savings | ❌    | ✅    | N/A       |
| Date Arithmetic  | ✅    | ✅    | ✅        |
| UTC Conversion   | ❌    | ✅    | ✅        |



### Homework: Global Event Scheduler  
*Implement a program that:*  

1. **Creates timezone-aware events**  
   ```python
   webinar_utc = datetime.datetime(2023, 8, 15, 14, 0, tzinfo=pytz.UTC)
   conf_ny = pytz.timezone('America/New_York').localize(
       datetime.datetime(2023, 9, 20, 9, 0)
   )
   ```

2. **Performs time operations**  
   - Calculate webinar duration (2.5 hours) using `timedelta`  
   - Convert webinar time to Tokyo timezone  
   - Determine days until NY conference  

3. **Formats and compares times**  
   - Display all events in ISO format  
   - Check if webinar occurs before conference  
   - Format NY conference as "September 20, 2023 | 09:00 AM EDT"  

4. **Output schedule report**  
   ```markdown
   Global Event Schedule:
   
   Webinar (Tokyo): 
   2023-08-15 23:00:00+09:00
   
   NY Conference: 
   September 20, 2023 | 09:00 AM EDT
   
   Time until NY Conference: 45 days
   Webinar before conference: True
   ```

*Requirements:*  
- Use both naive and aware datetimes  
- Perform 3+ timedelta operations  
- Implement timezone conversions  
- Use strftime() formatting  
- Include comparison operations  



## Working with CSV Files in Python  
*The csv module provides robust tools for handling comma-separated value files. Understanding reading/writing modes, dialect customization, and efficient large-file processing is essential for data workflows.*



#### **1. Reading CSV Files**  
*Use `csv.reader` to parse CSV data into iterable rows. Context managers ensure proper file handling.*  

```python
import csv

# Basic CSV reading
with open('data.csv', 'r') as csv_file:
    csv_reader = csv.reader(csv_file)
    
    # Skip header row (optional)
    next(csv_reader)  
    
    for row in csv_reader:
        print(row[0], row[2])  # Access columns by index
```



#### **2. Writing CSV Files**  
*`csv.writer` creates new CSV files. Use 'w' mode to overwrite or 'a' to append.*  

```python
# Writing to a new CSV
headers = ['Name', 'Email', 'Phone']
data = [
    ['Alice', 'alice@example.com', '555-1234'],
    ['Bob', 'bob@domain.com', '555-5678']
]

with open('contacts.csv', 'w', newline='') as new_file:
    csv_writer = csv.writer(new_file)
    csv_writer.writerow(headers)  # Write header
    csv_writer.writerows(data)    # Write multiple rows
```



#### **3. Custom Dialects & Delimiters**  
*Handle non-standard formats using dialect parameters.*  

```python
# Pipe-delimited file with custom quoting
csv.register_dialect('pipes', delimiter='|', quoting=csv.QUOTE_MINIMAL)

with open('data.psv', 'r') as psv_file:
    reader = csv.reader(psv_file, dialect='pipes')
    for row in reader:
        print(row)
```



#### **4. Dictionary-Based Access**  
*`DictReader` and `DictWriter` enable column access via headers.*  

```python
# Reading with DictReader
with open('employees.csv', 'r') as emp_file:
    dict_reader = csv.DictReader(emp_file)
    for record in dict_reader:
        print(f"{record['first_name']} {record['last_name']}")

# Writing with DictWriter
with open('updated.csv', 'w', newline='') as out_file:
    fieldnames = ['ID', 'Department', 'Salary']
    dict_writer = csv.DictWriter(out_file, fieldnames=fieldnames)
    
    dict_writer.writeheader()
    dict_writer.writerow({'ID': '101', 'Department': 'Engineering', 'Salary': '85000'})
```



#### **5. Handling Large Files**  
*Process massive CSV files efficiently with chunked reading.*  

```python
CHUNK_SIZE = 10000  # Process 10k rows per batch

def process_large_csv(input_path):
    with open(input_path, 'r') as massive_file:
        reader = csv.reader(massive_file)
        header = next(reader)  # Save header
        
        chunk = []
        for i, row in enumerate(reader):
            chunk.append(row)
            if (i + 1) % CHUNK_SIZE == 0:
                process_chunk(chunk)  # Custom processing function
                chunk = []
        
        # Process remaining rows
        if chunk:  
            process_chunk(chunk)
```



### 💎 Key CSV Features Summary  
| Feature             | Reader Method      | Writer Method      |
|---------------------|--------------------|--------------------|
| Row-by-row access   | `csv.reader()`     | `csv.writer()`     |
| Dictionary access   | `csv.DictReader()` | `csv.DictWriter()` |
| Custom delimiters   | `delimiter='\t'`   | `delimiter=';'`    |
| Quote handling      | `quoting=` parameter | `quotechar=` parameter |



### Homework: Employee Database Manager  
*Implement a program that:*  

1. **Processes employee data**  
   - Input CSV: `employees.csv`  
     ```
     id,first_name,last_name,department,salary
     101,Alice,Johnson,Engineering,85000
     102,Bob,Smith,Marketing,72000
     ```
   - Output CSV: `updated_employees.csv`  

2. **Performs operations**  
   - Give 10% raise to Engineering department  
   - Add new employee: `103, Carol, Davis, Sales, 68000`  
   - Calculate average salary by department  

3. **Output formatted report**  
   ```markdown
   Department Report:
   - Engineering: $93,500 avg (2 employees)
   - Marketing: $72,000 avg (1 employee)
   - Sales: $68,000 avg (1 employee)
   
   Updated file saved: updated_employees.csv
   ```

*Requirements:*  
- Use `DictReader` for input processing  
- Use `DictWriter` for output generation  
- Implement chunked reading (simulate with small chunks)  
- Format currency as `$92,500`  
- Handle missing columns gracefully  

```python
# Sample starter code
import csv

def update_salaries(row):
    if row['department'] == 'Engineering':
        row['salary'] = str(int(float(row['salary']) * 1.1)
    return row
```
