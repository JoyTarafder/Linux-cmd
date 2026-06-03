# Linux Short Notes
### For DevOps Engineers
*by Train With Shubham*

---

## 🐧 History of LINUX

- Linux came from a Unix family. It is a free and open-source software operating system, developed by **Linus Torvalds** in September 1991.
- In 1991, Linus Torvalds was a student at the University of Helsinki, Finland.
- He developed the first code of **Linux 0.01** and posted it on the Minix newsgroup on **17 Sep 1991**. His code became so popular that people encouraged him to develop further, leading to the first "official" version — **Linux 0.02** on **October 5, 1991**.
- Today, **90% of the fastest Supercomputers** out of 500 run on Linux variants, including the top 10.

---

## 🐧 Linux File System Hierarchy

- In Linux, everything is represented as a file — including hardware programs.
- Files are stored in directories with a **tree structure** called the **File System Hierarchy (FSH)**.
- Linux uses a **single rooted, inverted tree-like structure**.
- The **Root Directory** is represented by `/` (forward slash) — the top-level directory.

### Directory Descriptions

| Directory | Name | Description |
|-----------|------|-------------|
| `/` | Root | The base of the Linux directory. Starting point of FSH. Every directory arises from here. |
| `/root` | Root Home | Home directory for the root user (superuser). |
| `/bin` | User Binaries | Contains binary executables. Common Linux commands used by all users. |
| `/sbin` | System Binaries | Binary executables used by system administrators for system maintenance (e.g., `iptables`, `reboot`, `fdisk`, `ifconfig`, `swapon`). |
| `/dev` | Device Files | Contains hardware device files — terminal devices, USB, etc. (e.g., `/dev/tty1`, `/dev/usbmon0`). |
| `/var` | Variable Files | Contains variable data files like logs. Includes `/var/log`, `/var/lib`, `/var/mail`, `/var/tmp`. |
| `/mnt` | Mount Directory | Used to mount a file system temporarily. |
| `/media` | Removable Media | Contains subdirectories where removable media devices are mounted. |
| `/usr` | User Binaries | Contains applications and files used by users (not the system). |
| `/etc` | Configuration Files | Stores all configuration files and startup/shutdown scripts. Controls OS/application behavior. |
| `/boot` | Boot Loader Files | Contains files needed to boot the system (GRUB boot loader files and Linux kernels). |
| `/opt` | Optional Applications | For third-party software not available in the Linux distribution. |
| `/home` | Home Directory | Contains home directories for secondary (non-root) users. |
| `/tmp` | Temporary Files | Temporary files created by the system and users. Deleted on reboot. |

---

## 🐧 Basic Commands

```bash
#pwd        # Shows the present working directory
#ls         # Shows files and directories in the current directory
#uname      # Shows the name of the kernel (OS)
#uname -r   # Shows the version of the kernel
#cd         # Change directory
#clear      # Clear the screen
#whoami     # Shows the currently logged-in username
#history    # Shows list of previously used commands
#date       # Shows current time and date
```

---

## 🐧 Create File or Directory

### mkdir — Create Directories

```bash
# 1. Create a single directory
#mkdir /shubham

# 2. Create multiple directories
#mkdir dev qa test

# 3. Create a directory path (directory inside directory)
#mkdir -p /dev/qa/test/devops

# 4. Create a numbered range of directories
#mkdir /student{1..10}
```

### touch — Create Empty Files

```bash
# 1. Create a single file
#touch notes

# 2. Create multiple files
#touch python java react

# 3. Create a numbered range of files
#touch books{1..10}
```

---

## 🐧 Copy, Move, Remove

### cp — Copy and Paste

**Syntax:** `#cp <option> <source> <destination>`

**Options:**
- `-r` → recursive
- `-v` → verbose
- `-f` → forcefully

```bash
# 1. Copy a file
#cp -rvf /root/anaconda-ks.cfg /home

# 2. Copy all files starting with 'D'
#cp -rvf /root/D* /home
```

### rm — Remove Files & Directories

```bash
# Delete a file or directory
#rm -rvf /india/pune
```

### mv — Move or Rename

```bash
# 1. Move a file or directory
#mv /home/shub/root/Desktop

# 2. Rename a file or directory
#mv dev devops
```

---

## 🐧 User Management

```bash
# Create a user account
#useradd shub

# Check user account properties
#grep shub /etc/passwd
# Output: shub:1001:1001: :/home/shub:/bin/bash

# Create a user password
#passwd shub

# Check user password properties
#grep shub /etc/shadow

# Switch user account
#su shub

# Logout from user account
#exit
# Or press Ctrl+D

# Delete a user account
#userdel shub

# Change user login name
#usermod -l devops shub
```

---

## 🐧 Group Management

> A group is a collection of user accounts. Very useful for administrators to manage and apply permissions to multiple users.

```bash
# Add a group account
#groupadd ibmgrp

# Check group account property
#grep ibmgrp /etc/group
# Output: Ibmgrp:x:1001:ajay,vijay,sachin

# Check group admin property
#grep ibmgrp /etc/gshadow

# Delete a group account
#groupdel ibmgrp

# Add a single member to a group
#gpasswd -a ajay ibmgrp

# Add multiple members to a group
#gpasswd -M rahul,virat,rohit ibmgrp

# Remove a group member
#gpasswd -d virat ibmgrp

# Make a user a group admin
#gpasswd -A sachin ibmgrp
```

---

## 🐧 Linux File System Permission

### Types of File Permission
- Basic Permission
- Special Permission
- Access Control List (ACL) Permission

### Permission Structure

```
drwxrwxrwx
│└──┴──┴──┘
│  │  │  └── Other (o)
│  │  └───── Group (g)
│  └──────── User/Owner (u)
└─────────── File type (d = directory, - = file)
```

Each `rwx` stands for:
- `r` → Read
- `w` → Write
- `x` → Execute

### Permission Groups

| Entity | Symbol | Description |
|--------|--------|-------------|
| Owner | `u` | Permissions for the file owner |
| Group | `g` | Permissions for group members |
| Other | `o` | Permissions for all other users |

### Permission Set

| Permission | Access for a File | Access for a Directory |
|------------|-------------------|------------------------|
| Read (r) | Display and copy file contents | View contents of directory |
| Write (w) | Modify file contents | Modify contents of a directory |
| Execute (x) | Execute the file if executable | Allow use of `cd` command to access |

### Permission with Numeric & Symbol

| Number | Permission Type | Symbol |
|--------|----------------|--------|
| 0 | No Permission | `---` |
| 1 | Execute | `--x` |
| 2 | Write | `-w-` |
| 3 | Execute + Write | `-wx` |
| 4 | Read | `r--` |
| 5 | Read + Execute | `r-x` |
| 6 | Read + Write | `rw-` |
| 7 | Read + Write + Execute | `rwx` |

### Check Permissions

```bash
# Check file permission
#ls -l /notes.txt
# Output: -rw-r--r--. 1 root root 0 Jan 4 14:59 /notes.txt

# Check directory permission
#ls -ld /dev
```

### Change Permissions (chmod)

```bash
# Add read permission to owner
#chmod u+r /notes.txt

# Add read & write permission to group
#chmod g+rw /notes.txt

# Remove read permission from others
#chmod o-r /notes.txt

# Set permission with numeric value (r=4, w=2, x=1)
#chmod 751 /shub
```

### Change Ownership

```bash
# Change file/directory owner
# Syntax: #chown <user name> <file/directory name>
#chown ajay /notes.txt

# Change group ownership
# Syntax: #chgrp <group name> <file/directory name>
#chgrp ibmgrp /notes.txt
```

---

## 🐧 Access Control List (ACL)

> ACL provides a more flexible permission mechanism for file systems. It allows giving special permissions to specific users/groups on particular files or directories — even without making them group members.

```bash
# Check ACL permission
# Syntax: #getfacl <name of file or directory>
#getfacl /devops

# Set ACL permission to a user
#setfacl -m u:shub:rwx /de

# Remove ACL permission of a user
#setfacl -x u:shub: /devops

# Set ACL permission to a group
#setfacl -m g:shubgrp:rwx /devops

# Remove ACL permission of a group
#setfacl -x g:shubgrp: /devops

# Remove all ACL permissions
#setfacl -b /devops
```

---

## 🐧 Regular Expressions & GREP

> **Regular Expressions** are special characters that help search data by matching complex patterns.

> **GREP (Global Regular Expression Print)** — searches a file for a particular pattern of characters and displays all lines that contain that pattern.

```bash
# Search a word/string in a file
#grep root /etc/passwd

# Search a string in multiple files
#grep root /etc/passwd /etc/group

# Search a string case-insensitively
#grep -i Root /etc/passwd

# Search a string in all files recursively
#grep -r root /

# Invert the string match (show lines that DON'T match)
#grep -v root /etc/passwd

# Display total number of matching lines
#grep -c root /etc/passwd

# Display file names that contain the string
#grep -l root /etc/passwd /etc/shadow

# Display file names that do NOT contain the string
#grep -L root /etc/passwd /etc/shadow

# Display matching lines with line numbers
#grep -n root /etc/passwd

# Display lines that START with a string
#grep ^root /etc/passwd

# Display lines that END with a string
#grep /bin/bash$ /etc/passwd

# Search and redirect output to a new file
#grep root /etc/passwd > /mnt/find.txt
```

---

## 🐧 Find Command

> The Linux `find` command is one of the most important commands in Linux. It is used to search and locate files and directories based on conditions like permissions, users, groups, file type, date, size, etc.

```bash
# Find files under Home directory
#find /home -name shub.txt

# Find files with SUID permission
#find / -perm 4755

# Find files with GUID permission
#find / -perm 2644

# Find files with sticky bit permission
#find / -perm 1755

# Find based on user
#find / -user root

# Find based on group
#find / -group shubgrp

# Find files smaller than 10MB
#find /tmp -size -10M

# Find files larger than 10MB
#find /tmp -size +10M
```

---

## 🐧 WC (Word Count)

> The `wc` command is used to count words and line numbers.

```bash
# Count number of lines
#wc -l /etc/passwd

# Count number of words
#wc -w /etc/passwd
```

---

## 🐧 head & tail

### head — Display Top Lines

```bash
# Display top 10 lines of a file
#head /etc/passwd

# Display top N specific lines
#head -n 15 /etc/passwd
```

### tail — Display Bottom Lines

```bash
# Display bottom 10 lines of a file
#tail /etc/passwd

# Display bottom N specific lines
#tail -n 5 /etc/passwd
```

---

## 🐧 Archive File in Linux (tar)

> **Archiving** is the process of combining multiple files and directories into one file. Useful for backup and data compression.

> **tar** (tape archive) uses compression algorithms like `gzip`, `bz2`, and `xz`.

**Syntax:** `#tar <options> <files>`

### Commonly Used Options

| Option | Meaning |
|--------|---------|
| `c` | Create |
| `x` | Extract |
| `v` | Verbose |
| `f` | Forcefully |
| `t` | Test |
| `z` | gzip compression |
| `j` | bz2 compression |
| `J` | xz compression |
| `C` | Specific destination |

```bash
# Create a tar archive
# tar -cvf /mnt/backup.tar /var

# Show file size in human-readable format
#du -sh /var
#du -sh /mnt/backup.tar

# Extract a tar archive to default location
#tar -xvf /mnt/backup.tar

# Extract a tar archive to a specific location
#tar -xvf /mnt/backup.tar -C /root/Desktop/

# Create tar with gzip compression
# tar -cvzf /mnt/backup.tar.gz /var

# Extract gzip tar archive
#tar -xvzf /mnt/backup.tar.gz

# Create tar with bzip2 compression
# tar -cvjf /mnt/backup.tar.bz2 /var

# Extract bzip2 tar archive
#tar -xvjf /mnt/backup.tar.bz2

# Create tar with xz compression
#tar -cvJf /mnt/backup.tar.xz /var

# Extract xz tar archive
#tar -xvJf /mnt/backup.tar.xz
```

---

## 🐧 Job Automation

> Job automation allows performing tasks automatically in the OS using tools. Useful for scheduling tasks when the administrator is unavailable.

### Two Types of Job Automation

1. **`at`** — Execute a job only **one time**
2. **`crontab`** — Execute a job **multiple times**

### at Command

```bash
# Set a job with at command
#date
#at 8:10 AM
at> useradd shub
at>
Ctrl+d  (write & quit)

# Show pending jobs
#atq

# Remove a job
#atrm 2

# Restrict a user from using at
#vim /etc/at.deny
# Add username here (e.g., Shub)
:wq (write & quit)
```

### crontab Command

**Crontab format:**
```
* * * * * /path/to/script.sh
│ │ │ │ │
│ │ │ │ └── Day of Week (0-7, where 0 and 7 are Sunday)
│ │ │ └──── Month of Year (1-12)
│ │ └────── Day of Month (1-31)
│ └──────── Hour (0-23)
└────────── Minute (0-59)
```

```bash
# Start crond service
#systemctl start crond

# Enable crond service permanently
#systemctl enable crond

# Set cron jobs (open editor)
#crontab -e

# Show cron jobs of current user
#crontab -l

# Remove all cron jobs
#crontab -r

# Set cron job for another user
#crontab -u shub -e

# Show cron jobs of another user
#crontab -u shub -l

# Restrict a user from crond service
#vim /etc/cron.deny
```

---

## 🐧 Sudo Command

> **sudo** ("superuser do" or "switch user do") allows a user with proper permissions to execute a command as another user (e.g., the superuser). It works according to specifications in `/etc/sudoers`.

### Provide sudo Privilege to a User

```bash
# vim /etc/sudoers
root ALL=(ALL) ALL
amir ALL=(ALL) ALL   # Add this line (~line 101)
:wq
```

### Provide sudo Privilege to a Group

```bash
# vim /etc/sudoers
%punegrp ALL=(ALL) ALL   # (~line 108)
:wq
# All members of punegrp group get sudo privileges
```

### Wheel Group

> **Wheel** is a system group that by default has sudo privileges. Adding a user to this group grants them sudo access.

```bash
#grep wheel /etc/group
#useradd shub
#passwd shub
#gpasswd -a shub wheel
# All members of the wheel group get sudo privileges
```

### sudo Without Password

```bash
# vim /etc/sudoers
amir ALL=(ALL) NOPASSWD: ALL
%punegrp ALL=(ALL) NOPASSWD: ALL
:wq
```

---

## 🐧 Managing Networking (Red Hat Enterprise Linux)

### Show IP Address

```bash
#ifconfig
# Or
#ip addr
```

### Configure Networking with nmcli

> **Network Manager** is a daemon that monitors and manages network settings. `nmcli` is the command used to manage networking.

```bash
# Show all connections
#nmcli con show

# Show active connections
#nmcli con show --active

# Show a specific connection
#nmcli con show "citynet"

# Show device status
#nmcli dev status

# Create a new connection
#nmcli con add con-name "citynet" ifname ens33 type ethernet \
  ipv4.add 192.168.0.2/24 gw4 192.168.0.1 ip4.dns 192.168.0.1 \
  connection.autoconnect yes ipv4.method manual

# Modify an existing connection
#nmcli con mod "citynet" ipv4.add 192.168.0.100
#nmcli con mod "citynet" gw4 192.168.0.254
#nmcli con mod "citynet" ipv4.dns 192.168.0.254

# Activate a connection
#nmcli con up "citynet"
#nmcli con show --active

# Deactivate a connection
#nmcli con down citynet

# Switch from old to new connection
#nmcli connection modify "citynet" connection.autoconnect no
#nmcli connection modify "pune" connection.autoconnect yes

# Remove a connection
#nmcli con delete citynet

# Set hostname
#hostnamectl set-hostname it.citynet.com

# Show hostname
#hostname
```

### Configure Networking with nmtui (Text UI)

```bash
#nmtui
```

---

## 🐧 IP Address Configuration Files

> All connections created with `nmcli` and `nmtui` are stored at:

```bash
#cd /etc/NetworkManager/system-connections/
#ls
```

> **Note:** You can modify connection files directly, but it is **not recommended**. If you do update a file, restart NetworkManager to apply changes:

```bash
#systemctl restart NetworkManager
```

---

*Linux Short Notes — Train With Shubham*
