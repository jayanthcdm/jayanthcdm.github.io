---
title: 'Linux Filesystem Administration & Linux Users, Groups and Permissions'
description: 'Linux administration depends heavily on two areas: how data is organized in the filesystem and who is allowed to access that data…'
pubDate: 2026-08-15
category: 'Linux'
tags:
  - 'Linux'
  - 'System Administration'
  - 'Permissions'
---
---

### Linux Filesystem Administration & Linux Users, Groups and Permissions

Linux administration depends heavily on two areas: **how data is organized in the filesystem** and **who is allowed to access that data**. Understanding these concepts is essential for managing servers securely and reliably.

### Linux Filesystem Administration

Linux uses a hierarchical filesystem that starts from the root directory `/`. Files, directories, devices, configuration, logs, and application data are organized below this point.

![](https://cdn-images-1.medium.com/max/800/1*RegX-5_9RUlvT_fjiHauPQ.png)

Some important directories are:

DirectoryPurpose`/`Root of the filesystem`/etc`System and application configuration`/home`Normal users' home directories`/root`Root user's home directory`/var`Variable data and logs`/tmp`Temporary files`/boot`Boot-related files`/dev`Device files`/proc`Process and kernel information`/sys`Hardware and kernel information

A useful way to remember the most important ones is:

```bash
/etc      → Configuration
```

```bash
/home     → Users
```

```kotlin
/var      → Variable data / Logs
```

```bash
/boot     → Boot
```

```bash
/dev      → Devices
```

```bash
/proc     → Processes / Kernel
```

### Navigating and Inspecting

Common filesystem commands include:

```bash
pwd
```

```bash
ls
```

```bash
cd
```

```lua
find
```

```bash
du
```

```bash
df
```

`pwd` shows the current location, `ls` lists directory contents, and `cd` changes directories. `find` searches for files, while `du` and `df` help identify disk and filesystem usage.

```bash
df -h
```

```bash
du -sh /var/*
```

`df` shows available filesystem space, while `du` helps identify which files or directories are consuming space.

### Mounting Filesystems

Linux makes storage available through **mount points**. A simplified storage structure is:

```typescript
Disk
```

```typescript
↓
```

```sql
Partition
```

```typescript
↓
```

```typescript
Filesystem
```

```typescript
↓
```

```typescript
Mount Point
```

```typescript
↓
```

```typescript
Files
```

Useful commands include:

```typescript
lsblk
```

```typescript
mount
```

```typescript
findmnt
```

```bash
df -h
```

Persistent mounts are commonly configured through:

```bash
/etc/fstab
```

Understanding mounts is important when dealing with additional disks, storage failures, and filesystem configuration.

### Linux Users, Groups and Permissions

Linux is a **multi-user operating system**. Access to files and system resources is controlled through users, groups, ownership, and permissions.

A file has three primary permission categories:

```sql
User     → Owner
```

```sql
Group    → Group members
```

```bash
Other    → Everyone else
```

The basic permissions are:

```typescript
r → Read
```

```typescript
w → Write
```

```sql
x → Execute
```

For example:

```diff
-rwxr-xr--
```

can be interpreted as:

```typescript
Owner  → rwx
```

```sql
Group  → r-x
```

```lua
Other  → r--
```

### File Ownership

Every file normally has an owner and a group.

```bash
ls -l
```

Example:

```css
-rw-r--r--  jayanth  developers  notes.txt
```

Here, `jayanth` is the owner and `developers` is the group.

Ownership can be changed using:

```bash
chown user file
```

```bash
chgrp group file
```

### Changing Permissions

The `chmod` command changes permissions.

```bash
chmod 755 script.sh
```

This gives:

```lua
Owner → read + write + execute
```

```lua
Group → read + execute
```

```lua
Other → read + execute
```

Permissions can also be modified symbolically:

```bash
chmod u+x script.sh
```

```bash
chmod g-w file.txt
```

```bash
chmod o+r file.txt
```

### Users and Groups

Common user-management commands include:

```typescript
useradd
```

```typescript
usermod
```

```typescript
userdel
```

```typescript
passwd
```

Groups can be managed using:

```typescript
groupadd
```

```typescript
groupmod
```

```typescript
groupdel
```

A user’s identity and group membership can be inspected with:

```bash
id username
```

```bash
groups username
```

### Root and sudo

The `root` user has extensive administrative privileges. Because unrestricted root access can be dangerous, Linux commonly uses `sudo` to perform individual administrative operations.

```bash
sudo command
```

The principle is:

> ***Use the minimum privileges required to perform the task.***

### Special Permissions

Linux also provides three special permission mechanisms:

```typescript
SUID
```

```typescript
SGID
```

```typescript
Sticky Bit
```

**SUID** allows an executable to run with the privileges of its owner.

**SGID** can provide group-based execution behavior and group inheritance on directories.

**Sticky Bit** is commonly used on shared directories such as `/tmp` to prevent users from deleting files belonging to other users.

These permissions are important for both Linux administration and security.

### Administrator Perspective

Filesystem administration answers:

> ***Where is the data and how is it organized?***

Permissions answer:

> ***Who can access or modify it?***

Together:

```typescript
Filesystem
```

```typescript
↓
```

```typescript
Files & Directories
```

```typescript
↓
```

```sql
Owner + Group
```

```typescript
↓
```

```typescript
Permissions
```

```typescript
↓
```

```typescript
Controlled Access
```

A Linux administrator should always consider **location, ownership, permissions, and available storage** when managing files.
