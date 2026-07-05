## Linux Filesystem

/
├── home
├── etc
├── var
├── usr
├── tmp
├── opt
├── boot
└── dev

### `/`

The root directory where the entire filesystem hierarchy begins.

As a user or administrator, I understand that every single file, folder, and mounted drive on my system branches off from this single starting point.


### `/boot`

Contains the essential files needed to start the operating system, including the kernel and bootloader configurations.

As an administrator, I rarely touch this directory unless I am troubleshooting startup issues, configuring GRUB, or installing a custom kernel.


### `/dev`

Holds special device files that represent the physical hardware components attached to the system.

As an administrator, I access this directory when I need to partition a new hard drive (`/dev/sda`), mount a USB stick, or interact directly with hardware.


### `/etc`

Stores system-wide configuration files.

As an administrator, I will frequently modify files in this directory when configuring services such as SSH, Nginx, and Samba.


### `/home`

Contains the personal directories, files, and hidden application settings for individual users.

As a regular user, I spend most of my time here organizing my personal documents, downloads, and custom scripts.


### `/opt`

Reserved for the installation of optional, add-on, or third-party software packages.

As an administrator, I check this directory when managing manually installed, self-contained applications like commercial VPNs, proprietary databases, or standalone web browsers.


### `/tmp`

Serves as a temporary storage space for files created by the system and running applications.

As a user or developer, I use this space for quick scratch-work, expecting that the files I place here will usually be automatically deleted when the system reboots.


### `/usr`

Stores the majority of installed user applications, shared libraries, source code, and read-only system data.

As an administrator, I know that when I install standard software via the package manager, its executable commands usually end up in `/usr/bin`.


### `/var`

Holds variable data files that are expected to grow and change frequently during system operation, such as logs, caches, and print queues.

As an administrator, this is my first stop for troubleshooting, as I regularly check `/var/log` to investigate system errors, security audits, or service failures.

## Company Data Directory

The server stores departmental data under:

```text
/srv/company-data/
```

Structure:

```text
company-data/
├── HR/
├── Accounting/
├── IT/
├── Public/
├── Sales/
└── Shared/
```

Purpose:

- HR — Employee documents
- Accounting — Financial files
- IT — Administrative scripts and backups
- Public — Files accessible to all users
- Sales — Company sales and revenue
- Shared — Collaboration folder
