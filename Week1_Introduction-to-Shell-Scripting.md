# **Training Plan: Week 1 - Introduction to Shell Scripting**  
## **Session 1: Introduction to Shell Scripting**  

### **Objective**
By the end of this session, participants will understand the fundamentals of Shell scripting, navigate Linux/UNIX systems, and create and run a simple script.

---

### **Session Structure**
- **Duration**: 2 hours  
- **Format**: Lecture (1 hour) + Hands-On Practice (1 hour)  

---

### **Training Agenda**

#### **1. Overview of Shell Scripting (15 minutes)**  
**Topics to Cover**:  
- **What is Shell Scripting?**
  - A Shell script is a text file containing a series of commands that the Shell can execute sequentially.  
  - It helps automate repetitive tasks, configure systems, and manage files.

- **Common Shell Types**:
  - **Bash** (Bourne Again Shell): Default on most Linux systems.
  - **Zsh**: Advanced scripting features, enhanced interactivity.
  - **Ksh** (Korn Shell): Known for scripting compatibility.
  - **Tcsh**: C-style syntax.

- **Why Use Shell Scripting?**
  - Automate repetitive tasks.
  - Save time and reduce errors.
  - Increase productivity in system administration.

---

#### **2. Basic Linux/UNIX Commands and Navigation (20 minutes)**  
**Topics to Cover**:  
- **Filesystem Basics**:
  - Home directory: `~`
  - Root directory: `/`

- **Navigating Directories**:
  - `pwd`: Print current directory.  
  - `ls`: List files and directories.  
  - `cd [directory]`: Change directory.  
  - `mkdir [directory_name]`: Create a new directory.  
  - `rmdir [directory_name]`: Remove an empty directory.

- **File Operations**:
  - `touch [file_name]`: Create an empty file.  
  - `cp [source] [destination]`: Copy files.  
  - `mv [source] [destination]`: Move/rename files.  
  - `rm [file_name]`: Remove files.

- **Viewing File Contents**:
  - `cat`: View file content.  
  - `head`: Display the first few lines.  
  - `tail`: Display the last few lines.  

---

#### **3. Script Structure and Syntax (15 minutes)**  
**Topics to Cover**:  
- **Structure of a Shell Script**:
  - Start with a Shebang: `#!/bin/bash`
    - Specifies the interpreter to use.
  - Write commands line by line.
  - Add comments for readability using `#`.

- **Basic Syntax**:
  - Variables: Assign values using `=` (no spaces around `=`).
    ```bash
    greeting="Hello, World!"
    echo $greeting
    ```
  - Input and Output:
    - `echo`: Print output to the terminal.
    - `read`: Accept user input.
      ```bash
      read -p "Enter your name: " name
      echo "Hello, $name!"
      ```

---

#### **4. Creating and Running a Simple Script (10 minutes)**  
**Steps to Create and Run a Script**:  
1. Open a text editor (e.g., `nano`, `vi`, `vim`) and write the script:
   ```bash
   #!/bin/bash
   echo "System Information"
   echo "Hostname: $(hostname)"
   echo "Date: $(date)"
   echo "Uptime: $(uptime -p)"
   echo "Logged-in Users: $(who)"
   ```
2. Save the script with a `.sh` extension (e.g., `system_info.sh`).  
3. Make the script executable:
   ```bash
   chmod +x system_info.sh
   ```
4. Run the script:
   ```bash
   ./system_info.sh
   ```

---

### **Hands-On Practice (60 minutes)**  

#### **Activity 1: Writing a Simple Script**
1. Create a script named `my_first_script.sh` that:
   - Greets the user.
   - Displays the current date and time.
   - Prints the system's uptime.

**Solution**:
```bash
#!/bin/bash
echo "Welcome to Shell Scripting!"
echo "Current Date and Time: $(date)"
echo "System Uptime: $(uptime -p)"
```

#### **Activity 2: Running Your Script**
1. Save the script in the home directory.  
2. Make it executable with `chmod +x my_first_script.sh`.  
3. Run it using `./my_first_script.sh`.  

#### **Activity 3: Experiment with Variables**
1. Modify your script to:
   - Accept the user’s name as input.
   - Display a personalized greeting.

**Solution**:
```bash
#!/bin/bash
read -p "Enter your name: " name
echo "Hello, $name! Welcome to Shell Scripting!"
echo "Today's date is $(date)."
echo "Your system has been running for $(uptime -p)."
```

---

### **Wrap-Up (5 minutes)**  
- Review key concepts:
  - Purpose of Shell scripting.
  - Basic Linux commands.
  - Writing and running a simple script.  

- Homework:
  - Create a script that:
    - Checks the available disk space using `df -h`.
    - Alerts the user if disk space usage exceeds 80%.  

- Next Session Preview:
  - **Variables and User Input in Shell Scripting**.

--- 

This training provides a strong foundation for Shell scripting and prepares participants for more advanced scripting concepts in subsequent sessions.
---


### **Week 1: Introduction to Shell Scripting**  
**Session 2: Working with Variables and User Input**

---

### **Session Objectives**:
By the end of this session, participants will:
1. Understand how to declare and use variables in shell scripting.
2. Learn how to read user input interactively.
3. Perform basic string manipulations.
4. Execute arithmetic operations within shell scripts.
5. Create a hands-on script that takes user input and performs a calculation.

---

### **Topics and Training Plan**

---

#### **1. Variables: Declaring and Using Variables**
**Explanation**: Variables store data that can be referenced and manipulated in your script. Shell variables do not require explicit data types.

**Examples**:  
```bash
# Declare a variable
name="John Doe"
age=25

# Use variables
echo "Name: $name"
echo "Age: $age"
```

**Key Notes**:
- Variables are case-sensitive.
- Use `$` to access the value of a variable.
- Avoid spaces between the variable name, `=` sign, and value.

---

#### **2. Reading User Input**
**Explanation**: You can prompt users to input data using the `read` command.

**Example**:  
```bash
echo "Enter your name:"
read user_name
echo "Hello, $user_name!"
```

**Key Notes**:
- `read` waits for user input and assigns it to the specified variable.
- You can prompt for multiple inputs:
  ```bash
  echo "Enter your first and last name:"
  read first_name last_name
  echo "Hello, $first_name $last_name!"
  ```

---

#### **3. Basic String Manipulation**
**Explanation**: Shell scripting allows basic string operations like concatenation and substring extraction.

**Examples**:
- **Concatenation**:
  ```bash
  first_name="John"
  last_name="Doe"
  full_name="$first_name $last_name"
  echo "Full Name: $full_name"
  ```

- **Substring Extraction**:
  ```bash
  string="HelloWorld"
  echo "Substring: ${string:0:5}"  # Output: Hello
  ```

---

#### **4. Arithmetic Operations**
**Explanation**: Arithmetic can be performed using `$(( ))` or the `expr` command.

**Examples**:
- **Using `$(( ))`**:
  ```bash
  num1=10
  num2=20
  sum=$((num1 + num2))
  echo "Sum: $sum"
  ```

- **Using `expr`**:
  ```bash
  num1=10
  num2=20
  sum=$(expr $num1 + $num2)
  echo "Sum: $sum"
  ```

**Key Notes**:
- Ensure variables contain only numeric values for arithmetic.
- Common operators: `+`, `-`, `*`, `/`, `%`.

---

### **Hands-On Activity**

**Goal**: Create a script that takes user input to perform a simple calculation and prints the result.

**Step-by-Step Instructions**:

1. Open a terminal and create a new script file:
   ```bash
   nano calculate.sh
   ```

2. Add the following script:
   ```bash
   #!/bin/bash

   # Prompt the user for two numbers
   echo "Enter the first number:"
   read num1

   echo "Enter the second number:"
   read num2

   # Perform calculations
   sum=$((num1 + num2))
   diff=$((num1 - num2))
   prod=$((num1 * num2))
   if [ "$num2" -ne 0 ]; then
       quot=$((num1 / num2))
       mod=$((num1 % num2))
   else
       quot="undefined (division by zero)"
       mod="undefined (division by zero)"
   fi

   # Display the results
   echo "Results:"
   echo "Sum: $sum"
   echo "Difference: $diff"
   echo "Product: $prod"
   echo "Quotient: $quot"
   echo "Modulo: $mod"
   ```

3. Save the file and make it executable:
   ```bash
   chmod +x calculate.sh
   ```

4. Run the script:
   ```bash
   ./calculate.sh
   ```

5. Test the script with various inputs to verify its functionality.

---

### **Key Takeaways**
- Variables in shell scripts store dynamic values for use within the script.
- User input is gathered interactively with the `read` command.
- String manipulations and arithmetic operations enhance the script’s flexibility.
- Hands-on practice solidifies the understanding of theoretical concepts.

---

### **Q&A and Troubleshooting**

- **Q: What if I forget to make the script executable?**
  - **A**: Run `chmod +x script_name.sh` to make the script executable.

- **Q: What happens if I divide by zero?**
  - **A**: The script checks for this condition and displays a message to avoid runtime errors.

- **Q: How can I debug errors in my script?**
  - **A**: Use `bash -x script_name.sh` to see step-by-step execution for debugging.

---

This training provides a foundational understanding of variables, user input, and operations, setting the stage for more advanced scripting topics in future sessions.
