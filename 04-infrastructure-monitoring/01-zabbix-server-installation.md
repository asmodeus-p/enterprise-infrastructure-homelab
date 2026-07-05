# Zabbix Server Installation

> **Project:** Enterprise Infrastructure Homelab
>
> **Category:** Infrastructure Monitoring
>
> **Status:** Completed
>
> **Purpose:** Deploy and validate a Zabbix Server on Ubuntu Server to provide centralized infrastructure monitoring for servers and network devices within the homelab environment.

---

## Project Overview

This document describes the deployment and validation of a Zabbix Server on Ubuntu Server.

Zabbix is an enterprise-grade infrastructure monitoring platform used to monitor the health, availability, and performance of servers, network devices, virtual machines, and applications. It provides centralized monitoring through metrics collection, dashboards, triggers, and alerting.

This deployment establishes the monitoring platform that will be used throughout the Enterprise Infrastructure Homelab.

---

## Objectives

- Deploy Zabbix Server on Ubuntu Server.
- Install the required software components.
- Configure the MySQL database.
- Configure the Zabbix Server.
- Verify required services.
- Validate that the Zabbix frontend is accessible.

---

## Environment

| Property | Value |
|----------|---------|
| Operating System | Ubuntu Server 26.04 LTS |
| Monitoring Platform | Zabbix 7.0 LTS |
| Database | MySQL |
| Web Server | Apache HTTP Server |
| Network Mode | Bridged Adapter |

---

# Implementation

## Update the Package Repository

Before installing Zabbix, the local APT package index was updated to retrieve the latest package information from the configured repositories.

### Command

```bash
sudo apt update
```

---

## Select the Deployment Platform

The installation followed the official Zabbix installation guide. Installation parameters were selected according to the target deployment environment shown below.

### Official Documentation

https://www.zabbix.com/download

### Platform Selection

| Setting | Value |
|---------|-------|
| Zabbix Version | 7.0 LTS |
| Distribution | Ubuntu |
| Release | 26.04 |
| Components | Server, Frontend, Agent |
| Database | MySQL |
| Web Server | Apache |

> **Screenshot**
>
> *(Platform selection page)*

---

## Become the Root User

The remaining installation steps were performed from a root shell to simplify the execution of administrative commands throughout the deployment process.

### Command

```bash
sudo -s
```

---

## Install the Zabbix Repository

The official Zabbix package repository was added to the system to provide the latest compatible packages for Ubuntu Server 26.04 LTS.

### Commands

```bash
wget https://repo.zabbix.com/zabbix/7.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.0+ubuntu26.04_all.deb
```

```bash
dpkg -i zabbix-release_latest_7.0+ubuntu26.04_all.deb
```

```bash
apt update
```

---

## Install Zabbix Components

The required Zabbix components were installed, including the monitoring server, web frontend, agent, Apache configuration files, and SQL initialization scripts.

### Command

```bash
apt install zabbix-server-mysql \
zabbix-frontend-php \
zabbix-apache-conf \
zabbix-sql-scripts \
zabbix-agent
```

---

## Create the Initial Database

A dedicated MySQL database and database user were created for the Zabbix Server.

The database was configured using the UTF-8 character set recommended by the official documentation.

### Commands

```sql
mysql -uroot -p
```

```sql
CREATE DATABASE zabbix
CHARACTER SET utf8mb4
COLLATE utf8mb4_bin;

CREATE USER zabbix@localhost IDENTIFIED BY 'password';

GRANT ALL PRIVILEGES
ON zabbix.*
TO zabbix@localhost;

SET GLOBAL log_bin_trust_function_creators = 1;

QUIT;
```

---

## Import the Initial Database

The default database schema and application data were imported into the newly created Zabbix database.

### Command

```bash
zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | \
mysql --default-character-set=utf8mb4 -uzabbix -p zabbix
```

---

## Restore the MySQL Configuration

After the database import completed successfully, the temporary MySQL configuration used during initialization was reverted.

### Commands

```sql
mysql -uroot -p
```

```sql
SET GLOBAL log_bin_trust_function_creators = 0;

QUIT;
```

---

## Configure the Zabbix Server

The Zabbix Server configuration file was updated with the database credentials required to establish a connection to the MySQL database.

### Configuration File

```text
/etc/zabbix/zabbix_server.conf
```

Configuration:

```text
DBPassword=password
```

---

## Enable Required Apache Modules

The required Apache modules were enabled to support the Zabbix web frontend.

### Command

```bash
a2enmod proxy
a2enmod proxy_fcgi
```

---

## Start the Required Services

The Zabbix Server, Zabbix Agent, Apache Web Server, and PHP-FPM services were started and configured to launch automatically during system startup.

### Commands

```bash
systemctl restart zabbix-server zabbix-agent apache2 php8.5-fpm
```

```bash
systemctl enable zabbix-server zabbix-agent apache2 php8.5-fpm
```

---

## Verify Service Status

The status of each required service was verified to confirm that the monitoring platform was operating correctly.

### Commands

```bash
systemctl status zabbix-server
```

```bash
systemctl status zabbix-agent
```

```bash
systemctl status apache2
```

```bash
systemctl status mysql
```

Successful verification confirmed that all required services were active and ready to support the Zabbix deployment.

> **Screenshot**
>
> *(Service status)*

---

## Verify the Zabbix Frontend

After all required services were running, the Zabbix frontend was accessed through a web browser to verify that the installation completed successfully.

### URL

```text
http://192.168.100.108/zabbix
```

> **Screenshot**
>
> *(Zabbix login page)*

---

# Verification

| Task | Status |
|------|--------|
| Repository Installed | ✅ |
| Zabbix Components Installed | ✅ |
| MySQL Database Created | ✅ |
| Database Imported | ✅ |
| Apache Modules Enabled | ✅ |
| Server Configuration Completed | ✅ |
| Required Services Running | ✅ |
| Zabbix Frontend Accessible | ✅ |

---

## Observations

The Zabbix Server installation completed successfully and all required services were operational.

Key observations include:

- Zabbix depends on multiple services, including MySQL and Apache.
- Following the official installation documentation helps ensure package compatibility.
- Database initialization is a critical step in the deployment process.
- Successful deployment requires proper coordination between the web server, database, and monitoring services.
- Verifying service status before accessing the frontend simplifies troubleshooting.

---

## Technical Competencies Demonstrated

- Linux System Administration
- Infrastructure Monitoring
- Zabbix Administration
- MySQL Administration
- Apache HTTP Server Administration
- Package Management
- Linux Service Management
- Technical Documentation

---

## Lessons Learned

This project reinforced the importance of validating each stage of an enterprise application deployment before proceeding to the next.

Key takeaways include:

- Official vendor documentation should be used whenever possible.
- Enterprise applications often rely on multiple interconnected services.
- Database initialization is essential for successful deployment.
- Service status should always be verified before testing application accessibility.
- Structured documentation improves repeatability, troubleshooting, and long-term maintainability.

---

## Related Documentation

Several issues were encountered during the deployment process. These incidents have been documented separately as troubleshooting reports.

- Zabbix Web Frontend Not Accessible
- Zabbix Server Failed to Start
- MySQL Authentication Error
- Zabbix Web Interface Login Failure

---

## References

- Zabbix 7.0 LTS Official Installation Documentation
- Ubuntu Server 26.04 LTS Documentation

---

## Repository Navigation

| ⬅ Previous | 🏠 Section Home | Next ➡ |
|------------|----------------|---------|
| [Apache HTTP Server](../01-linux-server-deployment/05-apache-web-server.md) | [Infrastructure Monitoring](README.md) | [Initial Zabbix Configuration](02-zabbix-initial-configuration.md) |
