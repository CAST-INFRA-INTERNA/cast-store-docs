# Visão Geral

A **CAST Store** é a primeira loja social da CAST: um portal interno de compra de brindes
em que parte do valor arrecadado é convertido para ações sociais (divulgadas na CASTNet).
Colaboradores navegam pelo catálogo, montam o carrinho e enviam pedidos; as equipes internas
(TI, Gestores, Marketing, Compras/Facilities) administram catálogo, estoque, campanhas,
cupons e relatórios por um painel com perfis de acesso.

## Princípios do projeto

- Frontend 100% estático (HTML/CSS/JavaScript puro), hospedado em servidor on-premise da
  CAST (IIS/Apache/Nginx), sem dependência de frameworks.
- Backend evolutivo: começou sem servidor (arquivo `data.js` + e-mail), ganhou integrações
  Office 365/SharePoint direto do navegador e, na fase atual, uma **API Node.js + MySQL**.
- Identidade visual oficial CAST e regras de negócio da operação real (notas fiscais,
  estoque por destino, margens, curva ABC, inventários).

## Estado atual (16/10/2026)

| Frente | Situação |
|---|---|
| Loja e painel | **v29** em produção (HTML/JS puro + API Node.js + MySQL) |
| Pedidos | Saem por **mailto + PDF**; ainda não são gravados no banco nem baixam estoque |
| Modernização | [Assessment v29](../modernizacao/assessment-v29.md) concluído; [Backend FastAPI](../modernizacao/backend-fastapi.md) com a fatia 1 entregue e a Fase 2a em homologação |

## Responsável

| Papel | Pessoa |
|---|---|
| Owner do projeto | Rafael Martim (rafael.martim@cast4it.com) |

## Por onde seguir

- [A Loja](a-loja.md) — a jornada do colaborador, da vitrine ao pedido.
- [Perfis de Acesso](perfis-de-acesso.md) — quem pode o quê no painel.
- [Arquitetura](../arquitetura/visao-geral.md) — modo arquivo × modo banco.
- [Painel de Administração](../operacao/painel-admin.md) — onde produto, estoque e relatórios são geridos.
- [Roadmap](roadmap.md) — pendências combinadas.
- [Modernização](../modernizacao/assessment-v29.md) — riscos, decisões e o novo backend.

## Documentos complementares

`REGRAS-DE-NEGOCIO.md` (regras detalhadas por área), `HISTORICO-desenvolvimento.md`
(narrativa completa do desenvolvimento), `MAPA-DE-REIMPORTACAO.md` (restauração do backup),
`GUIA-MYSQL-API.md` e `PASSO-A-PASSO-SharePoint.md` (implantação).
