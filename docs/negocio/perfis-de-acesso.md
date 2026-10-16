# Perfis de Acesso do Painel

O acesso usa **Office 365 (Entra ID)** quando ativo — o grupo é definido pelo e-mail da
conta — ou **usuários locais** (e-mail + senha com hash SHA-256). Sem nada configurado,
o painel abre em modo de configuração inicial (como admin, com aviso).

## Matriz de permissões

| Aba | Admin TI | Gestores | Marketing | Compras |
|---|---|---|---|---|
| Entradas & Estoque | ✔ | ✔ | — | ✔ |
| Catálogo | ✔ | ✔ | ✔ (sem fiscal/estoque) | ✔ |
| Marketing | ✔ | ✔ | ✔ | — |
| Cupons | ✔ | ✔ | — | ✔ |
| Relatórios | ✔ | ✔ | — | ✔ |
| Configurações | ✔ | — | — | — |

## Perfis

- **Administradores (TI):** acesso total; únicos que alteram níveis de acesso, usuários,
  O365, SharePoint, domínios e API.
- **Gestores CAST Store:** operam tudo e emitem relatórios; não alteram configurações.
- **Marketing:** edita a cara da loja (nome, fotos, preços de venda/promo, descrição,
  selos, visibilidade) e campanhas; não vê NCM/imposto/estoque.
- **Compras e Facilities:** notas fiscais, cadastro de produtos, estoque, cupons e relatórios.

> **Nota de segurança:** em site estático o controle é aplicado no navegador — é uma camada
> organizacional. Proteção forte = login O365 + restrição do `admin.html` no servidor;
> na fase da API, as permissões passam a ser validáveis no servidor.

> ⚠️ **Risco SEC-02 (assessment v29):** sem O365 e sem usuários locais configurados, o painel abre
> como **administrador**. Mitigação imediata: restringir o `admin.html` no proxy. Alvo: Entra ID
> validado na API, com App Roles `Store.Admin`, `Store.Manager`, `Store.Marketing` e
> `Store.Purchasing` (ver [Backend FastAPI](../modernizacao/backend-fastapi.md)).

Veja também: [Painel de Administração](../operacao/painel-admin.md) e
[Backup e Segurança](../operacao/backup-e-seguranca.md).
