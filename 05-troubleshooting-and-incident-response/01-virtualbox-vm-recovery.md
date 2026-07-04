# Infrastructure Incident: VirtualBox Snapshot Recovery

> **Project:** Enterprise Infrastructure Homelab
>
> **Category:** Troubleshooting & Incident Response
>
> **Status:** Resolved
>
> **Severity:** Medium
>
> **Purpose:** Investigate and recover an Ubuntu Server virtual machine that became inaccessible following an interrupted VirtualBox snapshot and saved-state operation.

---

## Project Overview

This document records a real infrastructure incident encountered while maintaining the Enterprise Infrastructure Homelab.

Following the creation of a VirtualBox snapshot, the host computer was shut down while VirtualBox was processing a saved state. The VirtualBox process was forcibly terminated during shutdown, leaving the Ubuntu Server virtual machine inaccessible.

Rather than immediately attempting corrective actions, a structured troubleshooting methodology was followed to preserve data integrity, identify the root cause, and determine the safest recovery strategy.

---

## Incident Summary

| Property | Value |
|----------|---------|
| Affected System | Ubuntu Server 26.04 LTS |
| Platform | Oracle VirtualBox 7.2.2 |
| Incident Type | Virtual Machine Inaccessible |
| Impact | Ubuntu Server unavailable |
| Root Cause | Interrupted snapshot/save-state operation |
| Resolution | Recovered server using existing base virtual disk |

---

# Symptoms

The following symptoms were observed:

- Ubuntu Server appeared as **`<inaccessible>`** within VirtualBox.
- VM settings could not be opened.
- VirtualBox displayed the following error:

```
Cannot be directly attached because it has 1 differencing child hard disks.
```

- The virtual machine could not be started.

>**Screenshot**
>
><img width="862" height="197" alt="Screenshot 2026-07-04 222117" src="https://github.com/user-attachments/assets/cf71f518-74f1-49d2-b7e5-36992585e4d5" />

---

# Investigation

The investigation focused on determining whether the incident involved:

- Virtual disk corruption
- Snapshot corruption
- Virtual machine configuration corruption
- VirtualBox registration issues

The following diagnostic steps were performed.

---

## Step 1 — Verify Virtual Machine Files

The virtual machine directory was inspected to confirm that critical files still existed.

Verified files included:

- Ubuntu Server LTS.vdi
- Ubuntu Server LTS.vbox
- Ubuntu Server LTS.vbox-prev
- Snapshots directory
- Saved-state (.sav) file

Result:

- Base virtual disk present
- Snapshot files present
- Configuration files present

---

## Step 2 — Verify Virtual Disk Integrity

The following commands were executed.

```cmd
VBoxManage showmediuminfo "Ubuntu Server LTS.vdi"
```

```cmd
VBoxManage showmediuminfo "{Snapshot UUID}.vdi"
```

Result:

- Base disk healthy
- Snapshot disk healthy
- Parent-child UUID relationship verified
- Snapshot chain intact

This eliminated virtual disk corruption as the primary cause.

---

## Step 3 — Verify Virtual Machine Registration

Commands executed:

```cmd
VBoxManage list vms
```

```cmd
VBoxManage list hdds
```

Observations:

- Ubuntu Server appeared as `<inaccessible>`.
- Virtual disks remained registered.
- Base disk and snapshot disk were accessible.

This suggested the issue was isolated to the virtual machine configuration rather than the storage layer.

---

## Step 4 — Inspect Virtual Machine Configuration

The following files were reviewed:

- Ubuntu Server LTS.vbox
- Ubuntu Server LTS.vbox-prev
- VirtualBox.xml

Observations:

- VM configuration files existed.
- Virtual machine remained registered.
- Snapshot chain existed.
- Saved-state file was referenced.

---

## Step 5 — Analyze VirtualBox Logs

VirtualBox service logs were reviewed.

The following message was identified:

```
Hard disk 'Ubuntu Server LTS.vdi'
cannot be directly attached
because it has 1 differencing child hard disks.
```

This indicated that VirtualBox attempted to attach the base virtual disk while a differencing disk already existed.

---

# Root Cause Analysis

The investigation determined that the incident occurred during the following sequence:

```
Create Snapshot
        │
        ▼
Create Differencing Disk
        │
        ▼
Begin Save State
        │
        ▼
Host Shutdown Initiated
        │
        ▼
VirtualBox Process Terminated
        │
        ▼
Incomplete VM Metadata Update
        │
        ▼
Virtual Machine Becomes Inaccessible
```

The interruption prevented VirtualBox from completing the snapshot/save-state operation.

Although the virtual disks remained healthy, the virtual machine metadata became inconsistent, preventing the VM from attaching the correct virtual disk during startup.

---

# Risk Assessment

At this stage of the investigation, modifying the virtual machine configuration manually presented unnecessary risk.

Potential risks included:

- Breaking the snapshot chain
- Corrupting virtual machine metadata
- Permanent data loss
- Complicating future recovery efforts

Because the integrity of the virtual disks had already been verified, no manual modifications were performed.

---

# Escalation Assessment

Within an enterprise environment, this incident would be a strong candidate for escalation.

## Why Escalation May Be Required

Although initial diagnostics successfully isolated the problem, the issue involved:

- Virtual machine metadata corruption
- Snapshot management
- Hypervisor configuration
- Potential virtual disk dependency issues

These components typically fall outside the responsibilities of first-level support.

Accordingly, after preserving evidence and completing initial diagnostics, the incident could be escalated to an **L2/L3 Infrastructure, Virtualization, or Systems Administration team** for advanced recovery.

The information collected during the investigation—including configuration files, virtual disk status, UUID relationships, and VirtualBox logs—would provide sufficient context to support efficient escalation and reduce troubleshooting time.

---

# Resolution

Because the snapshot contained no important changes, recovery focused on restoring the server to its state immediately before the snapshot was created.

A new VirtualBox virtual machine was created using the existing base virtual disk.

```
Existing Ubuntu Server LTS.vdi
            │
            ▼
New Virtual Machine
            │
            ▼
Successful Boot
```

The operating system booted successfully without requiring restoration from backup.

---

# Verification

Following recovery, the following components were verified:

| Component | Status |
|----------|--------|
| Ubuntu Server Boot | ✅ |
| Existing Files | ✅ |
| SSH Service | ✅ |
| Apache HTTP Server | ✅ |
| Zabbix Server | ✅ |
| Network Connectivity | ✅ |

The server resumed normal operation with no significant data loss.

---

# Lessons Learned

This incident reinforced several important operational practices.

Key takeaways include:

- Avoid interrupting snapshot or saved-state operations.
- Create backups before performing recovery procedures.
- Preserve evidence before modifying virtual machine metadata.
- Validate virtual disk integrity before assuming disk corruption.
- Follow a structured troubleshooting methodology.
- Recognize situations that require escalation to specialized infrastructure teams.

---

# Technical Competencies Demonstrated

- Infrastructure Troubleshooting
- Virtual Machine Recovery
- Oracle VirtualBox Administration
- Root Cause Analysis
- Incident Response
- Risk Assessment
- Log Analysis
- Linux Infrastructure Support
- Technical Documentation
- Escalation Decision-Making

---

## Repository Navigation

| ⬅ Previous | 🏠 Section Home | Next ➡ |
|------------|----------------|---------|
| Previous Incident | [Troubleshooting & Incident Response](README.md) | Next Incident |
