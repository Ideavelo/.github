# Integração da governança com a Factory — v1.0

Antes de provisionar um produto, o Orchestrator deve: carregar versão vigente das políticas; validar propriedade, categoria e nome; verificar duplicidade; registrar produto no Registry; solicitar autorização exigida; provisionar GitHub/infra por adaptadores; registrar identificadores reais e evidências; executar validações e reportar estado.

Regras críticas devem ser verificadas por código e testes, não apenas por prompts. Provisionamento deve usar operações idempotentes, privilégios mínimos, trilha de auditoria, limites de custo e mecanismos de compensação. Nunca presumir que a documentação por si só já implementou esses controles.

A Factory deve permitir provedores de deploy além do Coolify e manter produtos independentes da disponibilidade do Orchestrator.
