# OAuth, credenciais e conexões — proposta v1

**Status:** proposta para revisão de segurança e compatibilidade com plataforma.

## Login Ideavelo

Utilizar OIDC/OAuth 2.0 Authorization Code com PKCE para usuários e sessões. Tokens de acesso curtos, refresh rotativo quando suportado, validação de issuer/audience/expiry/state/nonce quando aplicável. Sessões por dispositivo com revogação. MFA exigido para ações de alto risco e administração, sujeito ao provedor e política.

## Conexão ChatGPT ↔ plugin

Cada plugin expõe identidade e recursos MCP compatíveis com a versão exigida pelo cliente e fluxo OAuth suportado pela plataforma. A autorização deve vincular usuário, tenant selecionado, plugin e escopos concedidos. Não usar um token universal para todas as organizações ou plugins. Validar audience/resource, PKCE e consentimento, sem presumir que a simples existência do MCP concede autorização.

## Coolify

1. Usuário autenticado escolhe organização Ideavelo e registra URL da instância Coolify.
2. Serviço valida URL contra SSRF, redirects, DNS rebinding e destinos internos não autorizados, com política explícita para instalações privadas.
3. Usuário fornece credencial de API Coolify por canal seguro; backend verifica capacidade e permissões, sem registrar segredo em logs.
4. Credencial é cifrada e armazenada em cofre, associada à instalação; chamadas recuperam credencial apenas em execução autorizada.
5. Rotação e revogação tornam credencial anterior inutilizável; desconexão elimina acesso, observadas retenções legais de auditoria.

Não tratar o Bearer Coolify como credencial de login no ChatGPT; a plataforma Ideavelo atua como intermediária autorizada.

## GitHub

Preferir GitHub App com instalação por organização/conta e permissões mínimas. Fluxo de instalação vincula callback e state ao tenant Ideavelo. Tokens de instalação de curta duração obtidos sob demanda; webhooks com assinatura e proteção contra replay. Conferir ID da instalação e permissões em cada ação. Não usar PAT amplo como padrão comercial.

## Segurança operacional

Criptografia em repouso com envelope encryption/KMS quando disponível, TLS, rotação de chaves, segregação por tenant, política de retenção, logs redigidos, rate limiting, trilha de consentimento, proteção contra CSRF e replay. Segredos nunca em prompts, URLs, métricas ou traces.

## Revogação

A revogação de acesso Ideavelo bloqueia imediatamente chamadas futuras no gateway. Revogação externa (GitHub App uninstall / Coolify token revogado) deve invalidar instalação ao ser detectada. Diferenciar suspensão da assinatura de revogação de credenciais.
