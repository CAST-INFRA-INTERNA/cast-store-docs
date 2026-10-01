# Operação, Backup e Segurança

- **Publicar** após qualquer edição (banco ou arquivo); o rascunho local não é backup.
- **Backups:** dump diário do MySQL (DBA) + pacote de backup do projeto
  (`cast-store-backup-vNN.zip`, com docs de contexto, regras, histórico e mapa de
  reimportação).
- **Segredos** (fora de qualquer backup): senha do MySQL, `API_KEY`, IDs do app Azure —
  cofre de senhas da TI.
- O MySQL não deve ser exposto à rede; apenas a API o acessa. `API_KEY` circula somente
  entre o navegador dos administradores e a API.

> Em site estático o controle de perfis é aplicado no navegador — é uma camada
> organizacional. Proteção forte = login O365 + restrição do `admin.html` no servidor.
> A validação de token Entra na API está no [Roadmap](../negocio/roadmap.md).
