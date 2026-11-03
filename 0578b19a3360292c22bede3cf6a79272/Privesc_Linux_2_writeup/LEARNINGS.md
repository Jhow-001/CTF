# Aprendizados e habilidades — Privesc Linux - 2

## Técnicas praticadas

- Enumeração de diretórios ocultos e arquivos de backup (`.config`, `.credentials.bak`)
- Movimentação lateral via credenciais hardcoded em arquivos de configuração
- Análise de scripts de backup e cron jobs
- Escrita em script executado com privilégios elevados (root via cron)
- Adição de usuário ao `sudoers` via append em arquivo de configuração
- Escalação de privilégios local por cron + script writable

## Conceitos reforçados

- **Hidden files e backups**: Credenciais frequentemente vazam em `.bak`, `.old`, `.config` e diretórios ocultos.
- **Cron + writable script**: Se um script rodado por root (ou via sudo) é gravável pelo usuário, ele vira RCE com privilégios do executor.
- **sudoers NOPASSWD**: Uma linha maliciosa em `/etc/sudoers` concede root permanente sem senha.
- **Notas internas**: Arquivos como `notes.txt` costumam revelar exatamente o vetor (paths, logs, tarefas pendentes).

## Ferramentas e comandos úteis

```bash
# Enumeração básica
ls -la
find / -writable 2>/dev/null | grep -v proc
ls -la /opt/scripts/
cat /var/log/backup.log
crontab -l
cat /etc/crontab
ls -la /etc/cron.*

# Verificação de permissões
ls -la /opt/scripts/backup.py
stat /opt/scripts/backup.py

# Confirmação de cron
grep -r backup /etc/cron* /var/spool/cron/ 2>/dev/null
```

## O que lembrar para o próximo box

1. Sempre checar diretórios ocultos e arquivos de backup logo após o acesso inicial.
2. Quando existir menção a “backup automático” ou “script em /opt”, priorizar checagem de permissões e cron.
3. Append em `/etc/sudoers` é simples e eficaz quando o script roda como root.
4. Alternativas válidas: reverse shell no script, SUID binary, capabilities, etc.
