# Plano de validação de segurança e isolamento — proposta v1

## Testes mínimos antes de MVP

1. Usuário membro de dois tenants: troca explícita de contexto e impossibilidade de usar instalação de outro tenant.
2. Usuário removido/suspenso: tokens e sessões anteriores deixam de autorizar chamadas futuras.
3. Assinatura suspensa: operações protegidas negadas conforme entitlement; auditoria e obrigações de dados preservadas.
4. Dois clientes com IDs de recursos externos coincidentes: nenhum acesso cruzado.
5. Instalação GitHub revogada: operação bloqueada, token não reutilizado, webhook validado.
6. Token Coolify revogado/rotacionado: falha segura e reconexão guiada.
7. URL Coolify maliciosa (localhost, metadata cloud, redirecionamento, DNS rebinding): bloqueio ou política de rede explicitamente autorizada.
8. OAuth: state/PKCE, audience, issuer, expiry, refresh replay e sessão inválida.
9. Ações R3: negar execução sem confirmação e permissão reforçada; auditar tentativas.
10. Logs e traces: nenhum token, segredo ou dado sensível indevido.
11. Falha no cofre ou núcleo de autorização: negar novas ações, sem fallback inseguro.
12. Quotas e rate limits: limites por tenant/instalação e proteção contra abuso.

## Gates

Testes unitários, integração, segurança e validação manual em staging isolado; documentação de evidências, falhas, correções e aprovação. Não usar o staging da Missão 18.1 sem autorização. Não declarar conformidade LGPD ou aprovação marketplace apenas com estes testes.
