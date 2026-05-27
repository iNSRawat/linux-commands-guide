# Fedora Networking

Network configuration and management on Fedora.

## Network Information

### View Network Configuration
```bash
ip addr                  # IP addresses
ip link                  # Network interfaces
ip route                 # Routing table
hostname                 # System hostname
hostname -I              # IP addresses only
nmcli device status      # NetworkManager device status
```

## NetworkManager (nmcli)

### Connection Management
```bash
nmcli connection show           # List connections
nmcli connection up <name>      # Activate connection
nmcli connection down <name>    # Deactivate connection
nmcli connection reload         # Reload all connections
```

### Device Management
```bash
nmcli device               # List devices
nmcli device show <device> # Device details
nmcli device wifi list    # List WiFi networks
nmcli device wifi connect <SSID> password <password>
```

## Firewall (firewalld)

### Basic Commands
```bash
sudo firewall-cmd --state            # Check firewall status
sudo firewall-cmd --get-zones        # List zones
sudo firewall-cmd --get-active-zones # Active zones
sudo firewall-cmd --list-all         # List all settings
```

### Port Management
```bash
sudo firewall-cmd --add-port=8080/tcp --permanent
sudo firewall-cmd --remove-port=8080/tcp --permanent
sudo firewall-cmd --reload           # Apply changes
```

### Service Management
```bash
sudo firewall-cmd --add-service=http --permanent
sudo firewall-cmd --add-service=https --permanent
sudo firewall-cmd --list-services    # List allowed services
```

## SSH Configuration & Remote Access

Fedora uses OpenSSH for remote connection management.

### Key Management
* `ssh-keygen -t ed25519 -C "email@example.com"` - Generate a new secure SSH key pair.
* `ssh-copy-id -i ~/.ssh/id_ed25519.pub user@remote_host` - Copy public SSH key to a remote host (enables passwordless login).
* `ssh user@remote_host` - Connect to a remote server.

### Securing OpenSSH Daemon
The main SSH daemon configuration file is `/etc/ssh/sshd_config`. To secure SSH, you can modify:
* `PasswordAuthentication no` - Disable password-based logins (require SSH keys).
* `PermitRootLogin no` - Disable root login.
* `Port 2222` - Change default port to reduce scan noise.

Apply changes by restarting the service:
```bash
sudo systemctl restart sshd
```

## Testing & Diagnostics

### Connection Testing
```bash
ping -c 4 google.com     # Test connectivity
traceroute google.com    # Trace route
mtr google.com          # Network diagnostic tool
```

### Port & Service Testing
```bash
ss -tuln                 # List open ports
netstat -tuln            # Alternative (older)
nmap localhost           # Scan local ports
```

### DNS
```bash
nslookup google.com      # DNS lookup
dig google.com           # Detailed DNS query
host google.com          # Quick DNS query
```

---

**Previous**: [System Services](03-fedora-system-services.md) | **Next**: [System Commands Guide](05-fedora-system-commands-guide.md)
