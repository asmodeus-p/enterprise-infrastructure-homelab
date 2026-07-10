# SNMPv3 Configuration for Raspberry Pi

## Objective

Configure an SNMPv3 agent on a Raspberry Pi and integrate it with a Zabbix Server for secure infrastructure monitoring.

---

## Prerequisites

### Hardware

- Raspberry Pi
- Ubuntu Server (Zabbix Server)

### Software

- Raspberry Pi OS
- Net-SNMP (`snmpd`)
- Zabbix Server 7.x

### Network

- Raspberry Pi reachable from the Zabbix Server
- UDP Port 161 accessible
- Static IP assigned to the Raspberry Pi

---

# Step-by-Step Procedures

## 1. Update Package Repository

```bash
sudo apt update
```

---

## 2. Install SNMP Packages

```bash
sudo apt install snmp snmpd -y
```

---

## 3. Configure SNMP

Open the configuration file.

```bash
sudo nano /etc/snmp/snmpd.conf
```

Configure the SNMP daemon.

```conf
agentAddress udp:161

sysLocation Home Lab
sysContact Administrator

rouser monitor_user authpriv
```

Save the configuration file.

---

## 4. Create an SNMPv3 User

Create a read-only monitoring account.

```bash
sudo net-snmp-create-v3-user \
-ro \
-a SHA \
-A "YourAuthPassword" \
-x AES \
-X "YourPrivPassword" \
monitor_user
```

---

## 5. Restart the SNMP Service

Restart the daemon.

```bash
sudo systemctl restart snmpd
```

Enable automatic startup.

```bash
sudo systemctl enable snmpd
```

---

## 6. Verify the Service

Check the daemon status.

```bash
sudo systemctl status snmpd
```

Verify that UDP port 161 is listening.

```bash
sudo ss -ulpn | grep 161
```

---

# Configuration Commands

## Check SNMP Service

```bash
sudo systemctl status snmpd
```

---

## Restart SNMP

```bash
sudo systemctl restart snmpd
```

---

## Enable SNMP at Boot

```bash
sudo systemctl enable snmpd
```

---

## Test SNMPv3 Connectivity

Run the following command from the Ubuntu Server (Zabbix Server).

```bash
snmpwalk \
-v3 \
-u monitor_user \
-l authPriv \
-a SHA \
-A YourAuthPassword \
-x AES \
-X YourPrivPassword \
192.168.100.64 \
1.3.6.1.2.1.1.1.0
```

---

# Validation Steps

## Verify SNMP Service

```bash
sudo systemctl status snmpd
```

**Expected Output**

```text
Active: active (running)
```

---

## Verify Port Availability

```bash
sudo ss -ulpn | grep 161
```

**Expected Output**

```text
udp   UNCONN   0   0   *:161
```

---

## Verify SNMPv3 Response

```bash
snmpwalk \
-v3 \
-u monitor_user \
-l authPriv \
-a SHA \
-A YourAuthPassword \
-x AES \
-X YourPrivPassword \
192.168.100.64 \
1.3.6.1.2.1.1.1.0
```

**Expected Output**

```text
iso.3.6.1.2.1.1.1.0 = STRING: Linux raspberrypi ...
```

Successful execution confirms:

- SNMP daemon is running.
- Authentication is successful.
- Encryption is functioning correctly.
- The Raspberry Pi is reachable from the monitoring server.

---

# Screenshot

<img width="1901" height="870" alt="image" src="https://github.com/user-attachments/assets/d4879fee-1b98-4fe5-8dfc-70cc393b9d69" />

---

# Troubleshooting Notes

## Issue

### `zbx_snmp_open_session() failed`

**Cause**

The SNMPv3 session could not be established.

**Resolution**

Verified:

- SNMP daemon status
- Network connectivity
- Username
- Authentication password
- Privacy password
- SHA authentication
- AES encryption

Confirmed functionality using `snmpwalk`.

---

## Issue

### Authentication failure (incorrect password, community or key)

**Cause**

Incorrect SNMPv3 authentication or privacy credentials.

**Resolution**

Recreated the SNMPv3 user.

```bash
sudo net-snmp-create-v3-user
```

Restarted the SNMP daemon.

---

## Issue

### The supplied password length is too short

**Cause**

SNMPv3 requires authentication and privacy passwords with a minimum length of eight characters.

**Resolution**

Created new passwords that satisfied the minimum length requirement.

---

## Issue

### cannot resolve address [[zabbix.pi]:161]

**Cause**

Zabbix attempted to resolve a hostname instead of connecting to the configured IP address.

**Resolution**

Configured the SNMP interface to connect using the Raspberry Pi IP address.

---

## Issue

### SNMP items remained unsupported despite successful `snmpwalk`

**Cause**

The **Context Name** field in the Zabbix SNMP interface was incorrectly configured.

**Resolution**

Leave the **Context Name** field blank.

Configure only:

- **Security Name:** `monitor_user`

---

## Issue

### SNMPv3 user changes were not recognized

**Cause**

The SNMP daemon was not restarted after creating the SNMPv3 user.

**Resolution**

Restart the daemon.

```bash
sudo systemctl restart snmpd
```

---

# Lessons Learned

- Always verify SNMP functionality with `snmpwalk` before configuring Zabbix.
- Restart the SNMP daemon after creating or modifying SNMPv3 users.
- The SNMPv3 username belongs in the **Security Name** field, **not** the **Context Name** field.
- Verify each infrastructure layer independently to isolate configuration issues efficiently.
- SNMPv3 provides significantly stronger security than SNMPv2c by using authentication and encryption.
- Documenting troubleshooting steps improves future maintenance and demonstrates systematic system administration practices.
