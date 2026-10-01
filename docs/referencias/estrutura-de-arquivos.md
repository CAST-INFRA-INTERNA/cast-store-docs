# Estrutura de Arquivos

| Arquivo/pasta | Função |
|---|---|
| `index.html` | A loja (vitrine, produto, carrinho, checkout, meus pedidos) — JS embutido |
| `admin.html` | Painel de administração (estrutura/HTML) |
| `admin.js` | Lógica do painel (perfis, abas, NF, catálogo, relatórios, API) |
| `data.js` | Catálogo, configurações, notas e movimentações (modo arquivo) |
| `styles.css` | Estilos com a paleta oficial CAST |
| `assets/` | Logos oficiais (`logo-store-white.png`, `logo-store-navy.png`) |
| `api/server.js` | API Node.js/Express (mysql2) |
| `api/env-exemplo.txt` | Modelo do `.env` da API |
| `api/Dockerfile`, `docker-compose.yml`, `nginx.conf` | Implantação opcional em containers |
| `banco-de-dados/schema-mysql.sql` | Criação do banco `cast_store` |
| `banco-de-dados/schema-upgrade-v25.sql` | Upgrade obrigatório (fiscais, destino/unidade, notas) |
| `LEIA-ME.txt` | Manual de operação resumido |
| `GUIA-MYSQL-API.md` | Guia de implantação da fase 2 |
| `PASSO-A-PASSO-SharePoint.md` | Guia das integrações Office 365/SharePoint |

```text
cast-store/
├── index.html
├── admin.html
├── admin.js
├── data.js
├── styles.css
├── assets/
├── api/
│   ├── server.js
│   ├── env-exemplo.txt
│   ├── Dockerfile
│   ├── docker-compose.yml
│   └── nginx.conf
└── banco-de-dados/
    ├── schema-mysql.sql
    └── schema-upgrade-v25.sql
```
