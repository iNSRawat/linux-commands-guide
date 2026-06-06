# Arch Linux Basics

Essential commands and concepts for getting started with Arch Linux.

## System Information

### Check Arch Version and OS Details
```bash
cat /etc/os-release      # Detailed OS information
hostnamectl              # System hostname and virtualisation info
uname -a                 # Kernel info (release, version, architecture)
```

### System Resources
```bash
free -h                  # Memory usage (RAM & Swap)
df -h                    # Disk space usage
du -sh /path             # Directory size summary
lsblk                    # List block devices (drives, partitions)
lscpu                    # CPU information
```

## File System Navigation

### Basic Navigation
```bash
pwd                      # Print working directory
ls                       # List files in current directory
ls -la                   # List all files (including hidden ones) with detailed info
cd /path/to/directory    # Change directory
cd ~                     # Navigate to home directory
cd ..                    # Move to parent directory
cd -                     # Move to previous directory
```

### File Operations
```bash
mkdir directory          # Create new directory
mkdir -p path/to/dir     # Create nested directories
touch file.txt           # Create empty file or update timestamps
cp source dest           # Copy file
cp -r dir1 dir2          # Copy directory recursively
mv old new               # Move or rename file/directory
rm file                  # Remove file
rm -rf directory         # Remove directory and contents recursively (use with caution!)
```

### Viewing Files
```bash
cat file.txt             # Display file content
less file.txt            # Page through file (q to quit)
head -n 20 file          # Display first 20 lines
tail -n 20 file          # Display last 20 lines
tail -f logfile          # Follow file updates (useful for debugging logs)
```

### Searching Files
```bash
find /path -name "*.txt"  # Find files by name
find . -type f -size +10M # Files larger than 10MB
locate filename          # Quick file search (requires mlocate/plocate package)
which command            # Locate command binary path
```

## Text Processing

### Search and Filter
```bash
grep "pattern" file      # Search in file
grep -r "text" /path     # Recursive search in directory
grep -i "text" file      # Case-insensitive search
grep -v "exclude" file   # Invert match (exclude lines)
```

### Text Manipulation
```bash
sed 's/old/new/' file    # Replace first occurrence on each line
sed 's/old/new/g' file   # Replace all occurrences
awk '{print $1}' file    # Print first column
cut -d',' -f1 file.csv   # Extract CSV column (delimiter: ',')
sort file.txt            # Sort lines
uniq file.txt            # Remove duplicate lines
wc -l file               # Count lines in a file
```

## User Management

### User Information
```bash
whoami                   # Current user
id                       # User ID and group memberships
groups                   # List user groups
users                    # Logged-in users
w                        # Who is logged in and what they are doing
last                     # Login history
```

### User Operations (requires sudo/root)
```bash
sudo useradd -m username    # Create user with home directory
sudo passwd username        # Set/change password
sudo usermod -aG group user  # Add user to a group (e.g. wheel, video)
sudo userdel -r username    # Delete user and their home directory
sudo groupadd groupname     # Create group
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
chmod 755 file           # rwxr-xr-x (Owner: full, Group/Others: read/execute)
chmod 644 file           # rw-r--r-- (Owner: read/write, Group/Others: read)
chmod +x script.sh       # Add execute permission
chmod -w file            # Remove write permission
chown user:group file    # Change ownership
chown -R user:group dir/ # Recursive ownership change
```

## Process Management

### Viewing Processes
```bash
ps aux                   # List all running processes
ps -ef                   # Full format listing of processes
top                      # Interactive process viewer
htop                     # Better, interactive process viewer (optional/install first)
pgrep process_name       # Find process ID by name
```

### Managing Processes
```bash
kill PID                 # Kill process by ID
kill -9 PID              # Force kill (SIGKILL)
killall process_name     # Kill all processes by name
pkill pattern            # Kill matching processes
bg                       # Move process to background
fg                       # Bring background process to foreground
jobs                     # List background jobs
```

### Process Priority
```bash
nice -n 10 command       # Run command with lower priority
renice 10 -p PID         # Change running process's priority
```

## Networking Basics

### Network Information
```bash
ip addr                  # IP addresses and interfaces
ip a                     # Short form of ip addr
ip link                  # Network interfaces status
ip route                 # Routing table
hostname                 # System hostname
hostname -I              # Network IP addresses
```

### Network Testing
```bash
ping google.com          # Test connectivity
ping -c 4 8.8.8.8        # Send 4 packets
traceroute google.com    # Trace route to host
ss -tuln                 # Socket statistics (list listening ports)
```

### Download Files
```bash
curl -O https://url      # Download file from URL
wget https://url         # Download file from URL
curl -I https://url      # Get HTTP headers only
```

## Archive and Compression

### Creating Archives
```bash
tar -czf archive.tar.gz directory/   # Create compressed gzip archive
tar -cjf archive.tar.bz2 directory/  # Create compressed bzip2 archive
zip -r archive.zip directory/        # Create zip archive
```

### Extracting Archives
```bash
tar -xzf archive.tar.gz              # Extract gzip archive
tar -xjf archive.tar.bz2             # Extract bzip2 archive
unzip archive.zip                    # Extract zip archive
tar -tzf archive.tar.gz              # List gzip archive contents
```

## Disk Management

### Disk Usage
```bash
df -h                    # Disk space by partition
df -i                    # Inode usage
du -sh *                 # Size of each item in current directory
du -h --max-depth=1      # Directory sizes (1 level deep)
```

### Mounting
```bash
mount                    # Show mounted filesystems
sudo mount /dev/sdb1 /mnt  # Mount partition to /mnt
sudo umount /mnt         # Unmount partition
lsblk                    # List block devices
```

## Environment Variables

### Viewing Variables
```bash
echo $HOME               # Display home directory variable
env                      # List all environment variables
echo $PATH               # Display command search paths
printenv                 # Print environment
```

### Setting Variables
```bash
export VAR="value"       # Set environment variable
export PATH="$PATH:/new/path"  # Add directory to PATH
unset VAR                # Remove environment variable
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
!n                       # Run command number n from history
!string                  # Run last command starting with string
Ctrl+R                   # Interactive reverse search history
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
Ctrl+C       - Cancel/stop current command
Ctrl+Z       - Suspend current command (move to bg)
Ctrl+D       - Exit terminal or log out
Ctrl+L       - Clear screen
Ctrl+A       - Move cursor to start of line
Ctrl+E       - Move cursor to end of line
Ctrl+U       - Delete from cursor to start of line
Ctrl+K       - Delete from cursor to end of line
Ctrl+W       - Delete word before cursor
Ctrl+R       - Search command history
Tab          - Auto-complete command or filename
```

## Getting Help

### Documentation
```bash
man command              # Manual page for command
command --help           # Quick help menu
info command             # Info documentation
whatis command           # Brief description of command
apropos keyword          # Search manual page descriptions
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
alias update='sudo pacman -Syu'

# Apply changes
source ~/.bashrc
```

## System Monitoring

### Resource Monitoring
```bash
top                      # CPU and memory usage
uptime                   # System uptime and load average
```

## Tips for Beginners

1. **Use Tab Completion**: Press Tab to auto-complete commands and filenames.
2. **Read Error Messages**: Arch is verbose; errors tell you exactly what's wrong.
3. **Use `man` pages**: Most commands have detailed documentation.
4. **Start with `sudo`**: For system-wide changes (use with caution).
5. **Practice in a Safe Environment**: Test commands in a test directory first.
6. **Keep Backups**: Before modifying configuration files.
7. **Use `history`**: Learn from your previous commands.

---

**Next**: [Arch Linux Package Management](02-arch-package-management.md)
