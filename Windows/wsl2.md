# WSL

## Setup the virtual machine feature

Open **PowerShell** as **Administrator and run this command:

```bash
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```
cf.: [Windows Subsystem for Linux Installation Guide for Windows 10](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

Download the [Linux Kernel Update](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

Set wsl to version 2:

```bash
wsl --set-default-version 2
```

---

## Install Arch Linux 

Download the bootstrap image [archlinux-bootstrap](https://ftp.halifax.rwth-aachen.de/archlinux/iso/latest/)

Extract and repackage it:

```bash
tar -zxvf archlinux-bootstrap-<version>-x86_64.tar.gz
cd root.x86_64
tar -zcvf arch_bootstrap.tar.gz .
```

Import the Arch Linux bootstrap image:

```bash
wsl --import Arch C:\Users\Michael\WSL2\Arch C:\Users\Michael\WSL2\Arch\arch_bootstrap.tar.gz
```

Install Arch Linux:

- Launch the installation: `wsl -d Arch`
- Initialize the keyring required to run pacman: `pacman-key --init`
- Fill the new keyring with Arch's latest set of keys: `pacman-key --populate archlinux`
- Pacman's mirrorlist is already installed but entirely commented out. Fetch a new one and override the existing one: `curl "https://archlinux.org/mirrorlist/?country=US&protocol=https&ip_version=4&use_mirror_status=on" | cut -c 2- > /etc/pacman.d/mirrorlist`
- Update the repos and install the latest packages: `pacman -Syu`
- There will also be a handful of missing "base" packages that are always useful to have and can be installed with: `pacman -S base base-devel`

```bash
useradd -m -g users -G wheel,audio,video,disk,storage,optical,scanner,rfkill,input -s /bin/bash michael
passwd michael
```

### Add Arch Linux to Windows Terminal

Open the settings menu of windows terminal:

- Name: Arch Linux Michael
- Command Line: `wsl ~ -u michael`
- Starting directory: `%USERPROFILE%` (remove the tick under *Use parent process directory*)
- Choose your own *Icon*
- Choose your own *Tab title*