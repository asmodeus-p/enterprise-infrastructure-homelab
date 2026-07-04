# SSH Remote Administration

> **Project:** Enterprise Infrastructure Homelab
>
> **Category:** Linux Administration
>
> **Status:** Completed
>
> **Purpose:** Configure and verify Secure Shell (SSH) to enable secure remote administration of the Ubuntu Server from other devices within the homelab.

---

## Project Overview

This document demonstrates the configuration and validation of Secure Shell (SSH) for remote administration of the Ubuntu Server.

SSH is the standard protocol used by Linux system administrators to securely manage servers over a network. Configuring SSH allows administrators to remotely access systems, perform maintenance tasks, deploy services, and troubleshoot issues without requiring direct physical access.

---

## Objectives

- Install and configure OpenSSH Server.
- Verify the SSH service status.
- Enable secure remote administration.
- Validate network connectivity.
- Test remote login from another machine.
- Practice basic SSH administration.

---

## Environment

| Property | Value |
|----------|---------|
| Operating System | Ubuntu Server 26.04 LTS |
| SSH Software | OpenSSH Server |
| Client System | Kali Linux |
| Authentication | Username and Password |
| Network Mode | Bridged Adapter |

# Implementation

## Verify OpenSSH Installation
Standard Ubuntu Server installations commonly come with the OpenSSH server pre-installed and enabled.
The following command was used to verify that the SSH service was installed and running.

### Command
```bash
sudo systemctl status ssh
```

> **Screenshot**
>
> <img width="728" height="342" alt="image" src="https://github.com/user-attachments/assets/3262ada9-0473-48d2-a16c-f50c36a3f0dd" />

---

## Verify SSH Service at Startup

The SSH service was configured to start automatically during system boot. The following command verified that the service was enabled.

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

Before attempting remote administration, the server's network connectivity and IP address were verified.

### Commands

```bash
hostname -I
```

```bash
ping 192.168.100.xxx
```

> **Screenshot**
>
>  <img width="507" height="30" alt="image" src="https://github.com/user-attachments/assets/b046372a-0b54-4f3f-a818-d475c40992ea" />

Check if the IP address of the server is reachable by pinging from another device in the same network:

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
```

```bash
whoami
```

```bash
pwd
```

> **Screenshot**
>
> <img width="517" height="337" alt="image" src="https://github.com/user-attachments/assets/8c670fcc-2ef1-4c76-88bb-1e4d8ff682c9" />

---

## Close the SSH Session

The SSH session was terminated after completing administrative tasks.

### Command

```bash
exit
```

# Security Considerations

SSH provides encrypted communication between the client and server, helping protect authentication credentials and administrative sessions from interception.

Basic security practices include:

- Restrict administrative access to authorized users.
- Keep OpenSSH updated.
- Disable unused accounts.
- Use strong passwords or SSH key authentication.
- Review SSH logs regularly.

# Verification

| Task | Status |
|------|--------|
| OpenSSH Installed | ✅ |
| SSH Service Running | ✅ |
| SSH Enabled at Boot | ✅ |
| TCP Port 22 Listening | ✅ |
| Remote Login Successful | ✅ |
| Remote Administration Verified | ✅ |

## Observations

The SSH service was configured successfully and allowed secure remote administration of the Ubuntu Server.

Key observations include:

- SSH enables secure remote administration over encrypted connections.
- The server accepted remote authentication from another machine.
- Remote administration eliminates the need for direct physical access.
- Proper service verification ensures SSH availability after reboot.

## Technical Competencies Demonstrated

- Linux System Administration
- OpenSSH Administration
- Remote Server Management
- Service Management
- Linux Networking
- Authentication
- System Verification
- Technical Documentation

## Lessons Learned

This project reinforced the importance of secure remote administration within Linux environments.

Key takeaways include:

- SSH is the primary method of administering Linux servers remotely.
- Verifying service status is an important step after installation.
- Network connectivity must be validated before troubleshooting SSH issues.
- Enabling services at boot improves operational reliability.
- Secure remote administration improves efficiency while maintaining system security.

---

## Repository Navigation

| ⬅ Previous | 🏠 Section Home | Next ➡ |
|------------|----------------|---------|
| [User and Group Management](04-user-group-management.md) | [Linux Server Deployment](README.md) | [Apache HTTP Server](06-apache-web-server.md) |
