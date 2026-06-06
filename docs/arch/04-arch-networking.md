# Arch Linux Networking

Network configuration, firewall security (`ufw`), wireless connections (`iwctl`), and remote management on Arch Linux.

## Network Information

### View Network Interfaces and Configuration
```bash
ip addr                  # Show IP addresses and status of interfaces (short form: ip a)
ip link                  # Show network interfaces and link layer status
ip route                 # View routing tables (gateway routes)
hostname                 # View hostname
hostname -I              # View local IP addresses only
```

---

## Interactive WiFi Connection (`iwctl`)

During Arch Linux installation or in minimal setups, `iwd` (Internet Wireless Daemon) is standard. Connection details are managed via `iwctl`.

### Running `iwctl`
Start the interactive client prompt:
```bash
iwctl
```

### Commands inside `iwctl` prompt:
```text
device list                                # 1. List wireless devices (e.g., wlan0)
station wlan0 scan                         # 2. Scan for available networks (replace wlan0)
station wlan0 get-networks                 # 3. List scanned WiFi networks
station wlan0 connect "SSID_Name"          # 4. Connect to network (use quotes if spaces exist)
                                           # 5. Type password when prompted
exit                                       # 6. Exit the interactive shell
```

---

## NetworkManager (`nmcli` & `nmtui`)

After desktop installation, **NetworkManager** is the standard utility for network configuration.

### Text User Interface (TUI)
For an easy interactive menu in the terminal:
```bash
nmtui                        # Opens an interactive terminal network manager
```

### CLI Command Management (`nmcli`)
```bash
nmcli connection show                      # List all saved network connections
nmcli connection up "SSID_Name"            # Activate a connection
nmcli connection down "SSID_Name"          # Deactivate a connection
nmcli device status                        # Show current status of network devices
nmcli device wifi list                     # Scan and list available Wi-Fi networks
nmcli device wifi connect "SSID" password "pass" # Connect to wireless network
```

---

## Firewall Protection (`ufw`)

Arch Linux recommends the Uncomplicated Firewall (`ufw`) as a simple front-end for iptables/nftables.

### Enabling the Firewall
```bash
sudo pacman -S ufw                         # Install UFW package
sudo systemctl enable --now ufw            # Start and enable the UFW daemon
sudo ufw enable                            # Enable the firewall (runs rules on boot)
```

### Managing Rules
```bash
sudo ufw status verbose                    # View current rules and status
sudo ufw default deny incoming             # Default: Block all incoming traffic (Recommended)
sudo ufw default allow outgoing            # Default: Allow all outgoing traffic (Recommended)
sudo ufw allow 22/tcp                      # Allow incoming SSH connections (Port 22)
sudo ufw allow 80/tcp                      # Allow HTTP traffic (Port 80)
sudo ufw allow 443/tcp                     # Allow HTTPS traffic (Port 443)
sudo ufw deny 111                          # Block specific port (e.g. port 111)
sudo ufw delete allow 22/tcp               # Remove a rule
```

---

## SSH Remote Access

Install and configure OpenSSH for encrypted shell access.

### Client and Key Setup
```bash
ssh-keygen -t ed25519 -C "user@email"      # Generate a secure SSH key pair
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@remote_ip # Copy public key to remote server
ssh user@remote_ip                         # Connect to remote server
```

### Securing the SSH Server
Edit configuration in `/etc/ssh/sshd_config`:
```ini
# Recommended settings inside /etc/ssh/sshd_config:
PasswordAuthentication no                  # Require SSH keys (disable passwords)
PermitRootLogin no                         # Disable root user login via SSH
Port 2222                                  # Change default port (22) to reduce bot scans
```

Apply rules by restarting OpenSSH:
```bash
sudo systemctl restart sshd
```

---

## Testing & Diagnostics

### Diagnostic Testing
```bash
ping -c 4 google.com                       # Send 4 ICMP echo requests to verify connection
traceroute google.com                      # Trace network hop route
mtr google.com                             # Combined ping and traceroute diagnostic tool
ss -tuln                                   # List active TCP & UDP ports (listening sockets)
```

### DNS Queries
```bash
nslookup google.com                        # Perform a quick DNS check
dig google.com                             # Query detailed domain information
```

---

**Previous**: [Arch Linux System Services](03-arch-system-services.md) | **Next**: [Arch Linux Installation Guide](05-arch-installation-guide.md)
