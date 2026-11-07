# Instruções corporativas para agentes Ideavelo

Antes de criar, renomear, provisionar ou implantar um produto, consultar `docs/governance/`, `docs/architecture/` e ADRs vigentes em `docs/decisions/` neste repositório.

1. Confirmar propriedade `internal`/`customer`, categoria e identificador de produto.
2. Validar padrão de nomes e registrar no Product Registry; não inferir que um repositório ou deploy existe apenas porque foi documentado.
3. Usar adaptadores de provedores e reutilizar recursos existentes. Não criar estruturas aninhadas em Coolify.
4. Preservar `Infrastructure` independente e `ideavelo-website` temporário; não alterar gateway Coolify existente sem autorização e migração.
5. Aplicar menor privilégio, segregação de tenants, aprovação para ações sensíveis, orçamento e auditoria.
6. Registrar evidências e distinguir `planejado`, `criado`, `implantado` e `homologado`.
7. Se houver conflito, não improvisar: solicitar decisão e registrar novo ADR.

**Importante:** este arquivo é uma orientação corporativa; sua leitura automática por agentes de outros repositórios requer integração explícita na Factory e/ou instruções locais nesses repositórios. Validadores automáticos devem reforçar as regras.
