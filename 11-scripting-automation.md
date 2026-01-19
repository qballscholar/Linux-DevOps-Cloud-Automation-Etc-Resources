**\========================================**  
**CATEGORY 11: SCRIPTING & AUTOMATION**  
**\========================================**

**11.1 BASH SCRIPTING FUNDAMENTALS:**

**/\* COMMENT: Bash scripting automates repetitive tasks and system administration.**  
   **Understanding variables, conditionals, loops, and functions is essential**  
   **for effective automation. \*/**

**KEY CONCEPTS:**  
**• Shebang: \#\!/bin/bash at script start**  
**• Variables: Store and manipulate data**  
**• Conditionals: if/else logic**  
**• Loops: for, while, until**  
**• Functions: Reusable code blocks**

**BASIC STRUCTURE:**  
**\#\!/bin/bash**  
**\# Script description**

**\# Variables**  
**NAME="John"**  
**COUNT=10**

**\# Command output to variable**  
**CURRENT\_DIR=$(pwd)**  
**DATE=\`date \+%Y-%m-%d\`**

**\# String operations**  
**echo "Hello, $NAME"**  
**echo "Length: ${\#NAME}"**  
**echo "Substring: ${NAME:0:2}"**

**CONDITIONALS:**  
**\# If statement**  
**if \[ $COUNT \-gt 5 \]; then**  
    **echo "Count is greater than 5"**  
**elif \[ $COUNT \-eq 5 \]; then**  
    **echo "Count is 5"**  
**else**  
    **echo "Count is less than 5"**  
**fi**

**\# File tests**  
**if \[ \-f /etc/passwd \]; then**  
    **echo "File exists"**  
**fi**

**if \[ \-d /var/log \]; then**  
    **echo "Directory exists"**  
**fi**

**\# String comparison**  
**if \[ "$NAME" \= "John" \]; then**  
    **echo "Name is John"**  
**fi**

**LOOPS:**  
**\# For loop**  
**for i in 1 2 3 4 5; do**  
    **echo "Number: $i"**  
**done**

**\# For loop with range**  
**for i in {1..10}; do**  
    **echo "Count: $i"**  
**done**

**\# For loop with files**  
**for file in /var/log/\*.log; do**  
    **echo "Processing $file"**  
**done**

**\# While loop**  
**COUNTER=0**  
**while \[ $COUNTER \-lt 5 \]; do**  
    **echo "Counter: $COUNTER"**  
    **((COUNTER++))**

**done**

**FUNCTIONS:**  
**\# Define function**  
**function backup\_files() {**  
    **local source=$1**  
    **local dest=$2**  
    **echo "Backing up $source to $dest"**  
    **cp \-r "$source" "$dest"**  
**}**

**\# Call function**  
**backup\_files "/home/user/data" "/backup/"**

**\# Function with return value**  
**function is\_root() {**  
    **if \[ "$(id \-u)" \-eq 0 \]; then**  
        **return 0  \# True**  
    **else**  
        **return 1  \# False**  
    **fi**  
**}**

**if is\_root; then**  
    **echo "Running as root"**  
**fi**

**PRACTICAL EXAMPLE \- BACKUP SCRIPT:**  
**\#\!/bin/bash**  
**\# Automated backup script**

**\# Variables**  
**BACKUP\_SOURCE="/home/user/data"**  
**BACKUP\_DEST="/backup"**  
**DATE=$(date \+%Y-%m-%d\_%H-%M-%S)**  
**BACKUP\_FILE="backup\_${DATE}.tar.gz"**  
**LOG\_FILE="/var/log/backup.log"**  
**RETENTION\_DAYS=7**

**\# Function to log messages**  
**log\_message() {**  
    **echo "\[$(date '+%Y-%m-%d %H:%M:%S')\] $1" \>\> "$LOG\_FILE"**  
**}**

**\# Check if source exists**  
**if \[ \! \-d "$BACKUP\_SOURCE" \]; then**  
    **log\_message "ERROR: Source directory does not exist"**  
    **exit 1**  
**fi**

**\# Create backup directory if not exists**  
**mkdir \-p "$BACKUP\_DEST"**

**\# Create backup**  
**log\_message "Starting backup of $BACKUP\_SOURCE"**  
**tar \-czf "${BACKUP\_DEST}/${BACKUP\_FILE}" "$BACKUP\_SOURCE" 2\>\> "$LOG\_FILE"**

**if \[ $? \-eq 0 \]; then**  
    **log\_message "Backup completed successfully: $BACKUP\_FILE"**  
**else**  
    **log\_message "ERROR: Backup failed"**  
    **exit 1**  
**fi**

**\# Remove old backups**  
**log\_message "Removing backups older than $RETENTION\_DAYS days"**  
**find "$BACKUP\_DEST" \-name "backup\_\*.tar.gz" \-mtime \+$RETENTION\_DAYS \-delete**

**log\_message "Backup process completed"**

**BEST PRACTICES:**  
**• Always use shebang (\#\!/bin/bash)**  
**• Quote variables to handle spaces**  
**• Use meaningful variable names**  
**• Implement error checking**  
**• Add comments for clarity**  
**• Make scripts executable (chmod \+x)**  
**• Log important operations**  
**• Use functions for reusability**

**11.2 PYTHON FOR AUTOMATION:**

**/\* COMMENT: Python is excellent for complex automation tasks, API interactions,**  
   **and data processing. Its extensive libraries make it ideal for DevOps**  
   **automation beyond simple shell scripts. \*/**

**KEY CONCEPTS:**  
**• Libraries: requests, paramiko, boto3, fabric**  
**• Exception Handling: try/except blocks**  
**• File Operations: Read/write files**  
**• API Interactions: REST APIs**  
**• Data Structures: Lists, dicts, tuples**

**BASIC SCRIPT STRUCTURE:**  
**\#\!/usr/bin/env python3**  
**import os**  
**import sys**  
**import logging**  
**from datetime import datetime**

**\# Setup logging**  
**logging.basicConfig(**  
    **level=logging.INFO,**  
    **format='%(asctime)s \- %(levelname)s \- %(message)s'**  
**)**

**def main():**  
    **logging.info("Script started")**  
    **\# Your code here**  
    **logging.info("Script completed")**

**if \_\_name\_\_ \== "\_\_main\_\_":**  
    **main()**

**FILE OPERATIONS:**  
**import os**  
**import shutil**

**\# Read file**  
**with open('file.txt', 'r') as f:**  
    **content \= f.read()**  
      
**\# Write file**  
**with open('output.txt', 'w') as f:**  
    **f.write("Hello, World\!\\n")**

**\# Append to file**  
**with open('log.txt', 'a') as f:**  
    **f.write(f"{datetime.now()}: Log entry\\n")**

**\# Check if file/directory exists**  
**if os.path.exists('/path/to/file'):**  
    **print("File exists")**

**if os.path.isdir('/path/to/directory'):**  
    **print("Directory exists")**

**\# List files**  
**for filename in os.listdir('/var/log'):**  
    **print(filename)**

**\# Copy/move files**  
**shutil.copy('source.txt', 'destination.txt')**  
**shutil.move('old\_location.txt', 'new\_location.txt')**

**SYSTEM COMMANDS:**  
**import subprocess**

**\# Run command and capture output**  
**result \= subprocess.run(**  
    **\['ls', '-la', '/var/log'\],**  
    **capture\_output=True,**  
    **text=True**  
**)**

**if result.returncode \== 0:**  
    **print("Output:", result.stdout)**  
**else:**  
    **print("Error:", result.stderr)**

**\# Run command with shell**  
**subprocess.run('echo $HOME', shell=True)**

**HTTP REQUESTS:**  
**import requests**  
**import json**

**\# GET request**  
**response \= requests.get('https://api.example.com/users')**  
**if response.status\_code \== 200:**  
    **data \= response.json()**  
    **print(data)**

**\# POST request**  
**headers \= {'Content-Type': 'application/json'}**  
**data \= {'name': 'John', 'email': 'john@example.com'}**  
**response \= requests.post(**  
    **'https://api.example.com/users',**  
    **headers=headers,**  
    **json=data**  
**)**

**\# With authentication**  
**response \= requests.get(**  
    **'https://api.example.com/data',**  
    **auth=('username', 'password')**  
**)**

**PRACTICAL EXAMPLE \- SERVER MONITORING:**  
**\#\!/usr/bin/env python3**  
**import psutil**  
**import logging**  
**import smtplib**  
**from email.mime.text import MIMEText**  
**from datetime import datetime**

**logging.basicConfig(**  
    **filename='/var/log/server\_monitor.log',**  
    **level=logging.INFO,**  
    **format='%(asctime)s \- %(levelname)s \- %(message)s'**  
**)**

**\# Thresholds**  
**CPU\_THRESHOLD \= 80**  
**MEMORY\_THRESHOLD \= 85**  
**DISK\_THRESHOLD \= 90**

**def check\_cpu():**  
    **cpu\_percent \= psutil.cpu\_percent(interval=1)**  
    **if cpu\_percent \> CPU\_THRESHOLD:**  
        **message \= f"High CPU usage: {cpu\_percent}%"**  
        **logging.warning(message)**  
        **send\_alert(message)**  
        **return False**  
    **return True**

**def check\_memory():**  
    **memory \= psutil.virtual\_memory()**  
    **if memory.percent \> MEMORY\_THRESHOLD:**  
        **message \= f"High memory usage: {memory.percent}%"**  
        **logging.warning(message)**  
        **send\_alert(message)**  
        **return False**  
    **return True**

**def check\_disk():**  
    **disk \= psutil.disk\_usage('/')**  
    **if disk.percent \> DISK\_THRESHOLD:**  
        **message \= f"High disk usage: {disk.percent}%"**  
        **logging.warning(message)**  
        **send\_alert(message)**  
        **return False**  
    **return True**

**def send\_alert(message):**  
    **\# Send email alert (simplified)**  
    **logging.info(f"Alert sent: {message}")**  
    **\# Implement email sending logic here**

**def main():**  
    **logging.info("Starting server monitoring")**  
      
    **all\_ok \= True**  
    **all\_ok \= check\_cpu() and all\_ok**  
    **all\_ok \= check\_memory() and all\_ok**  
    **all\_ok \= check\_disk() and all\_ok**  
      
    **if all\_ok:**  
        **logging.info("All systems normal")**  
    **else:**  
        **logging.warning("Some systems require attention")**

**if \_\_name\_\_ \== "\_\_main\_\_":**  
    **main()**

**BEST PRACTICES:**  
**• Use virtual environments**  
**• Implement proper error handling**  
**• Use logging instead of print statements**  
**• Follow PEP 8 style guide**  
**• Use type hints for better code clarity**  
**• Implement unit tests**

**11.3 CRON JOBS:**

**/\* COMMENT: Cron automates recurring tasks by scheduling scripts to run at**  
   **specific times. Essential for backups, monitoring, log rotation,**  
   **and maintenance tasks. \*/**

**KEY CONCEPTS:**  
**• Crontab: User's cron schedule file**  
**• Cron Syntax: minute hour day month weekday command**  
**• System Cron: /etc/cron.d/, /etc/cron.daily/, etc.**  
**• Environment: Limited PATH and variables**  
**• Output: Mailed to user or redirected to logs**

**CRON SYNTAX:**  
**\# Format: minute hour day month weekday command**  
**\# \* \* \* \* \* command**  
**\#   │ │ │ │ │**  
**\#   │ │ │ │ └── Day of week (0-7, both 0 and 7 are Sunday)**  
**\#   │ │ │ └──── Month (1-12)**  
**\#   │ │ └────── Day of month (1-31)**  
**\#   │ └──────── Hour (0-23)**  
**\#   └────────── Minute (0-59)**

**CRONTAB COMMANDS:**  
**\# View current crontab**  
**crontab \-l**

**\# Edit crontab**  
**crontab \-e**

**\# Remove crontab**  
**crontab \-r**

**\# Edit another user's crontab (as root)**  
**sudo crontab \-u username \-e**

**COMMON EXAMPLES:**  
**\# Every minute**  
**\* \* \* \* \* /path/to/script.sh**

**\# Every 5 minutes**  
**\*/5 \* \* \* \* /path/to/script.sh**

**\# Every hour at minute 30**  
**30 \* \* \* \* /path/to/script.sh**

**\# Daily at 2:30 AM**  
**30 2 \* \* \* /path/to/script.sh**

**\# Every Monday at 3:00 AM**  
**0 3 \* \* 1 /path/to/script.sh**

**\# First day of month at midnight**  
**0 0 1 \* \* /path/to/script.sh**

**\# Every weekday (Mon-Fri) at 9 AM**  
**0 9 \* \* 1-5 /path/to/script.sh**

**\# Multiple times: 8 AM, 12 PM, 6 PM**  
**0 8,12,18 \* \* \* /path/to/script.sh**

**PRACTICAL EXAMPLES:**  
**\# Backup database daily at 2 AM**  
**0 2 \* \* \* /usr/local/bin/backup\_database.sh \>\> /var/log/db\_backup.log 2\>&1**

**\# Clean temporary files every 6 hours**  
**0 \*/6 \* \* \* find /tmp \-type f \-mtime \+7 \-delete**

**\# Check disk space hourly**  
**0 \* \* \* \* df \-h | mail \-s "Disk Space Report" admin@example.com**

**\# System update check weekly (Sunday 3 AM)**  
**0 3 \* \* 0 /usr/bin/apt update && /usr/bin/apt list \--upgradable**

**\# Log rotation daily at midnight**  
**0 0 \* \* \* /usr/sbin/logrotate /etc/logrotate.conf**

**\# Certificate renewal check twice daily**  
**0 0,12 \* \* \* /usr/bin/certbot renew \--quiet**

**SPECIAL STRINGS:**  
**@reboot    \# Run once at startup**  
**@yearly    \# Run once a year (0 0 1 1 \*)**  
**@annually  \# Same as @yearly**  
**@monthly   \# Run once a month (0 0 1 \* \*)**  
**@weekly    \# Run once a week (0 0 \* \* 0\)**  
**@daily     \# Run once a day (0 0 \* \* \*)**  
**@hourly    \# Run once an hour (0 \* \* \* \*)**

**EXAMPLES WITH SPECIAL STRINGS:**  
**@reboot /path/to/startup\_script.sh**  
**@daily /usr/local/bin/daily\_backup.sh**  
**@hourly /usr/local/bin/check\_services.sh**

**ENVIRONMENT VARIABLES:**  
**\# Set variables in crontab**  
**SHELL=/bin/bash**  
**PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin**  
**MAILTO=admin@example.com**  
**HOME=/home/user**

**\# Then your cron jobs**  
**0 2 \* \* \* /path/to/script.sh**

**BEST PRACTICES:**  
**• Use absolute paths for commands**  
**• Redirect output to logs (\>\> /var/log/script.log 2\>&1)**  
**• Test scripts before scheduling**  
**• Set appropriate MAILTO for notifications**  
**• Don't run resource-intensive tasks too frequently**  
**• Use locking to prevent overlapping executions**  
**• Document your cron jobs**
