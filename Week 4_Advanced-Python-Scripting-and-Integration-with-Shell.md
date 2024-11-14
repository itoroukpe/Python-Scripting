### **Training Plan: Week 4 – Advanced Python Scripting and Integration with Shell**

#### **Session 7: File Handling and Libraries**

---

**Learning Objectives:**
1. Understand how to read from and write to files in Python.
2. Learn to utilize `os` and `sys` libraries for system-level operations.
3. Automate repetitive tasks using Python scripting.

---

**Topics Covered:**

1. **Reading from and Writing to Files**
   - **Reading files:**
     - Open files in different modes (`r`, `rb`, `r+`).
     - Read files line by line or as a whole.
   - **Writing files:**
     - Open files in write (`w`) or append (`a`) mode.
     - Write strings or structured data (e.g., JSON).
   - **Example Code:**
     ```python
     # Reading from a file
     with open('input.txt', 'r') as file:
         data = file.readlines()

     # Writing to a file
     with open('output.txt', 'w') as file:
         for line in data:
             file.write(line.upper())
     ```

2. **Working with the `os` and `sys` Libraries**
   - **`os` library:**
     - File and directory manipulation (e.g., create, delete, rename).
     - Fetching environment variables and working with paths.
   - **`sys` library:**
     - Accessing command-line arguments.
     - Exiting programs or modifying the Python path.
   - **Example Code:**
     ```python
     import os
     import sys

     # Create a directory
     os.mkdir('test_directory')

     # Fetch command-line arguments
     if len(sys.argv) > 1:
         print(f"First argument: {sys.argv[1]}")
     ```

3. **Automating Tasks with Python**
   - Example use cases:
     - Data preprocessing.
     - File organization and renaming.
     - Log file monitoring.
   - **Hands-On Exercise:**
     - Develop a script that:
       1. Reads data from `input.txt`.
       2. Processes the data (e.g., converts to uppercase).
       3. Writes the processed data to `output.txt`.

---

**Hands-On Task:**
1. **Objective**: Develop a script that reads a file, processes its contents, and writes the output to another file.
2. **Steps**:
   - Create an `input.txt` file with sample text.
   - Write a script that reads the file, converts the text to uppercase, and writes it to `output.txt`.
   - Add error handling for missing files or invalid input.

---

#### **Session 8: Shell and Python Integration, Project & Review**

---

**Learning Objectives:**
1. Learn to integrate Shell and Python scripts for workflow automation.
2. Understand when to use Shell vs. Python for specific tasks.
3. Develop a final project to automate a real-world task.

---

**Topics Covered:**

1. **Integrating Shell and Python Scripts**
   - **Use Cases**:
     - Shell scripts for system-level tasks (e.g., scheduling, file permissions).
     - Python scripts for data manipulation and complex logic.
   - **Executing Shell commands in Python**:
     - Using `subprocess` or `os.system`.
     ```python
     import subprocess

     # Run a shell command
     result = subprocess.run(['ls', '-l'], capture_output=True, text=True)
     print(result.stdout)
     ```
   - **Calling Python scripts from Shell**:
     - Use `python3 script.py` in a Shell script.

2. **Automating Workflows with Shell and Python**
   - **Example Workflow**:
     - Shell script to monitor disk usage and trigger a Python backup script.
     - Python script compresses files and uploads to a cloud server.

3. **Final Project Overview**
   - **Objective**: Develop a script that automates a real-world task.
   - **Example Task**:
     - Monitor disk usage.
     - Compress files into a ZIP archive.
     - Transfer backups to a remote server via SCP.

---

**Final Project Instructions:**

1. **Scenario**:
   - Automate the backup process for a directory.
   - Include monitoring disk usage and sending backups to a remote server.

2. **Steps**:
   - Write a Shell script to:
     - Monitor disk usage and log the data.
     - Trigger a Python script if disk usage is below a threshold.

   - Write a Python script to:
     - Compress files in a specific directory.
     - Transfer the compressed file to a remote server using `paramiko` (for SCP) or any other preferred library.
   - **Python Backup Script Example**:
     ```python
     import os
     import zipfile
     import paramiko

     def compress_files(source_dir, output_file):
         with zipfile.ZipFile(output_file, 'w', zipfile.ZIP_DEFLATED) as zipf:
             for root, dirs, files in os.walk(source_dir):
                 for file in files:
                     zipf.write(os.path.join(root, file),
                                os.path.relpath(os.path.join(root, file), source_dir))
         print(f"Backup created: {output_file}")

     def transfer_backup(zip_file, remote_host, username, password):
         ssh = paramiko.SSHClient()
         ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
         ssh.connect(remote_host, username=username, password=password)
         sftp = ssh.open_sftp()
         sftp.put(zip_file, f'/remote/path/{os.path.basename(zip_file)}')
         sftp.close()
         ssh.close()
         print("Backup transferred successfully")

     # Example usage
     compress_files('source_directory', 'backup.zip')
     transfer_backup('backup.zip', '192.168.1.100', 'username', 'password')
     ```

---

### **Assessment**

1. Submit the final project script.
2. Include documentation or comments explaining the workflow.
3. Evaluate based on:
   - Functionality and correctness.
   - Efficient use of Shell and Python integration.
   - Creativity in solving real-world problems.

---

### **Outcome**

Participants will:
- Gain advanced skills in Python scripting for file handling and system operations.
- Learn to integrate Shell and Python for comprehensive workflow automation.
- Complete a real-world project demonstrating mastery of the skills learned.
