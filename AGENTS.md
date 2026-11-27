# Documentação do Zazz Chat

Site de documentação da API pública do Zazz Chat, feito com [Mintlify](https://www.mintlify.com/docs). As páginas são MDX com frontmatter YAML. A configuração fica em `docs.json`.

## Antes de editar

- Consulte a doc do Mintlify, não a memória. Índice para agentes: `https://www.mintlify.com/docs/llms.txt`. MCP de busca: `https://mintlify.com/docs/mcp`.
- Skill do Mintlify para agentes: `npx skills add https://mintlify.com/docs` (ou `mint agent setup --agent claude-code`).
- Preview local: `npx mint dev` (porta 3000).
- Antes de commitar: `npx mint validate` e `npx mint broken-links`.

## Estrutura

| Caminho | Conteúdo |
|---------|----------|
| `docs.json` | Navegação por `versions` (v2 padrão, v1 com tag `Deprecated`), redirects. Sem `openapi` nas abas: cada página aponta o próprio spec (com `openapi` na aba o Mintlify gera um grupo duplicado com todos os endpoints) |
| `guias/` | Guias: `api-v2` (v2), `usar-com-ia` (MCP, skill e llms.txt para assistentes de IA), `introducao` (v1 legada), `webhooks`, `socket` |
| `api-reference/openapi-v2.json` | Spec da v2 e dos webhooks |
| `api-reference/openapi.json` | Spec da v1 legada |
| `api-reference/v2/` | Páginas de endpoint da v2 |
| `api-reference/endpoint/` | Páginas de endpoint da v1 legada |
| `api-reference/webhooks/`, `api-reference/socket/` | Eventos de webhook e Socket.IO (valem para v1 e v2) |

## API v1 e v2

- A v2 (`https://api.zazzinternet.com/v2/...`) é a API atual. Só API key de conta (`Authorization: ApiKey zk_live_...`).
- A v1 (`/channel-api/...`) está descontinuada e sai do ar em **31/12/2026**. Não documente recurso novo na v1. Depois dessa data, as páginas da v1 saem do site.
- A fonte da spec v2 é `docs/api/public-api-v2.openapi.yaml` no repo `public-api-gateway-node-zazz`. Ao mudar a API, atualize `openapi-v2.json` a partir dela.

## Regras de frontmatter

- Toda página tem `title` e `description`.
- Página de endpoint referencia o arquivo da spec com barra inicial e método em maiúsculas: `openapi: "/api-reference/openapi-v2.json POST /v2/messages"`. O caminho do arquivo é obrigatório porque o repo tem mais de uma spec.
- Webhook: `openapi: "/api-reference/openapi-v2.json webhook message_received"`.
- Página da v1: `deprecated: true`.

## Estilo

- Português do Brasil, segunda pessoa ("você"), voz ativa.
- Uma ideia por frase. Títulos com só a primeira letra maiúscula.
- Elementos de tela em negrito: **Configurações → API Keys**.
- Código, arquivos, campos e headers em `código`.
- Todo bloco de código com a linguagem. Exemplos testados de verdade.
- Links internos relativos (`/guias/api-v2`).
- Nunca use token, telefone ou ID reais em exemplos. Use `zk_live_...`, `5511999990000` e `66cc000000000000000000d1`.

## Não fazer

- Não documentar rota interna, tela de admin ou detalhe de infraestrutura.
- Não inventar campo ou comportamento: confira na spec ou no código do gateway.
- Não commitar direto na `main`: use branch e PR.
