# Reunião de alinhamento do MVP com o gestor da CAST Store

- **Data da reunião:** não consta nas anotações (registrada na documentação em 29/10/2026). Prazos citados
  ("ainda nesta semana", "amanhã à tarde") ficam **relativos**, sem conversão para data.
- **Participantes (por função):** gestor da CAST Store (negócio) e desenvolvimento.
- **Fonte:** anotações geradas por IA e revisadas pela dona técnica. Cada ponto foi classificado em
  **decidido**, **a validar** ou **backlog**; tarefa sugerida não é compromisso confirmado.
- **Resultado:** **GO para o MVP; NO-GO para regra financeira definitiva de CAST Coins.**
- Regras consolidadas: `docs/negocio/regras-de-negocio-v1.md` (v1.1).

## Decidido

| # | Decisão | Regra |
|---|---|---|
| M1 | MVP: catálogo + administração de produtos + entrada e separação de estoque + pedido por PIX manual ou centro de custo + registro + PDF + área administrativa para autorizados | RN-00 |
| M2 | Entrada de nota com produto, quantidade recebida, custo unitário, unidade/local, quantidade CPF e institucional; impedir CPF + institucional > recebido; feedback vermelho/verde | RN-01 |
| M3 | Estoque por produto + variação + unidade + finalidade | RN-02 |
| M4 | Margem configurável (global e por produto); 25% como ponto de partida, não como regra final | RN-10 |
| M5 | Institucional: centro de custo, finalidade, validação antes do débito, sem margem, **sem moedas** | RN-10, RN-12 |
| M6 | Moedas apenas em compras por CPF (integral, parcial ou misto — regras a definir) | RN-07 |
| M7 | Marketing: fotos, descrições e conteúdo; adiciona moedas; não altera custo, preço, estoque ou regras financeiras. TI remove moedas e cuida dos controles sensíveis. Gestão CAST Store para Compras/Facilities | RN-06 |
| M8 | Usuário que sai: inativo, saldo zerado e registrado, histórico preservado | RN-11 |
| M9 | Pedido CPF com PIX manual (comprovante validado pela equipe), sem QR Code; entrega por correio com rastreio ou retirada | RN-12 |
| M10 | Painel administrativo pode ser reorganizado (V26 como referência), sem mudar regras nem remover campos | RN-09 |
| M11 | Acesso administrativo inicial para três validadores, via Entra ID + permissão administrativa | RN-05, RN-06 |

## A validar (pendências com o gestor)

Valor do CAST Coin e conversão (Q-17) · pagamento misto (Q-17) · produtos elegíveis (Q-17) · margem de 25% como
padrão (Q-18) · arredondamento (Q-19) · mecanismo de inativação e aprovador do zeramento (Q-21) · divisão exata
Marketing × TI (Q-16) · dados obrigatórios do centro de custo (Q-23) · fluxo pelo Posso Ajudar (Q-22) · momento
exato da baixa (Q-03b) · conteúdo e destinatários do e-mail (Q-26) · "pedido social" como tipo próprio (Q-24) ·
planilha como carga inicial ou cadastro permanente (Q-20).

## Adiado (backlog)

Confirmação de recebimento · encerramento automático · automação do despacho e da entrega · e-mail automático
(Microsoft 365) · PIX automático · QR Code · regras definitivas do pagamento misto.

## Responsabilidades (por função)

| Função | Itens |
|---|---|
| Desenvolvimento (dona técnica) | Estrutura de produto; custo, margem e preço sugerido; entrada de notas; separação CPF × institucional; validação de quantidades; estoque por unidade; grupos de acesso e separação Marketing / Gestão CAST Store / Gestão Coins / TI; inativos; administração de produtos; pedido PIX e por centro de custo; pedido e PDF; finalidade institucional; ativar acesso administrativo e validar os três acessos; revisar o painel com base na V26; registrar confirmação de recebimento no backlog |
| Gestor | Conversão real × moeda; elegíveis; pagamento misto; estratégia de preço sugerido; versão mais recente do protótipo; revisão do desenvolvimento |
| Compras/Facilities | Estoque, notas, custos, validação de pagamento, separação, despacho |
| Marketing | Fotos, descrições, conteúdo, adição de moedas |
| TI | Remoção de moedas, controles sensíveis, suporte técnico e de acesso |

## Observações de rastreabilidade

- Esta reunião **reverte** a regra de 23/10 que ligava o estoque institucional às moedas (DV-01).
- A hipótese de defeito de estado no JavaScript do formulário de entrada é hipótese técnica, não diagnóstico.
- Próximo alinhamento: dia seguinte à reunião, no meio da tarde (horário não registrado).
