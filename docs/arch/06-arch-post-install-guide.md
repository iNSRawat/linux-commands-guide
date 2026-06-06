# Arch Linux Post-Installation Guide

Essential configurations and software to transform a clean Arch Linux install into a robust, secure, and fully-featured daily driver system.

---

## 1. Update and Optimize Mirrors

By default, Arch Linux downloads packages from a generic list of mirrors. You can speed up your downloads by filtering for the fastest, most recently synchronized servers using `reflector`.

### Install Reflector
```bash
sudo pacman -S reflector
```

### Rank and Save the Top 10 Mirrors
Query the latest 10 mirrors using HTTPS, sort them by download rate, and write the list back to the configuration file:
```bash
sudo reflector --latest 10 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
```

### Perform a Full System Upgrade
Now that your mirrors are optimized, run a full system update:
```bash
sudo pacman -Syu
```

---

## 2. Enable Bluetooth

Arch Linux does not start the Bluetooth software stack by default.

### Install Bluetooth Packages
```bash
sudo pacman -S bluez bluez-utils
```

### Enable and Start the Bluetooth Service
Configure systemd to start the Bluetooth daemon immediately and on subsequent boot-ups:
```bash
sudo systemctl enable --now bluetooth
```

*(You can now manage and connect to your Bluetooth peripherals using your desktop environment's setting panel or the CLI tool `bluetoothctl`.)*

---

## 3. Secure Your System (Firewall)

Protecting your computer on public wireless networks is critical. The Uncomplicated Firewall (`ufw`) is the easiest tool to secure your system.

### Install UFW
```bash
sudo pacman -S ufw
```

### Set Default Policies and Enable Firewall
Block all incoming traffic by default, allow all outgoing connections, enable the firewall ruleset, and start the system service:
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw enable
sudo systemctl enable --now ufw
```

---

## 4. Install an AUR Helper (yay)

The Arch User Repository (AUR) contains thousands of community-maintained software packages (such as Chrome, VS Code, Discord, and Spotify). To install these easily, build the `yay` helper from source code.

### Install Compilation Dependencies
```bash
sudo pacman -S --needed base-devel git
```

### Clone the Repository
Clone the build recipe folder from the AUR repository:
```bash
git clone https://aur.archlinux.org/yay.git
```

### Compile and Install
Enter the directory and run `makepkg` to compile and install (`-s` automatically fetches dependencies via pacman, `-i` installs the final package):
```bash
cd yay
makepkg -si
```

*(Once installed, you can clean up the build folder: `cd .. && rm -rf yay`.)*
*(Now, you can search and install AUR packages using `yay -S package_name`.)*

---

## 5. Set Up System Snapshots (Timeshift)

Since Arch is a rolling release distro, system updates are continuous. Creating system checkpoints ensures you can roll back your system configurations if an update breaks a system component.

### Install Timeshift
```bash
sudo pacman -S timeshift
```

### Configuration
1. Open **Timeshift** from your application launcher menu.
2. Select **RSYNC** as the snapshot type.
3. Choose your target partition to store snapshots.
4. Set up your backup schedule (e.g. keep 3 daily snapshots).
5. Run your first manual snapshot.

---

## 6. Install Processor Microcode

Microcode updates supply stability corrections and security hotfixes for your computer's CPU. You should install the corresponding microcode package for your processor architecture.

### For Intel Processors
```bash
sudo pacman -S intel-ucode
```

### For AMD Processors
```bash
sudo pacman -S amd-ucode
```

*Note: Your bootloader (systemd-boot or GRUB) will automatically load the microcode file on next boot.*

---

## 7. Install Graphics Drivers

To get full performance, hardware acceleration, and battery life optimization, install the correct GPU drivers:

### Intel Integrated Graphics
```bash
sudo pacman -S mesa vulkan-intel Intel-media-driver
```

### AMD Radeon Graphics
```bash
sudo pacman -S mesa xf86-video-amdgpu vulkan-radeon
```

### NVIDIA Dedicated GPU
```bash
sudo pacman -S nvidia nvidia-utils nvidia-settings
```

---

## 8. Customize Pacman Settings (QoL)

You can enable colors and parallel downloads to improve your `pacman` output and download speeds.

1. Open the configuration file in a terminal editor:
   ```bash
   sudo nano /etc/pacman.conf
   ```
2. Locate the `# Misc options` section.
3. Uncomment (remove the `#` character) these options:
   ```ini
   Color
   ILoveCandy          # Adds a retro pacman animation to package downloads
   ParallelDownloads = 5
   ```
4. Save and exit (in Nano: `Ctrl+O`, `Enter`, then `Ctrl+X`).

---

## 9. Unlock GNOME (Tweaks & Extensions)

Arch Linux provides a completely "vanilla" GNOME desktop experience. To customize your desktop layout, change fonts, manage themes, or add desktop indicators, you need GNOME Tweaks and Extension Manager.

### Install GNOME Tweaks & Extension Manager
```bash
sudo pacman -S gnome-tweaks extension-manager
```

### Essential Customizations
1. **Extension Manager**: Open the app, click the **Browse** tab, and install:
   - **Dash to Dock**: Adds a highly customizable, macOS-style dock at the bottom of your screen.
   - **AppIndicator and KStatusNotifierItem Support**: Restores the system tray in the top bar for apps like Spotify, Discord, and Steam.
2. **GNOME Tweaks**: Adjust window titlebar buttons (minimize/maximize), system fonts, startup applications, and desktop themes.

---

**Previous**: [Arch Linux Installation Guide](05-arch-installation-guide.md) | **Next**: [Arch Linux Quick Reference](arch-quick-reference.md)

