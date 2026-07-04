# User and Group Management

> **Project:** Enterprise Infrastructure Homelab
>
> **Category:** Linux Administration
>
> **Status:** Completed
>
> **Purpose:** Demonstrate Linux user and group administration by creating user accounts, managing groups, assigning permissions, and verifying user access within an Ubuntu Server environment.

---

## Project Overview

This document demonstrates fundamental Linux user and group administration tasks performed within the Ubuntu Server environment.

User and group management is a fundamental responsibility of Linux system administrators. Proper account management helps enforce security policies, organize user permissions, and implement the principle of least privilege.

---

## Objectives

- Create local user accounts.
- Create and manage Linux groups.
- Assign users to appropriate groups.
- Verify account configuration.
- Understand Linux permission management.
- Practice administrative account management.

---

## Environment

| Property | Value |
|----------|---------|
| Operating System | Ubuntu Server 26.04 LTS |
| Platform | Oracle VirtualBox |
| User Privileges | sudo |
| Shell | Bash |

# Implementation

## Create User

The `adduser` command creates a new local user account and automatically generates the user's home directory, default shell configuration, and user-specific configuration files.

### Command

```bash
sudo adduser alice
```

> **Screenshot**
>
> <img width="413" height="190" alt="Screenshot 2026-06-27 223634" src="https://github.com/user-attachments/assets/0f07893d-9f07-4174-b1f7-5b3cd90c4661" />

---

## Create Group

A dedicated Linux group was created to organize users with similar responsibilities and simplify permission management.

### Command

```bash
sudo groupadd HR
```

> **Screenshot**
>
> <img width="320" height="58" alt="Screenshot 2026-06-27 224213" src="https://github.com/user-attachments/assets/ad7cc329-5729-4656-81ed-aa469dc58eab" />

---

## Add User to Group

The user was added to the **HR** group using the `usermod` command.

The `-aG` option appends the user to an existing supplementary group without removing any existing group memberships.

### Command

```bash
sudo usermod -aG HR alice
```

> **Screenshot**
>
> <img width="628" height="215" alt="Assigning Groups to Users" src="https://github.com/user-attachments/assets/041a0697-ccfb-4937-b4a5-eec959ff5b1d" />

---

## Verify Group Membership

Group membership was verified to ensure that the user had been successfully assigned to the intended group.

### Commands

```bash
groups alice
```

or

```bash
id alice
```

> **Screenshot**
>
> <img width="342" height="37" alt="image" src="https://github.com/user-attachments/assets/2fc8b161-f6e2-4345-bc37-82f39a9ca873" />

---

## Switch User

The newly created account was accessed to verify that the user could successfully authenticate and log in to the system.

### Command

```bash
su - alice
```

> **Screenshot**
>
> <img width="463" height="42" alt="image" src="https://github.com/user-attachments/assets/8de482d6-8867-483c-9cce-af04e1a09d35" />

---

## User Information

The `getent passwd` command retrieves user account information from the system's configured name service database, including entries stored in `/etc/passwd`. This method is preferred because it works consistently across both local and centralized authentication environments.

Verification confirmed that the newly created user account exists within the operating system.

### Command

```bash
getent passwd | awk -F: '$3 >= 1000 && $1 != "nobody" {print $1}'
```

> **Screenshot**
>
> <img width="666" height="102" alt="image" src="https://github.com/user-attachments/assets/7cb321bf-0d28-40c8-b81e-1306a7757b88" />

---

# Permission Management

Linux permissions determine which users can read, write, or execute files and directories.

Permission assignments are divided into three categories:

- **Owner** — The user who owns the file.
- **Group** — Members of the assigned group.
- **Others** — All remaining users.

The `ls -l` command is commonly used to display file and directory permissions.

To demonstrate this, the root directory (`/`) was listed using the following command.

### Command

```bash
ls -l /
```

> **Screenshot**
>
> <img width="582" height="126" alt="image" src="https://github.com/user-attachments/assets/73d41157-8475-40c0-a616-213294639e6a" />

Example permission string:

```text
-rwxr-xr--
```

Meaning:

| Entity | Permission |
|----------|------------|
| Owner | Read, Write, Execute |
| Group | Read, Execute |
| Others | Read |

---

# Verification

| Task | Status |
|-------|--------|
| User Created | ✅ |
| Group Created | ✅ |
| User Added to Group | ✅ |
| Group Membership Verified | ✅ |
| User Authentication Verified | ✅ |
| User Information Verified | ✅ |

---

## Observations

The user and group administration tasks were completed successfully.

Key observations include:

- Linux stores user account information within `/etc/passwd`.
- Group membership simplifies permission management.
- The `sudo` privilege should be granted only when necessary.
- Verifying group membership helps prevent configuration errors.
- Proper account management supports secure system administration.
- Linux groups provide a scalable method of managing permissions for multiple users.

---

## Technical Competencies Demonstrated

- Linux System Administration
- Linux User Administration
- Linux Group Administration
- Permission Management
- User Authentication
- Linux CLI
- Account Verification
- Technical Documentation

---

## Lessons Learned

This project reinforced the importance of structured account management within Linux systems.

Key takeaways include:

- User accounts should follow the principle of least privilege.
- Groups simplify permission administration.
- Administrative changes should always be verified after implementation.
- Proper documentation improves maintainability and troubleshooting.
- Consistent user and group naming conventions simplify long-term system administration.

---

## Repository Navigation

| ⬅ Previous | 🏠 Section Home | Next ➡ |
|------------|----------------|---------|
| [Server Information](02-server-information.md) | [Linux Server Deployment](README.md) | [SSH Remote Administration](05-ssh-configuration.md) |
