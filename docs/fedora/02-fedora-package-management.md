# Fedora Package Management (DNF)

Complete guide to managing packages on Fedora using DNF (Dandified YUM).

## DNF Basics

### System Updates
```bash
sudo dnf check-update        # Check for available updates
sudo dnf update              # Update all packages
sudo dnf upgrade             # Upgrade (removes obsolete packages)
sudo dnf update --security   # Security updates only
sudo dnf update package-name # Update specific package
```

### Installing Packages
```bash
sudo dnf install package     # Install package
sudo dnf install pkg1 pkg2   # Install multiple
sudo dnf reinstall package   # Reinstall package
sudo dnf downgrade package   # Downgrade to previous version
```

### Removing Packages
```bash
sudo dnf remove package      # Remove package
sudo dnf autoremove          # Remove unused dependencies
sudo dnf clean all           # Clean package cache
```

### Searching Packages
```bash
dnf search keyword           # Search for packages
dnf list available           # List available packages
dnf list installed           # List installed packages
dnf list updates             # List available updates
dnf info package             # Package details
```

### Package Groups
```bash
dnf group list               # List available groups
dnf group info "Group Name"  # Group details
sudo dnf group install "Development Tools"
sudo dnf group remove "Group Name"
```

### Repository Management
```bash
dnf repolist                 # List enabled repos
dnf repolist all             # List all repos
sudo dnf config-manager --set-enabled repo-name
sudo dnf config-manager --set-disabled repo-name
```

### Add Third-Party Repos
```bash
# RPM Fusion (Free)
sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm

# RPM Fusion (Nonfree)
sudo dnf install https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

### History
```bash
dnf history                  # Show transaction history
dnf history info <ID>        # Details of transaction
sudo dnf history undo <ID>   # Undo transaction
sudo dnf history redo <ID>   # Redo transaction
```

### Dependencies
```bash
dnf deplist package          # Show dependencies
dnf repoquery --requires package
dnf repoquery --whatrequires package
```

### Local RPM Files
```bash
sudo dnf install ./package.rpm
sudo rpm -ivh package.rpm    # Install RPM
sudo rpm -Uvh package.rpm    # Upgrade RPM
sudo rpm -e package          # Remove
rpm -qa                      # List installed
rpm -qi package              # Query info
```

## Common Package Names

### Development Tools
```bash
sudo dnf group install "Development Tools"
sudo dnf groupinstall "C Development Tools and Libraries" # Essential libraries for compiling C projects
sudo dnf install gcc gcc-c++ make cmake
sudo dnf install kernel-devel kernel-headers              # Necessary for kernel modules and drivers
sudo dnf install git curl wget
```

### Python Development
```bash
sudo dnf install python3 python3-pip python3-devel
sudo dnf install python3-virtualenv
```

### System Utilities
```bash
sudo dnf install htop ncdu tree
sudo dnf install vim nano
sudo dnf install tmux screen
```

---

**Previous**: [Fedora Basics](01-fedora-basics.md) | **Next**: [System Services](03-fedora-system-services.md)
