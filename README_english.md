[中文](README.md) | English

# Droidspaces USB Manager

USB device management tool designed for the **Droidspaces** Linux container environment. Automatically detects and manages USB storage devices and ADB devices.

## Features

- Auto-detect USB storage devices (USB drives, portable hard drives, etc.)
- Auto-create device nodes
- Auto-mount/unmount partitions
- Support opening mounted directories (Dolphin file manager)
- Support ejecting devices (safe removal)
- Auto-detect ADB devices (Android phones, etc.)
- System tray icon
- **Chinese/English language switching** (auto-detect system language)
- Support Wayland and X11
- Multi-partition support (each partition mounted independently)

## Installation

### Method 1: Using deb package (Recommended)

```bash
sudo dpkg -i usb-manager-v1.2.deb
sudo apt-get install -f  # Auto-install dependencies
```

### Method 2: Manual Installation

```bash
# Install dependencies
sudo apt-get install python3 python3-pyqt5 udev util-linux

# Copy files
sudo cp src/usb-manager.py /usr/share/usb-manager/
sudo cp src/usb-passthrough.sh /usr/share/usb-manager/
sudo cp src/usb-storage-passthrough.sh /usr/share/usb-manager/

# Create desktop shortcut
sudo cp desktop/usb-manager.desktop /usr/share/applications/

# Create launch script
sudo cp debian/usr/bin/usb-manager /usr/bin/
sudo chmod +x /usr/bin/usb-manager

# Configure sudoers (optional, for passwordless mount)
sudo cp debian/etc/sudoers.d/usb-storage /etc/sudoers.d/
sudo chmod 440 /etc/sudoers.d/usb-storage
```

## Usage

### Launch Application

```bash
# Launch from application menu
# Or launch from terminal
usb-manager
```

### Feature Description

1. **Auto-detect**: Application automatically scans USB storage devices and ADB devices
2. **Auto-mount**: Newly inserted USB drives are automatically mounted to `~/USB-Storage/<partition_name>`
3. **Open Directory**: Click "Open Dir" button to open Dolphin file manager
4. **Eject Device**: Click "Eject" button to unmount device and prompt safe removal
5. **ADB Device**: Auto-detect Android phones and other ADB devices

### Mount Points

- Default mount point: `~/USB-Storage/<partition_name>`
- Each partition is mounted to its own subdirectory
- Can modify `MOUNT_BASE` variable in code

## Dependencies

### Required

- `python3`: Python 3.x
- `python3-pyqt5`: Qt5 GUI library
- `udev`: Device management
- `util-linux`: blkid, mount, etc.

### Optional

- `ntfs-3g`: NTFS filesystem support (for Windows-formatted USB drives)
- `exfat-fuse`: exFAT filesystem support
- `kio-admin`: KDE Dolphin admin mode support

### NTFS Support

To mount NTFS-formatted USB drives, manually install ntfs-3g:

```bash
sudo apt-get install ntfs-3g
```

## Uninstall

```bash
sudo dpkg -r usb-manager
```

## File Description

- `usb-manager.py`: Main program
- `usb-passthrough.sh`: ADB device node creation script
- `usb-storage-passthrough.sh`: USB storage device node creation script
- `usb-manager.desktop`: Desktop shortcut
- `usb-manager`: Launch script
- `usb-storage`: sudoers configuration file

## License

MIT License
