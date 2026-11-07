# ADR-003 — Organização Coolify

- **Status:** Aceita
- **Data:** 2026-11-07

## Decisão
Manter projetos Coolify de raiz planos, com `Ideavelo-product-internal` e `Ideavelo-product-customer`. `Infrastructure` é projeto independente. Não alterar `ideavelo-website` temporário. Usar Registry para agrupamento lógico dos produtos.

## Consequências
Evita proliferação de projetos por SaaS e acoplamento entre catálogo e infraestrutura. Isolamento e permissões precisam ser implementados e verificados.
