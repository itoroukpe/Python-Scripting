# **Lab Exercise: Automating System Monitoring with Bash Scripting**  

## **Objective**  
By the end of this lab, students will be able to:  
✅ Write a Bash script to **monitor system health** (CPU, memory, and disk usage).  
✅ Use **conditional statements** to trigger alerts.  
✅ Schedule the script to run automatically using **cron jobs**.  
✅ Log alerts to a file for later analysis.  

---

## **Lab Setup**
### **Requirements**  
🛠️ **A Linux environment** (Ubuntu, CentOS, or MacOS)  
🛠️ **Bash Shell** (`bash` must be installed, which is default on Linux/Mac)  
🛠️ **Basic knowledge of Bash scripting**  
🛠️ **Cron (for scheduling tasks)**  

📌 **Before You Begin:**  
- Run `bash --version` to verify you are using Bash.  
- Ensure you have `mail` installed for email notifications:
  ```bash
  sudo apt install mailutils  # Debian/Ubuntu
  sudo yum install mailx      # CentOS/RHEL
  ```

---

## **Step 1: Create a System Monitoring Script**
1️⃣ **Create a new script file:**  
```bash
nano health_check.sh
```
2️⃣ **Paste the following script:**
```bash
#!/bin/bash
# System Monitoring Script: Logs CPU, Memory, and Disk Usage

LOG_FILE="/var/log/system_health.log"
CPU_THRESHOLD=80
MEM_THRESHOLD=80
DISK_THRESHOLD=90

# Get CPU Usage
CPU_USAGE=$(top -bn1 | grep "Cpu(s)" | awk '{print $2 + $4}')

# Get Memory Usage
MEM_USAGE=$(free | awk '/Mem/ {print $3/$2 * 100.0}')

# Get Disk Usage (root partition)
DISK_USAGE=$(df -h / | awk 'NR==2 {print $5}' | tr -d '%')

# Function to log alerts
log_alert() {
    local message="$1"
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $message" >> $LOG_FILE
}

# Check CPU Usage
if (( $(echo "$CPU_USAGE > $CPU_THRESHOLD" | bc -l) )); then
    log_alert "⚠️ High CPU Usage Detected: $CPU_USAGE%"
fi

# Check Memory Usage
if (( $(echo "$MEM_USAGE > $MEM_THRESHOLD" | bc -l) )); then
    log_alert "⚠️ High Memory Usage Detected: $MEM_USAGE%"
fi

# Check Disk Usage
if (( DISK_USAGE > DISK_THRESHOLD )); then
    log_alert "⚠️ High Disk Usage Detected: $DISK_USAGE%"
fi

echo "✅ System health check completed. Logs saved at $LOG_FILE"
```
3️⃣ **Save the file (`CTRL+X`, then `Y`, then `Enter`)**  

4️⃣ **Give the script execution permission:**
```bash
chmod +x health_check.sh
```

---

## **Step 2: Run the Script**
📌 **Test the script manually** by running:  
```bash
./health_check.sh
```
📌 **Check the logs:**  
```bash
cat /var/log/system_health.log
```

✅ **Expected Output (if no alerts):**
```
✅ System health check completed. Logs saved at /var/log/system_health.log
```
✅ **Expected Output (if alerts are triggered in log file):**
```
2025-02-25 14:00:10 - ⚠️ High CPU Usage Detected: 85.3%
2025-02-25 14:00:11 - ⚠️ High Memory Usage Detected: 92.5%
```

---

## **Step 3: Automate with Cron Job**
Students will schedule the script to run automatically **every 5 minutes**.

1️⃣ **Open crontab:**  
```bash
crontab -e
```
2️⃣ **Add this line at the end of the file:**
```bash
*/5 * * * * /path/to/health_check.sh
```
3️⃣ **Save and exit.**  

✅ **Verify the cron job is set up:**  
```bash
crontab -l
```

📌 **After 10-15 minutes, check the logs again:**  
```bash
cat /var/log/system_health.log
```

---

## **Step 4: Lab Questions for Students**
1. What command is used to **make a Bash script executable**?  
2. How does `awk` help extract system metrics in the script?  
3. How would you modify the script to **send email alerts** instead of just logging?  
4. What change would you make to **monitor network activity** (hint: `ifconfig` or `ip a`)?  
5. How do you remove a scheduled cron job?  

---

## **Bonus Challenge 🚀**
Modify the script to:  
- Send an **email alert** when thresholds are exceeded.  
- Include **network usage monitoring** in the log report.  
- Log system uptime using `uptime` command.  

---

### **Expected Learning Outcomes**
🔹 Understand how Bash scripting **automates system monitoring**.  
🔹 Gain experience with **log file management**.  
🔹 Learn **cron job scheduling** for automation.  
🔹 Enhance **problem-solving skills** by modifying and improving scripts.  

---

# **Advanced Bash Scripting Lab for DevOps Students**  
💡 **Objective:** These additional exercises will help students expand their Bash scripting skills by automating **process monitoring, auto-restarts, and disk cleanup**. Each lab contains a **step-by-step guide, script implementation, and follow-up questions**.  

---

## **Lab 1: Process Monitoring & Auto-Restart**  
🔹 **Use Case:** Ensure that critical services (e.g., **Nginx, MySQL, or Apache**) are running. If a service crashes, the script will **automatically restart it** and log the incident.

### **Step 1: Create the Script**
1️⃣ **Create a new script file:**  
```bash
nano process_monitor.sh
```

2️⃣ **Paste the following script:**
```bash
#!/bin/bash
# Script to monitor critical services and restart if down

LOG_FILE="/var/log/process_monitor.log"
SERVICES=("nginx" "mysql" "docker")

# Function to log status
log_status() {
    local message="$1"
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $message" >> $LOG_FILE
}

for SERVICE in "${SERVICES[@]}"
do
    if ! systemctl is-active --quiet $SERVICE; then
        log_status "⚠️ $SERVICE is down! Restarting..."
        systemctl restart $SERVICE
        if systemctl is-active --quiet $SERVICE; then
            log_status "✅ $SERVICE restarted successfully!"
        else
            log_status "❌ Failed to restart $SERVICE!"
        fi
    fi
done
```

3️⃣ **Save and make it executable:**  
```bash
chmod +x process_monitor.sh
```

4️⃣ **Test the script manually:**  
```bash
./process_monitor.sh
```

### **Step 2: Automate with Cron Job**
1️⃣ Open cron job editor:  
```bash
crontab -e
```
2️⃣ Add this line to check every **3 minutes**:  
```bash
*/3 * * * * /path/to/process_monitor.sh
```
✅ **Now the script will monitor and restart any failed services every 3 minutes!**

---

### **Lab 1 Questions**
1. What command is used to check if a service is active?  
2. How can you modify the script to send an **email alert** when a service is down?  
3. If a service fails to restart, what action should be taken?  

---

## **Lab 2: Automated Disk Cleanup**  
🔹 **Use Case:** Remove **old logs** and **unnecessary files** to free up disk space.

### **Step 1: Create the Script**
1️⃣ **Create a new script file:**  
```bash
nano disk_cleanup.sh
```

2️⃣ **Paste the following script:**
```bash
#!/bin/bash
# Script to clean up old log files and free disk space

LOG_DIR="/var/log"
BACKUP_DIR="/backup"
DAYS=7
LOG_FILE="/var/log/disk_cleanup.log"

# Function to log status
log_status() {
    local message="$1"
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $message" >> $LOG_FILE
}

log_status "Starting disk cleanup..."

# Delete log files older than 7 days
find $LOG_DIR -name "*.log" -type f -mtime +$DAYS -exec rm -f {} \;
log_status "Deleted old log files from $LOG_DIR."

# Delete backups older than 30 days
find $BACKUP_DIR -name "*.tar.gz" -type f -mtime +30 -exec rm -f {} \;
log_status "Deleted old backups from $BACKUP_DIR."

log_status "Disk cleanup completed!"
```

3️⃣ **Save and make it executable:**  
```bash
chmod +x disk_cleanup.sh
```

4️⃣ **Test the script manually:**  
```bash
./disk_cleanup.sh
```

### **Step 2: Automate with Cron Job**
1️⃣ Open cron job editor:  
```bash
crontab -e
```
2️⃣ Add this line to schedule cleanup every **Sunday at midnight**:  
```bash
0 0 * * 0 /path/to/disk_cleanup.sh
```
✅ **Now the script will run weekly, keeping disk usage under control!**

---

### **Lab 2 Questions**
1. What does `find $LOG_DIR -name "*.log" -type f -mtime +$DAYS -exec rm -f {} \;` do?  
2. How can you modify the script to send an alert if disk usage is over **90%**?  
3. What are the risks of **automating file deletions**, and how can they be mitigated?  

---

## **Lab 3: System Uptime & Network Monitoring**  
🔹 **Use Case:** Monitor system uptime, check network activity, and detect connectivity issues.

### **Step 1: Create the Script**
1️⃣ **Create a new script file:**  
```bash
nano network_monitor.sh
```

2️⃣ **Paste the following script:**
```bash
#!/bin/bash
# Script to monitor system uptime and network connectivity

LOG_FILE="/var/log/network_monitor.log"
ALERT_EMAIL="admin@example.com"

# Function to log status
log_status() {
    local message="$1"
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $message" >> $LOG_FILE
}

# Check system uptime
UPTIME=$(uptime -p)
log_status "System Uptime: $UPTIME"

# Check Internet Connectivity
ping -c 2 8.8.8.8 &> /dev/null
if [ $? -eq 0 ]; then
    log_status "✅ Internet is available."
else
    log_status "❌ Internet is down!"
    echo "Internet connectivity lost on $(date)" | mail -s "Network Alert" $ALERT_EMAIL
fi

# Check Open Network Ports
log_status "Active network connections:"
netstat -tulnp | grep LISTEN >> $LOG_FILE
```

3️⃣ **Save and make it executable:**  
```bash
chmod +x network_monitor.sh
```

4️⃣ **Test the script manually:**  
```bash
./network_monitor.sh
```

### **Step 2: Automate with Cron Job**
1️⃣ Open cron job editor:  
```bash
crontab -e
```
2️⃣ Add this line to check network status **every 10 minutes**:  
```bash
*/10 * * * * /path/to/network_monitor.sh
```
✅ **Now the script will monitor uptime and network connectivity every 10 minutes!**

---

### **Lab 3 Questions**
1. What does `ping -c 2 8.8.8.8 &> /dev/null` do?  
2. How can you modify the script to **detect high network usage**?  
3. What command can be used to monitor **live network activity** (hint: `iftop` or `nload`)?  

---

# **Final Challenge: Comprehensive System Monitoring & Automation Script**  
💡 **Objective:** This script **combines all previous labs** into a single **powerful Bash automation tool** that:  
✅ **Monitors system health (CPU, memory, disk usage)**  
✅ **Auto-restarts critical services if they crash**  
✅ **Cleans up old logs to free disk space**  
✅ **Checks network connectivity and alerts if down**  
✅ **Sends a summary email report**  

---

## **Step 1: Create the Script**
1️⃣ **Create a new script file:**  
```bash
nano system_monitor.sh
```

2️⃣ **Paste the following script:**
```bash
#!/bin/bash
# Comprehensive System Monitoring & Automation Script

LOG_FILE="/var/log/system_monitor.log"
ALERT_EMAIL="admin@example.com"
CPU_THRESHOLD=80
MEM_THRESHOLD=80
DISK_THRESHOLD=90
LOG_CLEANUP_DAYS=7
SERVICES=("nginx" "mysql" "docker")

# Function to log status
log_status() {
    local message="$1"
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $message" >> $LOG_FILE
}

log_status "🚀 Running System Monitoring Script..."

# Monitor CPU Usage
CPU_USAGE=$(top -bn1 | grep "Cpu(s)" | awk '{print $2 + $4}')
if (( $(echo "$CPU_USAGE > $CPU_THRESHOLD" | bc -l) )); then
    log_status "⚠️ High CPU Usage Detected: $CPU_USAGE%"
fi

# Monitor Memory Usage
MEM_USAGE=$(free | awk '/Mem/ {print $3/$2 * 100.0}')
if (( $(echo "$MEM_USAGE > $MEM_THRESHOLD" | bc -l) )); then
    log_status "⚠️ High Memory Usage Detected: $MEM_USAGE%"
fi

# Monitor Disk Usage
DISK_USAGE=$(df -h / | awk 'NR==2 {print $5}' | tr -d '%')
if (( DISK_USAGE > DISK_THRESHOLD )); then
    log_status "⚠️ High Disk Usage Detected: $DISK_USAGE%"
fi

# Auto-Restart Critical Services if Down
for SERVICE in "${SERVICES[@]}"
do
    if ! systemctl is-active --quiet $SERVICE; then
        log_status "❌ $SERVICE is down! Restarting..."
        systemctl restart $SERVICE
        if systemctl is-active --quiet $SERVICE; then
            log_status "✅ $SERVICE restarted successfully!"
        else
            log_status "❌ Failed to restart $SERVICE!"
        fi
    fi
done

# Clean Up Old Log Files
log_status "🧹 Cleaning up log files older than $LOG_CLEANUP_DAYS days..."
find /var/log -name "*.log" -type f -mtime +$LOG_CLEANUP_DAYS -exec rm -f {} \;
log_status "✅ Old logs cleaned up."

# Network Connectivity Check
ping -c 2 8.8.8.8 &> /dev/null
if [ $? -eq 0 ]; then
    log_status "✅ Internet is available."
else
    log_status "❌ Internet is down! Sending alert..."
    echo "Internet connectivity lost on $(date)" | mail -s "🚨 Network Alert" $ALERT_EMAIL
fi

# Send Summary Email Report
mail -s "🚀 System Monitoring Report" $ALERT_EMAIL < $LOG_FILE

log_status "✅ System monitoring completed!"
```

---

## **Step 2: Make It Executable**
```bash
chmod +x system_monitor.sh
```

---

## **Step 3: Test the Script**
```bash
./system_monitor.sh
```
✅ **Check the log file output:**
```bash
cat /var/log/system_monitor.log
```

✅ **If thresholds are exceeded, an email should be sent automatically.**  

---

## **Step 4: Automate with Cron Job**
1️⃣ Open cron job editor:  
```bash
crontab -e
```
2️⃣ Add this line to run the script **every 10 minutes**:  
```bash
*/10 * * * * /path/to/system_monitor.sh
```

✅ **Now, the system is continuously monitored and self-healing!**

---

## **Final Challenge Questions**
1. How would you modify the script to also **monitor network bandwidth usage**?  
2. What other **services** might be critical to restart automatically?  
3. How can you modify the script to **send alerts to Slack or a webhook** instead of email?  
4. How can you **store monitoring history in a database (MySQL/PostgreSQL)?**  

---


