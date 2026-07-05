# Apache HTTP Server

> **Project:** Enterprise Infrastructure Homelab
>
> **Category:** Linux Services
>
> **Status:** Completed
>
> **Purpose:** Deploy, configure, and validate the Apache HTTP Server to provide web services within the Ubuntu Server homelab environment.

---

## Project Overview

This document demonstrates the deployment, configuration, and validation of the Apache HTTP Server on Ubuntu Server.

Apache is one of the most widely used web servers in enterprise environments. Deploying a web server provides practical experience with Linux service management, package installation, network connectivity, and service verification.

---

## Objectives

- Install Apache HTTP Server.
- Verify the Apache service status.
- Confirm web server accessibility.
- Validate network connectivity.
- Verify HTTP service availability.
- Practice Linux service administration.

---

## Environment

| Property | Value |
|----------|---------|
| Operating System | Ubuntu Server 26.04 LTS |
| Web Server | Apache HTTP Server |
| Client Device | Kali Linux / Windows Host |
| Service Port | TCP 80 |
| Network Mode | Bridged Adapter |

---

## Implementation

### Install Apache HTTP Server

Apache HTTP Server was installed using Ubuntu's APT package manager.

### Command

```bash
sudo apt update
sudo apt install apache2
```

> **Screenshot**
>
> *(Insert installation screenshot)*

---

### Verify Apache Service

The Apache service was verified to ensure it was installed successfully and running.

### Command

```bash
sudo systemctl status apache2
```

> **Screenshot**
>
> *(Insert screenshot)*

---

### Verify Automatic Startup

The Apache service was verified to ensure it was enabled during system startup.

### Command

```bash
sudo systemctl is-enabled apache2
```

> **Screenshot**
>
> *(Insert screenshot)*

---

### Verify Listening Port

The server was checked to confirm that Apache was listening on TCP port 80.

### Command

```bash
sudo ss -tln | grep :80
```

> **Screenshot**
>
> *(Insert screenshot)*

---

### Verify Local Web Service

The web server was accessed locally from the Ubuntu Server to verify successful deployment.

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
> *(Insert screenshot)*

---

### Verify Network Connectivity

The server's IP address was identified before testing remote access.

### Command

```bash
hostname -I
```

> **Screenshot**
>
> *(Insert screenshot)*

The web server was then accessed from another device on the same network using a web browser.

Example:

```text
http://192.168.100.105
```

> **Screenshot**
>
> *(Insert browser screenshot showing the Apache default page)*

---

## Service Management

Apache service management was verified using systemd.

### Commands

Start service

```bash
sudo systemctl start apache2
```

Stop service

```bash
sudo systemctl stop apache2
```

Restart service

```bash
sudo systemctl restart apache2
```

Reload configuration

```bash
sudo systemctl reload apache2
```

---

## Troubleshooting

### Unable to Access Apache Web Server

#### Symptoms

- Browser could not access the web server.
- HTTP requests timed out.

#### Root Cause

The Apache service was not running or the server's network connectivity had not yet been verified.

#### Resolution

The Apache service status was verified using `systemctl`, and network connectivity was confirmed before accessing the web server.

#### Verification

The Apache default page was successfully accessed from another device on the local network.

---

## Security Considerations

Basic security practices for Apache include:

- Keep Apache updated.
- Disable unused modules.
- Restrict unnecessary network exposure.
- Monitor web server logs.
- Apply operating system security updates regularly.

---

## Verification

| Task | Status |
|------|--------|
| Apache Installed | ✅ |
| Apache Service Running | ✅ |
| Service Enabled at Boot | ✅ |
| TCP Port 80 Listening | ✅ |
| Local Access Verified | ✅ |
| Remote Access Verified | ✅ |

---

## Observations

The Apache HTTP Server was deployed successfully and provided web services across the local network.

Key observations include:

- Apache listens on TCP port 80 by default.
- Linux services are managed using systemd.
- Network connectivity must be verified before testing web access.
- Successful service deployment requires both a running service and proper network configuration.
- The default Apache page confirms a successful installation.

---

## Technical Competencies Demonstrated

- Linux System Administration
- Apache HTTP Server Administration
- Linux Service Management
- Network Verification
- TCP/IP Networking
- Package Management
- Service Validation
- Technical Documentation

---

## Lessons Learned

This project reinforced the importance of validating Linux services after deployment.

Key takeaways include:

- Services should always be verified after installation.
- Network connectivity should be confirmed before troubleshooting applications.
- Understanding listening ports simplifies service verification.
- Service management using systemd is a fundamental Linux administration skill.
- Documentation improves repeatability and troubleshooting efficiency.

---

## Repository Navigation

| ⬅ Previous | 🏠 Section Home | Next ➡ |
|------------|----------------|---------|
| [SSH Remote Administration](05-ssh-remote-administration.md) | [Linux Server Deployment](README.md) | [Zabbix Monitoring Server](07-zabbix-server.md) |
