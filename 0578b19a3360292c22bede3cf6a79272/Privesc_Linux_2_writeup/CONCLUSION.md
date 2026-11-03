# Conclusão e retrospectiva — Privesc Linux - 2

## Resumo da cadeia

1. Acesso inicial via SSH com credenciais fornecidas (`ctfplayer`).
2. Enumeração de arquivos ocultos → `.config/app/.credentials.bak` com senha de `sysadmin`.
3. Movimentação lateral para `sysadmin` → flag de usuário (`user.txt`).
4. Análise de `notes.txt` → indicação de script de backup em `/opt/scripts` executado via cron.
5. Escrita no script `backup.py` (executado como root) → append de linha no `/etc/sudoers`.
6. `sudo su` → root → flag de root (`/root/root.txt`).

## Impacto

- **Critical**: Escalação de privilégios local para root através de script writable executado por cron.
- Credenciais hardcoded em backup facilitaram a movimentação lateral.
- Falta de controle de permissões em scripts de automação.

## Lições principais

- Scripts de backup/automação rodando como root e graváveis por usuários de baixo privilégio são um clássico vetor de privesc.
- Arquivos `.bak` e notas internas frequentemente entregam o caminho completo da exploração.
- A técnica de append no `sudoers` é direta e não exige reverse shell, sendo ideal em ambientes com restrições de saída.

## Melhorias no lab / hardening sugerido

- Remover credenciais hardcoded e migrar para vault (como indicado no próprio TODO).
- Garantir que scripts em `/opt/scripts` não sejam graváveis por usuários não privilegiados.
- Executar o backup com usuário dedicado e permissões mínimas (não root).
- Monitorar alterações em scripts de cron e no `/etc/sudoers`.

## Tempo e dificuldade

- Dificuldade: Easy / Introductory privesc
- Tempo estimado: 10–20 minutos após o acesso SSH
- Dependências: enumeração básica + entendimento de cron e sudoers

---

**Flags obtidas**:
- user: `hackingclub{l4t...}`
- root: `hackingclub{cr0t...}`
