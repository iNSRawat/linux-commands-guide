# Fedora System Services (systemd)

Manage system services using systemd on Fedora.

## Service Management

### Basic Commands
```bash
sudo systemctl start service     # Start service
sudo systemctl stop service      # Stop service
sudo systemctl restart service   # Restart service
sudo systemctl reload service    # Reload configuration
sudo systemctl status service    # Check status
```

### Enable/Disable Services
```bash
sudo systemctl enable service    # Auto-start on boot
sudo systemctl disable service   # Disable auto-start
sudo systemctl is-enabled service # Check if enabled
```

### Common Services
```bash
sudo systemctl status firewalld
sudo systemctl status sshd
sudo systemctl status httpd
sudo systemctl status mariadb
```

### System State
```bash
systemctl list-units             # List active units
systemctl list-units --all       # All units
systemctl list-unit-files        # All unit files
systemctl list-dependencies      # Show dependencies
```

### System Control
```bash
sudo systemctl reboot            # Reboot system
sudo systemctl poweroff          # Power off
sudo systemctl suspend           # Suspend
sudo systemctl hibernate         # Hibernate
```

---

**Previous**: [Package Management](02-fedora-package-management.md) | **Next**: [Networking](04-fedora-networking.md)
