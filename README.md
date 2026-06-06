# Linux Commands Guide 🐧

A comprehensive guide to Linux commands for **Ubuntu**, **Fedora**, and **Arch Linux**, organized by skill level and use case. Perfect for beginners learning Linux on WSL or native installations, and experienced users looking for quick reference.

## 📚 Table of Contents

- [Getting Started](#-getting-started)
- [Repository Structure](#-repository-structure)
- [Documentation](#-documentation)
- [Scripts](#%EF%B8%8F-scripts)
- [Examples](#-examples)
- [Contributing](#-contributing)
- [License](#-license)

## 🚀 Getting Started

This repository contains:
- Organized command documentation from beginner to advanced levels
- Ubuntu (apt) and Fedora (dnf) package management guides
- Complete Docker & WSL2 setup and commands
- Practical shell scripts for common tasks
- Real-world examples and use cases
- Configuration templates

### Prerequisites

- Ubuntu 20.04 LTS or later / Fedora 38 or later (also works on WSL2 on Windows)
- Basic familiarity with terminal/command line
- Text editor (vim, nano, or VS Code)

## 📁 Repository Structure

```
linux-commands-guide/
├── README.md
├── docs/
│   ├── docker-guide.md
│   ├── kubernetes-guide.md
│   ├── data-science-guide.md
│   ├── ubuntu/
│   │   ├── 01-beginner-commands.md
│   │   ├── 02-intermediate-commands.md
│   │   ├── 03-advanced-commands.md
│   │   ├── 04-data-science-commands.md
│   │   ├── 05-git-github-commands.md
│   │   ├── 06-docker-commands.md
│   │   └── quick-reference.md
│   ├── fedora/
│   │   ├── 01-fedora-basics.md
│   │   ├── 02-fedora-package-management.md
│   │   ├── 03-fedora-system-services.md
│   │   ├── 04-fedora-networking.md
│   │   ├── 05-fedora-system-commands-guide.md
│   │   ├── 06-fedora-44-post-install-guide.md
│   │   └── fedora-quick-reference.md
│   └── arch/
│       ├── 01-arch-basics.md
│       ├── 02-arch-package-management.md
│       ├── 03-arch-system-services.md
│       ├── 04-arch-networking.md
│       ├── 05-arch-installation-guide.md
│       ├── 06-arch-post-install-guide.md
│       └── arch-quick-reference.md
├── scripts/
│   ├── setup-aliases.sh
│   ├── install-ds-stack.sh
│   └── backup-script.sh
├── examples/
│   ├── batch-rename.sh
│   ├── csv-processor.sh
│   └── git-workflow.sh
└── config/
    ├── bashrc-template
    ├── bash_aliases
    └── gitconfig.sh
```

## 📖 Documentation

### 🟠 Ubuntu Commands

1. **[Beginner Commands](docs/ubuntu/01-beginner-commands.md)**
   - Navigation, file/directory operations
   - Basic system commands (echo, clear, history, sudo)
   - Text viewing and editing
   - Package management basics (apt)
   - WSL-specific commands & keyboard shortcuts

2. **[Intermediate Commands](docs/ubuntu/02-intermediate-commands.md)**
   - Process management
   - Permissions and ownership
   - Network commands (ssh, scp, curl, wget)
   - System monitoring
   - Aliases, environment variables, tmux/screen, lsof

3. **[Advanced Commands](docs/ubuntu/03-advanced-commands.md)**
   - Shell scripting (functions, error handling)
   - System administration & journalctl logs
   - Advanced find, awk, pipes
   - Disk usage & cleanup

4. **[Data Science Commands](docs/ubuntu/04-data-science-commands.md)**
   - Python environment setup (System Python + venv)
   - Virtual environment management
   - Core DS library installation
   - Jupyter notebook setup
   - Docker for data science

5. **[Git & GitHub Commands](docs/ubuntu/05-git-github-commands.md)**
   - Repository management
   - Branching and merging
   - Remote operations
   - git stash, tags, .gitignore templates

6. **[Docker Commands](docs/ubuntu/06-docker-commands.md)**
   - Docker Engine installation on Ubuntu/WSL2
   - Container & image management
   - Docker Compose, volumes, networking

7. **[Quick Reference](docs/ubuntu/quick-reference.md)**

### 🔵 Fedora Commands

1. **[Fedora Basics](docs/fedora/01-fedora-basics.md)**
   - Navigation, file/directory operations
   - System information, users
   - Keyboard shortcuts & terminal tips

2. **[Fedora Package Management (dnf)](docs/fedora/02-fedora-package-management.md)**
   - dnf install, remove, update, search, info
   - dnf history & rollback
   - RPM Fusion setup
   - Flatpak basics

3. **[Fedora System Services](docs/fedora/03-fedora-system-services.md)**
   - systemctl (start/stop/enable/disable)
   - journalctl logs
   - firewalld & SELinux basics

4. **[Fedora Networking](docs/fedora/04-fedora-networking.md)**
   - nmcli, ip, ping, curl, wget
   - SSH setup on Fedora

5. **[Fedora System Commands Guide](docs/fedora/05-fedora-system-commands-guide.md)**
   - Package management (dnf), systemctl, journalctl
   - System info, networking, security & firewall (firewalld, SELinux)

6. **[Fedora 44 Post Install Guide](docs/fedora/06-fedora-44-post-install-guide.md)**
   - Post-install setup, DNF configurations, multimedia codecs
   - NVIDIA drivers, Docker, NetBird, SMB shares, GNOME Tweaks & extensions

7. **[Fedora Quick Reference](docs/fedora/fedora-quick-reference.md)**

### ⚫ Arch Linux Commands

1. **[Arch Linux Basics](docs/arch/01-arch-basics.md)**
   - Navigation and basic command-line operations
   - Common file operations, user management, and keyboard shortcuts

2. **[Arch Package Management](docs/arch/02-arch-package-management.md)**
   - Standard `pacman` update, install, and remove syntax
   - AUR (Arch User Repository) and helper setup (`yay` and `paru`)

3. **[Arch System Services](docs/arch/03-arch-system-services.md)**
   - Managing services using `systemctl` (start/enable/status)
   - Checking system logs with `journalctl`
   - Bootloaders overview (systemd-boot and GRUB)

4. **[Arch Networking](docs/arch/04-arch-networking.md)**
   - WiFi connection setup using `iwctl`
   - NetworkManager commands (`nmcli` and `nmtui`)
   - Firewall protection (`ufw` installation and ruleset)
   - OpenSSH server security configuration

5. **[Arch Installation Guide](docs/arch/05-arch-installation-guide.md)**
   - Bootable USB creation and HP BIOS boot configuration
   - Connecting to Wi-Fi from the command-line install medium
   - Using the guided installer script (`archinstall`)

6. **[Arch Post-Install Guide](docs/arch/06-arch-post-install-guide.md)**
   - Mirrorlist speed optimization using `reflector`
   - Sound setup (PipeWire), Bluetooth, graphics drivers, and microcode
   - System backup snapshots (Timeshift) and Pacman configurations

7. **[Arch Quick Reference](docs/arch/arch-quick-reference.md)**

### 🐳 Standalone & Cross-Platform Guides

1. **[Docker & Dockerfile Complete Guide](docs/docker-guide.md)**
   - Concepts for absolute beginners (cargo ship analogy)
   - Expert-level installation & configuration for Windows (WSL2), macOS, and Linux
   - Dockerfile deep dive, layering, caching, and multi-stage builds
   - Comprehensive learning & execution resources

2. **[Kubernetes & YAML Manifest Complete Guide](docs/kubernetes-guide.md)**
   - Concepts for absolute beginners (Harbor Master analogy)
   - Expert-level installation & setup for Windows (WSL2), macOS, and Linux (Minikube, k3s, Kind)
   - Production-grade manifest construction (Deployment, Service) and health probes
   - Command continuation & execution differences on Windows CMD vs. PowerShell vs. Linux/macOS
   - Curated learning & cluster management resources

3. **[Data Science & ML Stack Complete Guide](docs/data-science-guide.md)**
   - Concepts for absolute beginners (laboratory kitchen analogy)
   - Map of the entire modern DS/ML tech stack (Polars, PyTorch, Hugging Face, Vector DBs, MLOps)
   - Expert-level GPU acceleration setup (NVIDIA CUDA on Windows/WSL2/Linux & Apple Silicon MPS on macOS)
   - Environment and package managers compared (venv, Mamba, Poetry)
   - Execution control, background processes, and troubleshooting in Windows CMD, PowerShell, and Bash

## 🛠️ Scripts

### Available Scripts
- **setup-aliases.sh**: Set up useful bash aliases for productivity
- **install-ds-stack.sh**: Install complete data science stack
- **backup-script.sh**: Automated backup script

### Usage
```bash
chmod +x scripts/*.sh
./scripts/setup-aliases.sh
```

## 💡 Examples

- **batch-rename.sh**: Rename multiple files based on patterns
- **csv-processor.sh**: Process CSV files with command-line tools
- **git-workflow.sh**: Common Git workflows automated

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 🎯 Use Cases

This guide is perfect for:
- Data science students using WSL2/Ubuntu or Fedora
- Developers containerizing apps with Docker
- System administrators managing Ubuntu/Fedora/Arch Linux servers
- Anyone learning Linux command line from scratch

### Quick update commands

**Ubuntu:**
```bash
sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y
```

**Fedora:**
```bash
sudo dnf upgrade --refresh -y
```

**Arch Linux:**
```bash
sudo pacman -Syu    # Official repositories update
# Or update both official repositories and AUR:
yay -Syu
```

## 🗺️ Resources

- [Docker & Dockerfile Complete Guide](docs/docker-guide.md) - Our detailed containerization guide
- [Kubernetes & YAML Manifest Complete Guide](docs/kubernetes-guide.md) - Our detailed container orchestration guide
- [Data Science & ML Stack Complete Guide](docs/data-science-guide.md) - Our detailed ML workflow setup guide
- [Linux Roadmap](https://roadmap.sh/linux) - A structured roadmap to learn Linux
- [Ubuntu Documentation](https://help.ubuntu.com/)
- [Fedora Documentation](https://docs.fedoraproject.org/)
- [Arch Wiki](https://wiki.archlinux.org/) - Comprehensive Arch Linux documentation
- [Archinstall Documentation](https://archlinux.org/packages/extra/any/archinstall/)

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👤 Author

**iNSRawat** - GitHub: [@iNSRawat](https://github.com/iNSRawat)

## ⭐ Show Your Support

Give a ⭐️ if this project helped you!

---
*Last Updated: May 2026*
