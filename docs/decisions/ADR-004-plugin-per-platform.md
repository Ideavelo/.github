# ADR-004 — Plugin independente por plataforma

- **Status:** Aceita
- **Data:** 2026-11-07

## Contexto
Usuários descobrem integrações pelo nome da ferramenta, e MCP nativo nem sempre equivale a conexão simples com ChatGPT.

## Decisão
Um plugin comercial independente por plataforma, com arquitetura de serviços compartilhados. Coolify e GitHub são os dois primeiros produtos definidos; demais plataformas são candidatas.

## Consequências
Identidade comercial, publicação, versionamento e evolução separados; OAuth, segurança e faturamento podem reutilizar serviços. A publicação no marketplace depende de critérios e aprovação da plataforma.
