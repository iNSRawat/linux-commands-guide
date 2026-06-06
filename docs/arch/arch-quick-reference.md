# Arch Linux Quick Reference

Quick reference guide for essential Arch Linux commands and shortcuts.

## Package Management (Pacman & AUR)

```bash
sudo pacman -Syu                 # Update official system packages
yay -Syu                         # Update official AND AUR packages (using yay)
sudo pacman -S package           # Install package from official repositories
yay -S package                   # Install package from official repos or AUR
sudo pacman -Rns package         # Remove package, config files, and unused dependencies
pacman -Ss keyword               # Search official repositories
yay -Ss keyword                  # Search repositories and AUR
pacman -Qs keyword               # Search installed packages
pacman -Qi package               # View information about installed package
sudo pacman -Rns $(pacman -Qtdq) # Remove all orphaned packages (cleanup)
sudo pacman -Scc                 # Clear package cache completely
```

## System Services (systemd)

```bash
sudo systemctl start service     # Start a service
sudo systemctl stop service      # Stop a service
sudo systemctl restart service   # Restart a service
sudo systemctl enable service    # Enable service to start on boot
sudo systemctl enable --now serv # Enable and start service immediately
sudo systemctl disable service   # Disable service from starting on boot
sudo systemctl status service    # View service status and logs
systemctl list-units --type=serv # List all running services
```

## Networking & Firewall

```bash
ip addr                          # View IP addresses and interfaces (or: ip a)
ip route                         # View routing tables
nmcli connection show            # List network connections
nmcli device wifi list           # List nearby Wi-Fi networks
nmcli device wifi connect "SSID" # Connect to Wi-Fi network
nmtui                            # Interactive network manager terminal interface
sudo ufw status verbose          # View firewall status and active rules
sudo ufw enable                  # Enable firewall (rules start on boot)
sudo ufw allow port/protocol     # Allow incoming traffic (e.g. 22/tcp)
```

## File Operations

```bash
ls -la                           # List all files (including hidden) with details
cp -r source dest                # Copy files or folders recursively
mv old new                       # Move or rename files/folders
rm -rf directory                 # Force remove directory and contents recursively
find . -name "pattern"            # Find files by name pattern
grep -ri "text" /path            # Case-insensitive recursive text search
```

## System Information

```bash
uname -a                         # Kernel and system architecture details
cat /etc/os-release              # Operating System release information
hostnamectl                      # Hostname and machine properties
free -h                          # RAM and Swap memory usage
df -h                            # Disk space usage per partition
lsblk                            # Block devices layout
```

## User Management

```bash
sudo useradd -m username         # Create new user with a home directory
sudo passwd username             # Set or update user password
sudo usermod -aG group user      # Add user to a supplementary group
sudo userdel -r username         # Delete user and delete home directory files
```

## File Permissions

```bash
chmod 755 file                   # Set rwxr-xr-x permissions
chmod 644 file                   # Set rw-r--r-- permissions
chmod +x script.sh               # Make script executable
chown user:group file            # Change owner and group of file
chown -R user:group directory/   # Change ownership of folder recursively
```

## Process Management

```bash
ps aux                           # View all active system processes
htop                             # Interactive process monitor
kill PID                         # Gracefully terminate process by ID
kill -9 PID                      # Force terminate process by ID
killall name                     # Kill all processes with matching name
```

---

**Previous**: [Post Install Guide](06-arch-post-install-guide.md)
