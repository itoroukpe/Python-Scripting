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
