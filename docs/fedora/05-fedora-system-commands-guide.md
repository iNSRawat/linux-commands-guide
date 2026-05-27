# Fedora Linux System Commands Guide

Fedora is a cutting-edge Linux distribution known for adopting new technologies early. It uses `dnf` for package management, heavily integrates `systemd`, and enforces `SELinux` by default.

## 1. Package Management (DNF) & Development Setup
Fedora uses `dnf` (Dandified YUM) as its default package manager.

* `sudo dnf install <package_name>`: Install a new package.
* `sudo dnf remove <package_name>`: Remove an installed package.
* `sudo dnf upgrade`: Upgrade all installed packages to their latest versions.
* `sudo dnf search <keyword>`: Search the repositories for a package.
* `sudo dnf list installed`: View a list of all currently installed packages.
* `sudo dnf info <package_name>`: Display detailed information about a package.
* `sudo dnf clean all`: Clean the cache to free up disk space.
* `sudo dnf history`: View the transaction history (useful for rolling back installations).
* `sudo dnf groupinstall "<Group Name>"`: Install a bundle of software (e.g., "Development Tools").

### Compiling and Tooling Dependencies
When building software from source (such as compiling specialized Python libraries like NumPy or SciPy) or loading custom drivers:
* `sudo dnf groupinstall "C Development Tools and Libraries"`: Installs essential compilation headers and development libraries.
* `sudo dnf install kernel-devel kernel-headers`: Installs kernel development packages required to compile kernel modules.

## 2. System and Service Management (Systemd)
Fedora relies on `systemd` to initialize and manage services.

* `systemctl start <service>`: Start a service immediately.
* `systemctl stop <service>`: Stop a running service.
* `systemctl restart <service>`: Restart a service.
* `systemctl enable <service>`: Configure a service to start automatically on boot.
* `systemctl disable <service>`: Prevent a service from starting on boot.
* `systemctl status <service>`: Check the current status and recent logs of a service.
* `journalctl -xe`: View the system journal/logs for immediate troubleshooting.
* `journalctl -u <service>`: View logs specific to a single service.

### Containerization Daemons
To manage development environments using containerization engines:
* `sudo systemctl start docker` / `sudo systemctl enable docker.service`: Start and configure Docker to run automatically at system boot.
* `sudo usermod -aG docker $USER`: Add the current user to the `docker` group (requires a shell restart to run containers without prefixing `sudo`).

## 3. System Information & Resource Monitoring
* `cat /etc/os-release`: Display specific Fedora release and version details.
* `uname -r`: Check the currently active kernel version.
* `lscpu`: Display detailed CPU architecture information.
* `free -m` or `free -h`: Show available and used RAM.
* `df -h`: Check disk space usage across mounted file systems.
* `du -sh <directory>`: Check the total size of a specific directory.
* `top` (or `htop` if installed): Monitor system processes, CPU, and memory usage in real-time.

## 4. Network Configuration & SSH Provisioning
Fedora uses NetworkManager for most network configurations and OpenSSH for secure remote shells.

* `ip addr`: Show IP addresses and network interfaces.
* `ip route`: Display the current routing table.
* `nmcli dev status`: Check the status of all network devices.
* `nmcli connection show`: List all saved network connections.
* `ss -tuln`: List all listening ports and active network connections.

### Cloud Instance & SSH Provisioning
* `ssh-keygen -t ed25519 -C "your_email@example.com"`: Generate a secure SSH key pair.
* `ssh-copy-id -i ~/.ssh/id_ed25519.pub user@remote_host`: Copy your public key to a remote host for passwordless key-based login.
* **Securing OpenSSH daemon (`/etc/ssh/sshd_config`)**:
  Open the configuration file (`sudo nano /etc/ssh/sshd_config`) and enforce the following settings to secure a cloud instance:
  ```ini
  PasswordAuthentication no   # Force SSH key authentication only
  PermitRootLogin no           # Disable direct root account logins
  Port 2222                    # Change port from 22 to reduce scan noise
  ```
  Apply settings using: `sudo systemctl restart sshd`

## 5. Security, Firewall, and SELinux
Fedora uses `firewalld` for firewall management and `SELinux` (Security-Enhanced Linux) for mandatory access control.

### Firewalld
* `sudo firewall-cmd --state`: Check if the firewall is actively running.
* `sudo firewall-cmd --get-active-zones`: View currently active network zones.
* `sudo firewall-cmd --add-port=<port>/tcp --permanent`: Open a specific port permanently.
* `sudo firewall-cmd --reload`: Apply changes made with the `--permanent` flag.

### SELinux Configuration & Advanced Troubleshooting
* `sestatus`: Check the current status and mode of SELinux.
* `sudo setenforce 0`: Temporarily switch SELinux to permissive mode (useful for troubleshooting denials).
* `sudo setenforce 1`: Switch SELinux back to enforcing mode.
* `sudo tail /var/log/audit/audit.log` or `sudo ausearch -m AVC -ts recent`: View recent SELinux denials.
* **Resolving SELinux Denials**:
  Instead of disabling SELinux globally, resolve issues using policies:
  * `sudo restorecon -Rv /path/to/directory`: Recursively restore default SELinux security contexts on a directory (e.g., after copying files into webserver folders).
  * `sudo audit2allow -a -M my_custom_policy`: Parse audit logs and generate a custom security policy module to allow flagged operations.
  * `sudo semodule -i my_custom_policy.pp`: Install and load the generated custom policy module.

## 6. File Permissions & Cross-Environment Quirks
* `chmod +x <file>`: Make a file executable.
* `chown <user>:<group> <file>`: Change the ownership of a file or directory.
* `ls -la`: List all files, including hidden ones, with their detailed permissions.

### WSL 2 Cross-Environment Quirks
If you are running Fedora within WSL 2 (Windows Subsystem for Linux):
* **File Permissions on Host Drives**: Standard commands like `chmod` and `chown` will not work on mounted Windows drives (e.g., `/mnt/c`) unless metadata mount options are enabled. Add the following to `/etc/wsl.conf`:
  ```ini
  [automount]
  options = "metadata"
  ```
* **Bridged Network Querying**: Since WSL 2 runs on a lightweight utility VM, network interfaces are virtualized. Use `ip route show | grep default` to locate the virtual switch IP address connecting WSL to your host machine.

---

**Previous**: [Networking](04-fedora-networking.md) | **Next**: [Post Install Guide](06-fedora-44-post-install-guide.md)
