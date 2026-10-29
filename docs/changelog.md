# Changelog

Histórico de versões do projeto (resumo).

| Versão | Entrega principal |
|---|---|
| v29 | Publicação fatiada (contorna 413); versão/data no rodapé do admin |
| v27–v28 | env visível; diagnóstico de erros HTTP nos pop-ups |
| v26 | Fase 2: upgrade SQL, API Node, publicar no banco, guia |
| v25 | Dropdowns grupo/cor; tamanhos em checkbox com N/A; alinhamento |
| v24 | Curva ABC |
| v23 | Produto nasce na NF; aba Catálogo; custo médio ponderado; margens por entrada |
| v22 | NCM/imposto; rateio total=inst+cpf por unidades; inventários periódicos |
| v21 | Perfis + abas; custo⇄margem⇄preço; notas de entrada; estoque inst×CPF por unidade |
| v19–v20 | Limpar carrinho / − remove; hero da loja social |
| v18 | Schema MySQL |
| v17 | Logo oficial; guia SharePoint |
| v16 | Pedido social × institucional (CC/IC/CV); pop-up de sucesso visual |
| v15 | Destaques/mais vistos; similares; promoção -%; cores reais; telefone; campanhas; cupons |
| v14 | Agradecimento pós-pedido; carrinho limpo; marca "CAST Store" |
| v13 | Estoque online SharePoint com baixa automática |
| v10–v12 | Frame fixo do modal; fluxo único em tela cheia; selo no topo da foto |
| v9 | Selo novidade; vitrine ampliada com frame padrão; carrinho tela cheia |
| v8 | Variações = produtos com código próprio + grupos; galeria com setas |
| v7 | Nº de pedido; SharePoint (pedidos); estoque; Meus pedidos; QR/prazos/favicon |
| v6 | Pop-ups de validação/alerta |
| v5 | ViaCEP; validação de domínios; PDF do pedido; código único |
| v4 | Tamanho/cor; modal ampliado; zoom |
| v3 | 1–5 fotos; entrega em casa; avisos PIX |
| v2 | Login O365 (MSAL) + envio via Graph; unidades de retirada |
| v1 | Loja + painel + identidade CAST; pedido por e-mail |

## Modernização

| Data | Entrega |
|---|---|
| 13/10/2026 | Backlog: BL-001 (assistente de pedido/kit com IA) registrado; leitura assistida de NF descartada |
| 09/10/2026 | Backend FastAPI — Fase 2a (GO com ressalvas): defesa somente leitura, `admin/state` provisório, scripts de reconciliação, 187 testes |
| 09/10/2026 | Backend FastAPI — fatia 1: catálogo público somente leitura |
| 09/10/2026 | Assessment da v29: 103 regras, 19 divergências, 5 riscos prioritários |

## Documentação

| Data | Mudança |
|---|---|
| 29/10/2026 | **Regras v1.2** alinhadas ao knowledge source de requisitos (IDs MVP, relatórios financeiros, visibilidade, estoque das compras por pontos pendente, DV-10 a DV-14, Q-27 a Q-31); **Roadmap de Implementação** (estado atual × futuro, fases R0–R4 e T1–T6); arquitetura-alvo proposta na Visão Geral da Arquitetura |
| 29/10/2026 | **Regras de Negócio v1.1** a partir da reunião do MVP com o gestor: escopo do MVP, precificação, usuários inativos e fluxo de pedido PIX manual/centro de custo; **RN-01 revertida** (institucional não usa moedas; moedas só no CPF); perfis e moedas reabertos; Q-15 a Q-26. Página da reunião do MVP; Estado dos Ambientes atualizado para a homologação de 28/10 |
| 23/10/2026 | **Regras de Negócio v1** (RN-01 a RN-09, divergências DV-01 a DV-06, questões Q-01 a Q-13); **Estado dos Ambientes**; avisos de histórico em A Loja e Perfis; IP interno removido da página da reunião; status da home sem "v29 em produção" |
| 22/10/2026 | Registro da reunião "Cast Store \| Review" (decidido, incerto, em aberto, impacto técnico); modelo de acesso alvo em Perfis; piloto com login no Roadmap; BL-002 a BL-005 no Backlog |
| 16/10/2026 | Nova seção **Modernização** (Assessment v29, Backend FastAPI, Backlog); avisos de risco e divergências nas páginas de loja, perfis, arquitetura, painel, endpoints, segurança e roadmap |
| 01/10/2026 | Publicação do portal de documentação no GitHub Pages, a partir da documentação oficial v29 |
