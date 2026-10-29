# Estado dos Ambientes

| Metadado | Valor |
|---|---|
| Versão | 1.1 — 29/10/2026 (estado técnico de 28/10/2026) |
| Observação | Versão resumida para o portal. Detalhes operacionais e de segurança ficam no runbook interno (acesso restrito) |

## Situação

| Item | Situação |
|---|---|
| Nova CAST Store (FastAPI + React) | Homologação **em execução**, isolada, acessível **somente pela rede corporativa/VPN** |
| HTTP | Acessível pela VPN |
| HTTPS | Validado no servidor; liberação na VPN **pendente** |
| Certificado definitivo | **Pendente de emissão** |
| Login Entra ID | Código pronto; **desligado** na homologação |
| Pedidos e escrita do painel | **Desligados** (flags) |
| Banco | Leitura, sem migrações |
| Publicação externa | **Não existe** evidência; o domínio é tratado como DNS interno |
| Loja legada (v29) | **Não deve ser considerada funcional** no servidor |
| Substituição do legado | **Não autorizada / não iniciada** |

> Há registro de "aplicação publicada" em 28/10 no chat com o gestor; a evidência técnica do mesmo dia mostra
> acesso apenas pela VPN. Vale a evidência técnica até novo teste.

## Impacto no MVP

O MVP definido com o gestor exige pedido, escrita do painel e login — hoje desligados — além de telas do painel,
checkout e PDF ainda em construção. Ver [Regras de Negócio](../negocio/regras-de-negocio.md) (RN-00).

## Pré-requisitos para publicar

Certificado definitivo · liberação HTTPS na VPN · redirect URI do Entra ID · aceite funcional do gestor ·
aceite de Infra e Segurança · plano de rollback · autorização formal do corte.
