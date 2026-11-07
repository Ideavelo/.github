# Modelo lógico PostgreSQL — núcleo de plugins v1

**Status:** proposta para revisão; sem migration ou banco criado.

## Convenções

PostgreSQL 16+ como hipótese de arquitetura (validar versão disponível). UUID como PK, `timestamptz` em UTC, `created_at`/`updated_at`, versionamento otimista `row_version` quando aplicável. Nomes `snake_case`. Segredos fora do banco de negócio; armazenar somente referências opacas a cofre. Isolamento por tenant imposto na aplicação e, onde adequado, por PostgreSQL Row-Level Security (RLS), sem confiar em RLS isoladamente.

## Entidades

| Tabela | Campos principais | Regras |
|---|---|---|
| `accounts` | id, status, display_name, created_at | Conta humana; PII mínima |
| `account_identities` | id, account_id, issuer, subject, verified_at | UNIQUE(issuer, subject) |
| `organizations` | id, slug, name, status, created_at | UNIQUE(slug) |
| `memberships` | id, organization_id, account_id, role, status | UNIQUE(organization_id, account_id) |
| `plugins` | id, slug, name, status | UNIQUE(slug); coolify/github |
| `plans` | id, plugin_id, code, status | UNIQUE(plugin_id, code) |
| `subscriptions` | id, organization_id, plan_id, status, current_period_end | Fonte de faturamento reconciliada |
| `entitlements` | id, organization_id, plugin_id, capability, limit_value, valid_until | UNIQUE(org, plugin, capability) com política de vigência |
| `installations` | id, organization_id, plugin_id, provider, external_id, status, config | UNIQUE(org, plugin, provider, external_id) quando external_id não nulo |
| `credential_refs` | id, organization_id, installation_id, vault_path, key_version, status, rotated_at | Sem material secreto |
| `oauth_clients` | id, client_id, plugin_id, status, metadata | Clientes registrados e validados |
| `oauth_grants` | id, account_id, organization_id, client_id, plugin_id, scopes, revoked_at | Consentimento por tenant e plugin |
| `audit_events` | id, occurred_at, organization_id, actor_id, plugin_id, installation_id, action, resource, decision, outcome, correlation_id, metadata | Append-only; metadados redigidos |
| `idempotency_records` | id, organization_id, operation, key_hash, request_hash, response_ref, status, expires_at | UNIQUE(org, operation, key_hash) |
| `outbox_events` | id, organization_id, event_type, payload, occurred_at, delivered_at | Entrega assíncrona com retry |

## Chaves e isolamento

Todas as FKs de dados tenant-scoped devem garantir mesmo `organization_id` (preferir chaves compostas/constraints ou triggers testados quando FKs simples não garantirem). Não permitir vincular `credential_refs` de uma organização à instalação de outra. Indexar `(organization_id, status)` em instalações/assinaturas e `(organization_id, occurred_at)` em auditoria. Definir retenção e particionamento da auditoria por volume real.

## RLS e sessões

Se usar RLS, ativar `FORCE ROW LEVEL SECURITY` nas tabelas tenant-scoped e usar role de aplicação sem `BYPASSRLS`. Configurar tenant efetivo por transação, nunca por sessão de pool sem limpeza garantida. O contexto deve ser derivado de autenticação e autorização, não do body HTTP. Testar pool, jobs, suporte e migrações com roles distintas.

## Integridade e concorrência

Operações de provisionamento e faturamento precisam de idempotência transacional, outbox e restrições de unicidade. Status devem ser modelados por enum/check ou tabelas de domínio com migrações compatíveis. Dados de billing externos reconciliados via webhook verificado, deduplicado e reprocessável.

## Privacidade

LGPD: minimização, políticas de retenção, exportação e exclusão conforme base legal, sem remover evidências que devam ser legalmente retidas. Não armazenar tokens em JSON de configuração, auditoria ou outbox.
