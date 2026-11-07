# Organização de infraestrutura — v1.0

Coolify usa projetos planos, ambientes e recursos; **não** suporta projetos aninhados. Projetos de raiz existentes incluem `Ideavelo-factory`, `Ideavelo-product-internal`, `Ideavelo-product-customer`, `Infrastructure` e `ideavelo-website` (site temporário), além de outros projetos independentes.

- `Ideavelo-product-internal`: aplicações de produtos pertencentes à Ideavelo.
- `Ideavelo-product-customer`: aplicações de produtos de clientes, com isolamento e autorização por cliente.
- `Infrastructure`: projeto independente, nunca filho de outro projeto.
- `ideavelo-website`: projeto temporário existente; não alterar sem decisão específica.
- Ambientes `staging` e `production` são a convenção-alvo, sujeitos à disponibilidade e ao provisionamento real.

Evitar criar um projeto Coolify por produto por padrão; o Registry faz o agrupamento lógico. Provisionamento deve ser idempotente, auditável e independente de um único provedor. Produtos implantados devem continuar operando quando a Factory estiver indisponível.
