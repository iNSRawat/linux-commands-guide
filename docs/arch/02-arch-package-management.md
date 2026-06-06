# Arch Linux Package Management (Pacman & AUR)

Complete guide to managing software on Arch Linux using the default package manager (`pacman`) and the Arch User Repository (AUR).

## Pacman Basics

Unlike Debian-based (`apt`) or RedHat-based (`dnf`) distributions, `pacman` uses short, single-character operation flags combined with sub-options.

### System Updates
```bash
sudo pacman -Syu             # Synchronize databases and perform a full system upgrade
sudo pacman -Syyu            # Force refresh databases (even if up to date) and upgrade
sudo pacman -Syuw            # Download updates but do not install them yet
```

### Installing Packages
```bash
sudo pacman -S package       # Install a package from official repositories
sudo pacman -S pkg1 pkg2     # Install multiple packages
sudo pacman -S --needed pkg  # Install only if not already installed/up-to-date
sudo pacman -Sf package      # Force install a package (overwrite files - use with caution!)
```

### Removing Packages
```bash
sudo pacman -R package       # Remove package, leaving its dependencies
sudo pacman -Rs package      # Remove package and its unused dependencies
sudo pacman -Rns package     # Remove package, unused dependencies, and configuration files (Recommended)
sudo pacman -Rdd package     # Force remove a package, skipping dependency checks (Dangerous!)
```

### Searching and Querying Packages
```bash
pacman -Ss keyword           # Search official repositories for a package
pacman -Qs keyword           # Search installed packages for a keyword
pacman -Si package           # View detailed information about a repository package
pacman -Qi package           # View detailed information about an installed package
pacman -Ql package           # List all files installed by a package
pacman -Qo /path/to/file     # Find which package owns a specific file
pacman -Qe                   # List all explicitly installed packages
pacman -Qm                   # List all installed packages from the AUR (foreign packages)
```

### Database Cleanup and Maintenance
```bash
pacman -Qtdq                 # List orphaned packages (installed as dependencies but no longer needed)
sudo pacman -Rns $(pacman -Qtdq)  # Remove all orphaned packages recursively
sudo pacman -Scc             # Clean the entire package cache (removes all cached tarballs)
sudo pacman -Sc              # Clean uninstalled package files from the cache
```

### Package Databases and Locks
If you get a `db.lck` error:
```bash
# This happens if a transaction was interrupted. Ensure no other instance is running, then:
sudo rm /var/lib/pacman/db.lck
```

---

## The Arch User Repository (AUR)

The official Arch repositories do not contain everything. For proprietary, niche, or community-maintained packages (e.g. Spotify, Google Chrome, VS Code), users turn to the **AUR**.

### Manual Compilation from AUR (Standard Method)
Every AUR helper is installed this way first:
```bash
# 1. Install prerequisites
sudo pacman -S --needed base-devel git

# 2. Clone the package build files (PKGBUILD) from the AUR
git clone https://aur.archlinux.org/yay.git

# 3. Navigate into the cloned folder
cd yay

# 4. Compile and install the package
makepkg -si
# Flags: -s (sync dependencies via pacman) and -i (install package)
```

---

## AUR Helpers (`yay` & `paru`)

Once an AUR helper is installed, you can search, install, and update official AND AUR packages with a single tool using syntax identical to `pacman`.

### Using `yay` (Go-based helper)
```bash
yay -Syu                     # Update both official repositories AND AUR packages (Recommended)
yay -S package               # Install package from repositories or AUR
yay -Rns package             # Remove package and configuration files
yay -Ss keyword              # Search repositories and AUR for a keyword
yay -Si package              # Detailed info for a package
yay -Sua                     # Update AUR packages only
yay -Yc                      # Clean unneeded dependencies and build files
```

### Using `paru` (Rust-based helper)
`paru` is another modern alternative, written in Rust, by one of the co-creators of `yay`.
```bash
paru -Syu                    # Update system and AUR
paru -S package              # Install package
paru -Ss keyword             # Search packages
paru -G package              # Get (download) PKGBUILD of a package to modify
```

---

## Common Group and Utility Package Names

### Compilation and System Tools
```bash
sudo pacman -S --needed base-devel git  # Developer tools and compiler tools (make, gcc)
sudo pacman -S linux-headers            # Essential if compilation needs kernel modules (e.g. VirtualBox, Nvidia drivers)
sudo pacman -S wget curl rsync openssh  # Basic downloading & networking tools
```

### Text Editors & System Shells
```bash
sudo pacman -S vim nano neovim          # Core terminal editors
sudo pacman -S bash-completion          # Enable tab-completion for system commands
```

### System Monitoring
```bash
sudo pacman -S htop btop ncdu           # Interactive monitors and disk space analyzers
```

---

**Previous**: [Arch Linux Basics](01-arch-basics.md) | **Next**: [Arch Linux System Services](03-arch-system-services.md)
