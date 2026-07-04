# Server Information

> **Project:** Enterprise Infrastructure Homelab
>
> **Category:** Linux Server Deployment
>
> **Status:** Completed
>
> **Purpose:** Document the baseline hardware, operating system, and resource configuration of the Ubuntu Server used throughout the homelab.

 ## Project Overview

This document records the baseline specifications of the Ubuntu Server deployed within the Enterprise Infrastructure Homelab.

The collected information serves as a configuration baseline that can be referenced throughout future infrastructure projects, troubleshooting activities, and performance monitoring.

---

## Objectives

- Record baseline server specifications.
- Verify successful deployment.
- Establish a reference configuration.
- Document hardware and virtualization settings.
- Support future troubleshooting and monitoring activities.

---

## Network Information

### Command
```bash
ip addr show
```
>**Screenshot**
>
><img width="838" height="367" alt="image" src="https://github.com/user-attachments/assets/311e5992-b5b1-477e-b43a-ec6b45a5d2b9" />

| Property | Value |
|----------|-------|
| Hostname | ubuntu |
| IPv4 Address | 192.168.100.105 |
| Network Mode | Bridged Adapter |
| Interface | enp0s3 |

## CPU Information

### Command
```bash
lscpu
```
The server's processor configuration was verified using the `lscpu` command.
> **Screenshot**
>
><img width="678" height="257" alt="image" src="https://github.com/user-attachments/assets/ebe59eae-15ff-4aaa-be36-fa5dbe297fbe" />

### Processor

| Property | Value |
|----------|-------|
| CPU Model | AMD Ryzen 7 7730U with Radeon Graphics |
| Vendor | AuthenticAMD |
| CPU Family | 25 |
| Model | 80 |
| Architecture | x86_64 |
| CPU Modes | 32-bit, 64-bit |
| Endianness | Little Endian |

### Virtual CPU Allocation

| Property | Value |
|----------|-------|
| vCPUs | 4 |
| Online CPUs | 0-3 |
| Cores per Socket | 4 |
| Threads per Core | 1 |
| Socket(s) | 1 |
| NUMA Nodes | 1 |

## Memory Information

### Command
```bash
free -h
```
The server's memory configuration and utilization were verified using the `free -h` command.
>**Screenshot**
>
><img width="656" height="77" alt="image" src="https://github.com/user-attachments/assets/39e5cec2-f148-4800-82cb-d0a94740c09d" />

| Property | Value |
|----------|-------|
| Total RAM | 3.8 GiB |
| Used | 454 MiB |
| Free | 3.0 GiB |
| Shared | 1.1 MiB |
| Buff/Cache | 516 MiB |
| Available | 3.3 GiB |
| Swap | Disabled (0 B) |

## Storage Information

### Command
```bash
df -h
```
The storage layout and filesystem utilization were verified using the `df -h` command.
>**Screenshot**
>
><img width="658" height="177" alt="image" src="https://github.com/user-attachments/assets/b3bc5607-263c-4751-92e6-143135948c97" />


| Filesystem | Size | Used | Available | Usage | Mount Point |
|------------|------|------|-----------|-------|------------|
| `/dev/sda2` | 30 GB | 3.1 GB | 25 GB | 11% | `/` |
| `tmpfs` | 774 MB | 773 KB | 774 MB | 1% | `/run` |
| `tmpfs` | 1.9 GB | 0 B | 1.9 GB | 0% | `/dev/shm` |
| `tmpfs` | 1.9 GB | 0 B | 1.9 GB | 0% | `/tmp` |
| `tmpfs` | 387 MB | 8 KB | 387 MB | 1% | `/run/user/1000` |
| `tmpfs` | 387 MB | 8 KB | 387 MB | 1% | `/run/user/1001` |

## Virtualization Information

### Command
```bash
hostnamectl
```
The server's virtualization information was verified using the `hostnamectl` command.
>**Screenshot**
>
><img width="535" height="256" alt="image" src="https://github.com/user-attachments/assets/281f7f69-ff13-4400-9fbb-cd3b8b6ed8cf" />

| Property | Value |
|----------|-------|
| Virtualization Platform | Oracle VirtualBox |
| Hardware Version | 1.2 |
| Virtualization | Oracle |
| Hardware Vendor | innotek GmbH |
| Hardware Model | VirtualBox |

---

## Observations

The deployed Ubuntu Server is operating within expected resource limits.

Current observations include:

- CPU resources are sufficient for lightweight infrastructure workloads.
- Memory utilization remains low, leaving capacity for additional services.
- Root storage has adequate free space for future deployments.
- Swap is currently disabled.
- The server is suitable for hosting infrastructure services such as Apache, SSH, and Zabbix.
- The server provides sufficient resources for hosting additional homelab services without exceeding available system capacity.
- The baseline configuration documented here will serve as a reference for future troubleshooting, monitoring, and performance comparisons.

## Summary of Commands Used

The following Linux commands were used to collect the information documented in this file.

| Command | Purpose |
|---------|----------|
| df -h | Display filesystem usage |
| free -h | Display memory usage |
| hostnamectl | Display operating system and hardware information |
| lsb_release -a | Verify Ubuntu release information |
| lscpu | Display processor information |

---

## Repository Navigation

| ⬅ Previous | 🏠 Section Home | Next ➡ |
|----------|---------|------|
| [Ubuntu Server Deployment](01-ubuntu-server-installation.md) | [Linux Server Deployment](README.md) | Basic Linux Configuration |
