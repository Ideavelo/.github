# Plano de implementação do núcleo — sem interferência na Factory

1. Revisar e aprovar modelo de entidades, fluxos OAuth e limites de autorização.
2. Definir provedores de identidade, cofre, pagamentos e infraestrutura; realizar threat modeling e avaliação de custos.
3. Provisionar repositório `internal-platform-core` e repositórios `internal-plugin-coolify`/`internal-plugin-github` após aprovação de arquitetura e disponibilidade de provisionador.
4. Criar migrations PostgreSQL com constraints, RLS quando aplicável, testes de rollback e backup/restore.
5. Implementar endpoints de identidade, organizações e instalações; contrato OpenAPI e testes de autorização.
6. Implementar cofre, OAuth por plugin, rotação e revogação de credenciais.
7. Integrar entitlements e billing com webhooks idempotentes.
8. Integrar adaptador Coolify sem regressão do gateway existente; depois GitHub App.
9. Homologar em staging isolado, com testes de isolamento, SSRF, OAuth, auditoria e operações de risco.
10. Publicar apenas após critérios de segurança, revisão da plataforma e validação comercial.

**Bloqueios:** não tocar no staging da Missão 18.1; não criar infraestrutura ou gerar custos antes da decisão técnica e autorização. Nenhum item deste plano está marcado como implementado.
