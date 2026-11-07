# Produto 001 — Ideavelo for Coolify

**Propriedade:** internal | **Categoria:** plugin | **Repositório planejado:** `Ideavelo/internal-plugin-coolify` | **Status:** especificação.

## Proposta de valor

Permitir que um usuário conecte sua instância Coolify ao ChatGPT sem configurar manualmente um servidor MCP remoto com Bearer Token. O usuário mantém controle sobre instâncias, permissões e operações.

## Escopo inicial

1. Cadastro de instâncias Coolify por tenant, validação de conectividade e identificação de versão.
2. Conexão OAuth do usuário com o plugin e vinculação segura de credencial de API Coolify por instância.
3. Descoberta de projetos, ambientes, aplicações, recursos, deployments e estado de saúde, respeitando as permissões efetivas.
4. Operações administrativas de risco graduado, com confirmação explícita para mutações sensíveis e auditoria.
5. Diagnóstico de erros, observabilidade, rate limits e mensagens acionáveis.
6. Desconexão, revogação e rotação de credenciais.

## Reuso e migração

Existe o repositório operacional `Ideavelo/coolify-mcp-gateway`, que não deve ser alterado, substituído ou interrompido sem inventário de ferramentas, testes de compatibilidade e plano de migração. A solução comercial poderá reutilizar seus contratos e adaptadores após auditoria, sem acoplamento irreversível. Não presumir que o gateway atual já é multi-tenant ou apto a marketplace.

## Segurança

Segredos criptografados em repouso, nunca em logs; isolamento por tenant e instância; OAuth com PKCE onde aplicável; escopos mínimos; autorização server-side por operação; proteção contra SSRF na configuração de URLs; limites de taxa; auditoria de identidade, recurso, ação e resultado; ações destrutivas sujeitas a confirmação e política.

## Publicação

Verificar requisitos vigentes de publicação e revisão da plataforma antes de definir fluxo final de distribuição. Não prometer aprovação automática nem conexão sem consentimento.

## Critérios de aceite MVP

Um usuário conecta uma instância autorizada, consulta recursos, executa uma operação não destrutiva permitida, recebe erros inteligíveis, pode revogar o acesso, e ações de outros tenants permanecem isoladas. Evidências de testes e de não regressão do gateway existente são obrigatórias.
