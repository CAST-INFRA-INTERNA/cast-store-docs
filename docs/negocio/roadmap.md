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

## Modernização (strangler incremental)

Sequência recomendada pelo [Assessment v29](../modernizacao/assessment-v29.md), preservando a vitrine:

| Etapa | Estado (16/10/2026) |
|---|---|
| Contenção imediata (quick wins de segurança) | ⏳ A fazer |
| Baseline em Git + testes de caracterização | 🟡 Novo backend com Git/CI e 187 testes; legado v29 ainda sem Git |
| `data.js` público reduzido | ✅ Adaptador no FastAPI (desligado por padrão) |
| Autenticação no servidor | 🟡 `admin/state` com chave provisória; Entra ID pendente |
| Livro-razão + comandos granulares | ⏳ A fazer |
| Fase 2b — pedido no servidor | ⛔ Bloqueada por DAT-01 e SEC-03 |
| Paralelismo com reconciliação → cutover | ⏳ A fazer |

### Etapas de produto (reunião do MVP, 29/10/2026)

| Etapa | Conteúdo |
|---|---|
| 1 — Primeira versão vendável | Produtos, notas, custo e margem, estoque CPF × institucional por unidade, pedido PIX manual e institucional, PDF, acesso administrativo |
| 2 — Validação operacional | Acessos, quantidades, baixa, fluxos CPF/institucional, retirada e rastreio, ajustes do painel |
| 3 — CAST Coins | Conversão, elegíveis, pagamento misto, gestão de saldo, inativos |
| 4 — Automações | Recebimento, encerramento, Microsoft 365, PIX automático, QR Code, entrega |

Regras e questões em aberto: [Regras de Negócio v1.1](regras-de-negocio.md).

### Piloto (atualização 22/10/2026)

O piloto passa a **exigir login Entra ID** — não é mais só navegação. Identidade e perfis (S3)
entram no caminho crítico. Escopo de compra no piloto e autorização para trocar o servidor
seguem em aberto. Ver [Reunião 22/10](../modernizacao/reuniao-2026-10-22.md).

**Próximo passo:** executar os scripts da Fase 2a em homologação (`.env.hml` com usuário SELECT),
fazer o stamp da baseline com o DBA e validar a imagem Docker aprovada.

Ideias fora das fases: [Backlog](../modernizacao/backlog.md).
