# Zabbix Configuration Procedure
### Objective:
              Build a homelab with an enterprise-style infrastructure monitoring solution using
              Ubuntu Server and Zabbix to monitor Linux hosts, generate alerts, and visualize
              system health. This project demonstrates Linux administration, networking
              fundamentals, monitoring, troubleshooting, and documentation practices relevant to NOC
              engineer and Systems Administrator roles.

## 1. Update the Ubuntu Server
```
sudo apt update
```
## 2. Install Zabbix to your machine
### Follow the link bellow:
https://www.zabbix.com/download?zabbix=7.0&os_distribution=ubuntu&os_version=26.04&components=server_frontend_agent&db=mysql&ws=apache

### Choose the platform based on this
| Zabbix Version | OS Distribution | OS Version | Zabbix Component | Database | Web Server |
| ------------- |-------------| -----|-----|-----|-----|
| 7.0 LTS | Ubuntu | 26.04 Resolute |Server, Frontend, Agent | MySQL | Apache |

### Follow the official documentation instructions

# Troubleshooting: Zabbix Installation and Database Authentication

## Overview

During the installation of Zabbix 7.0 on Ubuntu Server, several issues were encountered that prevented the Zabbix Server and Web Frontend from operating correctly. This document outlines the troubleshooting process, identifies the root causes, and describes the solutions implemented.

---

# Environment

| Component        | Version       |
| ---------------- | ------------- |
| Operating System | Ubuntu Server |
| Zabbix           | 7.0.27        |
| Database         | MySQL         |
| Web Server       | Apache2       |

---

# Issue 1: Zabbix Web Frontend Not Accessible

## Symptoms

* Browser could not access the Zabbix web interface.
* Apache was running, but the expected Zabbix page was unavailable.

## Investigation

The following checks were performed:

* Verified that Apache was installed and running.
* Confirmed Apache was listening on port 80.
* Checked whether the Zabbix frontend package was installed.
* Verified Apache configuration files.

## Root Cause

The incorrect Zabbix package had been installed while following a third-party tutorial. As a result, the Zabbix frontend package and Apache configuration required for the web interface were missing.

## Resolution

* Installed the correct Zabbix frontend package.
* Configured Apache for Zabbix.
* Restarted the Apache service.
* Verified that the Zabbix installation page was accessible through the browser.

---

# Issue 2: Zabbix Server Failed to Start

## Symptoms

The service failed to start with the following message:

```text
Job for zabbix-server.service failed because the service did not take the steps required by its unit configuration.
```

The Zabbix log contained:

```text
cannot use database "zabbix": its "users" table is empty
```

## Investigation

The following components were verified:

* MySQL service status
* Zabbix server logs
* Database existence
* Number of database tables
* SQL initialization files

## Root Cause

The initial database import was interrupted before completion, leaving the database only partially initialized. The required default data, including entries in the `users` table, was not imported successfully.

## Resolution

* Recreated the Zabbix database.
* Imported the official database initialization script:

```bash
zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql -u zabbix -p zabbix
```

* Allowed the import process to complete before restarting the Zabbix Server.

---

# Issue 3: MySQL Authentication Error During Frontend Setup

## Symptoms

The frontend displayed:

```text
Cannot connect to the database.

Access denied for user 'zabbix'@'localhost' (using password: YES)
```

## Investigation

The following verification steps were performed:

* Confirmed the MySQL service was running.
* Verified the existence of the `zabbix` database.
* Compared the database credentials configured in:

```text
/etc/zabbix/zabbix_server.conf
```

with the credentials used by MySQL.

* Tested direct database authentication using the MySQL client.

## Root Cause

The database credentials entered during the Zabbix frontend configuration did not match the credentials configured for the MySQL `zabbix` user.

## Resolution

* Verified the configured database username and password.
* Updated the frontend configuration using the correct database credentials.
* Successfully established the database connection.

---

# Issue 4: Unable to Log In to Zabbix Web Interface

## Symptoms

After completing the installation, the following message appeared on the login page:

```text
Incorrect user name or password or account is temporarily blocked.
```

## Investigation

Initially, the MySQL database credentials were assumed to be identical to the Zabbix web application credentials.

The following checks were performed:

* Verified that the `users` table contained the default application accounts.
* Confirmed the `Admin` account existed.
* Verified the database import had completed successfully.

## Root Cause

The credentials required by the Zabbix web interface are **independent** of the MySQL database credentials.

Two different authentication systems are used:

### MySQL Database Authentication

Used internally by the Zabbix Server and Frontend to connect to the database.

Example:

| Setting  | Value                          |
| -------- | ------------------------------ |
| Database | zabbix                         |
| Username | zabbix                         |
| Password | Configured during installation |

### Zabbix Web Authentication

Used to log in to the Zabbix application after installation.

Default credentials:

| Username | Password |
| -------- | -------- |
| Admin    | zabbix   |

The database credentials were mistakenly assumed to be the login credentials for the web application.

## Resolution

Logged in using the default Zabbix application account:

| Username | Password |
| -------- | -------- |
| Admin    | zabbix   |

Login was successful, confirming that the installation had completed correctly.

---

# Verification Steps

The following validation steps were performed to ensure the installation was functioning correctly.

## Verify MySQL Service

```bash
sudo systemctl status mysql
```

---

## Verify Zabbix Server

```bash
sudo systemctl status zabbix-server
```

---

## Verify Apache

```bash
sudo systemctl status apache2
```

---

## Verify Database Connection

```bash
mysql -u zabbix -p zabbix
```

---

## Verify Database Tables

```sql
USE zabbix;

SHOW TABLES;
```

---

## Verify Default Users

```sql
SELECT userid, username
FROM users;
```

Expected output:

```text
Admin
guest
```

---

## Verify Server Configuration

```bash
grep "^DB" /etc/zabbix/zabbix_server.conf
```

---

# Lessons Learned

* Follow the official Zabbix documentation whenever possible, as package names and installation procedures may differ between distributions and versions.
* Allow database initialization scripts to complete before interrupting the process.
* Validate service status and review application logs before making configuration changes.
* Verify database connectivity independently using the MySQL client.
* Distinguish between **database authentication** and **application authentication**.
* Confirm assumptions by checking configuration files and testing credentials rather than relying solely on memory.

---

# Key Takeaway

This troubleshooting process reinforced the importance of systematic problem isolation. Rather than assuming a single point of failure, each layer of the deployment—web server, database service, database initialization, configuration, and application authentication—was validated independently until the underlying issues were identified and resolved. This structured approach mirrors real-world systems administration practices and results in more reliable and repeatable troubleshooting.
