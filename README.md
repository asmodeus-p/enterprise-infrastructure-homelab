# Enterprise Infrastructure Homelab

![Status](https://img.shields.io/badge/Status-Active-success)
![Platform](https://img.shields.io/badge/Platform-Ubuntu%20Server-orange)
![Monitoring](https://img.shields.io/badge/Monitoring-Zabbix%20%2B%20SNMPv3-red)
![Virtualization](https://img.shields.io/badge/VirtualBox-7.2.2-blue)
![License](https://img.shields.io/badge/License-MIT-green)

> **Last Updated:** October 2026

An enterprise-inspired homelab for hands-on practice in Linux system administration, networking, infrastructure monitoring, and IT operations. Every service is deployed, validated, troubleshot, and documented as if it were running in production.

---

## At a Glance

| | |
|---|---|
| **Nodes** | Windows 11 host, Ubuntu Server VM, Kali Linux VM, Raspberry Pi |
| **Core services** | OpenSSH, Apache HTTP Server, Zabbix Server (MySQL backend) |
| **Security** | UFW host firewall on the Raspberry Pi (default deny, SSH on a non-default port) |
| **Monitoring** | Zabbix monitoring the Ubuntu Server (agent) and the Raspberry Pi (SNMPv3) |
| **Documentation** | Step-by-step guides with validation, troubleshooting, and lessons learned |

---

## Table of Contents

- [Lab Environment](#lab-environment)
- [Architecture](#architecture)
- [Current Progress](#current-progress)
- [Documentation](#documentation)
- [Troubleshooting Highlights](#troubleshooting-highlights)
- [Technologies](#technologies)
- [Skills Demonstrated](#skills-demonstrated)
- [Roadmap](#roadmap)
- [Why This Project?](#why-this-project)

---

## Lab Environment

| Node | Type | Operating System | Role |
|------|------|------------------|------|
| Host | Physical laptop | Windows 11 | Runs Oracle VirtualBox |
| Ubuntu Server | Virtual machine | Ubuntu Server LTS | Primary server: SSH, Apache, Zabbix Server |
| Kali Linux | Virtual machine | Kali Linux | Administration workstation and test client |
| Raspberry Pi | Physical device | Raspberry Pi OS | Monitored via SNMPv3; hosts an Apache SNMP dashboard; protected by UFW |

---

## Architecture

```text
                       Windows 11 Host
                              │
                       Oracle VirtualBox
                  ┌───────────┴───────────┐
                  │                       │
            Ubuntu Server             Kali Linux
          (Primary Server)        (Admin / Test Client)
                  │                       │
      ┌───────────┼───────────┐           └── SSH ──► Ubuntu Server
      │           │           │
   OpenSSH     Apache      Zabbix Server ◄──── SNMPv3 (UDP 161) ──── Raspberry Pi
                           + MySQL                                (Raspberry Pi OS)
```

Zabbix on the Ubuntu Server monitors its own host and polls the Raspberry Pi over SNMPv3 with authentication and encryption.

---

## Current Progress

| Area | Status |
|------|--------|
| Linux Server Deployment | Completed |
| Infrastructure Monitoring (Zabbix + SNMPv3) | Completed |
| Troubleshooting and Incident Response | Ongoing (VM recovery documented) |
| Linux Administration | In Progress |
| Network Administration | In Progress |
| Security | In Progress (UFW firewall completed) |

---

## Documentation

### 01 · Linux Server Deployment
- [Ubuntu Server Installation](01-linux-server-deployment/01-ubuntu-server-installation.md)
- [Server Information](01-linux-server-deployment/02-server-information.md)
- [User and Group Management](01-linux-server-deployment/03-user-group-management.md)
- [SSH Remote Administration](01-linux-server-deployment/04-ssh-remote-administration.md)
- [Apache Web Server](01-linux-server-deployment/05-apache-web-server.md)

### 04 · Infrastructure Monitoring
- [Zabbix Server Installation](04-infrastructure-monitoring/01-zabbix-server-installation.md)
- [SNMPv3 Configuration for Raspberry Pi](04-infrastructure-monitoring/02-snmp-configuration.md)

### 05 · Troubleshooting and Incident Response
- [Incident: VirtualBox Snapshot Recovery](05-troubleshooting-and-incident-response/01-virtualbox-vm-recovery.md)

### 06 · Security
- [UFW Firewall Configuration](06-security/01-ufw-firewall-configuration.md)

Each guide follows the same format: objectives, environment, implementation steps, commands, validation, troubleshooting, and lessons learned. Documentation is organized by technical area to mirror an enterprise knowledge base.

---

## Troubleshooting Highlights

Real issues hit while building the lab, each with its cause and fix documented:

| Issue | Root Cause | Resolution |
|-------|-----------|------------|
| Zabbix SNMP items stayed unsupported even though `snmpwalk` worked | SNMPv3 username was entered as the Context Name | Left Context Name blank; set the user as Security Name |
| `cannot resolve address [[zabbix.pi]:161]` | Zabbix tried to resolve a hostname | Pointed the SNMP interface at the Pi's static IP |
| New SNMPv3 user not recognized | `snmpd` not restarted after the change | `sudo systemctl restart snmpd` |
| Ubuntu Server VM showed as `<inaccessible>` and would not start | Host shut down mid snapshot/save-state, leaving a broken differencing disk | Recovered the server from the existing base virtual disk ([write-up](05-troubleshooting-and-incident-response/01-virtualbox-vm-recovery.md)) |

---

## Technologies

| Category | Tools |
|----------|-------|
| Operating systems | Ubuntu Server LTS, Kali Linux, Raspberry Pi OS, Windows 11 |
| Virtualization | Oracle VirtualBox |
| Services | OpenSSH, Apache HTTP Server, MySQL |
| Security | UFW |
| Monitoring | Zabbix Server, Zabbix Agent, SNMPv3 (net-snmp) |
| Administration | Bash, GNU/Linux CLI, systemd |
| Version control | Git, GitHub |

---

## Skills Demonstrated

- **Linux administration:** server installation, users and groups, file permissions, package and service management with systemd
- **Remote administration:** SSH setup and access from a separate client workstation
- **Infrastructure monitoring:** Zabbix deployment, host monitoring, SNMPv3 device monitoring, dashboards
- **Networking:** IP addressing, static IPs, virtual networking, client-server connectivity, network troubleshooting
- **Security:** host-based firewall with a default-deny policy (UFW), non-default SSH port, firewall rules for monitoring traffic
- **Incident response:** root cause analysis, VM recovery, incident documentation
- **Technical documentation:** reproducible, validated guides written as a knowledge base

---

## Roadmap

**Completed**
- [x] Ubuntu Server deployment
- [x] User and group management
- [x] SSH remote administration
- [x] Apache HTTP Server
- [x] Zabbix Server installation and host monitoring
- [x] Raspberry Pi monitoring via SNMPv3
- [x] VirtualBox VM recovery write-up
- [x] UFW firewall on the Raspberry Pi

**Next**
- [ ] Network administration documentation
- [ ] UFW firewall on the Ubuntu Server
- [ ] Server hardening (SSH keys, Fail2ban)
- [ ] DNS and DHCP services
- [ ] Bash automation (backups, maintenance)
- [ ] Docker and Nginx reverse proxy
- [ ] Ansible configuration management

---

## Why This Project?

Entry-level IT operations, NOC, and infrastructure roles expect hands-on experience with Linux, networking, monitoring, and troubleshooting. This lab bridges the gap between academic knowledge and real operations work, with an emphasis on validation, root cause analysis, and clear documentation rather than just installing software.

---

*Built and maintained by [Marc Danielle Ipapo](https://linkedin.com/in/marc-danielle-ipapo) · BS Computer Engineering, Bulacan State University. For educational and personal skill development.*
