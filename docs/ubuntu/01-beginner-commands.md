# Beginner Ubuntu Commands

Essential commands for anyone starting with Ubuntu or Linux.

## Table of Contents
- [Navigation Commands](#navigation-commands)
- [File and Directory Operations](#file-and-directory-operations)
- [File Viewing and Editing](#file-viewing-and-editing)
- [System Information](#system-information)
- [Package Management](#package-management)
- [Help and Documentation](#help-and-documentation)

## Navigation Commands

### pwd - Print Working Directory
Shows your current location in the file system.
```bash
pwd
# Output: /home/username/Documents
```

### ls - List Directory Contents
Displays files and folders in the current directory.
```bash
ls               # Basic listing
ls -l            # Detailed listing
ls -la           # Include hidden files
ls -lh           # Human-readable file sizes
ls -lt           # Sort by modification time
ls -ltr          # Reverse time sort (oldest first)
```

### cd - Change Directory
Navigate between directories.
```bash
cd Documents     # Go to Documents folder
cd ..            # Go up one level
cd ~             # Go to home directory
cd /             # Go to root directory
cd -             # Go to previous directory
```

## File and Directory Operations

### mkdir - Make Directory
Create new directories.
```bash
mkdir project                  # Create single directory
mkdir -p project/src/main      # Create nested directories
mkdir dir1 dir2 dir3           # Create multiple directories
```

### touch - Create Empty File
Create new files or update timestamps.
```bash
touch file.txt                 # Create new file
touch file1.txt file2.txt      # Create multiple files
```

### cp - Copy Files/Directories
Copy files and directories.
```bash
cp file.txt backup.txt         # Copy file
cp file.txt /path/to/dest/     # Copy to different directory
cp -r folder backup_folder     # Copy directory recursively
cp -i file.txt dest.txt        # Interactive (ask before overwrite)
```

### mv - Move/Rename Files
Move or rename files and directories.
```bash
mv oldname.txt newname.txt     # Rename file
mv file.txt /path/to/dest/     # Move file
mv -i file.txt dest/           # Interactive mode
mv *.txt documents/            # Move all .txt files
```

### rm - Remove Files/Directories
Delete files and directories.
```bash
rm file.txt                    # Delete file
rm -i file.txt                 # Interactive deletion
rm -r folder                   # Delete directory recursively
rm -rf folder                  # Force delete (use with caution!)
rm *.txt                       # Delete all .txt files
```

**⚠️ Warning**: `rm -rf` is dangerous and cannot be undone!

## File Viewing and Editing

### cat - Display File Contents
View entire file contents.
```bash
cat file.txt                   # Display file
cat file1.txt file2.txt        # Display multiple files
cat > newfile.txt              # Create file and type content (Ctrl+D to save)
```

### less - View File Page by Page
Better for large files.
```bash
less largefile.txt
# Navigation:
#   Space - Next page
#   b - Previous page
#   / - Search
#   q - Quit
```

### head/tail - View File Start/End
View beginning or end of files.
```bash
head file.txt                  # First 10 lines
head -n 20 file.txt            # First 20 lines
tail file.txt                  # Last 10 lines
tail -n 20 file.txt            # Last 20 lines
tail -f log.txt                # Follow file updates (useful for logs)
```

### nano - Simple Text Editor
User-friendly terminal text editor.
```bash
nano file.txt
# Common commands:
#   Ctrl+O - Save
#   Ctrl+X - Exit
#   Ctrl+K - Cut line
#   Ctrl+U - Paste
#   Ctrl+W - Search
```

### grep - Search Text in Files
Search for patterns inside files or command output.
```bash
grep "word" file.txt             # Search for word in file
grep -i "word" file.txt          # Case-insensitive search
grep -r "word" /path/            # Search recursively in directory
grep -n "word" file.txt          # Show line numbers
grep -l "word" *.txt             # List filenames with match
grep -v "word" file.txt          # Show lines that do NOT match
grep "error" logfile | less      # Pipe grep output to less
```

### find - Find Files and Directories
Search for files/directories by name, size, type, or date.
```bash
find . -name "file.txt"          # Find by exact name
find . -name "*.py"              # Find all Python files
find /home -type d               # Find only directories
find /home -type f               # Find only files
find . -size +100M               # Find files larger than 100MB
find . -mtime -7                 # Files modified in last 7 days
find . -name "*.log" -delete     # Find and delete log files
```

### chmod - Change File Permissions
Set who can read, write, or execute a file.
```bash
chmod 755 script.sh              # rwxr-xr-x (owner full, others read+exec)
chmod 644 file.txt               # rw-r--r-- (owner read+write, others read)
chmod +x script.sh               # Add execute permission
chmod -x script.sh               # Remove execute permission
chmod -R 755 folder/             # Recursively change permissions
```

**Permission numbers:** 4=read, 2=write, 1=execute (add together for each group)

### chown - Change File Owner
Change who owns a file or directory.
```bash
chown user file.txt              # Change owner
chown user:group file.txt        # Change owner and group
chown -R user:group folder/      # Recursively change ownership
sudo chown root file.txt         # Give ownership to root
```

## System Information

### whoami - Current User
Displays your username.
```bash
whoami
# Output: username
```

### hostname - System Name
Shows your system's hostname.
```bash
hostname
# Output: your-computer-name
```

### uname - System Information
Display system information.
```bash
uname -a                         # All system information
uname -r                         # Kernel release
uname -m                         # Machine hardware
```

### df - Disk Space
Show disk space usage.
```bash
df                               # Basic disk usage
df -h                            # Human-readable format
df -h /home                      # Specific directory
```

### du - Directory Size
Estimate file/directory space usage.
```bash
du -h file.txt                   # File size
du -sh folder                    # Directory size summary
du -h --max-depth=1              # Size of subdirectories
```

### free - Memory Usage
Display memory information.
```bash
free                             # Basic memory info
free -h                          # Human-readable format
```

## Package Management

### apt update - Update Package List
Refresh available package information.
```bash
sudo apt update
```

### apt upgrade - Upgrade Packages
Upgrade installed packages.
```bash
sudo apt upgrade                 # Upgrade all packages
sudo apt upgrade package-name    # Upgrade specific package
```

### apt install - Install Packages
Install new software.
```bash
sudo apt install package-name
sudo apt install vim git python3
```

### apt remove - Uninstall Packages
Remove installed packages.
```bash
sudo apt remove package-name
sudo apt autoremove              # Remove unused dependencies
```

### apt search - Search Packages
Search for packages.
```bash
apt search keyword
apt search python
```

### Update all installed packages
Update package list, upgrade installed packages, and remove unused dependencies:
```bash
sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y
```

Check whether anything is still pending:
```bash
apt list --upgradable
```

If no packages are listed, your Ubuntu system is up to date.

## Help and Documentation

### man - Manual Pages
View command documentation.
```bash
man ls                           # View ls manual
man man                          # Learn about man itself
```

### --help Flag
Quick help for commands.
```bash
ls --help
cp --help
```

### which - Locate Commands
Find where a command is located.
```bash
which python3
which git
```

## Useful Tips for Beginners

1. **Tab Completion**: Press Tab to auto-complete file/directory names
2. **Command History**: Use ↑ and ↓ arrow keys to navigate previous commands
3. **Ctrl+C**: Stop a running command
4. **Ctrl+L**: Clear the terminal screen (or type `clear`)
5. **Ctrl+R**: Search command history
6. **&&**: Chain commands (run second only if first succeeds)
```bash
sudo apt update && sudo apt upgrade
```

## Common Pitfalls to Avoid

1. Don't use `sudo rm -rf /` (deletes everything!)
2. Always double-check before using `rm -rf`
3. Use `rm -i` for interactive confirmation
4. Be careful with wildcards (`*`) in delete commands
5. Always backup important files before major operations

## Practice Exercises

1. Create a project structure:
```bash
mkdir -p myproject/{src,docs,tests}
touch myproject/README.md
ls -R myproject
```

2. Create and view a file:
```bash
echo "Hello Ubuntu!" > greeting.txt
cat greeting.txt
```

3. Find disk usage:
```bash
df -h
du -sh ~/*
```

---

**Next**: [Intermediate Commands](02-intermediate-commands.md)

---

## Essential Commands Missing for Beginners

### echo - Print Text / Write to Files
Print text to terminal or write content to a file.
```bash
echo "Hello World"               # Print text
echo $HOME                       # Print variable
echo "text" > file.txt           # Write to file (overwrite)
echo "text" >> file.txt          # Append to file
echo -e "Line1\nLine2"          # Print with newlines
```

### clear - Clear Terminal Screen
```bash
clear                            # Clear screen
# Or use keyboard shortcut: Ctrl+L
```

### history - Command History
View and reuse previously typed commands.
```bash
history                          # Show all history
history 20                       # Show last 20 commands
!!                               # Repeat last command
!50                              # Run command number 50
history | grep docker            # Search history
Ctrl+R                           # Interactive reverse search
```

### sudo - Run as Superuser
Run commands with administrator (root) privileges.
```bash
sudo command                     # Run command as root
sudo apt install vim             # Install software
sudo -i                          # Switch to root shell
sudo !!                          # Re-run last command as sudo
whoami                           # Check current user
sudo whoami                      # Should print: root
```

> ⚠️ Always be careful with sudo — it has full system access!

### ln - Create Links (Shortcuts)
Create shortcuts (symlinks) to files or folders.
```bash
ln -s /path/to/original /path/to/link      # Symbolic link
ln -s ~/projects/myapp ~/Desktop/myapp     # Shortcut on Desktop
ls -la                                     # See symlinks (shown with ->)
rm linkname                                # Remove symlink only
```

### file - Check File Type
Find out what type a file is (text, binary, image, etc.).
```bash
file document.pdf                # Check file type
file script.sh                   # Check shell script
file image.png                   # Check image
file *                           # Check all files in folder
```

### Running Shell Scripts
How to create and run your own scripts.
```bash
# Step 1: Create script
nano myscript.sh

# Step 2: Add content (inside nano)
#!/bin/bash
echo "Hello from my script!"

# Step 3: Make it executable
chmod +x myscript.sh

# Step 4: Run it
./myscript.sh
```

### WSL-Specific Commands (Windows Subsystem for Linux)
Commands useful when running Ubuntu inside WSL on Windows.
```bash
# From Windows PowerShell/CMD:
wsl                              # Open default WSL distro
wsl --list --verbose             # List installed distros
wsl --shutdown                   # Shutdown all WSL instances
wsl --set-default-version 2      # Set WSL 2 as default

# From inside WSL Ubuntu:
explorer.exe .                   # Open current folder in Windows Explorer
notepad.exe file.txt             # Open file in Windows Notepad
cd /mnt/c/Users/YourName         # Access Windows C: drive
cd ~                             # Go to WSL home directory
pwd                              # Shows /home/yourusername

# Access WSL files from Windows:
# Open File Explorer and type: \\wsl$
```

### Keyboard Shortcuts (Extended)

| Shortcut | What it does |
|----------|---------------|
| `Ctrl+C` | Stop/kill running command |
| `Ctrl+Z` | Pause/suspend command |
| `Ctrl+D` | Exit terminal / logout |
| `Ctrl+L` | Clear screen |
| `Ctrl+R` | Search command history |
| `Ctrl+A` | Jump to start of line |
| `Ctrl+E` | Jump to end of line |
| `Ctrl+U` | Delete entire line |
| `Ctrl+K` | Delete from cursor to end |
| `Ctrl+W` | Delete previous word |
| `Tab` | Auto-complete file/command name |
| `Tab Tab` | Show all possible completions |
| `↑ / ↓` | Navigate command history |
