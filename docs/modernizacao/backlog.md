# Backlog

Ideias avaliadas e guardadas para depois. Não fazem parte de nenhuma fase em andamento.

## BL-001 · Assistente de montagem de pedido e kit (IA)

| Campo | Valor |
|---|---|
| Status | **No backlog** |
| Registrado em | 13/10/2026 |
| Origem | Debate sobre IA no projeto |
| Dona | Fabia |

**Proposta:** agente que faz até 3 perguntas e sugere produtos do catálogo, focado em
**pedidos institucionais e presentes** com restrições combinadas (quantidade, orçamento, unidade
de retirada, tamanhos, prazo, campanha). Termina num **carrinho pré-montado** que a pessoa revisa
e finaliza.

**Fora do escopo:** chat genérico de vitrine e pedido social simples.

### Condições de desenho

1. O modelo conversa; **o código decide** — filtro, estoque e encaixe no orçamento são funções
   determinísticas do backend.
2. Só sugere o que vem das ferramentas de consulta: nunca produto, preço ou estoque inventado.
3. Nunca cria pedido; só monta o carrinho.
4. Quando nada atende, diz isso e mostra a alternativa mais próxima.
5. Sem dados pessoais, custos ou fornecedores — só o catálogo público.

### Dependências e lacunas

- Usa `GET /api/v1/storefront/catalog` (já existe, somente leitura).
- **Lacuna:** o catálogo público não traz saldo institucional **por unidade**.
- Interface: a vitrine v29 não será alterada agora → entra com o front novo (Fases 8/9) ou como página separada.
- Provedor de IA aprovado pela Cast (contrato sem retenção de dados).

### Avaliação e continuidade

- Evals com cenários de restrições sobre o catálogo sintético dos testes; checagens automáticas
  (produto existe, ativo, com estoque no destino, cabe no orçamento, tem o tamanho).
- Rubrica: ≤ 3 perguntas; admite quando nada atende.
- **Critério do piloto:** % de conversas que viram carrinho e tempo até o carrinho. Se não ganhar
  da vitrine nos pedidos institucionais, encerrar.
- **Reavaliar** quando o front novo estiver em andamento, o catálogo crescer ou kits ganharem volume.

## Itens da reunião de 22/10/2026

Sem regra de negócio definida — ver [Reunião 22/10](reuniao-2026-10-22.md).

| ID | Item | Quando | Dependências |
|---|---|---|---|
| BL-002 | Histórico de compras por usuário | Pós-piloto | Entra ID; pedidos gravados no servidor |
| BL-003 | Consulta do próprio saldo de moedas | Pós-piloto | Entra ID; Moedas-1 |
| BL-004 | Cadastro/ajuste de saldo de moedas por pessoa, com grupo próprio de ajuste | Pós-piloto | Nova role/grupo (não definida); responsável do negócio (A4); estoque consumido (I2) |
| BL-005 | Carga de produtos e fotos para o piloto | **Piloto** | Lista do negócio; script versionado e reversível, só no DSV |

## Ideias descartadas

| Ideia | Decisão | Motivo |
|---|---|---|
| Leitura assistida de NF de entrada (DANFE → pré-preenchimento) | Descartada (13/10/2026) | Volume baixo de notas; ganho pequeno para o esforço e o risco. A loja não emite NF. |
| Chat genérico / busca semântica na vitrine | Descartada | Catálogo pequeno; filtros e busca atuais resolvem. |
| Previsão de reposição com LLM | Descartada como IA | Se necessário, é estatística simples sobre os movimentos. |
