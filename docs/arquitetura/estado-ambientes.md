# Estado dos ambientes — CAST Store

| Metadado | Valor |
|---|---|
| Versão | 1.0 — rascunho para revisão |
| Data | 2026-10-23 |
| Origem | Instrução de produto de 23/10/2026 · reunião de 22/10/2026 · relatório de status de 21/10/2026 · `runbook-piloto.md` |
| Regra deste documento | Só se afirma "publicado" ou "operacional" com **evidência técnica** registrada na coluna "Evidência" |

## Situação confirmada

| Item | Situação | Evidência |
|---|---|---|
| Domínio `store.cast4it.com` | Tratado como **DNS interno** (resolve com VPN/rede interna). **Não há evidência de publicação externa** | Reunião 22/10; sem teste externo registrado |
| Publicação legada (v29) no servidor | **Não deve ser descrita como funcional** | Instrução de 23/10; o painel publica no endereço errado (relatório 21/10, item 30) |
| Acesso SSH ao servidor | **Depende de liberação pela Segurança** | Chamado #495532 (acesso ao MySQL DSV/logs) ainda pendente |
| Portas e TLS | **Precisam de validação** pela Infra (correções prontas só em branch: porta direta da API, cadeia TLS) | Relatório 21/10, itens 34–35 |
| Certificado | Reemissão com chave nova pendente (A3 da reunião 22/10) | — |
| Vitrine React / FastAPI / proxy novo | Prontos e testados **localmente**; **não aplicados** no servidor | Relatório 21/10 |
| Login Entra ID | Código pronto; **login real não validado** | `cast-store-backend/docs/security/entra-id-registro.md` |

## Pré-requisitos para publicação (piloto ou produção)

1. **HTTPS** com certificado válido e cadeia completa.
2. **Redirect URI** do app SPA no Entra ID correspondente **exatamente** à URL publicada.
3. **Validações da Segurança** (critérios do piloto ainda não definidos — Q-11) e, para acesso fora da rede
   interna, certificado SSL e aprovação explícita (D8 de 22/10).
4. Autorização do negócio para substituir o que está no servidor (A2 de 22/10), com backup conferido.
5. Portas e regras de firewall validadas pela Infra (Q-10).

Enquanto esses itens não tiverem evidência, os documentos devem dizer "pronto localmente" ou
"pendente de validação", nunca "publicado".

## Questões em aberto

- Q-10 URL, TLS, portas e redirect URI do ambiente publicado — TI/Infra · Segurança.
- Q-11 Critérios de segurança para liberar o piloto — Segurança.
- Acesso SSH — Segurança.
