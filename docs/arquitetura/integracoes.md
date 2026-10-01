# Integrações Office 365 / SharePoint (opcionais)

| Integração | O que faz | Observações |
|---|---|---|
| **Login corporativo (Entra ID/MSAL)** | Autentica colaboradores e define o grupo do painel pelo e-mail | Exige registro de app no Azure (SPA com as URLs do site; permissões delegadas `User.Read`, `Mail.Send`, `Sites.ReadWrite.All`) |
| **Envio de pedido via Graph** | E-mail sai da conta do colaborador com PDF anexo e CC | Requer O365 ativo |
| **Lista de pedidos no SharePoint** | Fila com status gerida pela equipe | Alimenta o "Meus pedidos" |
| **Estoque online (lista SharePoint)** | Saldo total por produto com baixa automática | Recurso da fase 1; na fase 2 o MySQL assume esse papel com atomicidade real |

## Dependências de internet no navegador

| Host | Uso |
|---|---|
| `alcdn.msauth.net` | MSAL |
| `cdnjs.cloudflare.com` | jsPDF, QRCode |
| `viacep.com.br` | Busca de CEP |
| `login.microsoftonline.com` | Login (só com O365 ativo) |
| `graph.microsoft.com` | E-mail/SharePoint (só com O365 ativo) |

Guia completo: `PASSO-A-PASSO-SharePoint.md`.
