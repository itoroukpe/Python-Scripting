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
This script is designed to:

1. **Read Data from a File**:
   - The script opens a file named `input.txt` in **read mode** (`'r'`).
   - It reads all the lines from the file and stores them in the variable `data`. Each line is treated as a separate string and stored in a list (one string per line).

2. **Process the Data**:
   - The script processes the content of the `data` list by converting each line to **uppercase** using the `.upper()` method.

3. **Write Processed Data to a New File**:
   - The script opens a file named `output.txt` in **write mode** (`'w'`), which creates the file if it doesn’t exist or overwrites it if it does.
   - For each line in the `data` list, it converts the line to uppercase and writes it to the `output.txt` file.
---
In Python, the `open()` function allows you to work with files in different modes. These modes define how the file will be opened (e.g., for reading, writing, or both) and whether the file's content should be treated as text or binary data.

---

### **1. Modes for Reading Files**

#### **Text Mode (`r`)**
- **Usage**: `open('filename.txt', 'r')`
- **Purpose**: Opens the file for reading text. This is the default mode if no mode is specified.
- **Behavior**:
  - The file must exist; otherwise, it raises a `FileNotFoundError`.
  - The file's content is treated as a string.
  - Reads the file line by line or in chunks.
- **Example**:
  ```python
  with open('example.txt', 'r') as file:
      for line in file:
          print(line.strip())  # Reads and prints each line
  ```

---

#### **Binary Mode (`rb`)**
- **Usage**: `open('filename.txt', 'rb')`
- **Purpose**: Opens the file for reading in binary mode.
- **Behavior**:
  - The file must exist; otherwise, it raises a `FileNotFoundError`.
  - The file's content is treated as bytes, not text.
  - Useful for non-text files like images, videos, or audio files.
- **Example**:
  ```python
  with open('example.jpg', 'rb') as file:
      content = file.read()
      print(content[:10])  # Prints the first 10 bytes
  ```

---

#### **Read and Write Mode (`r+`)**
- **Usage**: `open('filename.txt', 'r+')`
- **Purpose**: Opens the file for both reading and writing.
- **Behavior**:
  - The file must exist; otherwise, it raises a `FileNotFoundError`.
  - Allows modifications to the file's content while preserving its original data.
  - The file pointer is initially placed at the beginning of the file.
- **Example**:
  ```python
  with open('example.txt', 'r+') as file:
      content = file.read()
      print("Original Content:", content)
      file.write("\nNew content added.")  # Adds new content at the end
  ```

---

### **Comparison of Modes**

| Mode | Full Name      | Behavior                                                                                   |
|------|----------------|--------------------------------------------------------------------------------------------|
| `r`  | Read           | Opens the file for reading text. Raises an error if the file doesn't exist.                |
| `rb` | Read Binary    | Opens the file for reading binary data. Used for non-text files.                           |
| `r+` | Read/Write     | Opens the file for both reading and writing. Allows modifying existing content.            |

---

### **When to Use Each Mode**
1. **`r` (Read)**:
   - Use when you only need to read a file's text content.
   - Example: Reading a log file or a configuration file.

2. **`rb` (Read Binary)**:
   - Use when working with non-text files like images, videos, or compressed files.
   - Example: Reading an image to process its binary content.

3. **`r+` (Read/Write)**:
   - Use when you need to read a file and update its content.
   - Example: Modifying an existing log file or appending data to an existing file.

By understanding these modes, you can choose the appropriate way to interact with files based on your application's needs.
---
### **Purpose**
The script effectively reads all text from `input.txt`, converts it to uppercase, and saves the modified content into a new file called `output.txt`.

### **Example Use Case**
- If `input.txt` contains:
  ```
  Hello World
  This is a test.
  ```
- The resulting `output.txt` will contain:
  ```
  HELLO WORLD
  THIS IS A TEST.
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
This script performs two primary tasks:

### **1. Create a Directory**
- **Code**: `os.mkdir('test_directory')`
- **Purpose**: 
  - It creates a new directory called `test_directory` in the current working directory where the script is executed.
  - If a directory with the same name already exists, the script will raise a `FileExistsError`.

---

### **2. Fetch Command-Line Arguments**
- **Code**: 
  ```python
  if len(sys.argv) > 1:
      print(f"First argument: {sys.argv[1]}")
  ```
- **Purpose**: 
  - It checks if any command-line arguments were passed when the script was executed.
  - The `sys.argv` list contains the script's name as its first element (`sys.argv[0]`) and any additional arguments as subsequent elements.
  - If at least one argument (beyond the script name) is passed, the script prints the first argument (`sys.argv[1]`).

---

### **Example Usage:**
#### Running the Script
```bash
python script.py hello
```

#### Output:
1. Creates a directory named `test_directory` in the current directory.
2. Prints:
   ```
   First argument: hello
   ```

---

### **Key Notes:**
- **Error Handling**: 
  - If `test_directory` already exists, the `os.mkdir` line will throw a `FileExistsError`.
  - The script does not handle this error, so it will terminate unless the directory name is changed or removed beforehand.
- **Command-Line Argument**: If no argument is passed, the script will silently skip printing anything because `len(sys.argv)` will be `1` (only the script name).

### **Summary:**
The script demonstrates basic functionality:
1. Creating a directory using Python's `os` module.
2. Reading and printing a command-line argument using `sys.argv`.
   
---
4. **Automating Tasks with Python**
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
This script is designed to perform two primary tasks related to file backup and transfer:

### 1. **Compress Files into a ZIP Archive**
   - **Function**: `compress_files(source_dir, output_file)`
   - **Purpose**: This function compresses all files in the specified `source_dir` directory into a single ZIP archive file (`output_file`).
   - **How it works**:
     - It uses the `os.walk` function to iterate through all directories and files within `source_dir`.
     - For each file, it adds the file to a ZIP archive (`output_file`) using `zipfile.ZipFile` in write mode with compression (`ZIP_DEFLATED`).
     - Relative paths are maintained in the ZIP file for proper structure.
   - **Example**:
     If the `source_dir` contains:
     ```
     /source_dir/
       file1.txt
       folder1/
         file2.txt
     ```
     The resulting `backup.zip` would have:
     ```
     file1.txt
     folder1/file2.txt
     ```

---

### 2. **Transfer the Backup File to a Remote Server**
   - **Function**: `transfer_backup(zip_file, remote_host, username, password)`
   - **Purpose**: This function securely transfers the created ZIP archive (`zip_file`) to a remote server using the Secure File Transfer Protocol (SFTP) via the `paramiko` library.
   - **How it works**:
     - Establishes an SSH connection to the remote server using `paramiko.SSHClient`.
     - Authenticates with the given `username` and `password`.
     - Opens an SFTP session and uploads the specified `zip_file` to the `/remote/path/` directory on the remote server.
     - Closes the SFTP session and SSH connection after the transfer is complete.
   - **Example**:
     If the `zip_file` is named `backup.zip`:
     - The file is uploaded to `/remote/path/backup.zip` on the remote server specified by `remote_host`.

---

### **Script Workflow**
1. **Compress Files**:
   - Use the `compress_files` function to create a ZIP archive of the files in a specific directory.
   - Output: A ZIP file containing all the compressed files from the directory.

2. **Transfer the ZIP File**:
   - Use the `transfer_backup` function to securely upload the ZIP file to a remote server.
   - The file will be saved in the specified remote directory.

---

### **Real-World Use Case**
This script is useful for:
- Backing up important files or directories locally and transferring the backup to a remote server for safekeeping.
- Automating the backup and transfer process as part of a disaster recovery or archiving solution.

---

### **Example Usage**
```python
# Compress files in the "my_files" directory into "backup.zip"
compress_files('my_files', 'backup.zip')

# Transfer "backup.zip" to a remote server
transfer_backup('backup.zip', '192.168.1.100', 'username', 'password')
```

In this example:
- The contents of `my_files` will be compressed into `backup.zip`.
- `backup.zip` will then be uploaded to the remote server at `192.168.1.100` under `/remote/path/` using the provided credentials.
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
