# Roadmap de implementação — estado atual e implementações futuras

| Metadado | Valor |
|---|---|
| Versão | 1.0 — rascunho para revisão |
| Data | 2026-10-29 |
| Substitui | Planilha `CAST-Store-atividades-por-fase.xlsx` (20/10/2026), que fica como histórico |
| Fontes | KS de requisitos (F1/F2/F3) · KS de deploy (28/10) · análise de arquitetura e arquitetura-alvo (29/10, **propostas**) · `painel-admin-fatias.md` (23/10) · ADR-010…014 · `docs/negocio/regras-de-negocio-v1.md` (v1.2) |
| Regra | "Implementado" = código existe (pode estar desligado). "Ativo" = ligado em algum ambiente. Nada aqui autoriza alterar código, flag, banco ou servidor |

## 1. Onde estamos (29/10/2026)

| Frente | Estado | Evidência |
|---|---|---|
| Vitrine React + catálogo FastAPI (leitura) | **Ativo na homologação** (só VPN) | KS de deploy §12 (smoke 49/49, 0 falhas HTTPS) |
| Homologação no servidor de produção | **Ativa**, isolada, banco de produção em sessão somente leitura | KS de deploy §11, §25 |
| Entra ID (backend + MSAL no front) | Implementado; **desligado** (`VITE_AUTH_ENABLED=false`, tenant não configurado) | KS de deploy §11.2 |
| Grupos Admin/Manager/Marketing/Purchasing | Criados no Entra ID (23/10); membros não administrativos pendentes | regras v1.2 RN-06 |
| Pedidos com baixa transacional (ADR-010) | Implementado; **desligado** (`ORDERS_ENABLED=false`) | ADR-010 |
| Mudança de status com estorno (S4) | Implementado; **desligado**; só `Store.Admin` | `migration/progresso-s0-s4.md` |
| Escrita do painel: NF, ajuste, produto, fotos, cupons (ADR-013) | Implementado; **desligado** (`ADMIN_WRITE_ENABLED=false`) | ADR-013 |
| Painel React `/admin` | **Fatia A** (base + visão geral) pronta, aguardando aprovação; fatias B–H não iniciadas | `painel-admin-fatias.md` |
| Checkout, "Meus pedidos", PDF | Não existem na nova aplicação | regras v1.2 RN-00 |
| Pagamentos (ADR-012) e moedas (ADR-011) | Propostas; sem tabelas nem rotas | ADR-011/012 |
| Legado v29 | Web em loop (não funcional); API Node ativa; publish do Node apaga `estoque_movimentos` | KS de deploy §3, §25 |
| Corte do legado | **Não autorizado** | KS de deploy §10 |

## 2. MVP (Etapa de produto 1) — o que falta, por item

| Item | Falta | Bloqueio | Dono |
|---|---|---|---|
| MVP-01 Catálogo | Regra "só visível com preço e estoque" (DV-10) | — | Dev |
| MVP-02/03 Produtos | Telas (fatia C); ligar escrita | Gate do publish do Node (A-10) | Dev · Node · Infra |
| MVP-04 NF | Tela (fatia B); regra ≤ × = (DV-13) | Q-25 | Gestor · Dev |
| MVP-05/06 Estoque CPF × inst. por unidade | Unidade na baixa (Q-15, Q-30); escritor único de `estoque_movimentos` | Q-30 | Gestor · Dev |
| Preço (RN-10) | Margem global persistida; arredondamento | Q-18, Q-19; tabela nova (DBA) | Gestor · DBA |
| MVP-07 Pedido PIX manual | Checkout; registro mínimo de pagamento; estados do fluxo manual | Q-03b, Q-08; ADR-012 | Gestor · Dev |
| MVP-08 Institucional | Campo finalidade; validação antes do débito | Q-23, Q-29 | Gestor · Dev |
| MVP-09 Registro + PDF | Geração de PDF (servidor, proposta) | — | Dev |
| MVP-10 Admin | Ligar Entra ID; redirect URI HTTPS; validar os três acessos | 8443 na VPN; certificado; TI | Infra · TI · Dev |
| Carga de produtos | Lista normalizada, divisão CPF × inst., custos | Q-27, Q-28 | Gestor · Dev |

**Caminho crítico:** produtos → entrada da nota → separação do estoque → preço → permissões → pedido PIX/CC → PDF →
validação operacional. **Pré-condição transversal:** bloquear o publish do Node no mesmo deploy que liga qualquer
escrita da FastAPI (A-10).

## 3. Implementações futuras

### 3.1 Etapas de produto (gestor)

| Etapa | Conteúdo | Status de negócio |
|---|---|---|
| 1 — Primeira versão vendável | Seção 2 | GO |
| 2 — Validação operacional | Acessos, quantidades, baixa, fluxos CPF/inst., retirada e rastreio, ajustes do painel (V26) | GO |
| 3 — CAST Coins | Conversão, elegíveis, pagamento integral/parcial/misto, gestão de saldo (Marketing adiciona, TI remove), inativos, trilha | **NO-GO** até CC-01…06 |
| 4 — Automações | Confirmação de recebimento, encerramento automático, M365, PIX automático, QR Code, entrega | Backlog |

### 3.2 Adequação de arquitetura (proposta de 29/10 — aguardando aprovação)

| Fase | Quando | Conteúdo |
|---|---|---|
| R0 — Guardas | Já, em paralelo | ADR-015; import-linter e ESLint boundaries em modo catraca; CI de integração também em MySQL 5.7 |
| R1 — Dependências | Antes de moedas/pagamentos | `get_principal` e `Capability` para `identity`; tirar `orders` de `core/config` |
| R2 — Migração por fatia | Junto do MVP | NF, estoque por unidade, pricing e pedido nascem nos módulos donos; `inventory` escritor único; `backoffice` só encolhe |
| R3 — Módulos novos | Após decisões | `payments`, `documents` (PDF), `coins` (esqueleto); outbox |
| R4 — Extração | Adiar | Só com 2+ gatilhos (seção 6 da análise) |

Transição do legado por capacidade (T1–T6): vitrine → login → escrita de estoque/NF/produto/preço (com bloqueio do
publish) → pedidos + pagamento + PDF → painel React substitui `admin.html` → desligar Node e `/data.js`.

Arquitetura-alvo: monolito modular com 12 módulos e fachadas, outbox + worker na mesma imagem, **reserva × baixa** de
estoque com máquina de estados configurável, autorização grupo → role → capacidade por configuração, pagamentos como
livro-razão multi-meio (base do pagamento misto) e política de resgate de moedas plugável (desligada até CC-01…06).

### 3.3 ADRs propostos (numeração a unificar)

As duas propostas de 29/10 numeram de forma diferente (**divergência DV-14**):

| Tema | Análise de arquitetura | Arquitetura-alvo |
|---|---|---|
| Monolito modular + fronteiras | ADR-015 | ADR-015 |
| Dono único de tabela / `inventory` | ADR-016 | ADR-016 |
| Comunicação entre módulos / outbox + worker | ADR-017 | ADR-017 |
| Autorização (identity, grupo → role → capacidade) | ADR-018 | ADR-019 |
| Contrato OpenAPI como artefato | ADR-019 | — |
| Reserva × baixa e máquina de estados | — | ADR-018 |
| Precificação | ADR-020 | ADR-020 |
| Pagamentos multi-meio | — | ADR-021 |
| Versão do MySQL | ADR-021 | ADR-022 |

Recomendação: adotar a numeração da **arquitetura-alvo** (documento posterior) e acrescentar "Contrato como artefato"
como ADR-023, ao aprovar.

## 4. Itens da planilha de 20/10 ainda abertos

| Item | Situação em 29/10 |
|---|---|
| CI verde no GitHub | Workflows de release HML criados; CI aprovado nos PRs de deploy (KS de deploy §8) |
| Paridade com massa real (VT-01) | Pendente |
| "Restam N", LCP, contraste AA | Decisões de negócio pendentes |
| Stamp Alembic, UTC, collation | Pendentes (DBA) |
| Usuário `caststore_orders`, integração MySQL na CI | Pendentes |
| Publish do Node | **Bloqueio** |
| Produto sem movimento | Decisão pendente (relacionada a DV-10) |
| Fotos reais em produto ativo | Pendente (carga) |
| Parceiros como convidados no tenant | Pergunta aberta |
| Supervisão/runbook operacional (INF-03) | Parcial: KS de deploy cobre a homologação |
| Fases 5–10 | 5 e 8 avançaram (rotas ADR-013 e fatia A do painel); 6, 7, 10 não iniciadas; 9 com carrinho local |

## 5. Decisões necessárias (consolidado)

| Quem | Decisões |
|---|---|
| Gestor | Q-03b momento da baixa · Q-08 PIX · Q-16 funções × roles · Q-17/CC-01…06 moedas · Q-18/Q-19 margem e arredondamento · Q-21 inativação · Q-23/Q-29 centro de custo e finalidade · Q-24 pedido social · Q-25 NF ≤ × = · Q-27 dados da carga · Q-30 unidade na entrega · P-05 piloto só CPF? · P-07 estoque das compras por pontos |
| TI (Entra ID) | Registro dos apps, membros dos grupos, redirect URI HTTPS |
| Infra | Regra da 8443 na VPN/ZTNA, certificado definitivo, registry, regras de proxy para escrita |
| DBA | MySQL 5.7 × 8.0, usuários por papel, stamp Alembic, tabelas novas |
| Segurança | Aceite para publicação/corte, M365 pelo servidor, destruição das cópias da chave, rotação de credenciais |
| Time do Node | Publish que não apague `estoque_movimentos` (ou bloqueio) |
