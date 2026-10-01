# Instalação e Implantação

## Modo arquivo (mínimo)

Copiar a pasta `cast-store/` para o servidor web → acessar `index.html`. Publicações via
download/substituição do `data.js`.

## Modo banco (fase 2)

1. **DBA:** rodar `schema-mysql.sql` + `schema-upgrade-v25.sql`; criar usuário `caststore_api`
   com privilégios mínimos.
2. **API:** criar `.env` (a partir de `api/env-exemplo.txt`) e subir com
   `npm install && npm start` **ou** `docker compose up -d --build`.
3. **Proxy no servidor web:** `/api/*` e `/data.js` → API (exemplo em `api/nginx.conf`).
4. **Migração:** abrir o painel → configurar URL/chave → **Publicar no banco**.

```bash
# API — instalação direta
cd api
cp env-exemplo.txt .env   # editar host, usuário, senha e API_KEY
npm install && npm start

# ou via containers
docker compose up -d --build
```

Guia completo: `GUIA-MYSQL-API.md`. Variáveis do `.env` em
[Endpoints da API](../referencias/endpoints.md).
