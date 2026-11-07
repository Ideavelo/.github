# Produto 002 — Ideavelo for GitHub

**Propriedade:** internal | **Categoria:** plugin | **Repositório planejado:** `Ideavelo/internal-plugin-github` | **Status:** especificação.

## Proposta de valor

Administração de GitHub por IA com foco em operações de governança e provisionamento de repositórios e organizações, complementando integrações oficiais existentes em vez de duplicá-las sem diferencial.

## Escopo inicial

1. Conexão de contas/organizações com consentimento e permissões granulares, preferencialmente via GitHub App.
2. Inventário de repositórios, branches, políticas e times conforme permissões concedidas.
3. Criação de repositórios e bootstrap de templates/políticas, quando autorizado.
4. Administração de acesso, colaboradores e regras de proteção, com checagem de privilégios e confirmação para alterações sensíveis.
5. Integração com padrões de nomenclatura Ideavelo e provisionamento da Factory, sem exigir que todo usuário seja cliente da Factory.
6. Registro de auditoria e relatórios de execução.

## Diferenciação

Validar lacunas reais das ferramentas oficiais disponíveis antes de construir cada operação. Evitar vender como exclusivo algo já oferecido nativamente. O foco é governança, políticas de organização, provisionamento seguro e fluxos administrativos auditáveis.

## Segurança

GitHub App com permissões mínimas por recurso; instalação por organização com aprovação de administrador; tokens de curta duração; webhook com assinatura verificada; validação de ownership; confirmação para exclusão/transferência/alteração de acesso; logs sem credenciais.

## Critérios de aceite MVP

Usuário autorizado instala e conecta a integração, lista repositórios permitidos, cria repositório com política validada, audita a ação e revoga a instalação. Testes cobrem permissões insuficientes, colisões, idempotência e segregação de organizações.
