# SSH Remote Administration

> **Project:** Enterprise Infrastructure Homelab
>
> **Category:** Linux Administration
>
> **Status:** Completed
>
> **Purpose:** Validate and demonstrate secure remote administration of an Ubuntu Server using OpenSSH within the homelab environment.

---

## Project Overview

This document demonstrates the verification, validation, and practical use of Secure Shell (SSH) for remote administration of the Ubuntu Server.

SSH is the standard protocol used by Linux system administrators to securely manage servers over a network. This project focuses on verifying the SSH service, validating network connectivity, and demonstrating secure remote administration from another machine within the homelab.

---

## Objectives

- Verify the OpenSSH Server installation.
- Validate the SSH service status.
- Confirm secure remote administration.
- Verify network connectivity.
- Test remote login from another machine.
- Practice Linux server administration over SSH.

---

## Environment

| Property | Value |
|----------|---------|
| Operating System | Ubuntu Server 26.04 LTS |
| SSH Software | OpenSSH Server |
| Client System | Kali Linux |
| Authentication | Username and Password |
| Network Mode | Bridged Adapter |

## Implementation

## Verify OpenSSH Installation
OpenSSH Server was selected during the Ubuntu Server installation process.
The following command was used to verify that the SSH service was installed, enabled, and running successfully.

### Command
```bash
sudo systemctl status ssh
```

> **Screenshot**
>
> <img width="728" height="342" alt="image" src="https://github.com/user-attachments/assets/3262ada9-0473-48d2-a16c-f50c36a3f0dd" />

---

## Verify SSH Service at Startup

The following command was used to verify that the SSH service was enabled to start automatically during system boot.

### Command

```bash
sudo systemctl is-enabled ssh
```

or

```bash
sudo systemctl status ssh
```

> **Screenshot**
>
> <img width="408" height="32" alt="image" src="https://github.com/user-attachments/assets/340b048e-2988-46cb-a085-1bafe860ae7e" />

---

## Verify Listening Port

The server was checked to confirm that SSH was listening for incoming connections on TCP port 22.

### Command

```bash
sudo ss -tln | grep :22
```

> **Screenshot**
>
> <img width="462" height="75" alt="image" src="https://github.com/user-attachments/assets/2e46c382-8212-47ad-8d7b-79c545731170" />

---

## Verify Network Connectivity

The server's IP address was first identified.

### Command
```bash
hostname -I
```
> **Screenshot**
>
>  <img width="507" height="30" alt="image" src="https://github.com/user-attachments/assets/b046372a-0b54-4f3f-a818-d475c40992ea" />

The server's IP address was then tested from another device on the same network to verify Layer 3 connectivity prior to establishing an SSH session.

### Command
```bash
ping 192.168.100.xxx
```

> **Screenshot**
>
> <img width="773" height="287" alt="image" src="https://github.com/user-attachments/assets/811d1e34-5737-4f84-9482-db98f1441c2c" />

---

## Connect from a Remote Machine

A secure SSH connection was established from a Kali Linux virtual machine using the server's IP address.

### Command

```bash
ssh marc@192.168.100.105
```

> **Screenshot**
>
> <img width="647" height="305" alt="image" src="https://github.com/user-attachments/assets/d0c32205-699e-4966-ad8c-c5940e0f62ed" />

---

## Verify Remote Administration

After authentication, administrative commands were executed remotely to verify successful access to the server.

### Commands
```bash
hostnamectl
whoami
pwd
```

> **Screenshot**
>
> <img width="517" height="337" alt="image" src="https://github.com/user-attachments/assets/8c670fcc-2ef1-4c76-88bb-1e4d8ff682c9" />

---

## Close the SSH Session

The SSH session was closed after administrative tasks were completed to terminate the secure remote connection properly.

### Command
```bash
exit
```

## Troubleshooting

## Unable to Connect via SSH

### Symptoms

- SSH connection timed out.
- Ubuntu Server could not be reached from the Kali Linux virtual machine.

### Root Cause

The Ubuntu Server virtual machine was configured to use a NAT network adapter, preventing direct communication with other devices on the local network.

### Resolution

The VirtualBox network adapter was changed from **NAT** to **Bridged Adapter**, allowing the Ubuntu Server to obtain an IP address on the local network and accept incoming SSH connections.

### Verification

Connectivity was verified by successfully pinging the server and establishing an SSH session from the Kali Linux virtual machine.

## Security Considerations

SSH provides encrypted communication between the client and server, helping protect authentication credentials and administrative sessions from interception.

Basic security practices include:

- Restrict administrative access to authorized users.
- Use strong passwords or SSH key authentication.
- Restrict SSH access using firewall rules where appropriate.
- Keep OpenSSH updated.
- Disable unused accounts.
- Review SSH logs regularly.

## Verification

| Task | Status |
|------|--------|
| OpenSSH Installed | ✅ |
| SSH Service Running | ✅ |
| SSH Enabled at Boot | ✅ |
| TCP Port 22 Listening | ✅ |
| Remote Login Successful | ✅ |
| Remote Administration Verified | ✅ |
| Network Connectivity Verified | ✅      |


## Observations

The SSH service was verified successfully and enabled secure remote administration of the Ubuntu Server.

Key observations include:

- SSH enables secure remote administration over encrypted connections.
- The server accepted remote authentication from another machine.
- Remote administration eliminates the need for direct physical access.
- Proper service verification ensures SSH availability after reboot.
- Successful SSH connectivity depends on both service availability and proper network configuration.

## Technical Competencies Demonstrated

- Linux System Administration
- Remote Server Administration
- OpenSSH Administration
- Linux Networking
- Service Management
- Authentication
- System Verification
- Technical Documentation

## Lessons Learned

This project reinforced the importance of secure remote administration within Linux environments.

Key takeaways include:

- SSH is the primary method of administering Linux servers remotely.
- Verifying service status confirms that SSH is operational before attempting remote administration.
- Network connectivity must be validated before troubleshooting SSH issues.
- Enabling services at boot improves operational reliability.
- Secure remote administration improves efficiency while maintaining system security.
- Understanding the underlying network configuration is essential when diagnosing remote connectivity issues.

---

## Repository Navigation

| ⬅ Previous | 🏠 Section Home | Next ➡ |
|------------|----------------|---------|
| [User and Group Management](03-user-group-management.md) | [Linux Server Deployment](README.md) | [Apache HTTP Server](05-apache-web-server.md) |
