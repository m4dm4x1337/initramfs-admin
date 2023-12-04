# Initramfs-Admin

## Description

### Text-based user interface for the initramfs

This package adds functionality to an initramfs built by initramfs-tools. When installed and enabled, the initramfs will display a grafical user interface which can be controlled with keyboard inputs.

Features include a network manager for LAN and WiFi, a crypto manager to manage LUKS keys, and to re-encrypt and resize a crypto partition. It is also possible to chroot to the root file system and to make changes to the system. This is particularly useful with a portable overlayfs protected root file system that normally does not allow changes. Many other features are available.

## Installation

**This package is primarily intended for Ubuntu/Debian systems that have an encrypted root partition. If you do not have an encrypted system, you should NOT INSTALL this package!**

Download the Debian package and run this commands:

```bash
sudo dpkg -i initramfs-admin_1.0_all.deb || sudo apt-get -f install
```

A quirk of this package is that it has soft dependencies instead of hard dependencies, so it is up to the user how much the initramfs grows by installing or not installing these soft dependencies.

If you want to make sure that all features are available install the following packages:

```bash
apt install \
  cmatrix \
  e2fsprogs \
  htop \
  lynx \
  mc \
  nano \
  netdiscover \
  openssh-client \
  openssh-server \
  parted \
  sharutils \
  util-linux
```

To have WiFi support in Initramfs, it is also recommended to install [Initramfs-Wifi](https://github.com/m4dm4x1337/initramfs-wifi).

Since this package can currently only be used for encrypted systems, it is assumed that the packages `cryptsetup`, `cryptsetup-initramfs` and `lvm2` are already installed.

## Configuration

Initramfs-Admin is an init script that must be activated explicitly via the kernel cmdline. The kernel parameter that causes activation is `initramfs-admin`.

Three execution modes are available:

* **Init script mode** - The script is executed directly on the screen when the computer boots up if the kernel cmdline parameter `initramfs-admin=yes` was found.

* **Dropbear command mode** - The script is executed as the dropbear command if the kernel cmdline parameter `initramfs-admin=dropbear` was found. This works even if you have a completely different command configured in dropbear.

* **Shell script mode** - The script is executed as a normal shell script by running the command `initramfs-admin` in a busybox shell.

## Changing the kernel cmdline

How to change the kernel cmdline depends on your hardware and/or software. If you are using a Raspberry Pi you need to change the file `cmdline.txt` in your `/boot` directory. If you are using grub as bootloader you need to change the kernel parameters in the variable `GRUB_CMDLINE_LINUX` in the file `/etc/default/grub`. The part that you need to add is:

```text
initramfs-admin=dropbear
```

or

```text
initramfs-admin=yes
```

depending on how you usually unlock your computer.

If you are using grub, then run `update-grub` afterwards.

## Usage

Restart, and if you are using dropbear, connect to dropbear and the graphical user interface should appear. Otherwise, if you have physical access to the computer and see the screen in front of you, wait for the graphical interface to appear during boot.

## Contributing

Contributions are welcome! Feel free to fork this repository and submit pull requests.

## License

This project is licensed under the GPLv3 License. See the COPYING file for details.

## Author

The Initramfs-Admin Debian package was created by m4dm4x1337.

## Donations 🥺

 ❤️ Please donate ❤️

![QR code for donations](https://raw.githubusercontent.com/m4dm4x1337/tor-router-gnome/master/tor-router-gnome/usr/share/pixmaps/tor-router-gnome-donation.png)

This project is open source, and the only income comes from the donators. If you like the project, please donate, thank you!

[bitcoin:bc1q9ha0l0tt7dghcpgext8jppejandefeshcukpxx](bitcoin:bc1q9ha0l0tt7dghcpgext8jppejandefeshcukpxx)
