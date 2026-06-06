# Arch Linux Installation Guide (archinstall)

Step-by-step instructions to install Arch Linux using the official `archinstall` guided installer wizard. This guide is designed for modern UEFI computers and laptops.

> [!WARNING]
> This guide assumes you are wiping your disk completely to install Arch Linux. If you want to dual-boot (keep Windows alongside Arch), you must shrink your Windows partition *before* starting, as the automatic partitioner will format your target drive.

---

## Step 1: Create a Bootable USB

Do this from your working computer/OS before booting the installer.

1. **Download the ISO**: Visit the [Arch Linux Downloads page](https://archlinux.org/download/) and download the latest `.iso` release.
2. **Download a Flashing Tool**:
   - For Windows: Download [Rufus](https://rufus.ie/).
   - For macOS or Linux: Use [BalenaEtcher](https://etcher.balena.io/) or the terminal `dd` tool.
3. **Flash the Drive**:
   - Insert a USB flash drive (minimum 4GB - **Note: All data on this USB will be erased**).
   - Open Rufus/Etcher, select the downloaded Arch Linux `.iso` file, choose your USB device, and click **Start/Flash**.
   - Keep settings on their default values.

---

## Step 2: Configure BIOS and Boot

To boot the installer, Secure Boot must be disabled.

1. Turn off your target computer completely.
2. Turn it on and immediately tap your system's BIOS hotkey repeatedly (typically **F2**, **F10**, **F12**, or **Del**) until the BIOS setup menu appears.
3. Use the arrow keys to navigate to settings like **Security**, **System Configuration**, or **Boot Options**.
4. Locate **Secure Boot** and change it to **Disabled**. (Default Arch Kernels do not support Secure Boot out-of-the-box).
5. Save changes and exit BIOS (usually by pressing **F10** and confirming).
6. As the computer restarts, immediately tap the boot menu key (typically **F8**, **F9**, **F11**, or **F12**) to load the **Boot Device Options** menu.
7. Select your USB flash drive from the boot list and press **Enter**.
8. Select the first option on the startup screen: `"Arch Linux install medium (x86_64)"`.

---

## Step 3: Connect to the Internet

Arch Linux is net-installed; the guided script downloads packages from the internet dynamically. You will land on a terminal command line starting with:
`root@archiso ~ #`

### Option A: Wired Ethernet (Recommended)
Plug an Ethernet cable directly from your router into your laptop. Connection configuration happens automatically.

### Option B: Wireless Wi-Fi Connection
If you do not have Ethernet, connect to Wi-Fi using the `iwctl` tool:

1. Start the wireless command client:
   ```bash
   iwctl
   ```
2. Identify your wireless network interface card name (usually `wlan0`):
   ```text
   device list
   ```
3. Scan for available networks (replace `wlan0` with your interface name if it differs):
   ```text
   station wlan0 scan
   ```
4. List the discovered networks:
   ```text
   station wlan0 get-networks
   ```
5. Connect to your Wi-Fi network:
   ```text
   station wlan0 connect "Your_WiFi_Network_Name"
   ```
6. Enter your Wi-Fi password when prompted.
7. Exit the tool once connected:
   ```text
   exit
   ```
8. Verify internet connectivity by sending 3 pings to Google:
   ```bash
   ping -c 3 google.com
   ```
   *(If you receive replies, your internet connection is ready.)*

---

## Step 4: Run the Guided Installer

Arch Linux includes a script that runs a guided, interactive installer.

To start, type:
```bash
archinstall
```

A blue, menu-driven interface will load. Navigate options using your **Arrow keys** and press **Enter** to configure these primary parameters:

* **Mirrors**: Choose your region or country to select the fastest local servers for downloading package dependencies.
* **Locales**: Configure your language settings, system encoding (`UTF-8`), and keyboard layout.
* **Disk Configuration**:
  - Select **"Use a best-effort default partition layout"**.
  - Choose your laptop's main storage drive (e.g. SSD/NVMe).
  - Choose your filesystem: `ext4` (reliable and classic) or `btrfs` (modern, supports snapshotting).
* **Bootloader**: Select `systemd-boot` or `GRUB`. (Both work well; `systemd-boot` is simple and modern).
* **Hostname**: Choose a name for your system (e.g. `arch-desktop` or `arch-laptop`).
* **Root Password**: Define a strong password for the primary administrator root account.
* **User Account**:
  - Choose **Add a user**.
  - Type your username and set a secure password.
  - When asked if this user should be a superuser (have administrator/sudo privileges), select **"Yes"**.
* **Profile**: Navigate to **Type** > **Desktop** and select your preferred desktop environment. Classic choices include:
  - `KDE Plasma` (Modern, Windows-like, highly customizable)
  - `GNOME` (Clean, minimalist, similar to macOS/mobile style)
  - `XFCE` (Extremely lightweight, ideal for older laptops)
* **Audio**: Select `PipeWire` (the modern standard sound server).
* **Network Configuration**: Select **NetworkManager** (this is vital so your Wi-Fi device is controllable via desktop GUI after installation).

---

## Step 5: Start Installation and Reboot

1. Review your settings list. When satisfied, scroll down and select **Install**.
2. Press **Enter** to confirm disk partitioning.
3. The installer will format your disk partitions, download kernel files, install package configurations, and compile the desktop environment. This process takes 5 to 15 minutes depending on your internet bandwidth.
4. When installation finishes, you will be prompted: *"Would you like to chroot into the newly created installation?"* Select **No**.
5. Restart your system:
   ```bash
   reboot
   ```
6. Pull out the bootable USB drive as your computer turns off.

Your computer will start into your new Arch Linux system and load your chosen desktop environment login screen.

---

**Previous**: [Arch Linux Networking](04-arch-networking.md) | **Next**: [Arch Linux Post-Install Guide](06-arch-post-install-guide.md)
