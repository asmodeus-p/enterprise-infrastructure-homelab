# Enterprise Infrastructure Homelab

![Status](https://img.shields.io/badge/Status-Active-success)
![Platform](https://img.shields.io/badge/Platform-Ubuntu%20Server-orange)
![Virtualization](https://img.shields.io/badge/VirtualBox-7.2.2-blue)
![Documentation](https://img.shields.io/badge/Documentation-Professional-blueviolet)
![License](https://img.shields.io/badge/License-MIT-green)

> **Last Updated:** July 2026

> An enterprise-inspired homelab built to develop practical, hands-on skills in Linux System Administration, Networking, Infrastructure Monitoring, and IT Operations.

---

# Overview

This repository documents my hands-on journey of building and maintaining a Linux-based enterprise homelab. The objective is to simulate enterprise IT environments and gain practical experience beyond classroom learning.

Instead of simply installing software, every service is deployed, configured, tested, documented, and maintained as if it were part of a production environment.

This project serves as both a technical portfolio and a learning journal while preparing for roles such as:

- Junior Systems Administrator
- Junior NOC Engineer
- IT Infrastructure Engineer
- Technical Support Engineer

---

# Key Highlights

- Enterprise-inspired Linux infrastructure
- Production-style technical documentation
- Linux systems administration
- Infrastructure monitoring
- Troubleshooting and incident response
- Continuous project expansion

---

## Table of Contents

- [Overview](#overview)
- [Key Highlights](#key-highlights)
- [Objectives](#objectives)
- [Current Progress](#current-progress)
- [Lab Environment](#lab-environment)
- [Architecture](#architecture)
- [Repository Structure](#repository-structure)
- [Technologies](#technologies)
- [Skills Demonstrated](#skills-demonstrated)
- [Documentation](#documentation)
- [Roadmap](#roadmap)
- [Why This Project?](#why-this-project)
- [Disclaimer](#disclaimer)

---

# Objectives

- Build a production-like Linux environment
- Strengthen Linux administration skills
- Practice networking concepts and server deployment
- Learn infrastructure monitoring and incident response
- Develop structured troubleshooting methodology
- Produce professional technical documentation
- Continuously expand the environment with enterprise technologies

---

# Repository Goals

This repository is maintained as a long-term learning project. New technologies, services, troubleshooting scenarios, and documentation will continue to be added as practical experience grows.

---

## Current Progress

| Section | Status |
|---------|--------|
| Linux Server Deployment | **Completed** |
| Linux Administration | In Progress |
| Network Administration | In Progress |
| Infrastructure Monitoring | In Progress |
| Security | Planned |
| Incident Response | **Completed** |

---

# Lab Environment

## Host Machine

- Windows 11

## Virtualization Platform

- Oracle VirtualBox

## Virtual Machines

| Machine | Operating System | Purpose |
|---------|------------------|---------|
| Ubuntu Server | Ubuntu Server LTS | Primary Linux Server |
| Kali Linux | Kali Linux | Administration Workstation / Testing Client |

---

## Architecture

```text
                    Windows 11 Host
                           │
                           ▼
                  Oracle VirtualBox
                    ┌────────┴────────┐
                    │                 │
                    ▼                 ▼
            Ubuntu Server        Kali Linux
            (Primary Server)     (Client/Test Workstation)
                    │
        ┌───────────┼────────────┐
        │           │            │
        ▼           ▼            ▼
     OpenSSH     Apache        Zabbix
     Server    HTTP Server    Monitoring
```

---

# Repository Structure

```text
.
├── 01-linux-server-deployment/
├── 02-linux-administration/
├── 03-network-administration/
├── 04-infrastructure-monitoring/
├── 05-troubleshooting-and-incident-response/
├── 06-security/
├── 07-learning/
└── assets/
```

Each directory focuses on a specific area of system administration and contains detailed documentation, screenshots, configuration steps, troubleshooting notes, and lessons learned.
Documentation is organized by technical domain rather than chronology to mirror the structure of an enterprise knowledge base.

---

# Technologies

## Technologies Used

### Operating Systems
- Ubuntu Server LTS
- Kali Linux

### Infrastructure
- Oracle VirtualBox

### Administration
- Bash Shell
- GNU/Linux Command Line

### Services
- OpenSSH
- Apache HTTP Server

### Monitoring
- Zabbix (In Progress)

### Version Control
- Git
- GitHub

---

# Skills Demonstrated

## Linux Administration

- Server installation
- User and group management
- File permissions
- SSH administration
- Package management
- Service management

## Infrastructure

- Server deployment
- Service configuration
- Documentation
- Configuration management
- System maintenance
- Service validation

## Networking

- IP addressing
- Virtual networking
- SSH connectivity
- Client-server communication
- Network troubleshooting

## Infrastructure Monitoring

- Zabbix deployment
- Service monitoring
- Host monitoring
- Dashboard configuration

## Troubleshooting and Incident Response

- Root cause analysis
- Network diagnostics
- Virtual machine recovery
- Service troubleshooting
- Incident documentation

## Technical Documentation

Each project within this repository follows a consistent documentation format to improve readability, reproducibility, and troubleshooting.

Documentation typically includes:

- Project overview
- Objectives
- Environment
- Implementation steps
- Configuration commands
- Validation procedures
- Troubleshooting
- Lessons learned
- Repository navigation

---

# Documentation Standards

Every project follows a standardized documentation format that includes:

- Objectives
- Prerequisites
- Step-by-step procedures
- Configuration commands
- Validation steps
- Screenshots
- Troubleshooting notes
- Lessons learned

This approach mirrors the documentation standards commonly used in enterprise IT environments.

# Roadmap

## Completed

- [x] Ubuntu Server Deployment
- [x] User & Group Management
- [x] SSH Remote Administration
- [x] Apache HTTP Server
- [x] VirtualBox VM Recovery Documentation

## In Progress

- [ ] Network Administration
- [ ] Zabbix Monitoring

## Planned

- [ ] Docker
- [ ] Samba
- [ ] DNS
- [ ] DHCP
- [ ] Bash Automation
- [ ] Nginx Reverse Proxy
- [ ] UFW Firewall
- [ ] Infrastructure Hardening
- [ ] Ansible

---

# Why This Project?

Many entry-level Systems Administrator and Network Operations Center (NOC) roles require practical experience with Linux administration, networking, monitoring, troubleshooting, and technical documentation.

This homelab was built to bridge the gap between academic knowledge and real-world IT operations by providing hands-on experience with infrastructure deployment, service management, incident response, and operational documentation.

Rather than focusing solely on software installation, each project emphasizes deployment validation, troubleshooting, operational readiness, and structured documentation to simulate professional IT environments.

---

# Disclaimer

This project is intended for educational purposes and personal skill development. The environment is continuously updated as new technologies are learned and implemented.
