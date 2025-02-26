Here are some **practical use cases of Bash scripting** for automation in **DevOps and software development** that your students can implement:

---

### **1️⃣ Automating Code Compilation & Deployment**
**Use Case:** Automate the build and deployment of a software application.

📜 **Script: `build_deploy.sh`**
```bash
#!/bin/bash
# This script compiles code, runs tests, and deploys it to a server

set -e  # Exit on error

echo "Compiling source code..."
mvn clean package -DskipTests

echo "Running tests..."
mvn test

echo "Deploying application..."
scp target/*.jar user@server:/opt/app/

echo "Restarting application..."
ssh user@server 'systemctl restart myapp.service'

echo "Deployment successful!"
```
📌 **Concepts Covered:**  
- Compilation (`mvn clean package`)  
- Automated Testing  
- Secure File Copy (`scp`)  
- Remote Execution (`ssh`)  

---

### **2️⃣ Automated Log Monitoring & Alerting**
**Use Case:** Monitor application logs for errors and send alerts via email.

📜 **Script: `monitor_logs.sh`**
```bash
#!/bin/bash
# This script monitors logs and sends an email alert if errors are detected

LOG_FILE="/var/log/myapp.log"
ALERT_EMAIL="admin@example.com"

tail -F $LOG_FILE | while read LINE; do
    if echo "$LINE" | grep -q "ERROR"; then
        echo "Error detected in logs: $LINE" | mail -s "Log Error Alert" $ALERT_EMAIL
    fi
done
```
📌 **Concepts Covered:**  
- Log monitoring (`tail -F`)  
- String search (`grep`)  
- Email notification (`mail`)  

---

### **3️⃣ Automated Backup of a Database**
**Use Case:** Automatically backup a MySQL database every night.

📜 **Script: `backup_db.sh`**
```bash
#!/bin/bash
# This script backs up a MySQL database daily

DB_NAME="mydatabase"
DB_USER="root"
DB_PASS="password"
BACKUP_DIR="/backup"

mkdir -p $BACKUP_DIR
BACKUP_FILE="$BACKUP_DIR/${DB_NAME}_$(date +%F).sql"

echo "Backing up database..."
mysqldump -u $DB_USER -p$DB_PASS $DB_NAME > $BACKUP_FILE

echo "Backup completed: $BACKUP_FILE"
```
📌 **Concepts Covered:**  
- Database Backup (`mysqldump`)  
- Dynamic Filenames using `date`  
- Automating with `cron`  

🕒 **Set up a cron job for daily backups:**  
```bash
0 2 * * * /path/to/backup_db.sh
```

---

### **4️⃣ Automated Docker Container Deployment**
**Use Case:** Deploy an application inside a Docker container.

📜 **Script: `deploy_docker.sh`**
```bash
#!/bin/bash
# This script builds and runs a Docker container

IMAGE_NAME="myapp"
CONTAINER_NAME="myapp_container"

echo "Building Docker image..."
docker build -t $IMAGE_NAME .

echo "Stopping existing container..."
docker stop $CONTAINER_NAME 2>/dev/null || true
docker rm $CONTAINER_NAME 2>/dev/null || true

echo "Starting new container..."
docker run -d --name $CONTAINER_NAME -p 8080:8080 $IMAGE_NAME

echo "Deployment complete!"
```
📌 **Concepts Covered:**  
- Building Docker Images  
- Stopping & Removing Containers  
- Running New Containers  

---

### **5️⃣ Automated System Health Check**
**Use Case:** Monitor system resources (CPU, memory, disk usage).

📜 **Script: `health_check.sh`**
```bash
#!/bin/bash
# This script monitors system resources and sends alerts if usage is high

CPU_THRESHOLD=80
MEM_THRESHOLD=80
DISK_THRESHOLD=90
ALERT_EMAIL="admin@example.com"

CPU_USAGE=$(top -bn1 | grep "Cpu(s)" | awk '{print $2 + $4}')
MEM_USAGE=$(free | awk '/Mem/ {print $3/$2 * 100.0}')
DISK_USAGE=$(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')

if (( $(echo "$CPU_USAGE > $CPU_THRESHOLD" | bc -l) )); then
    echo "High CPU usage: $CPU_USAGE%" | mail -s "CPU Alert" $ALERT_EMAIL
fi

if (( $(echo "$MEM_USAGE > $MEM_THRESHOLD" | bc -l) )); then
    echo "High Memory usage: $MEM_USAGE%" | mail -s "Memory Alert" $ALERT_EMAIL
fi

if (( DISK_USAGE > DISK_THRESHOLD )); then
    echo "High Disk usage: $DISK_USAGE%" | mail -s "Disk Alert" $ALERT_EMAIL
fi
```
📌 **Concepts Covered:**  
- Resource monitoring (`top`, `free`, `df -h`)  
- Conditional Execution  
- Sending Alerts  

---

### **6️⃣ Git Automation: Pushing Code to Repository**
**Use Case:** Automate pushing local code changes to a Git repository.

📜 **Script: `git_push.sh`**
```bash
#!/bin/bash
# Automates Git commit & push process

REPO_DIR="/home/user/project"
cd $REPO_DIR

git add .
git commit -m "Automated commit on $(date +%F)"
git push origin main

echo "Code pushed successfully!"
```
📌 **Concepts Covered:**  
- Git Automation (`git add`, `git commit`, `git push`)  
- Dynamic Commit Messages  

🕒 **Schedule Auto Push Every Night:**  
```bash
0 3 * * * /path/to/git_push.sh
```

---

### **7️⃣ Auto Restart Services if They Crash**
**Use Case:** Restart a critical service (e.g., Nginx, Apache) if it crashes.

📜 **Script: `auto_restart.sh`**
```bash
#!/bin/bash
# Restart Nginx if it's not running

SERVICE="nginx"

if ! systemctl is-active --quiet $SERVICE; then
    echo "$SERVICE is down, restarting..." >> /var/log/service_monitor.log
    systemctl restart $SERVICE
fi
```
📌 **Concepts Covered:**  
- Checking Service Status (`systemctl is-active`)  
- Logging (`>> /var/log/service_monitor.log`)  
- Auto Restarting Services  

🕒 **Set up a cron job to check every 5 minutes:**  
```bash
*/5 * * * * /path/to/auto_restart.sh
```

---

### **8️⃣ Automated Security Patching**
**Use Case:** Update system packages automatically.

📜 **Script: `auto_update.sh`**
```bash
#!/bin/bash
# Automatically updates system packages

echo "Updating system packages..."
apt update && apt upgrade -y
echo "System update complete."
```
📌 **Concepts Covered:**  
- Automating Updates (`apt update && apt upgrade`)  

🕒 **Run Weekly Updates:**  
```bash
0 4 * * 1 /path/to/auto_update.sh
```

---

