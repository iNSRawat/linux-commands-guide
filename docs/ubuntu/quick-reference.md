# Ubuntu Commands Quick Reference

One-page cheat sheet for Ubuntu/WSL commands.

## 📁 File & Directory Operations

```bash
ls -lah              # List all files with details
cd ~/path            # Change directory
pwd                  # Print working directory
mkdir -p dir/subdir  # Create nested directories
rm -rf dir/          # Remove directory recursively
cp -r source dest    # Copy directory
mv old new           # Move/rename
find . -name "*.py"   # Find files by name
du -sh *             # Disk usage summary
```

## 📦 Package Management (APT)

```bash
sudo apt update                    # Update package list
sudo apt upgrade                   # Upgrade packages
sudo apt install <package>         # Install package
sudo apt remove <package>          # Remove package
sudo apt autoremove                # Remove unused dependencies
sudo apt search <keyword>          # Search packages
apt list --installed               # List installed packages
```

## 🔍 System Information

```bash
uname -a             # System information
lsb_release -a       # Ubuntu version
df -h                # Disk space
free -h              # Memory usage
top                  # Process monitor (press q to quit)
htop                 # Better process viewer
ps aux               # List all processes
which <command>      # Locate command
```

## 👤 User & Permissions

```bash
sudo <command>           # Run as superuser
sudo su                  # Switch to root user
chmod 755 file           # Change file permissions
chown user:group file    # Change file ownership
passwd                   # Change password
whoami                   # Current user
groups                   # User groups
```

## 📝 Text Processing

```bash
cat file.txt             # Display file
less file.txt            # Page through file
head -n 10 file          # First 10 lines
tail -f logfile          # Follow file updates
grep "pattern" file      # Search in file
grep -r "text" dir/      # Recursive search
sed 's/old/new/g' file   # Find and replace
awk '{print $1}' file    # Column extraction
```

## 🌐 Networking

```bash
ping google.com          # Test connectivity
curl https://api.com     # HTTP request
wget https://file.com    # Download file
ip addr                  # IP addresses
netstat -tuln            # Open ports
ssh user@host            # Remote login
scp file user@host:/path # Secure copy
```

## 🐍 Python & Data Science

```bash
python3 --version        # Check Python version
pip install package      # Install Python package
pip list                 # List installed packages
python3 -m venv venv     # Create virtual environment
source venv/bin/activate # Activate venv
deactivate               # Deactivate venv
jupyter notebook         # Start Jupyter
streamlit run app.py     # Run Streamlit app
```

## 🐙 Git Commands

```bash
git init                 # Initialize repo
git clone <url>          # Clone repository
git status               # Check status
git add .                # Stage all changes
git commit -m "message"  # Commit changes
git push origin main     # Push to remote
git pull                 # Pull updates
git branch               # List branches
git checkout -b new      # Create new branch
git log --oneline        # Commit history
```

## 🐳 Docker Quick Commands

```bash
docker ps                    # Running containers
docker images                # List images
docker run -it ubuntu bash   # Run container
docker exec -it <id> bash    # Enter container
docker stop <id>             # Stop container
docker rm <id>               # Remove container
docker build -t name .       # Build image
docker compose up -d         # Start services
docker system prune          # Clean up
```

## ⚙️ Service Management (systemd)

```bash
sudo systemctl start service     # Start service
sudo systemctl stop service      # Stop service
sudo systemctl restart service   # Restart service
sudo systemctl status service    # Check status
sudo systemctl enable service    # Auto-start on boot
sudo systemctl disable service   # Disable auto-start
```

## 🔄 Process Management

```bash
kill <PID>               # Kill process by ID
killall process_name     # Kill by name
ps aux | grep python     # Find Python processes
jobs                     # List background jobs
bg                       # Move job to background
fg                       # Bring job to foreground
Ctrl+C                   # Stop current process
Ctrl+Z                   # Suspend process
```

## 🗜️ Archive & Compression

```bash
tar -czf archive.tar.gz dir/     # Create compressed archive
tar -xzf archive.tar.gz          # Extract archive
zip -r archive.zip dir/          # Create zip
unzip archive.zip                # Extract zip
gzip file                        # Compress file
gunzip file.gz                   # Decompress
```

## 🔧 WSL-Specific Commands

```bash
wsl --list --verbose             # List WSL distributions
wsl --shutdown                   # Shutdown all WSL instances
wsl --set-default Ubuntu         # Set default distro
wsl --export Ubuntu backup.tar   # Export distro
wsl --import Ubuntu path backup.tar  # Import distro
cd /mnt/c/Users/                 # Access Windows files
explorer.exe .                   # Open folder in Windows Explorer
```

## 📊 Disk & File System

```bash
df -h                    # Disk space
du -sh *                 # Directory sizes
ncdu                     # Interactive disk usage
lsblk                    # List block devices
mount                    # Show mounted filesystems
fdisk -l                 # List disks (requires sudo)
```

## 🔐 SSH & Keys

```bash
ssh-keygen -t ed25519 -C "email"  # Generate SSH key
cat ~/.ssh/id_ed25519.pub          # Display public key
ssh-copy-id user@host              # Copy key to server
ssh-add ~/.ssh/key                 # Add key to agent
ssh-agent bash                     # Start SSH agent
```

## 📋 Aliases & Functions

```bash
alias ll='ls -lah'       # Create alias
alias gst='git status'   # Git shortcut
unalias ll               # Remove alias
type <command>           # Check if alias/function
alias                    # List all aliases
```

## 🛠️ Environment Variables

```bash
echo $PATH               # Display PATH
export VAR="value"       # Set variable
export PATH="$PATH:/new" # Add to PATH
env                      # List all variables
unset VAR                # Remove variable
source ~/.bashrc         # Reload bash config
```

## 💡 Tips & Tricks

```bash
history                  # Command history
!!                       # Repeat last command
!$                       # Last argument of previous command
Ctrl+R                   # Reverse search history
Ctrl+L                   # Clear screen
Ctrl+A                   # Move to start of line
Ctrl+E                   # Move to end of line
Ctrl+U                   # Delete line before cursor
Ctrl+K                   # Delete line after cursor
man <command>            # Manual/help for command
<command> --help         # Quick help
whatis <command>         # Brief description
```

## 🚀 Productivity Shortcuts

```bash
tree                     # Directory tree view
watch -n 2 command       # Run command every 2 seconds
time command             # Measure execution time
yes | command            # Auto-confirm prompts
command &                # Run in background
nohup command &          # Run after logout
screen                   # Terminal multiplexer
tmux                     # Better multiplexer
```

---

**📚 Related Documentation:**
- [Beginner Commands](01-beginner-commands.md)
- [Intermediate Commands](02-intermediate-commands.md)
- [Advanced Commands](03-advanced-commands.md)
- [Data Science Commands](04-data-science-commands.md)
- [Git & GitHub](05-git-github-commands.md)
- [Docker Commands](06-docker-commands.md)
