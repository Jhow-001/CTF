# Privesc Linux - 2

## Description
Linux privilege escalation lab. The goal is to obtain root access and capture the flags in `/home/sysadmin/user.txt` and `/root/root.txt`.

**Objective:** Gain root access and read `/root/root.txt`

**Hint:** Enumerate. Always enumerate.

## Initial Access
The lab provides SSH credentials:

```bash
user: ctfplayer
password: ctfplayer2026
ssh ctfplayer@<IP_MACHINE>
```

## Writeup Structure
- [METHODOLOGY.md](METHODOLOGY.md) - Enumeration and exploitation steps
- [LEARNINGS.md](LEARNINGS.md) - Lessons learned
- [CONCLUSION.md](CONCLUSION.md) - Conclusion and flag summary
- `images/` - Screenshots of the process

## Flags
- **User:** `hackingclub{l4t...}`
- **Root:** `hackingclub{cr0t...}`

## Techniques Used
- Hidden files enumeration
- Lateral movement via hardcoded credentials
- Abuse of cron job / backup script with elevated permissions
- Modification of a Python script executed by cron to add user to sudoers
