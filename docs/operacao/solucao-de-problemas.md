# Solução de Problemas

| Sintoma | Causa provável | Ação |
|---|---|---|
| "Unexpected token '<' ... not valid JSON" | URL apontando para página HTML (proxy/rota errada) ou erro do proxy | O pop-up mostra o código HTTP e a dica; conferir URL (raiz, sem `/api` no final) |
| HTTP 413 ao publicar | Limite de corpo do proxy | Publicação fatiada (v29) resolve; ou aumentar `client_max_body_size`/equivalente |
| HTTP 404 / 405 | Proxy não cobre `/api/` inteiro ou bloqueia POST/PATCH | Ajustar a regra de proxy |
| HTTP 502/504 | API parada ou timeout | Verificar serviço/logs; `proxy_read_timeout` |
| Health `"ok":false` | API não alcança o MySQL | `.env` (host/senha), firewall, usuário/grants |
| Login O365 não abre | Redirect URI não cadastrada como SPA | Registro do app no Azure |
| Produto não aparece na loja | Pendente (sem foto/preço), oculto ou inativo | Completar no Catálogo e ativar |
| Arquivo `.env` "não existe" | Dotfile oculto no Finder/Explorer | Usar `env-exemplo.txt`; Cmd+Shift+. no Finder |
