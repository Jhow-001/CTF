# Lessons Learned - Privesc Linux - 2

## Key Points

### 1. Hidden Files Enumeration
Always run `ls -la` in home and configuration directories. Files such as `.bak`, `.old`, or `.credentials` frequently contain cleartext credentials.

### 2. Hardcoded Credentials
The `.credentials.bak` file contained the `sysadmin` username and password in plaintext. This allowed immediate lateral movement.

**Defensive recommendation:** Never store passwords in backup files accessible to low-privileged users. Use secret managers (Vault, AWS Secrets Manager, etc.).

### 3. Abuse of Cron Jobs and Scripts with Elevated Permissions
The `backup.py` script in `/opt/scripts` was executed via cron (likely as root or with sufficient privileges to write to `/etc/sudoers`).

**Common vectors:**
- World-writable scripts executed by root cron
- Cron jobs with relative paths (PATH hijacking)
- Scripts that process user input without sanitization

### 4. Sudoers Injection via Cron
By modifying the script to append a line to `/etc/sudoers`, it was possible to obtain `NOPASSWD:ALL` for the `sysadmin` user.

**Alternative exploitation methods:**
- Reverse shell in the script
- Add SSH key to `/root/.ssh/authorized_keys`
- Copy `/bin/bash` with SUID
- Modify other configuration files

### 5. Importance of Permission Review
The `notes.txt` file explicitly mentioned the need to "Review permissions of scripts in `/opt/scripts`" — indicating that the lab creator knew this was a vector.

## Related Hardening Techniques
- Run cron scripts as low-privileged users
- Use `sudoers` with minimal permissions (principle of least privilege)
- Monitor changes to scripts in `/opt` and `/usr/local`
- Remove credentials from backup files
- Implement logging and alerts for modifications to critical files
