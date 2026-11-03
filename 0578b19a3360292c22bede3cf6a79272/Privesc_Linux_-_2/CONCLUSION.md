# Conclusion - Privesc Linux - 2

## Exploitation Summary

| Step               | Method                                      | Result                     |
|--------------------|---------------------------------------------|----------------------------|
| Initial Access     | SSH with provided credentials               | User `ctfplayer`           |
| Enumeration        | Hidden files in `~/.config/app/`            | `sysadmin` credentials     |
| Lateral Movement   | `su sysadmin`                               | User flag + `notes.txt`    |
| Escalation         | Modification of `/opt/scripts/backup.py`    | Entry in sudoers           |
| Root               | `sudo su` after cron execution              | Root flag                  |

## Captured Flags

- **User Flag** (`/home/sysadmin/user.txt`):  
  `hackingclub{l4t...}`

- **Root Flag** (`/root/root.txt`):  
  `hackingclub{cr0t...}`

## Estimated Time
- Initial enumeration: ~5-10 minutes
- Lateral movement: immediate after finding `.credentials.bak`
- Escalation via cron: ~1-2 minutes (waiting for execution)

## Difficulty
**Easy / Beginner** — The vector is straightforward and well hinted by `notes.txt`. Excellent for practicing:
- Basic Linux enumeration
- Lateral movement
- Cron job abuse

## Screenshots
See the `images/` folder for visual evidence of the process (SSH, enumeration, flags, and escalation).
