# Roadmap

Pendências combinadas, em ordem de prioridade.

| # | Item | Observação |
|---|---|---|
| 1 | Validar em produção a publicação fatiada (v29) | Contorna o limite de 1 MB dos proxies |
| 2 | **Fase 2b:** loja enviando pedidos ao `POST /api/pedidos` | Baixa atômica; "Meus pedidos" lendo do banco; e-mail vira notificação |
| 3 | Ativar Azure/Entra ID e SharePoint em produção | Ver [Integrações](../arquitetura/integracoes.md) |
| 4 | Automação da confirmação | Power Automate: resposta com PIX, mudança de status |
| 5 | Limites de valor por colaborador | Com fluxo de aprovação de gestor |
| 6 | SKU por tamanho | Estoque próprio por tamanho — o modelo de variações já suporta |
| 7 | Segurança server-side | Validação de token Entra na API e permissões por perfil |
