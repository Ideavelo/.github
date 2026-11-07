# Matriz inicial de autorização e risco — proposta v1

| Operação | Viewer | Operator | Admin | Owner | Controle adicional |
|---|---|---|---|---|---|
| Listar recursos autorizados | Sim | Sim | Sim | Sim | Tenant + instalação + entitlement |
| Ver estado e logs não sensíveis | Sim | Sim | Sim | Sim | Redação de segredos e dados pessoais |
| Iniciar deploy autorizado | Não | Sim | Sim | Sim | Escopo do recurso e auditoria |
| Alterar configurações de aplicações | Não | Não | Sim | Sim | Confirmação por risco |
| Criar repositório GitHub | Não | Conforme política | Sim | Sim | Template, org e política validados |
| Alterar permissões de repositório | Não | Não | Sim | Sim | Confirmação e privilégios GitHub |
| Excluir recursos / transferir ownership | Não | Não | Conforme política | Conforme política | Aprovação reforçada, nunca automática |
| Gerenciar assinatura | Não | Não | Conforme papel Billing | Sim | Separar cobrança de acesso técnico |
| Conectar / revogar instalação | Não | Não | Sim | Sim | Consentimento e MFA conforme risco |

**Regra:** permissões locais são apenas teto; o provedor externo pode impor restrições adicionais. Nenhuma ação destrutiva deve ser executada somente por instrução em linguagem natural sem autorização contextual e confirmação adequada.

## Classificação

- R0 leitura pública ou não sensível.
- R1 leitura privada autorizada e operação reversível de baixo impacto.
- R2 alteração operacional ou custo limitado: confirmação contextual conforme política.
- R3 exclusão, transferência, mudança de privilégio, segredos ou impacto financeiro significativo: aprovação reforçada e trilha de auditoria.

Políticas por cliente podem ser mais restritivas, nunca menos que os controles mínimos globais.
