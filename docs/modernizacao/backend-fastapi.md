# Backend FastAPI

Novo backend que substitui gradualmente a API Node (estratégia strangler — ver
[Assessment v29](assessment-v29.md)). Repositório: `cast-store-backend` (GitHub
`facurpa/cast-store-backend`, ainda sem commits).

## Status

| Fatia | Escopo | Estado (09/10/2026) |
|---|---|---|
| **Fatia 1** | Catálogo público, somente leitura | ✅ Entregue |
| **Fase 2a** | Defesa somente leitura + `admin/state` protegido + scripts de reconciliação | 🟡 GO com ressalvas — **não concluída** (falta execução real em HML) |
| Fase 2b | Pedido no servidor com baixa atômica | ⛔ Bloqueada (DAT-01, SEC-03) |

## Stack

Python 3.12 · FastAPI 0.143 · SQLAlchemy 2.1 async + aiomysql · Alembic 1.20 · uv (lock com hashes).

> Versões provisórias — não foi encontrado padrão corporativo.

## Endpoints

| Método e rota | Fase | Função |
|---|---|---|
| `GET /health/live` | 1 | Liveness |
| `GET /health/ready` | 1 | Readiness (banco) |
| `GET /api/v1/storefront/catalog` | 1 | Catálogo público (só colunas públicas; estoque agregado) |
| `GET /api/v1/storefront/photos/{id}` | 1 | Fotos (base64 do banco servidas por URL) |
| `GET /data.js` | 1 | Adaptador público compatível com a vitrine — **desligado por padrão** |
| `GET /api/v1/admin/state` | 2a | **Provisório**, desligado por padrão, proibido em produção; chave `X-Admin-Read-Key` (≥32), allowlist de origem, 401 genérico, 429, auditoria |

### `admin/state` — o que não sai

Hashes, IDs Entra/SharePoint, `config_json` integral, contato de fornecedor, `registrada_por` e
movimentos individuais. O contrato é por contexto, com *capabilities* (App Roles propostas:
`Store.Admin`, `Store.Manager`, `Store.Marketing`, `Store.Purchasing`).

> O `admin.html` também lê `/data.js`: trocar o proxy exige antes o `admin/state` protegido.

## Garantias de segurança

- Modelos só com colunas públicas; allowlist sobre `config_json`; estoque só agregado.
- **Somente leitura em três camadas:** usuário MySQL só com SELECT + `SET SESSION TRANSACTION READ ONLY`
  por conexão + guarda SQLAlchemy contra SQL de escrita (`DATABASE_READ_ONLY`, `false` só em teste).
- Erros padronizados com *correlation id*; logs JSON.
- Alembic: baseline vazia `0001_baseline` com stamp manual (ADR-007); produção e autogenerate
  bloqueados (com modelos parciais, o autogenerate propunha DROP de colunas administrativas).

## Scripts de homologação

| Script | Função |
|---|---|
| `inspect_schema.py` | Allowlist de consultas de metadados; aborta em produção ou com usuário de escrita |
| `reconcile_schema.py` | Tabela com classificações e bloqueadores; cruza com o Node |
| `check_encoding.py` | Detecta mojibake (só contagens/IDs) |
| `compare_catalog.py` | Node `data.js` × FastAPI com emulação independente da vitrine |

## Qualidade

| Métrica | Valor |
|---|---|
| Testes | **187** (123 unit · 39 contrato · 25 integração em MySQL real, incl. Node v29 × FastAPI) |
| Lint / tipos | ruff e mypy `--strict` limpos |
| Dependências | pip-audit sem vulnerabilidades |
| CI | `.github/workflows/ci.yml` |
| ADRs | 006, 007, 008 |

## Comportamentos da v29 preservados ⚠️

- Produto sem movimentos = estoque ilimitado.
- Placeholder conta como foto.
- Cupons ativos aparecem no `/data.js` público.

## Achados

- Um `nota_itens.dist_json` inválido derruba todo o `/api/data.js` do Node (HTTP 500); o FastAPI tolera.
- O Node converte custo `NULL` em 0; o "último custo" depende de `registrada_em`, que é reescrito a cada publish.

## Pendências da Fase 2a

1. `.env.hml` com usuário SELECT → rodar inspeção, reconciliação, encoding e comparação em homologação.
2. Docker com imagem-base aprovada (registry corporativo bloqueado; só imagem substituta testada).
3. Stamp manual da baseline Alembic após reconciliação + aprovação do DBA.
