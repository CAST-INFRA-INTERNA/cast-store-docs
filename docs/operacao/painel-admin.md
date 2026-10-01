# Painel de Administração (`admin.html`)

O rodapé do painel exibe **versão e data/hora de geração (GMT-3)** — confirma qual build
está no ar. As abas visíveis dependem do perfil: veja [Perfis de Acesso](../negocio/perfis-de-acesso.md).

## Entradas & Estoque — onde o produto nasce

- **Nota de entrada obrigatória** para toda entrada: número/série/data e fornecedor
  completo (razão social, CNPJ, IE, contato, telefone, e-mail, endereço).
- Item da nota: **produto existente** ou **produto novo** (cadastrado ali: código único,
  nome, cor/variação e grupo em dropdowns com "➕ Novo...", tamanhos em checkboxes com
  N/A exclusivo, NCM, imposto %). Produto novo nasce **oculto** no catálogo.
- Quantidades: **Total = Institucional + CPF** — preencher um calcula o outro; a soma é
  validada. Destino físico: **1 unidade** ou **várias** (rateio obrigatório por unidade,
  também dividido em inst/CPF, fechando com o item; mínimo 2 unidades no modo "várias").
- O custo unitário da NF atualiza o custo do produto e alimenta o histórico.
- Ajustes manuais (±) com motivo obrigatório; tabela de estoque atual (institucional ×
  CPF × total, com detalhe por unidade e **classe ABC**); log de movimentações
  (quem, quando, tipo, destino, unidade, quantidade, referência).

## Catálogo — a cara da loja

- Edição apenas (produtos nascem na NF); código somente leitura.
- Nome de exibição, categoria, descrição, fotos (1–5; Foto 1 obrigatória, redimensionadas
  a 800px), grupo/variação (dropdowns), tamanhos (checkboxes), selos (destaque, campanha,
  novidade), visibilidade.
- **Financeiro:** custo exibido = **média ponderada das entradas de NF** (com última
  entrada e NF de origem); margem (%) ⇄ preço calculados bidirecionalmente sobre o
  custo médio; preço promocional.
- **Sem foto ou sem preço → "Pendente"** — não pode ser ativado na loja.

## Marketing

Campanha ativa (Dia dos Pais, Natal, BlueDay... — selo 🎉 + filtro na vitrine),
link da CASTNet (pedido social) e gerador de **QR code** da loja (download PNG).

## Cupons

Código, tipo (% ou R$), valor, escopo (compra inteira ou um produto), ativo/inativo.

## Relatórios

- Cartões: produtos, itens em estoque, estoque a custo, potencial de venda, notas,
  movimentações.
- **Curva ABC** individual por produto — critérios: consumo (valor das saídas × custo
  médio) ou valor em estoque. Tabela na tela + CSV.

| Classe | Faixa do valor acumulado |
|---|---|
| A | até 80% |
| B | 80–95% |
| C | restante |

> O item que cruza a linha pertence à classe superior.

- **Inventários por período:** semanal (ISO), mensal, trimestral, semestral e anual —
  entradas, saídas e saldo final por produto e destino, com prévia do período recente.
- Exports CSV (abrem no Excel): estoque (destino × unidade + ABC), movimentações,
  compras/notas, catálogo (NCM/imposto/custos/margens), **margens por entrada de NF**
  (margem do preço atual sobre o custo de cada entrada).

## Configurações (somente TI)

Dados da loja (nome, e-mail dos pedidos, unidades, domínios permitidos, prazos),
**grupos de acesso** (4 listas de e-mails), **usuários locais** (e-mail/senha/grupo),
autenticação Office 365 (tenant/client ID), SharePoint (pedidos + estoque online) e
**Banco de dados/API** (URL + chave — a chave fica apenas no navegador do admin).

## Publicação

| Ação | Quando usar |
|---|---|
| **Publicar no banco (API)** | Fluxo oficial da fase 2: grava todo o estado no MySQL em transação (fatiado automaticamente quando grande) |
| **Baixar data.js** | Modo arquivo (plano B) — substituir o arquivo no servidor |
| Rascunho | As edições ficam no navegador (localStorage) até publicar; há botão de descarte |
