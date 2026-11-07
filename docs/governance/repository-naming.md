# Padrão de nomenclatura de repositórios — v1.0

**Status:** aprovado como convenção corporativa; aplicação em repositórios existentes requer migração explícita.

## Regra

Para novos produtos, usar `{propriedade}-{categoria}-{produto}`, com nomes minúsculos em kebab-case.

- Propriedade: `internal` (propriedade intelectual Ideavelo) ou `customer` (propriedade do cliente).
- Categorias iniciais: `plugin`, `saas`, `app`, `platform`.
- Para clientes, acrescentar identificador estável: `customer-{categoria}-{cliente}-{produto}`.
- Infraestrutura operacional pode usar `infra-{componente}`.

Exemplos: `internal-plugin-coolify`, `internal-plugin-github`, `internal-platform-integrations`, `customer-saas-acme-crm`.

## Exceções e legado

`factory`, `.github`, `website` e `coolify-mcp-gateway` são repositórios existentes; não renomear automaticamente. `internal-plugin-proxmox`, `internal-plugin-plesk` e `internal-plugin-dokploy` são apenas candidatos, não projetos aprovados.

## Metadados

Adicionar topics como `ideavelo-internal`/`ideavelo-customer`, categoria, `mcp` quando aplicável e tecnologia integrada. Nome e topics são índices auxiliares: o Product Registry é a fonte de verdade.
