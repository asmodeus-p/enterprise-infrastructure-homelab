# User and Group Management

This section demonstrates basic Linux user and group administration. The tasks include creating users, creating groups, and assigning users to groups.

---

# User Creation

<img width="413" height="190" alt="Screenshot 2026-06-27 223634" src="https://github.com/user-attachments/assets/0f07893d-9f07-4174-b1f7-5b3cd90c4661" />

## Objective

Create a new local user account on the system.

## Command

```bash
sudo adduser <username>
```

### Example

```bash
sudo adduser Alice
```

### What this command does

- Creates a new user account.
- Automatically creates a home directory (`/home/<username>`).
- Prompts for a password.
- Optionally asks for user information (Full Name, Phone Number, etc.).
- Creates a private group for the user (on Ubuntu).

### Verification

Display information about the newly created user.

```bash
id <username>
```

Example:

```bash
id Alice
```

---

# Group Creation

<img width="320" height="58" alt="Screenshot 2026-06-27 224213" src="https://github.com/user-attachments/assets/ad7cc329-5729-4656-81ed-aa469dc58eab" />

## Objective

Create a new Linux group that can later be assigned to users.

## Command

```bash
sudo groupadd <groupname>
```

### Example

```bash
sudo groupadd IT
```

### What this command does

- Creates a new group.
- Assigns a unique Group ID (GID).
- Does not automatically add users to the group.

### Verification

Display the group information.

```bash
getent group <groupname>
```

Example:

```bash
getent group IT
```

---

# Assigning Groups to Users

<img width="628" height="215" alt="image" src="https://github.com/user-attachments/assets/041a0697-ccfb-4937-b4a5-eec959ff5b1d" />


## Objective

Assign an existing user to an existing group.

## Commands

Assign the user to a supplementary group.

```bash
sudo usermod -aG <groupname> <username>
```

Display the user's group membership.

```bash
id <username>
```

### Example

```bash
sudo usermod -aG IT danielle

id danielle
```

### What these commands do

#### `usermod -aG`

- `-a` — Appends the user to the specified group(s).
- `-G` — Specifies supplementary group(s).

> **Important:** Always use `-aG` together. Using only `-G` will replace all existing supplementary groups for the user.

#### `id`

Displays:

- User ID (UID)
- Primary Group ID (GID)
- All supplementary groups assigned to the user

### Verification

Example output:

```text
uid=1001(danielle)
gid=1001(danielle)
groups=1001(danielle),1002(IT)
```

This confirms that the user **danielle** is now a member of the **IT** group.

---

# Summary

| Task | Command |
|------|---------|
| Create a user | `sudo adduser <username>` |
| Create a group | `sudo groupadd <groupname>` |
| Add user to a group | `sudo usermod -aG <groupname> <username>` |
| Display user information | `id <username>` |
| Display group information | `getent group <groupname>` |
