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

## Riscos e contenção (assessment v29)

| ID | Risco | Severidade |
|---|---|---|
| SEC-01 | `data.js` público expõe perfis, hashes, cupons, custos e fornecedores | 🔴 Crítico |
| SEC-02 | Autorização só no navegador; painel abre como admin sem configuração | 🔴 Crítico ❓ |
| DAT-01 | Publicação total a partir de rascunho local (last-writer-wins) | 🔴 Crítico |
| SEC-03/04 | Pedidos sem autenticação, preço do cliente, `API_KEY` única no navegador | 🟠 Alto |
| DAT-04 | Pedidos não baixam estoque | 🟠 Alto |

### Quick wins

- [ ] Restringir `admin.html` e `/api/pedidos` no proxy
- [ ] Tornar `CORS_ORIGIN` obrigatório
- [ ] Rotacionar a `API_KEY`
- [ ] `try/catch` e supervisor (pm2/systemd) na API Node
- [ ] Lockfile + `npm ci`
- [ ] Versão do rodapé gerada no deploy
- [ ] SRI nos scripts de CDN e cabeçalhos de segurança
- [ ] Atualizar o `LEIA-ME`
