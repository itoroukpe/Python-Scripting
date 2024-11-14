### Week 3: Introduction to Python Scripting Training Plan

---

#### **Session 5: Python Fundamentals**
**Objective**: Introduce participants to Python, covering its basic syntax, data types, and the process of writing and running scripts.

---

**Topics Covered**:

1. **Overview of Python: Why Python for Scripting?**
   - Python’s simplicity, readability, and versatility.
   - Popularity in automation, data analysis, web development, and machine learning.
   - Key advantages: cross-platform support, vast libraries, and strong community.

2. **Basic Syntax, Data Types, and Operators**
   - **Syntax**:
     - Indentation instead of braces.
     - Importance of consistent whitespace.
   - **Data Types**:
     - Strings, Integers, Floats, Booleans.
     - Examples of declaring and printing these types.
   - **Operators**:
     - Arithmetic operators (`+`, `-`, `*`, `/`, `%`).
     - Comparison operators (`==`, `!=`, `>`, `<`).
     - Logical operators (`and`, `or`, `not`).

3. **Variables and User Input**
   - Declaring and assigning variables.
   - Getting input from users with the `input()` function.
   - Example:
     ```python
     name = input("Enter your name: ")
     age = input("Enter your age: ")
     print(f"Hello, {name}! You are {age} years old.")
     ```

4. **Writing and Running a Python Script**
   - Using an IDE or text editor (e.g., VS Code or PyCharm).
   - Saving the file with `.py` extension.
   - Running the script via terminal/command prompt:
     ```bash
     python script_name.py
     ```

**Hands-On Exercise**:
Write a Python script that takes user input and prints a customized greeting:
- Prompt the user for their name and favorite color.
- Output a message like: `"Hello, [name]! Your favorite color is [color]."`

Example Solution:
```python
name = input("What is your name? ")
color = input("What is your favorite color? ")
print(f"Hello, {name}! Your favorite color is {color}.")
```

---

#### **Session 6: Working with Data Structures**
**Objective**: Introduce Python's core data structures, teach basic operations, and demonstrate how to iterate over them.

---

**Topics Covered**:

1. **Lists, Tuples, Dictionaries, and Sets**
   - **Lists**:
     - Mutable, ordered collection.
     - Example: `fruits = ["apple", "banana", "cherry"]`
   - **Tuples**:
     - Immutable, ordered collection.
     - Example: `coordinates = (10, 20)`
   - **Dictionaries**:
     - Key-value pairs.
     - Example: `contacts = {"Alice": "123-456", "Bob": "987-654"}`
   - **Sets**:
     - Unordered, unique elements.
     - Example: `unique_numbers = {1, 2, 3}`

2. **Basic Operations on Data Structures**
   - Lists: Append, remove, sort.
     ```python
     fruits.append("orange")
     fruits.remove("banana")
     fruits.sort()
     ```
   - Tuples: Access elements by index.
     ```python
     print(coordinates[0])
     ```
   - Dictionaries: Add, update, delete keys.
     ```python
     contacts["Charlie"] = "555-123"
     del contacts["Alice"]
     ```
   - Sets: Add, remove elements, set operations.
     ```python
     unique_numbers.add(4)
     unique_numbers.discard(2)
     ```

3. **Using Loops to Iterate Over Data Structures**
   - **For Loops**:
     ```python
     for fruit in fruits:
         print(fruit)
     ```
   - **While Loops**:
     ```python
     i = 0
     while i < len(fruits):
         print(fruits[i])
         i += 1
     ```
   - Iterating over dictionaries:
     ```python
     for name, phone in contacts.items():
         print(f"{name}: {phone}")
     ```

**Hands-On Exercise**:
Write a script that stores and retrieves data in a dictionary, simulating a simple address book:
1. Allow the user to add a name and phone number.
2. Let the user retrieve a phone number by entering a name.
3. Print all entries in the address book.

Example Solution:
```python
address_book = {}

while True:
    print("\nAddress Book Menu:")
    print("1. Add Contact")
    print("2. Retrieve Contact")
    print("3. Display All Contacts")
    print("4. Exit")
    
    choice = input("Enter your choice: ")
    
    if choice == "1":
        name = input("Enter contact name: ")
        phone = input("Enter phone number: ")
        address_book[name] = phone
        print(f"Contact {name} added.")
    elif choice == "2":
        name = input("Enter the name to retrieve: ")
        if name in address_book:
            print(f"{name}'s phone number is {address_book[name]}")
        else:
            print(f"No contact found for {name}.")
    elif choice == "3":
        print("\nAll Contacts:")
        for name, phone in address_book.items():
            print(f"{name}: {phone}")
    elif choice == "4":
        print("Exiting Address Book. Goodbye!")
        break
    else:
        print("Invalid choice. Please try again.")
```

---

### **Learning Outcomes**

By the end of Week 3, participants will:
- Understand Python’s syntax and its advantages for scripting.
- Be able to write scripts that handle user input and perform basic operations.
- Use Python’s core data structures effectively.
- Develop small but meaningful projects like a customized greeting generator and an address book application.

---

This structured training plan ensures participants gain both theoretical knowledge and practical experience to build confidence in Python scripting.
