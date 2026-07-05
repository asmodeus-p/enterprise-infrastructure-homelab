# Troubleshooting Log

---

## Issue #1

### Problem

Unable to SSH from Kali to Ubuntu.

### Symptoms

- SSH enabled
- Ubuntu reachable from Internet
- SSH connection timed out

### Investigation

- Verified SSH service
- Checked firewall
- Compared network configuration

### Root Cause

Ubuntu and Kali used different VirtualBox networking modes.

### Resolution

Configured both virtual machines to use the same virtual network.

### Lesson

Always verify network topology before troubleshooting services.
