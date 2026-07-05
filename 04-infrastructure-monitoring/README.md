# Infrastructure Monitoring

This section documents the deployment, configuration, validation, and troubleshooting of infrastructure monitoring solutions within the Enterprise Infrastructure Homelab.

The primary monitoring platform is Zabbix, which is used to monitor Linux hosts, visualize system health, and generate alerts.

## Objectives

- Deploy an enterprise monitoring solution
- Configure monitored hosts
- Validate monitoring functionality
- Practice incident investigation
- Document troubleshooting procedures

## Projects

| Project | Status |
|---------|--------|
| Zabbix Server Installation | ✅ |
| Initial Configuration | ✅ |
| Monitor Ubuntu Server | ✅ |
| Monitor Raspberry Pi via SNMP | Planned |

## Troubleshooting

Several installation and configuration issues were encountered during deployment and have been documented separately.

See:

- troubleshooting/01-zabbix-web-frontend-not-accessible.md
- troubleshooting/02-zabbix-server-failed-to-start.md
- troubleshooting/03-mysql-authentication-error.md
- troubleshooting/04-zabbix-login-failure.md
