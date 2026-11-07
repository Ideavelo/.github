# Contratos HTTP do núcleo compartilhado — v1 (proposta)

**Status:** contrato de desenho, não API implementada. Prefixo proposto `/v1`. JSON, OAuth Bearer, HTTPS. Identificadores UUID. Erros padronizados RFC 9457 `application/problem+json`, com `type`, `title`, `status`, `detail`, `instance`, `correlationId` e `code`.

## Identidade e organização

| Método | Rota | Função | Permissão |
|---|---|---|---|
| GET | `/v1/me` | Identidade e organizações acessíveis | Autenticado |
| GET | `/v1/organizations` | Listar memberships | Autenticado |
| POST | `/v1/organizations` | Criar tenant | Política de criação |
| GET | `/v1/organizations/{orgId}` | Detalhar tenant | Membro ativo |
| GET | `/v1/organizations/{orgId}/members` | Listar membros | Admin/Owner |
| POST | `/v1/organizations/{orgId}/invitations` | Convidar membro | Admin/Owner |
| PATCH | `/v1/organizations/{orgId}/members/{memberId}` | Alterar papel/estado | Owner ou política reforçada |

## Plugins, instalações e credenciais

| Método | Rota | Função | Permissão |
|---|---|---|---|
| GET | `/v1/plugins` | Catálogo público/contratável | Autenticado |
| GET | `/v1/organizations/{orgId}/installations` | Listar instalações | Viewer+ |
| POST | `/v1/organizations/{orgId}/installations` | Iniciar conexão | Admin/Owner + entitlement |
| GET | `/v1/organizations/{orgId}/installations/{id}` | Estado e metadados | Viewer+ |
| POST | `/v1/organizations/{orgId}/installations/{id}/credentials:rotate` | Rotação de segredo | Admin/Owner + MFA/confirm. |
| DELETE | `/v1/organizations/{orgId}/installations/{id}` | Revogar instalação | Admin/Owner + confirmação |
| GET | `/v1/organizations/{orgId}/audit-events` | Auditoria paginada | Admin/Owner, política de retenção |

POST de instalação recebe `pluginId`, `provider`, metadados mínimos e dados de conexão conforme fluxo seguro. Segredos não devem trafegar em query string ou retornar em GET. Coolify usa canal protegido de entrega ao cofre; GitHub usa instalação GitHub App com state/nonce. O backend valida que orgId da URL coincide com tenant autorizado.

## Assinaturas

| Método | Rota | Função | Permissão |
|---|---|---|---|
| GET | `/v1/organizations/{orgId}/subscriptions` | Assinaturas e status | Billing/Owner |
| POST | `/v1/organizations/{orgId}/checkout-sessions` | Iniciar checkout | Billing/Owner |
| GET | `/v1/organizations/{orgId}/entitlements` | Direitos efetivos | Admin/Owner/Billing |
| POST | `/v1/webhooks/billing/{provider}` | Eventos verificados do provedor | Assinatura criptográfica, sem Bearer humano |

## Convenções

- Paginação cursor-based, com limites server-side.
- `Idempotency-Key` obrigatória em POSTs de criação/checkout/rotação e operações administrativas mutáveis; armazenar hash e verificar payload consistente.
- `If-Match`/ETag ou versão de entidade em PATCH concorrente.
- `X-Correlation-Id` gerado/validado no gateway; nunca confiar em metadados de identidade vindos do cliente.
- Autorização server-side por actor, org, entitlement, instalação, recurso e classificação de risco.
- `202 Accepted` + `operationId` para operações assíncronas; endpoint de acompanhamento com escopo tenant.
- `401` não autenticado, `403` sem permissão, `404` recurso ausente ou ocultado por isolamento, `409` conflito/idempotência, `422` validação, `429` limite.

## Exemplo sem segredos

```json
{
  "pluginId": "<uuid>",
  "provider": "coolify",
  "displayName": "Produção",
  "endpoint": "https://coolify.example.com"
}
```

O registro inicial não deve armazenar credencial no payload persistido; a vinculação de segredo exige fluxo separado com autorização reforçada.
