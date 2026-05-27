# Fedora Quick Reference

Quick reference guide for essential Fedora commands.

## Package Management (DNF)

```bash
sudo dnf update                  # Update system
sudo dnf install package         # Install package
sudo dnf remove package          # Remove package
sudo dnf search keyword          # Search packages
dnf list installed               # List installed packages
sudo dnf group install "Group"   # Install package group
```

## System Services

```bash
sudo systemctl start service     # Start service
sudo systemctl stop service      # Stop service
sudo systemctl restart service   # Restart service
sudo systemctl enable service    # Enable on boot
sudo systemctl status service    # Check status
```

## Networking

```bash
ip addr                          # Show IP addresses
nmcli device status              # Network devices
sudo firewall-cmd --list-all     # Firewall rules
sudo firewall-cmd --add-port=80/tcp --permanent
sudo firewall-cmd --reload       # Reload firewall
```

## File Operations

```bash
ls -la                           # List files
cp source dest                   # Copy
mv old new                       # Move/rename
rm file                          # Remove
find . -name "pattern"            # Find files
grep "text" file                 # Search in files
```

## System Information

```bash
uname -a                         # System info
lsb_release -a                   # Fedora version
free -h                          # Memory usage
df -h                            # Disk usage
top                              # Process monitor
```

## User Management

```bash
sudo useradd username            # Create user
sudo passwd username             # Set password
sudo usermod -aG group user      # Add to group
sudo userdel username            # Delete user
```

## File Permissions

```bash
chmod 755 file                   # Change permissions
chmod +x script.sh               # Make executable
chown user:group file            # Change ownership
```

## Process Management

```bash
ps aux                           # List processes
kill PID                         # Kill process
killall name                     # Kill by name
top                              # Process viewer
```

---

**Previous**: [System Commands Guide](05-fedora-system-commands-guide.md)
