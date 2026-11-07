# Arquitetura de plugins por plataforma — v1.0

**Decisão:** um produto comercial e uma identidade de plugin por plataforma integrada, por exemplo Ideavelo for Coolify e Ideavelo for GitHub. O nome da plataforma é importante para descoberta. MCP é tecnologia de integração, não a categoria comercial principal.

Cada produto terá repositório, versão, documentação, publicação, permissões e ciclo de vida próprios. Poderá incluir `apps/api`, `apps/mcp-server`, `apps/portal` e adaptadores específicos, sem impor um layout de código antes do desenho técnico.

A camada compartilhada pode oferecer OAuth, contas, assinaturas, gestão de credenciais, autorização, auditoria e telemetria. Isolar dados e segredos por cliente; limitar escopos e operações destrutivas; evitar ponto único de falha nas funções críticas. Não modificar nem substituir o gateway Coolify existente sem migração planejada e testes.
