# Plataforma compartilhada de plugins

**Status:** arquitetura de referência, sujeita a desenho técnico e análise de custos.

## Responsabilidades centrais

- Identidade, OAuth e gestão de sessões.
- Tenants, usuários, instalações e autorizações.
- Cofre de credenciais e ciclo de vida de segredos.
- Catálogo de plugins, versões, planos, assinaturas e entitlements.
- Auditoria, observabilidade, rate limiting, quotas e medição de uso.
- Administração e suporte com segregação de acesso.

## Limites

O plano de controle pode ser compartilhado; cada plugin mantém seu adaptador, contrato de ferramentas, permissões e pipeline de entrega. Falha de um plugin não deve derrubar os demais. O núcleo compartilhado não deve exigir permissões de Coolify para operações de GitHub, nem vice-versa.

## Estrutura de repositórios proposta

- `Ideavelo/internal-platform-core`: identidade, tenants, assinaturas, credenciais e auditoria.
- `Ideavelo/internal-plugin-coolify`: API/MCP/adaptador Coolify e experiência específica.
- `Ideavelo/internal-plugin-github`: API/MCP/GitHub App e experiência específica.

A separação entre `internal-platform-core` e eventual `internal-platform-integrations` depende de necessidades reais, evitando abstração prematura. Esses repositórios ainda não foram criados.

## Infraestrutura

Novos serviços internos ficam logicamente no projeto Coolify `Ideavelo-product-internal`, com ambientes segregados. Não criar aplicações ou bancos antes da definição de limites de segurança e operação. `Infrastructure` permanece projeto independente.
