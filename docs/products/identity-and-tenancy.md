# Arquitetura de identidade e multi-tenancy — proposta v1

**Status:** proposta para revisão técnica; não representa implementação.

## Entidades e fronteiras

- **Account:** identidade humana global, verificada por provedor OIDC ou credencial própria com controles adequados.
- **Organization (tenant):** cliente comercial e limite primário de isolamento de dados, cobrança e políticas.
- **Membership:** relação Account–Organization com papel e estado, permitindo um usuário em múltiplas organizações.
- **Plugin:** produto comercial independente (Coolify, GitHub).
- **Subscription / Entitlement:** direito da Organization a usar recursos de um Plugin; não concede automaticamente permissão de infraestrutura.
- **Installation:** conexão de uma Organization a uma instância Coolify ou instalação GitHub App; pertence a um único tenant.
- **Credential reference:** ponteiro para segredo no cofre, associado a tenant, plugin e instalação; nunca token em texto simples no Registry.
- **Actor:** identidade humana ou de serviço autenticada, ligada à ação e ao tenant efetivo.
- **Audit event:** evento imutável contendo actor, tenant, installation, ação, recurso, decisão, resultado e correlação.

## Invariantes de isolamento

1. Todas as consultas/mutações de dados de negócio recebem tenant efetivo do contexto autenticado, não de parâmetro confiado do cliente.
2. `installation.tenant_id` é imutável; acesso exige membership ativa + entitlement + permissão específica + instalação ativa.
3. Chaves de cache, filas, logs pesquisáveis e rate limits devem incluir tenant e instalação, sem vazar dados sensíveis.
4. Identificadores de recursos externos são sempre qualificados por instalação; um UUID igual em duas instâncias não confere acesso cruzado.
5. Troca de organização requer seleção explícita e nova avaliação de autorização; tokens não podem ser reutilizados entre tenants sem checagem.
6. Operações administrativas e suporte são auditadas e têm acesso excepcional limitado, temporário e aprovado.

## Autorização

A decisão efetiva combina identidade, membership, papel, entitlement, instalação, operação, recurso, risco e permissões reais do provedor. Modelo deny-by-default; RBAC para papéis e ABAC para atributos de instalação/recurso. Não confiar somente em escopos declarados pelo cliente ou em texto de prompt.

Papéis iniciais propostos: Owner, Admin, Operator, Viewer, Billing. Permissões são por operação; Owner não dispensa confirmação de ações destrutivas.

## Lifecycle

Convite e aceitação, suspensão, remoção de membro, transferência de propriedade, desconexão de instalação, revogação de credenciais e cancelamento de assinatura devem ter estados explícitos e eventos de auditoria. Suspensão de cobrança não deve impedir recuperação/exportação de dados conforme política e obrigações legais.
