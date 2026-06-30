# User and Group Management

This section demonstrates basic Linux user and group administration, including creating users, creating groups, and assigning users to groups.

---

## Creating a User

<img width="413" height="190" alt="Screenshot 2026-06-27 223634" src="https://github.com/user-attachments/assets/0f07893d-9f07-4174-b1f7-5b3cd90c4661" />

### Objective

Create a new local user account on the system.

### Command

```bash
sudo adduser <username>
```

**Example**

```bash
sudo adduser Alice
```

### What This Command Does

* Creates a new user account.
* Automatically creates a home directory (`/home/<username>`).
* Prompts for a password.
* Optionally asks for additional user information (Full Name, Phone Number, etc.).
* Creates a private group for the new user (Ubuntu).

### Verification

Verify that the user was created successfully.

```bash
id <username>
```

**Example**

```bash
id Alice
```

---

## Creating a Group

<img width="320" height="58" alt="Screenshot 2026-06-27 224213" src="https://github.com/user-attachments/assets/ad7cc329-5729-4656-81ed-aa469dc58eab" />

### Objective

Create a Linux group that can be assigned to one or more users.

### Command

```bash
sudo groupadd <groupname>
```

**Example**

```bash
sudo groupadd IT
```

### What This Command Does

* Creates a new group.
* Assigns a unique Group ID (GID).
* Does not automatically add users to the group.

### Verification

Verify that the group exists.

```bash
getent group <groupname>
```

**Example**

```bash
getent group IT
```

---

## Assigning a User to a Group

<img width="628" height="215" alt="Assigning Groups to Users" src="https://github.com/user-attachments/assets/041a0697-ccfb-4937-b4a5-eec959ff5b1d" />

### Objective

Add an existing user to an existing group.

### Commands

Assign the user to a supplementary group.

```bash
sudo usermod -aG <groupname> <username>
```

Display the user's group membership.

```bash
id <username>
```

**Example**

```bash
sudo usermod -aG IT danielle

id danielle
```

### Command Breakdown

#### `usermod -aG`

* `-a` — Appends the user to existing supplementary groups.
* `-G` — Specifies the supplementary group(s) to add.

> **Important:** Always use `-aG` together. Using only `-G` replaces all existing supplementary groups for the user.

#### `id`

Displays the following information:

* User ID (UID)
* Primary Group ID (GID)
* Supplementary group memberships

### Verification

Example output:

```text
uid=1001(danielle)
gid=1001(danielle)
groups=1001(danielle),1002(IT)
```

This confirms that **danielle** is now a member of the **IT** group.

---

## Summary

| Task                      | Command                                   |
| ------------------------- | ----------------------------------------- |
| Create a user             | `sudo adduser <username>`                 |
| Create a group            | `sudo groupadd <groupname>`               |
| Add a user to a group     | `sudo usermod -aG <groupname> <username>` |
| Display user information  | `id <username>`                           |
| Display group information | `getent group <groupname>`                |

---

## Key Takeaways

* `adduser` creates a new user account along with a home directory.
* `groupadd` creates a new Linux group.
* `usermod -aG` safely adds a user to a supplementary group without removing existing group memberships.
* The `id` command verifies a user's UID, GID, and group memberships.
* `getent group` confirms that a group exists on the system.

## Groups

| Group | Purpose |
|--------|---------|
| hr | Human Resources |
| accounting | Accounting Department |
| it | IT Department |
| employees | All employees |
| Sales | Sales Department |

---

## Users

| Username | Department | Groups |
|----------|------------|--------|
| alice | HR | hr |
| bob | Accounting | Accounting |
| charlie | Sales | Sales |
| danielle | IT | IT, employee |

## Directory Permissions

| Directory | Owner | Group | Permission |
|-----------|-------|-------|------------|
| HR | root | hr | 770 |
| Accounting | root | accounting | 770 |
| IT | root | it | 770 |
| Public | root | root | 755 |
| Sales | root | Sales | 770 |
| Shared | root | employees | 775 |

---

## Explanation

HR data is only accessible by members of the hr group.

Accounting data is only accessible by accounting.

The Public directory allows read access for everyone.

Sales data is only accessible by sales department.

Shared allows collaboration between employees.
