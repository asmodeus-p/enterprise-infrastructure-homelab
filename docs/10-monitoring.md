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

## 2. Enabling SNMP
### Check if snmpd daemon is already installed in your Ubuntu server
```
systemctl list-units --type=service | grep snmpd
```

### If snmpd daemon is not installed, install it with this command
```
sudo apt install snmpd snmp -y
```

### Backing up the Original Configuration
Backup the default configuration files before making any changes using this command:
```
sudo cp /etc/snmp/snmpd.conf /etc/snmp/snmpd.conf.bak
```

### Edit the configuration file to configure SNMP settings
Open the file using a text editor:
```
sudo nano /etc/snmp/snmpd.conf
```

### Update agentAddress block to listen on all IPv4 interfaces
```
agentAddress udp:161
```
Save (Ctrl+O) and close (Ctrl+X) the file.

### Create the SNMPv3 User
Stop the SNMP service first before creating a user
Use this systemctl command to stop the service:
```
sudo systemctl stop snmpd
```
Create an SNMPv3 user with this command:
```
sudo net-snmp-create-v3-user
```
It will prompt you for Username, Authentication password, Privacy password

