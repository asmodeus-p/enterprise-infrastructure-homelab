# Apache HTTP Server

> **Project:** Enterprise Infrastructure Homelab
>
> **Category:** Linux Services
>
> **Status:** Completed
>
> **Purpose:** Deploy, configure, validate, and manage the Apache HTTP Server to provide web services within the Ubuntu Server homelab environment.

---

## Project Overview

This document demonstrates the deployment, configuration, validation, and administration of the Apache HTTP Server on Ubuntu Server.

Apache HTTP Server is one of the most widely used web servers in enterprise environments. Deploying a web server provides practical experience with Linux service management, package administration, network connectivity, service verification, and operational validation.

This project also demonstrates the process of verifying service availability after deployment and following infrastructure recovery activities.

---

## Objectives

- Install Apache HTTP Server.
- Verify the Apache service status.
- Confirm automatic service startup.
- Validate HTTP service availability.
- Verify local and remote web access.
- Practice Linux service administration.

---

## Environment

| Property | Value |
|----------|---------|
| Operating System | Ubuntu Server 26.04 LTS |
| Web Server | Apache HTTP Server |
| Package Manager | APT |
| Service Manager | systemd |
| Client Devices | Kali Linux / Windows Host |
| Service Port | TCP 80 |
| Network Mode | Bridged Adapter |

---

# Deployment Procedure

## Install Apache HTTP Server

Apache HTTP Server was installed using Ubuntu's Advanced Package Tool (APT). The package manager automatically downloaded and installed Apache along with its required dependencies.

### Command

```bash
sudo apt update
sudo apt install apache2
```

> **Screenshot**
>
> <img width="785" height="398" alt="image" src="https://github.com/user-attachments/assets/5b9eb0e6-a1e3-422d-a9a2-070bd52caf4b" />

---

## Verify Apache Service

After installation, the Apache service was verified to ensure that it started successfully and was operating normally.

### Command

```bash
sudo systemctl status apache2
```

> **Screenshot**
>
> <img width="982" height="301" alt="image" src="https://github.com/user-attachments/assets/63b615af-5952-4753-aa5f-1e0afe206de6" />

---

## Verify Automatic Startup

The Apache service was verified to ensure that it would automatically start during system boot.

### Command

```bash
sudo systemctl is-enabled apache2
```

> **Screenshot**
>
> <img width="406" height="32" alt="image" src="https://github.com/user-attachments/assets/cbe12f13-73d6-4800-ab1f-2e97beb0ac4a" />

---

## Verify Listening Port

After confirming that the service was running, the server was checked to verify that Apache was actively listening for incoming HTTP connections on TCP port 80.

### Command

```bash
sudo ss -tln | grep :80
```

> **Screenshot**
>
> <img width="497" height="73" alt="image" src="https://github.com/user-attachments/assets/fabe7141-641f-45cb-a77c-389997104f72" />

---

## Verify Local Web Service

The default Apache web page was retrieved locally to verify that the web server was functioning correctly before testing remote client access.

### Command

```bash
curl http://localhost
```

or

```bash
wget -qO- http://localhost
```

> **Screenshot**
>
> <img width="1452" height="528" alt="image" src="https://github.com/user-attachments/assets/01add14a-9505-40d0-8617-409598fc92a5" />

---

## Verify Remote Access

The server's IP address was identified and used to access the Apache default page from another device on the local network.

### Command

```bash
hostname -I
```

> **Screenshot**
>
> <img width="293" height="31" alt="image" src="https://github.com/user-attachments/assets/b6831e2a-a9eb-4ba5-a1a0-ae045dfe4810" />

The web server was then accessed remotely using a web browser.

Example:

```text
http://192.168.100.108
```

> **Screenshot**
>
> <img width="1918" height="1021" alt="image" src="https://github.com/user-attachments/assets/9590f1f3-5034-43ae-9093-749f50501672" />

Successful access confirmed that:

- Apache was operational.
- TCP port 80 was reachable.
- The web service was accessible from another device on the network.

---

# Service Management

Apache is managed using **systemd**, allowing administrators to control the service during routine maintenance and troubleshooting.

The following commands are commonly used during daily Linux administration.

### Start Service

```bash
sudo systemctl start apache2
```

### Stop Service

```bash
sudo systemctl stop apache2
```

### Restart Service

```bash
sudo systemctl restart apache2
```

### Reload Configuration

```bash
sudo systemctl reload apache2
```

---

# Troubleshooting

## Apache Service Verification After Virtual Machine Recovery

### Scenario

Following the recovery of the Ubuntu Server virtual machine from a VirtualBox snapshot failure, Apache functionality was verified to ensure that the service remained operational.

### Validation Steps

The following checks were performed:

- Verify the Apache service status.
- Confirm that TCP port 80 was listening.
- Retrieve the default web page locally.
- Access the web server remotely from another device.

### Result

Apache resumed normal operation without requiring reinstallation or additional configuration, confirming that the service configuration remained intact after infrastructure recovery.

---

# Security Considerations

Basic security practices for Apache include:

- Keep Apache updated with the latest security patches.
- Disable unnecessary Apache modules.
- Restrict network exposure where appropriate.
- Review Apache access and error logs regularly.
- Apply operating system security updates.

---

# Operational Validation

The Apache deployment was considered successful after verifying the following:

| Validation | Status |
|------------|--------|
| Apache Package Installed | ✅ |
| Apache Service Running | ✅ |
| Service Enabled at Boot | ✅ |
| TCP Port 80 Listening | ✅ |
| Local HTTP Requests Successful | ✅ |
| Remote HTTP Requests Successful | ✅ |

---

# Observations

The Apache HTTP Server was deployed successfully and provided web services across the local network.

Key observations include:

- Apache listens on TCP port 80 by default.
- Linux services are managed using **systemd**.
- Service validation should always follow software installation.
- Network connectivity should be verified before troubleshooting application-layer services.
- The default Apache web page confirms a successful deployment.
- Service validation following infrastructure recovery helps ensure application availability after system incidents.

---

# Technical Competencies Demonstrated

- Linux System Administration
- Linux Service Management
- Apache HTTP Server Administration
- TCP/IP Networking
- Network Verification
- Package Management
- Service Validation
- Technical Documentation

---

# Lessons Learned

This project reinforced the importance of validating Linux services after deployment and following infrastructure changes.

Key takeaways include:

- Services should always be verified after installation.
- Automatic service startup should be confirmed to improve operational reliability.
- Understanding listening ports simplifies service verification and troubleshooting.
- Network connectivity should be validated before investigating application-layer issues.
- Service functionality should be revalidated after infrastructure recovery to ensure operational continuity.
- Structured documentation improves repeatability, troubleshooting, and long-term maintenance.

---

## Repository Navigation

| ⬅ Previous | 🏠 Section Home | Next ➡ |
|------------|----------------|---------|
| [SSH Remote Administration](05-ssh-remote-administration.md) | [Linux Server Deployment](README.md) | [Zabbix Monitoring Server](07-zabbix-server.md) |
