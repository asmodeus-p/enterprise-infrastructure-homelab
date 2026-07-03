# Ubuntu Server Deployment
> **Project:** Enterprise Infrastructure Homelab
>
> **Category:** Linux Server Deployment
>
> **Status:** Completed
>
> **Platform:** Oracle VirtualBox
>
> **Operating System:** Ubuntu Server 26.04 LTS

## Project Overview

This document describes the deployment and initial configuration of an Ubuntu Server within my Enterprise Infrastructure Homelab.

The server acts as the primary infrastructure host supporting Linux administration, remote management, web services, and infrastructure monitoring. It provides the foundation for subsequent projects including Apache HTTP Server, Zabbix monitoring, SSH administration, and network troubleshooting.

---

## Architecture Diagram

```text
Windows 11 Host
        │
        ▼
Oracle VirtualBox
        │
        ▼
Ubuntu Server
        │
        ├── OpenSSH
        ├── Apache HTTP Server
        ├── Zabbix Server
        └── Future Infrastructure Services
```
 
---

## Objectives

- Deploy Ubuntu Server in a virtualized environment
- Configure a stable Linux server for administration tasks
- Prepare the server for remote management using SSH
- Establish a foundation for future infrastructure services
- Document the deployment process using professional technical documentation

---

## Environment

| Component | Details |
|-----------|---------|
| Operating System | Ubuntu Server 26.04 LTS |
| Deployment Type | Virtual Machine |
| Virtualization Platform | Oracle VirtualBox |
| Host Operating System | Windows 11 |
| Server Role | Infrastructure Server |
| Network Mode | Bridged Adapter |
| Architecture | x86_64 |

---

## Deployment Process

### 1. Create Virtual Machine

A new virtual machine was created in Oracle VirtualBox with the following specifications:

| Setting | Value |
|----------|-------|
| Name | Ubuntu Server LTS |
| Type | Linux |
| Version | Ubuntu (64-bit) |
| Memory | 4573 MB |
| CPU | 4 Cores |
| Storage | 30.00 GB |

> **Screenshot**
>
> <img width="792" height="637" alt="image" src="https://github.com/user-attachments/assets/c85ec855-7b18-4799-abfd-e9a8ff734128" />

### Configuration Rationale

The virtual machine was provisioned with sufficient CPU, memory, and storage resources to support Linux administration, web hosting, and infrastructure monitoring services. A Bridged Network Adapter was selected to allow direct communication with other devices on the local network.

---

### 2. Install Ubuntu Server

The Ubuntu Server LTS ISO was installed using the standard installation wizard.

The deployment included:

- Administrator account creation
- Disk partitioning
- Network configuration
- OpenSSH Server installation
- Initial system configuration

Following installation, the server was rebooted and verified before post-installation configuration.

---

### 3. Initial Login

The server was successfully accessed using the administrator account created during installation.

Successful login confirmed that the operating system had been installed correctly and was ready for post-deployment configuration.

---

### 4. Verify Installation

Basic system information was verified to ensure the installation completed successfully.

```bash
hostnamectl
```
<img width="547" height="255" alt="image" src="https://github.com/user-attachments/assets/7553360b-7fa6-4f00-9ad8-adbb90d624f8" />

```bash
lsb_release -a
```
<img width="517" height="92" alt="image" src="https://github.com/user-attachments/assets/761842f4-358a-4c54-b2ad-820ad35b9648" />

```bash
uname -r
```
<img width="502" height="35" alt="image" src="https://github.com/user-attachments/assets/1567012a-259c-4854-aa9d-bf3c1a382cd0" />


```bash
hostname -I
```
<img width="511" height="30" alt="image" src="https://github.com/user-attachments/assets/adf4a794-407a-462b-8ece-cd4bb29ec799" />


The following commands were executed to verify the successful deployment of the operating system and collect baseline system information.

| Command | Purpose |
|---------|---------|
| `hostnamectl` | Display system hostname, operating system, kernel version, virtualization platform, and hardware information. |
| `hostname -I` | Verify the assigned IP address. |
| `lsb_release -a` | Confirm the Ubuntu distribution and release version. |
| `uname -r` | Verify the running Linux kernel version. |

---

### 5. Update the Server

The package repository was refreshed and installed packages were upgraded to ensure the server was running the latest available software.

```bash
sudo apt update
```

```bash
sudo apt upgrade -y
```

System packages were successfully updated without errors.

---

### 6. Verify Network Connectivity

Connectivity was tested to confirm network access.

```bash
ping google.com
```

```bash
ping ubuntu.com
```

```bash
ping 8.8.8.8
```

Expected result:

- Successful DNS resolution
- Successful Internet connectivity

---

### Deployment Verification

The deployment was verified using standard Linux system utilities.

Verification confirmed:

- Ubuntu Server 26.04 LTS installed successfully
- Linux Kernel 7.0.0-27-generic running
- Oracle VirtualBox virtualization detected
- VirtualBox hardware model recognized
- Server assigned a valid IPv4 address
- System architecture identified as x86_64
---

## Result

The Ubuntu Server deployment was successfully completed.

The server was operational and ready for additional infrastructure services including:

- SSH Remote Administration
- Apache HTTP Server
- Zabbix Monitoring
- Future network services

---

## Skills Demonstrated

- Ubuntu Server Deployment
- Linux System Administration
- Virtual Machine Configuration
- Package Management
- Network Configuration
- Operating System Validation
- Infrastructure Documentation
- Linux Command Line

---

## Lessons Learned

This project reinforced the importance of establishing a stable server foundation before deploying additional infrastructure services.

Key takeaways include:

- Careful planning of virtual machine resources improves system stability.
- Verifying system health immediately after installation helps identify configuration issues early.
- Updating packages before deploying services reduces compatibility and security risks.
- Structured technical documentation improves reproducibility and simplifies future maintenance.

This deployment established the foundation for the remaining projects within the Enterprise Infrastructure Homelab.

---

## Post-Deployment Configuration

Following installation, the server was prepared for future infrastructure services by performing the following tasks:

- Updated installed packages
- Verified network connectivity
- Verified operating system information
- Confirmed SSH installation
- Validated Internet connectivity

---

## Next Project

➡️ **Server Information**

The next document covers the server specifications, hardware information, operating system details, and baseline system configuration used throughout the homelab.
