# Fedora Linux Basics

Essential commands and concepts for getting started with Fedora Linux.

## System Information

### Check Fedora Version
```bash
fedora-release           # Show Fedora version
cat /etc/fedora-release  # Detailed version info
hostnamectl              # System information
uname -a                 # Kernel info
```

### System Resources
```bash
free -h                  # Memory usage
df -h                    # Disk space
du -sh /path             # Directory size
lsblk                    # List block devices
lscpu                    # CPU information
```

## File System Navigation

### Basic Navigation
```bash
pwd                      # Print working directory
ls                       # List files
ls -la                   # List all with details
cd /path/to/directory    # Change directory
cd ~                     # Home directory
cd ..                    # Parent directory
cd -                     # Previous directory
```

### File Operations
```bash
mkdir directory          # Create directory
mkdir -p path/to/dir     # Create nested directories
touch file.txt           # Create empty file
cp source dest           # Copy file
cp -r dir1 dir2          # Copy directory
mv old new               # Move/rename
rm file                  # Remove file
rm -rf directory         # Remove directory recursively
```

### Viewing Files
```bash
cat file.txt             # Display file content
less file.txt            # Page through file
head -n 20 file          # First 20 lines
tail -n 20 file          # Last 20 lines
tail -f logfile          # Follow file updates
```

### Searching Files
```bash
find /path -name "*.txt"  # Find files by name
find . -type f -size +10M # Files larger than 10MB
locate filename          # Quick file search (requires updatedb)
which command            # Locate command path
```

## Text Processing

### Search and Filter
```bash
grep "pattern" file      # Search in file
grep -r "text" /path     # Recursive search
grep -i "text" file      # Case-insensitive
grep -v "exclude" file   # Invert match
```

### Text Manipulation
```bash
sed 's/old/new/' file    # Replace first occurrence
sed 's/old/new/g' file   # Replace all occurrences
awk '{print $1}' file    # Print first column
cut -d',' -f1 file.csv   # Extract CSV column
sort file.txt            # Sort lines
uniq file.txt            # Remove duplicates
wc -l file               # Count lines
```

## User Management

### User Information
```bash
whoami                   # Current user
id                       # User ID and groups
groups                   # List user groups
users                    # Logged in users
w                        # Who is logged in
last                     # Login history
```

### User Operations (requires sudo)
```bash
sudo useradd username    # Create user
sudo passwd username     # Set password
sudo usermod -aG group user  # Add user to group
sudo userdel username    # Delete user
sudo groupadd groupname  # Create group
```

## File Permissions

### Understanding Permissions
```
Format: rwxrwxrwx
        ||||||||
        ||||+++- Others (read, write, execute)
        |+++---- Group
        +------- Owner

Numbers:
4 = read (r)
2 = write (w)
1 = execute (x)
```

### Changing Permissions
```bash
chmod 755 file           # rwxr-xr-x
chmod 644 file           # rw-r--r--
chmod +x script.sh       # Add execute permission
chmod -w file            # Remove write permission
chown user:group file    # Change ownership
chown -R user:group dir/ # Recursive ownership change
```

## Process Management

### Viewing Processes
```bash
ps aux                   # List all processes
ps -ef                   # Full format listing
top                      # Interactive process viewer
htop                     # Better process viewer (install first)
pgrep process_name       # Find process by name
```

### Managing Processes
```bash
kill PID                 # Kill process by ID
kill -9 PID              # Force kill
killall process_name     # Kill by name
pkill pattern            # Kill matching processes
bg                       # Move to background
fg                       # Bring to foreground
jobs                     # List background jobs
```

### Process Priority
```bash
nice -n 10 command       # Run with priority
renice 10 -p PID         # Change priority
```

## Networking Basics

### Network Information
```bash
ip addr                  # IP addresses
ip a                     # Short form
ip link                  # Network interfaces
ip route                 # Routing table
hostname                 # System hostname
hostname -I              # IP addresses
```

### Network Testing
```bash
ping google.com          # Test connectivity
ping -c 4 8.8.8.8        # Send 4 packets
traceroute google.com    # Trace route
netstat -tuln            # Open ports
ss -tuln                 # Socket statistics (modern)
```

### Download Files
```bash
curl -O https://url      # Download file
wget https://url         # Download file
curl -I https://url      # Get headers only
```

## Archive and Compression

### Creating Archives
```bash
tar -czf archive.tar.gz directory/   # Create compressed archive
tar -cjf archive.tar.bz2 directory/  # Bzip2 compression
zip -r archive.zip directory/        # Create zip
```

### Extracting Archives
```bash
tar -xzf archive.tar.gz              # Extract gzip archive
tar -xjf archive.tar.bz2             # Extract bzip2
unzip archive.zip                    # Extract zip
tar -tzf archive.tar.gz              # List contents without extracting
```

## Disk Management

### Disk Usage
```bash
df -h                    # Disk space by partition
df -i                    # Inode usage
du -sh *                 # Size of each item
du -h --max-depth=1      # Directory sizes (1 level)
ncdu                     # Interactive disk usage (install first)
```

### Mounting
```bash
mount                    # Show mounted filesystems
sudo mount /dev/sdb1 /mnt  # Mount partition
sudo umount /mnt         # Unmount
lsblk                    # List block devices
```

## Environment Variables

### Viewing Variables
```bash
echo $HOME               # Display variable
env                      # List all variables
echo $PATH               # Display PATH
printenv                 # Print environment
```

### Setting Variables
```bash
export VAR="value"       # Set variable
export PATH="$PATH:/new/path"  # Add to PATH
unset VAR                # Remove variable
```

### Persistent Variables
```bash
# Add to ~/.bashrc or ~/.bash_profile
export EDITOR=nano
export PATH="$HOME/bin:$PATH"

# Reload configuration
source ~/.bashrc
```

## Command History

### History Commands
```bash
history                  # Show command history
history 20               # Last 20 commands
!!                       # Repeat last command
!n                       # Run command number n
!string                  # Run last command starting with string
Ctrl+R                   # Reverse search history
```

### History Settings
```bash
# In ~/.bashrc
export HISTSIZE=10000
export HISTFILESIZE=20000
export HISTTIMEFORMAT="%F %T "
```

## Keyboard Shortcuts

### Terminal Shortcuts
```
Ctrl+C       - Cancel current command
Ctrl+Z       - Suspend current command
Ctrl+D       - Exit terminal/end input
Ctrl+L       - Clear screen
Ctrl+A       - Move to start of line
Ctrl+E       - Move to end of line
Ctrl+U       - Delete from cursor to start
Ctrl+K       - Delete from cursor to end
Ctrl+W       - Delete word before cursor
Ctrl+R       - Search command history
Tab          - Auto-complete
```

## Getting Help

### Documentation
```bash
man command              # Manual page
command --help           # Quick help
info command             # Info documentation
whatis command           # Brief description
apropos keyword          # Search manual descriptions
```

## Shell Configuration

### Configuration Files
```bash
~/.bashrc                # Bash configuration
~/.bash_profile          # Login shell config
~/.bash_aliases          # Alias definitions
```

### Creating Aliases
```bash
# Add to ~/.bashrc
alias ll='ls -lah'
alias gs='git status'
alias update='sudo dnf update'

# Apply changes
source ~/.bashrc
```

## System Monitoring

### Resource Monitoring
```bash
top                      # CPU and memory usage
htop                     # Interactive monitor
iotop                    # I/O usage (requires sudo)
vmstat 2                 # System stats every 2 seconds
uptime                   # System uptime and load
```

## Tips for Beginners

1. **Use Tab Completion**: Press Tab to auto-complete commands and filenames
2. **Read Error Messages**: They usually tell you what went wrong
3. **Use `man` pages**: Most commands have detailed documentation
4. **Start with `sudo`**: For system-wide changes (be careful!)
5. **Practice in Safe Environment**: Test commands in a test directory first
6. **Keep Backups**: Before modifying important files
7. **Use `history`**: Learn from your previous commands

---

**Next**: [Fedora Package Management](02-fedora-package-management.md)
