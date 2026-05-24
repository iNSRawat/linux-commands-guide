# Advanced Ubuntu Commands

Powerful commands for system administration and advanced workflows.

## Shell Scripting

### Variables and Input
```bash
#!/bin/bash
VAR="value"
echo $VAR
read -p "Enter name: " name
echo "Hello $name"
```

### Conditionals
```bash
if [ -f file.txt ]; then
    echo "File exists"
fi

if [ $age -gt 18 ]; then
    echo "Adult"
else
    echo "Minor"
fi
```

### Loops
```bash
for i in {1..5}; do
    echo "Number $i"
done

while read line; do
    echo "$line"
done < file.txt
```

## System Administration

### systemctl - Service Management
```bash
sudo systemctl start service
sudo systemctl stop service
sudo systemctl restart service
sudo systemctl status service
sudo systemctl enable service
sudo systemctl disable service
systemctl list-units
```

### cron - Scheduled Tasks
```bash
crontab -e
crontab -l

# Format: minute hour day month weekday command
0 * * * * /path/to/script.sh
*/5 * * * * /path/to/command
```

### rsync - Advanced File Sync
```bash
rsync -av source/ destination/
rsync -avz --progress source/ user@remote:/path/
rsync -av --exclude='*.log' source/ dest/
```

## Advanced Text Processing

### find - Advanced File Search
```bash
find . -name "*.py"
find . -type f -mtime -7
find . -size +100M
find . -name "*.log" -delete
find . -type f -exec chmod 644 {} \;
```

### xargs - Build Commands
```bash
find . -name "*.txt" | xargs grep "pattern"
ls | xargs -I {} echo "File: {}"
```

---

**Previous**: [Intermediate Commands](02-intermediate-commands.md) | **Next**: [Data Science Commands](04-data-science-commands.md)


---

## Additional Advanced Commands

### Shell Script Functions
Reusable blocks of code inside your scripts.
```bash
#!/bin/bash

# Define a function
greet() {
    echo "Hello, $1!"
}

# Call it
greet "NSRawat"
greet "World"

# Function with return value
add_numbers() {
    local result=$(( $1 + $2 ))
    echo $result
}

sum=$(add_numbers 5 10)
echo "Sum: $sum"
```

### Shell Script Error Handling
Make your scripts safe and predictable.
```bash
#!/bin/bash

# Exit immediately if any command fails
set -e

# Exit if undefined variable is used
set -u

# Print each command before running (debug mode)
set -x

# Check if a command succeeded
if ! command -v python3 &> /dev/null; then
    echo "python3 not found!"
    exit 1
fi

# Check exit code manually
cp file.txt backup.txt
if [ $? -eq 0 ]; then
    echo "Copy succeeded"
else
    echo "Copy failed"
    exit 1
fi
```

### journalctl - View System Logs
Read logs from the system and services.
```bash
journalctl                          # All logs
journalctl -n 50                    # Last 50 lines
journalctl -f                       # Follow live logs (like tail -f)
journalctl -u docker                # Logs for docker service
journalctl -u ssh                   # Logs for SSH service
journalctl --since "1 hour ago"     # Recent logs
journalctl --since "2024-01-01"     # Logs since date
journalctl -p err                   # Only errors
journalctl --disk-usage             # How much space logs use
sudo journalctl --vacuum-time=3d    # Delete logs older than 3 days
```

### awk - Advanced Text Processing
Process and transform structured text files.
```bash
# Print specific columns
awk '{print $1}' file.txt           # First column
awk '{print $1, $3}' file.txt       # Columns 1 and 3
awk -F',' '{print $2}' data.csv     # CSV 2nd column

# Filter rows
awk '$3 > 100' file.txt             # Rows where col3 > 100
awk '/python/ {print}' file.txt     # Lines containing 'python'

# Math operations
awk '{sum+=$1} END {print "Total:", sum}' file.txt
awk '{count++} END {print "Lines:", count}' file.txt

# Real-world DS use: process CSV
awk -F',' 'NR>1 {print $1, $3}' data.csv    # Skip header, print cols
awk -F',' '$2=="yes" {print $0}' data.csv   # Filter rows by value
```

### Advanced find - File Search
Powerful file searching with actions.
```bash
# Find by name
find . -name "*.py"                 # All Python files
find . -name "*.log" -type f        # Log files only
find ~ -name "*.csv"               # CSV in home directory

# Find by time
find . -mtime -7                    # Modified in last 7 days
find . -mtime +30                   # Modified more than 30 days ago
find . -newer file.txt              # Newer than file.txt

# Find by size
find . -size +100M                  # Files larger than 100MB
find . -size -1k                    # Files smaller than 1KB
find . -empty                       # Empty files/folders

# Find and take action
find . -name "*.log" -delete        # Find and delete
find . -name "*.py" -exec wc -l {} \;   # Count lines in each
find . -name "*.csv" | xargs grep "error"  # Search inside found files
```

### Process Substitution & Pipes (Advanced)
Chaining commands powerfully.
```bash
# Pipe: send output of one command to another
cat data.csv | grep "2024" | sort | uniq -c

# Multiple pipes
ps aux | grep python | awk '{print $2}'

# Redirect stderr to file
python3 script.py 2> errors.log

# Redirect both stdout and stderr
python3 script.py > output.log 2>&1

# Run in background
python3 train.py &

# Run and disown (survives terminal close)
python3 train.py & disown

# Check last exit code
echo $?
# 0 = success, non-zero = error
```

### Disk Usage & Cleanup
Find and free up disk space.
```bash
# See what's taking up space
du -sh /*                           # Top-level usage
du -sh ~/*                          # Your home folder breakdown
du -sh * | sort -h                  # Sort by size

# Clear apt cache
sudo apt autoremove                 # Remove unused packages
sudo apt clean                      # Clear downloaded package cache
sudo apt autoclean                  # Remove outdated cached packages

# Find large files
find / -type f -size +500M 2>/dev/null    # Files > 500MB
find ~ -type f -size +100M 2>/dev/null    # In home directory

# Docker cleanup (if using Docker)
docker system prune                 # Remove stopped containers/dangling images
docker system df                    # Show Docker disk usage
```
