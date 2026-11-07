# Roadmap inicial e gates de entrega

## Fase A — Definição (agora)

Aprovar contratos de produto, diferenciação comercial, limites do núcleo compartilhado, modelo de autorização e requisitos de marketplace. Não requer Work nem modifica staging da Factory.

## Fase B — Provisionamento controlado

Criar repositórios privados de produtos e núcleo, com branch protection, topics, templates, CI de segurança e ownership; registrar no Product Registry quando este estiver disponível. Criação depende de capacidade de provisionamento e aprovação de mudanças.

## Fase C — MVP Coolify

Inventariar gateway existente; projetar isolamento multi-tenant e OAuth; implementar camada comercial sem regressão; testar com instância de staging isolada. **Não** reutilizar staging da Missão 18.1 sem autorização.

## Fase D — MVP GitHub

Implementar GitHub App e ferramentas administrativas de maior valor, com autorização e testes de idempotência/segurança. Validar lacunas versus conector oficial.

## Fase E — Comercialização

Planos, faturamento, onboarding, documentação, observabilidade e revisão de publicação. Testar mercado com usuários piloto antes de investir em expansão para outras plataformas.

## Gates transversais

Sem credenciais em código/logs; sem deploy em produção sem testes e aprovação; sem afirmação de compatibilidade de marketplace sem verificação atual; cada operação deve ser auditável e revogável quando aplicável.
