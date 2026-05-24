# Intermediate Ubuntu Commands

Building on the basics with more powerful commands and techniques.

## Table of Contents
- [Process Management](#process-management)
- [File Permissions](#file-permissions)
- [Network Commands](#network-commands)
- [System Monitoring](#system-monitoring)
- [Text Processing](#text-processing)
- [Archiving and Compression](#archiving-and-compression)

## Process Management

### ps - Process Status
View running processes.
```bash
ps                          # Processes in current shell
ps aux                      # All processes detailed
ps aux | grep python        # Find Python processes
ps -ef                      # Full format listing
ps -u username              # User's processes
```

### top/htop - Process Monitor
Real-time process monitoring.
```bash
top                         # Basic process monitor
htop                        # Enhanced process monitor (install first)

# Top commands:
# k - kill process
# r - renice (change priority)
# M - sort by memory
# P - sort by CPU
# q - quit
```

### kill - Terminate Processes
Stop processes by PID or name.
```bash
kill 1234                   # Terminate process 1234
kill -9 1234                # Force kill
kill -15 1234               # Graceful termination (default)
killall firefox             # Kill all firefox processes
pkill -f "python script.py" # Kill by pattern
```

### bg/fg - Background/Foreground
Manage job execution.
```bash
# Start process in background
command &

# Suspend current process (Ctrl+Z), then:
bg                          # Continue in background
fg                          # Bring to foreground
jobs                        # List background jobs
fg %1                       # Bring job 1 to foreground
```

### nohup - No Hangup
Run commands immune to hangups.
```bash
nohup python script.py &    # Run in background, survives logout
nohup ./long-task.sh > output.log 2>&1 &
```

## File Permissions

### chmod - Change Mode
Modify file permissions.
```bash
chmod 755 script.sh         # rwxr-xr-x
chmod +x script.sh          # Add execute permission
chmod -w file.txt           # Remove write permission
chmod u+x,g+x script.sh     # User and group execute
chmod -R 755 directory/     # Recursive

# Permission numbers:
# 4 = read (r)
# 2 = write (w)
# 1 = execute (x)
# 755 = rwxr-xr-x (owner:full, group:rx, others:rx)
# 644 = rw-r--r-- (owner:rw, group:r, others:r)
```

### chown - Change Owner
Change file ownership.
```bash
sudo chown user file.txt              # Change owner
sudo chown user:group file.txt        # Change owner and group
sudo chown -R user:group directory/   # Recursive
sudo chown :group file.txt            # Change group only
```

### umask - Default Permissions
Set default file creation permissions.
```bash
umask                       # Show current umask
umask 022                   # Set umask (default: 755 for dirs, 644 for files)
umask 002                   # More permissive
```

## Network Commands

### ping - Test Connectivity
Test network connectivity.
```bash
ping google.com             # Continuous ping
ping -c 4 google.com        # Ping 4 times
ping -i 2 google.com        # 2 second interval
```

### curl - Transfer Data
Transfer data from/to servers.
```bash
curl https://api.github.com                    # GET request
curl -o output.html https://example.com        # Save to file
curl -I https://example.com                    # Headers only
curl -X POST -d "data=value" https://api.com   # POST request
curl -H "Authorization: token" https://api.com # Custom headers
```

### wget - Download Files
Download files from the web.
```bash
wget https://example.com/file.zip              # Download file
wget -O custom-name.zip https://example.com/f  # Custom filename
wget -c https://example.com/large-file.iso     # Continue interrupted download
wget -r https://example.com                    # Recursive download
```

### ip - Network Configuration
Modern network configuration tool.
```bash
ip a                        # Show IP addresses
ip addr show                # Detailed IP info
ip link show                # Show network interfaces
ip route                    # Show routing table
ip route get 8.8.8.8        # Check route to specific IP
```

### netstat/ss - Network Statistics
Display network connections.
```bash
netstat -tuln               # All listening ports
netstat -tupn               # All active connections
netstat -r                  # Routing table

ss -tuln                    # Modern alternative (faster)
ss -tp                      # Show processes using sockets
```

## System Monitoring

### df - Disk Free
Check disk space usage.
```bash
df -h                       # Human-readable
df -h /home                 # Specific partition
df -i                       # Inode usage
df -T                       # Show filesystem type
```

### du - Disk Usage
Estimate file/directory space.
```bash
du -sh directory/           # Summary
du -h --max-depth=1         # One level deep
du -ah directory/           # All files
du -h | sort -h             # Sort by size
```

### free - Memory Usage
Display memory information.
```bash
free -h                     # Human-readable
free -m                     # In megabytes
free -s 2                   # Update every 2 seconds
```

### uptime - System Uptime
Show how long system has been running.
```bash
uptime                      # System uptime and load
uptime -p                   # Pretty format
```

### dmesg - Kernel Messages
Display kernel ring buffer messages.
```bash
dmesg                       # All kernel messages
dmesg | tail                # Recent messages
dmesg | grep -i error       # Search for errors
dmesg -T                    # Human-readable timestamps
```

## Text Processing

### grep - Search Text
Search for patterns in files.
```bash
grep "pattern" file.txt                # Search in file
grep -i "pattern" file.txt             # Case-insensitive
grep -r "pattern" directory/           # Recursive search
grep -v "pattern" file.txt             # Invert match (exclude)
grep -n "pattern" file.txt             # Show line numbers
grep -c "pattern" file.txt             # Count matches
grep -A 3 "pattern" file.txt           # 3 lines after match
grep -B 3 "pattern" file.txt           # 3 lines before match
```

### sed - Stream Editor
Text transformation and substitution.
```bash
sed 's/old/new/' file.txt              # Replace first occurrence
sed 's/old/new/g' file.txt             # Replace all occurrences
sed -i 's/old/new/g' file.txt          # In-place edit
sed '1d' file.txt                      # Delete first line
sed -n '1,5p' file.txt                 # Print lines 1-5
```

### awk - Text Processing
Powerful text processing language.
```bash
awk '{print $1}' file.txt              # Print first column
awk '{print $1, $3}' file.txt          # Print columns 1 and 3
awk -F',' '{print $1}' file.csv        # Custom delimiter (CSV)
awk '$3 > 100' file.txt                # Filter rows
awk '{sum+=$1} END {print sum}' file   # Sum first column
```

### sort - Sort Lines
Sort text files.
```bash
sort file.txt                          # Alphabetical sort
sort -r file.txt                       # Reverse sort
sort -n file.txt                       # Numeric sort
sort -u file.txt                       # Remove duplicates
sort -t',' -k2 file.csv                # Sort by 2nd column (CSV)
```

### uniq - Remove Duplicates
Filter duplicate lines.
```bash
uniq file.txt                          # Remove adjacent duplicates
sort file.txt | uniq                   # Remove all duplicates
uniq -c file.txt                       # Count occurrences
uniq -d file.txt                       # Show only duplicates
```

## Archiving and Compression

### tar - Archive Files
Create and extract archives.
```bash
# Create archives
tar -czf archive.tar.gz directory/     # Create gzip compressed
tar -cjf archive.tar.bz2 directory/    # Create bzip2 compressed
tar -cf archive.tar directory/         # Create uncompressed

# Extract archives
tar -xzf archive.tar.gz                # Extract gzip
tar -xjf archive.tar.bz2               # Extract bzip2
tar -xf archive.tar                    # Extract uncompressed

# List contents
tar -tzf archive.tar.gz                # List contents

# Options:
# c - create
# x - extract
# z - gzip
# j - bzip2
# f - file
# v - verbose
```

### zip/unzip - ZIP Archives
Work with ZIP files.
```bash
zip archive.zip file1 file2            # Create ZIP
zip -r archive.zip directory/          # Recursive ZIP
unzip archive.zip                      # Extract ZIP
unzip -l archive.zip                   # List contents
unzip archive.zip -d destination/      # Extract to directory
```

## Practice Exercises

1. **Process Management**:
   ```bash
   # Find and kill a process
   ps aux | grep firefox
   kill <PID>
   ```

2. **File Permissions**:
   ```bash
   # Create a script and make it executable
   echo '#!/bin/bash\necho "Hello"' > test.sh
   chmod +x test.sh
   ./test.sh
   ```

3. **Text Processing**:
   ```bash
   # Find all .py files and count lines
   find . -name "*.py" | xargs wc -l | sort -n
   ```

4. **System Monitoring**:
   ```bash
   # Watch disk space in real-time
   watch -n 5 df -h
   ```

---

**Previous**: [Beginner Commands](01-beginner-commands.md) | **Next**: [Advanced Commands](03-advanced-commands.md)


---

## Additional Intermediate Commands

### alias - Create Command Shortcuts
Create short names for long commands. Add to `~/.bashrc` to make permanent.
```bash
# Temporary alias (current session only)
alias ll='ls -lah'
alias ..='cd ..'
alias update='sudo apt update && sudo apt upgrade'
alias py='python3'
alias activate='source venv/bin/activate'
alias gs='git status'
alias gc='git commit -m'
alias gp='git push'

# View all aliases
alias

# Remove an alias
unalias ll

# Make permanent: add to ~/.bashrc
nano ~/.bashrc
# Add your alias lines at the bottom, then:
source ~/.bashrc   # Reload without restarting terminal
```

### export - Environment Variables
Set and use environment variables.
```bash
# Set a variable
export MY_VAR="hello"

# Use it
echo $MY_VAR

# Add to PATH (make a folder's programs available everywhere)
export PATH=$PATH:/new/path

# Common useful variables
echo $HOME          # Your home directory
echo $USER          # Your username
echo $PATH          # All directories Ubuntu looks for commands
echo $SHELL         # Current shell

# List all environment variables
env
printenv
printenv PATH

# Make permanent: add to ~/.bashrc
export MY_VAR="hello"    # Add this line to ~/.bashrc
```

### ssh - Secure Shell (Remote Login)
Connect to remote servers securely.
```bash
# Connect to a server
ssh username@server-ip
ssh username@192.168.1.100
ssh username@hostname.com

# Connect on a specific port
ssh -p 2222 username@server-ip

# Connect using a key file
ssh -i ~/.ssh/my_key.pem username@server-ip

# Copy SSH key to server (for passwordless login)
ssh-copy-id username@server-ip

# Exit SSH session
exit
```

### scp - Secure Copy (Transfer Files)
Copy files between your machine and a remote server.
```bash
# Copy file TO remote server
scp file.txt username@server:/path/to/destination/

# Copy file FROM remote server
scp username@server:/path/to/file.txt ./local-folder/

# Copy entire folder
scp -r myfolder/ username@server:/path/to/destination/

# Copy with specific port
scp -P 2222 file.txt username@server:/path/
```

### watch - Run Command Repeatedly
Run a command every N seconds and display output.
```bash
watch df -h                     # Watch disk space every 2 sec
watch -n 5 df -h                # Every 5 seconds
watch -n 1 nvidia-smi           # Watch GPU every 1 second
watch -n 2 free -h              # Watch memory every 2 sec
watch -d df -h                  # Highlight changes
# Press Ctrl+C to stop
```

### locate - Find Files Quickly
Fast file search using a pre-built database.
```bash
# Update the database first (run once)
sudo updatedb

# Find a file
locate filename.txt
locate '*.py'                   # Find all Python files
locate -i readme                # Case-insensitive
locate -c filename              # Count results only

# Note: locate is faster than find but may not show very new files
# For new files always use: find
```

### tee - Write to File AND Screen at Same Time
See output on screen and save it to a file simultaneously.
```bash
ls -la | tee filelist.txt              # Show AND save
python3 train.py | tee training.log    # See AND log ML training
command | tee -a logfile.txt           # Append (not overwrite)
```

### screen / tmux - Keep Sessions Running
Run long tasks that keep going even if you close the terminal.
```bash
# Install
sudo apt install screen tmux

# --- screen ---
screen                          # Start new session
screen -S mysession             # Start named session
Ctrl+A then D                   # Detach (leave running)
screen -ls                      # List sessions
screen -r mysession             # Re-attach to session
screen -r                       # Re-attach (if only one)

# --- tmux (more modern) ---
tmux                            # Start new session
tmux new -s mysession           # Named session
Ctrl+B then D                   # Detach
tmux ls                         # List sessions
tmux attach -t mysession        # Re-attach
# Split screen: Ctrl+B then " (horizontal) or % (vertical)
# Switch panes: Ctrl+B then arrow keys
```

### lsof - List Open Files / Port Usage
See which process is using a file or port.
```bash
lsof -i :8501                   # Who is using port 8501 (Streamlit)
lsof -i :8888                   # Who is using port 8888 (Jupyter)
lsof -i :80                     # Who is using port 80
lsof -u username                # All files opened by user
lsof | grep python              # Files opened by Python

# Kill process using a port
kill -9 $(lsof -t -i:8501)
```
