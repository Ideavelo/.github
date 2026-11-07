# Decisões propostas — núcleo compartilhado

**Status:** proposta para revisão arquitetural. Não substitui ADRs corporativas existentes.

## Decisão A — PostgreSQL

Usar PostgreSQL para dados transacionais do núcleo de plugins, com migrations versionadas, constraints de integridade, backups e restore testado. O cofre de segredos permanece separado. Versão do servidor e HA são decisões de infraestrutura futuras.

## Decisão B — Limites de serviço

Iniciar com núcleo modular com fronteiras explícitas (identity, tenants, installations, billing, audit), evitando microsserviços prematuros. Cada plugin tem serviço/adaptador independente e deploy desacoplado. Separar serviços quando volume, segurança ou autonomia justificar.

## Decisão C — Autorização

Permissões efetivas derivadas de identidade + membership + entitlement + instalação + permissões do provedor. Negação por padrão, verificações no backend e auditoria. RLS como defesa adicional, não substituta.

## Decisão D — Segurança de credenciais

Armazenar somente referências no banco de negócio; usar cofre com criptografia, rotação, revogação e auditoria. GitHub App para acesso GitHub; tokens Coolify específicos por instância.

## Decisão E — Contratos e compatibilidade

API versionada em `/v1`, idempotência em mutações, eventos via outbox e documentação OpenAPI. MCP/OAuth dos plugins devem ser verificados contra as especificações e requisitos vigentes antes da implementação.

## Questões pendentes para implementação

Provedor de identidade, cofre/KMS, provedor de billing, estratégia de hospedagem PostgreSQL, tenancy física versus lógica, retenção de auditoria, SLAs, custos e suporte a instâncias Coolify em redes privadas.
