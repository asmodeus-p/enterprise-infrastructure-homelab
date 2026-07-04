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

> **Purpose**
>
> This document records the deployment and validation of the primary Linux infrastructure server used throughout the Enterprise Infrastructure Homelab.
>
> Rather than focusing solely on operating system installation, this documentation emphasizes deployment validation, operational readiness, and repeatable infrastructure practices.

## Table of Contents

- [Project Overview](#project-overview)
- [Architecture Diagram](#architecture-diagram)
- [Objectives](#objectives)
- [Environment](#environment)
- [Deployment Process](#deployment-process)
- [Deployment Verification](#deployment-verification)
- [Skills Demonstrated](#skills-demonstrated)
- [Lessons Learned](#lessons-learned)
- [Post-Deployment Configuration](#post-deployment-configuration)
- [Next Project](#next-project)

## Project Information

| Property | Value |
|----------|---------|
| Estimated Deployment Time | ~30–45 minutes |
| Difficulty | Beginner–Intermediate |
| Environment | Homelab |

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
Ubuntu Server 26.04 LTS
        │
        ├── OpenSSH Server
        ├── Apache HTTP Server
        ├── Zabbix Server
        └── Infrastructure Services
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

## Implementation

### Create Virtual Machine

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

### Install Ubuntu Server

The Ubuntu Server LTS ISO was installed using the standard installation wizard.

The deployment included:

- Administrator account creation
- Disk partitioning
- Network configuration
- OpenSSH Server installation
- Initial system configuration

Following installation, the server was rebooted and verified before post-installation configuration.

---

### Initial Login

The server was successfully accessed using the administrator account created during installation.

Successful login confirmed that the operating system had been installed correctly and was ready for post-deployment configuration.

---

### Verify Installation

Basic system information was verified to ensure the installation completed successfully.

```bash
hostnamectl
```
> **Screenshot**
>
> <img width="547" height="255" alt="image" src="https://github.com/user-attachments/assets/7553360b-7fa6-4f00-9ad8-adbb90d624f8" />

```bash
lsb_release -a
```
> **Screenshot**
>
> <img width="517" height="92" alt="image" src="https://github.com/user-attachments/assets/761842f4-358a-4c54-b2ad-820ad35b9648" />

```bash
uname -r
```
> **Screenshot**
>
> <img width="502" height="35" alt="image" src="https://github.com/user-attachments/assets/1567012a-259c-4854-aa9d-bf3c1a382cd0" />


```bash
hostname -I
```
> **Screenshot**
>
> <img width="511" height="30" alt="image" src="https://github.com/user-attachments/assets/adf4a794-407a-462b-8ece-cd4bb29ec799" />


The following commands were executed to verify the successful deployment of the operating system and collect baseline system information.

| Command | Purpose |
|---------|---------|
| `hostnamectl` | Display system hostname, operating system, kernel version, virtualization platform, and hardware information. |
| `hostname -I` | Verify the assigned IP address. |
| `lsb_release -a` | Confirm the Ubuntu distribution and release version. |
| `uname -r` | Verify the running Linux kernel version. |

---

### Update the Server

The package repository was refreshed and installed packages were upgraded to ensure the server was running the latest available software.

```bash
sudo apt update
```

```bash
sudo apt upgrade -y
```

System packages were successfully updated without errors.

---

### Verify Network Connectivity

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

> **Screenshot**
>
> <img width="850" height="135" alt="image" src="https://github.com/user-attachments/assets/ed4adf7c-ba84-4e68-af1a-9a664f61b02b" />


### Validation Criteria

The connectivity test was considered successful after confirming:

- Successful ICMP communication with external hosts.
- Successful DNS name resolution.
- Stable network connectivity through the Bridged Adapter.

---

### Deployment Verification

The deployment was verified using standard Linux system utilities.

Verification confirmed:

| Validation | Status |
|------------|--------|
| Ubuntu Server Installed | ✅ |
| Kernel Verified | ✅ |
| Network Connectivity | ✅ |
| DNS Resolution | ✅ |
| IP Address Assigned | ✅ |
| Virtualization Detected | ✅ |
| Package Manager Functional | ✅ |

---

## Conclusion

The Ubuntu Server deployment was successfully completed and validated.

The server now provides a stable Linux environment that serves as the foundation for all infrastructure projects within this repository, including remote administration, web hosting, monitoring, and future network services.

---

## Technical Competencies Demonstrated

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
- Consistent documentation improves troubleshooting and long-term maintainability.

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

## References

- Ubuntu Server Documentation
- Oracle VirtualBox Documentation
- OpenSSH Documentation

---

## Next Project

➡️ **Repository Navigation**

The next document covers the server specifications, hardware information, operating system details, and baseline system configuration used throughout the homelab.

| Previous | Current | Next |
|----------|---------|------|
| — | **Ubuntu Server Deployment** | [02-server-information.md](Server Information) |
