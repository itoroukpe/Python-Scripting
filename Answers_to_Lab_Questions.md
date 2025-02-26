### **Step 4: Lab Questions & Answers**  

#### **1️⃣ What command is used to make a Bash script executable?**  
To make a Bash script executable, use the `chmod` command:  
```bash
chmod +x script_name.sh
```
🔹 Example:  
```bash
chmod +x health_check.sh
```
This grants **execute permissions** to the script, allowing it to be run as:  
```bash
./health_check.sh
```

---

#### **2️⃣ How does `awk` help extract system metrics in the script?**  
`awk` is a powerful text-processing tool used to **extract and manipulate specific fields from command outputs**.

🔹 **Example: Extracting CPU usage**  
```bash
top -bn1 | grep "Cpu(s)" | awk '{print $2 + $4}'
```
- `top -bn1`: Runs **top** command in batch mode for **one iteration**  
- `grep "Cpu(s)"`: Filters the line containing **CPU usage details**  
- `awk '{print $2 + $4}'`: Extracts the **user CPU% ($2) + system CPU% ($4)**  

🔹 **Example: Extracting Memory Usage**  
```bash
free | awk '/Mem/ {print $3/$2 * 100.0}'
```
- `free`: Shows memory usage  
- `awk '/Mem/ {print $3/$2 * 100.0}'`: Calculates memory usage percentage  

🔹 **Example: Extracting Disk Usage**  
```bash
df -h / | awk 'NR==2 {print $5}' | tr -d '%'
```
- `df -h /`: Shows disk usage for root `/` partition  
- `awk 'NR==2 {print $5}'`: Extracts the **percentage used**  
- `tr -d '%'`: Removes the **%** symbol for numeric comparisons  

---

#### **3️⃣ How would you modify the script to send email alerts instead of just logging?**  
You can use the `mail` or `mailx` command to send alerts via email.

🔹 **Modify the `log_status` function to send an email alert:**  
```bash
send_alert() {
    local message="$1"
    echo "$message" | mail -s "🚨 System Alert" admin@example.com
}
```

🔹 **Integrate into the script:**  
```bash
if (( $(echo "$CPU_USAGE > $CPU_THRESHOLD" | bc -l) )); then
    send_alert "⚠️ High CPU Usage Detected: $CPU_USAGE%"
fi
```
This will send an email **whenever CPU usage exceeds the threshold**.

📌 **Ensure Mail Utility is Installed:**  
```bash
sudo apt install mailutils  # Debian/Ubuntu
sudo yum install mailx      # CentOS/RHEL
```

---

#### **4️⃣ What change would you make to monitor network activity (hint: `ifconfig` or `ip a`)?**  
To monitor **network activity**, use `ifconfig`, `ip a`, or `netstat`.

🔹 **Check Network Interfaces**  
```bash
ifconfig | grep "inet "
```
or  
```bash
ip a | grep "inet"
```

🔹 **Monitor Active Network Connections**  
```bash
netstat -tulnp | grep LISTEN
```
- `netstat -tulnp`: Shows **TCP/UDP ports in listening state**  
- `grep LISTEN`: Filters only **active connections**  

🔹 **Modify the script to log network activity:**  
```bash
log_status "Active network connections:"
netstat -tulnp | grep LISTEN >> $LOG_FILE
```

🔹 **Monitor Internet Connectivity**  
```bash
ping -c 2 8.8.8.8 &> /dev/null
if [ $? -ne 0 ]; then
    log_status "❌ Internet is down!"
fi
```

---

#### **5️⃣ How do you remove a scheduled cron job?**  
To remove a scheduled **cron job**, follow these steps:

🔹 **List current cron jobs:**  
```bash
crontab -l
```

🔹 **Remove a specific cron job:**  
Edit the crontab file:  
```bash
crontab -e
```
- **Delete the line** corresponding to the scheduled script.  
- **Save & exit** (CTRL+X → Y → Enter).  

🔹 **Remove all scheduled cron jobs for the user:**  
```bash
crontab -r
```
📌 **Warning:** This **deletes ALL cron jobs** for the user!  

---

### ✅ **Summary of Key Commands**
| Task | Command |
|------|---------|
| **Make script executable** | `chmod +x script.sh` |
| **Extract CPU usage with awk** | `top -bn1 | grep "Cpu(s)" | awk '{print $2 + $4}'` |
| **Extract Memory usage with awk** | `free | awk '/Mem/ {print $3/$2 * 100.0}'` |
| **Extract Disk usage with awk** | `df -h / | awk 'NR==2 {print $5}' | tr -d '%'` |
| **Send email alerts in Bash** | `echo "Message" | mail -s "Subject" admin@example.com` |
| **Check network activity** | `netstat -tulnp | grep LISTEN` |
| **Check internet connectivity** | `ping -c 2 8.8.8.8` |
| **List scheduled cron jobs** | `crontab -l` |
| **Edit cron jobs** | `crontab -e` |
| **Remove all cron jobs** | `crontab -r` |
---
