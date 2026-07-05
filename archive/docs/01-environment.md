# Ubuntu Server Documentation

## System Overview

| Property | Value |
|----------|-------|
| Hostname | `ubuntu` |
| Operating System | Ubuntu 26.04 LTS |
| Release | 26.04 |
| Codename | Resolute |
| Kernel | Linux 7.0.0-27-generic |
| Architecture | x86_64 |
| Virtualization | Oracle VirtualBox |
| Hypervisor | KVM (Guest CPU) |
| Hardware Vendor | innotek GmbH |
| Hardware Model | VirtualBox |

---

# CPU Information

## Processor

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

---

# Memory Information

| Property | Value |
|----------|-------|
| Total RAM | 3.8 GiB |
| Used | 454 MiB |
| Free | 3.0 GiB |
| Shared | 1.1 MiB |
| Buff/Cache | 516 MiB |
| Available | 3.3 GiB |
| Swap | Disabled (0 B) |

---

# Storage Information

## Filesystem Usage

| Filesystem | Size | Used | Available | Usage | Mount Point |
|------------|------|------|-----------|-------|------------|
| `/dev/sda2` | 30 GB | 3.1 GB | 25 GB | 11% | `/` |
| `tmpfs` | 774 MB | 773 KB | 774 MB | 1% | `/run` |
| `tmpfs` | 1.9 GB | 0 B | 1.9 GB | 0% | `/dev/shm` |
| `tmpfs` | 1.9 GB | 0 B | 1.9 GB | 0% | `/tmp` |
| `tmpfs` | 387 MB | 8 KB | 387 MB | 1% | `/run/user/1000` |
| `tmpfs` | 387 MB | 8 KB | 387 MB | 1% | `/run/user/1001` |

---

# Virtualization Information

| Property | Value |
|----------|-------|
| Virtualization Platform | Oracle VirtualBox |
| Hypervisor Vendor | KVM |
| Virtualization Type | Full |
| Hardware Vendor | innotek GmbH |
| Hardware Model | VirtualBox |

---

# Machine Information

| Property | Value |
|----------|-------|
| Static Hostname | ubuntu |
| Icon Name | computer-vm |
| Chassis | VM |
| Machine ID | `28f61fc42e224776a7734a89a9c86ffa` |
| Boot ID | `96f9dcf857ee497ca98cc66b56fbd8b6` |
| Firmware Version | VirtualBox |
| Firmware Date | Fri 2006-12-01 |
| Firmware Age | 19 years, 6 months, 3 days |

---

# Security Status

## CPU Vulnerability Summary

| Vulnerability | Status |
|--------------|--------|
| Gather Data Sampling | Not affected |
| Ghostwrite | Not affected |
| Indirect Target Selection | Not affected |
| L1TF | Not affected |
| MDS | Not affected |
| Meltdown | Not affected |
| MMIO Stale Data | Not affected |
| Old Microcode | Not affected |
| Register File Data Sampling | Not affected |
| Retbleed | Not affected |
| Spec Store Bypass | Not affected |
| Spectre v1 | Mitigated |
| Spectre v2 | Mitigated |
| SRBDS | Not affected |
| TSX Async Abort | Not affected |
| VMCSApe | Not affected |
| Speculative Stack Overflow | Vulnerable (Safe RET, no microcode) |
| TSA | Vulnerable (No microcode) |

---

# CPU Features

- x86_64 Architecture
- 32-bit and 64-bit support
- AMD-V Virtualization Extensions
- SSE, SSE2, SSE3, SSE4.1, SSE4.2
- AVX
- AVX2
- AES-NI
- FMA
- BMI1 / BMI2
- SHA Extensions
- RDRAND
- RDSEED

---

# Resource Summary

| Resource | Configuration |
|----------|---------------|
| CPU | 4 vCPUs |
| RAM | 4 GB (3.8 GiB usable) |
| Storage | 30 GB Root Partition |
| Swap | Disabled |
| OS | Ubuntu Server 26.04 LTS |
| Kernel | Linux 7.0.0-27-generic |
| Virtualization | Oracle VirtualBox |

---

# Notes

- Running as a VirtualBox guest.
- CPU passthrough exposes the host AMD Ryzen 7 7730U processor.
- Swap is currently disabled.
- Root filesystem has approximately **25 GB** of free space.
- Memory usage is low (~12%), leaving sufficient resources for additional services.
- Suitable for lightweight server workloads such as:
  - SSH Server
  - Nginx/Apache
  - Docker
  - Samba
  - DNS Server
  - DHCP Server
  - Monitoring tools (Prometheus, Grafana)
  - Small homelab services

---

## Commands Used

```bash
hostnamectl
lsb_release -a
lscpu
free -h
df -h
```
