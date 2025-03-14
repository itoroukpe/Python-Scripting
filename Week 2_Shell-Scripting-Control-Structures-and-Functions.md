### **Week 2: Shell Scripting - Control Structures and Functions**

#### **Session 3: Conditional Statements and Loops**

---

#### **Topics Covered**

1. **if, else, elif Statements**
   - **Syntax**:
     ```bash
     if [ condition ]; then
         # commands
     elif [ condition ]; then
         # commands
     else
         # commands
     fi
     ```
   - **Example**: Check if a number is positive, negative, or zero
     ```bash
     read -p "Enter a number: " num
     if [ $num -gt 0 ]; then
         echo "The number is positive."
     elif [ $num -lt 0 ]; then
         echo "The number is negative."
     else
         echo "The number is zero."
     fi
     ```

2. **for Loops**
   - **Syntax**:
     ```bash
     for variable in list; do
         # commands
     done
     ```
   - **Example**: Print all files in the current directory
     ```bash
     for file in *; do
         echo "File: $file"
     done
     ```

3. **while Loops**
   - **Syntax**:
     ```bash
     while [ condition ]; do
         # commands
     done
     ```
   - **Example**: Countdown from 10 to 1
     ```bash
     counter=10
     while [ $counter -gt 0 ]; do
         echo $counter
         counter=$((counter - 1))
     done
     ```

4. **case Statements**
   - **Syntax**:
     ```bash
     case $variable in
         pattern1)
             # commands
             ;;
         pattern2)
             # commands
             ;;
         *)
             # default commands
             ;;
     esac
     ```
   - **Example**: Menu-driven script
     ```bash
     echo "Choose an option:"
     echo "1. Display date"
     echo "2. List files"
     echo "3. Exit"
     read -p "Enter your choice: " choice
     case $choice in
         1) date ;;
         2) ls ;;
         3) exit ;;
         *) echo "Invalid option" ;;
     esac
     ```

---

#### **Hands-On Exercise**

**Task**: Write a script that uses conditionals and loops to check for available system updates.

**Solution**:
```bash
#!/bin/bash
updates=$(sudo apt update 2>/dev/null | grep "packages can be upgraded" | awk '{print $1}')

if [ -z "$updates" ]; then
    echo "No updates available."
else
    echo "$updates packages can be upgraded."
    while true; do
        read -p "Do you want to upgrade now? (y/n): " answer
        case $answer in
            y|Y)
                sudo apt upgrade -y
                echo "System upgraded successfully."
                break
                ;;
            n|N)
                echo "Exiting without upgrading."
                break
                ;;
            *)
                echo "Invalid input. Please enter y or n."
                ;;
        esac
    done
fi
```
---
This **Bash script** checks for available **package updates** on a system using **APT (Advanced Package Tool)**, prompts the user to upgrade, and proceeds based on user input.

---

### **Code Breakdown**
```bash
#!/bin/bash
```
- The **shebang (`#!`)** specifies that the script should be executed using the **Bash shell**.

---

#### **Step 1: Check for Available Updates**
```bash
updates=$(sudo apt update 2>/dev/null | grep "packages can be upgraded" | awk '{print $1}')
```
- Runs `sudo apt update` to refresh the package list.
- Redirects **error messages** (`stderr`) to `/dev/null` to suppress any warnings.
- **Filters** the output using `grep "packages can be upgraded"` to find the line that indicates available updates.
- Uses **`awk '{print $1}'`** to extract the number of packages that can be upgraded and assigns it to the variable `$updates`.

---

#### **Step 2: Conditional Check for Updates**
```bash
if [ -z "$updates" ]; then
    echo "No updates available."
```
- If `$updates` is **empty**, prints `"No updates available."`
- The condition `[ -z "$updates" ]` checks whether `$updates` is an empty string (`-z` means "is empty").

---

#### **Step 3: Prompt User for Upgrade**
```bash
else
    echo "$updates packages can be upgraded."
```
- If updates are available, prints how many packages can be upgraded.

```bash
    while true; do
        read -p "Do you want to upgrade now? (y/n): " answer
```
- Starts a **loop** to repeatedly ask the user whether they want to upgrade (`y/n`).
- Uses `read -p` to prompt for input and store it in the variable `$answer`.

---

#### **Step 4: Handle User Input**
```bash
        case $answer in
            y|Y)
                sudo apt upgrade -y
                echo "System upgraded successfully."
                break
                ;;
```
- If the user enters **`y` or `Y`**, runs `sudo apt upgrade -y` to upgrade all packages **without confirmation**.
- Prints `"System upgraded successfully."`
- `break` **exits the loop**.

```bash
            n|N)
                echo "Exiting without upgrading."
                break
                ;;
```
- If the user enters **`n` or `N`**, prints `"Exiting without upgrading."` and exits the loop.

```bash
            *)
                echo "Invalid input. Please enter y or n."
                ;;
```
- If the user enters **anything else**, prints `"Invalid input. Please enter y or n."` and re-prompts.

---


---

#### **Session 4: Functions and Error Handling**

---

#### **Topics Covered**

1. **Defining and Calling Functions**
   - **Syntax**:
     ```bash
     function_name() {
         # commands
     }
     function_name  # Call the function
     ```
   - **Example**:
     ```bash
     greet() {
         echo "Hello, $1!"
     }
     greet "John"
     ```

2. **Scope of Variables in Functions**
   - **Global Variables**: Accessible everywhere in the script.
   - **Local Variables**: Defined using `local` keyword inside functions.
     ```bash
     demo_function() {
         local local_var="I am local"
         echo $local_var
     }
     demo_function
     echo $local_var  # This will not work
     ```

3. **Basic Error Handling**
   - Use `set -e` to stop the script on the first error.
   - Capture exit codes with `$?`.
     ```bash
     mkdir /restricted 2>/dev/null
     if [ $? -ne 0 ]; then
         echo "Error: Unable to create directory."
     fi
     ```

4. **Debugging Techniques**
   - Enable debugging with `set -x`.
   - Disable debugging with `set +x`.
   - Example:
     ```bash
     set -x
     echo "Debugging this script"
     set +x
     ```

---

#### **Hands-On Exercise**

**Task**: Develop a reusable function to check if a given directory or file exists, with error messages for invalid inputs.

**Solution**:
```bash
#!/bin/bash

check_file_or_dir() {
    if [ -e "$1" ]; then
        if [ -d "$1" ]; then
            echo "$1 is a directory."
        elif [ -f "$1" ]; then
            echo "$1 is a file."
        else
            echo "$1 exists but is neither a file nor a directory."
        fi
    else
        echo "Error: $1 does not exist."
    fi
}

# Test the function
read -p "Enter the file or directory path to check: " path
check_file_or_dir "$path"
```

---

### **Learning Outcomes**

By the end of Week 2, participants will:
1. Understand and implement conditional statements and loops in Shell scripting.
2. Write robust scripts using `if`, `for`, `while`, and `case` statements.
3. Create and use reusable functions for modularity and efficiency.
4. Handle errors gracefully and debug scripts effectively. 

This week’s lessons will equip participants with the foundational skills to write versatile, reliable, and maintainable Shell scripts.
