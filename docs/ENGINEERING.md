# Ideavelo Engineering Standards

These are organization-wide **recommended guidelines**, not a claim that automated enforcement is already configured. Repository-specific architecture, approved policies, operational runbooks and mandatory controls take precedence.

## 1. Technology and architecture

Technologies currently represented in parts of the Ideavelo ecosystem include:

| Domain | Technologies and capabilities |
| --- | --- |
| Frontend | React, Next.js, TypeScript |
| Backend | .NET, HTTP/REST APIs |
| Persistence | PostgreSQL |
| Identity | Keycloak, OAuth 2.0 / OpenID Connect |
| Infrastructure | Docker, Coolify, GitHub Actions |
| AI and integrations | LLM APIs, autonomous agents, MCP |

Do not assume identical versions or architecture across repositories. Use supported dependencies for new projects where feasible and evaluate migrations for compatibility, security, and operational impact.

## 2. Software design

- Keep business rules, infrastructure adapters and public contracts clearly separated when appropriate.
- Favor cohesive modules, explicit interfaces and documented architectural decisions.
- Avoid broad refactors during incident response or narrowly scoped verification work.
- Design APIs for predictable errors, backward compatibility, authorization and observability.
- Prefer idempotent handlers and safe retries for asynchronous or externally triggered operations.

## 3. AI and autonomous systems

- Default to disabled external inference unless explicitly authorized for the relevant environment and workflow.
- Require explicit, enforceable budgets, provider allowlists and kill switches for cost-bearing operations.
- Maintain a clear distinction between synthetic/mock execution and real provider execution.
- Apply independent approval and separation of duties for sensitive transitions where required by the workflow.
- Bind approvals to the exact scope, identity, policy version and immutable evidence being approved.
- Record auditable execution, authorization, reservations, settlement and failure outcomes without exposing secrets.
- Treat model output, retrieved content and tool results as untrusted input.
- Constrain agent tools to least privilege, approved resources and defined execution boundaries.
- Prevent duplicate external actions through idempotency, concurrency control and reconciliation.
- Never interpret a passing CI pipeline as proof of an operational end-to-end staging validation.

These principles do not authorize production inference or deployment. Existing environment-specific gates and project policies remain authoritative.

## 4. Identity, secrets and environment isolation

- Use short-lived, scoped credentials where supported; never commit tokens or private keys.
- Enforce authorization on the server, not solely in UI clients.
- Keep staging and production data, identities, secrets and permissions isolated as designed.
- Validate target environment and database before migrations or destructive operations.
- Apply least privilege to CI runners, service identities, MCP tools and operational integrations.
- Avoid exposing sensitive values in logs, CI artifacts, issue comments and pull requests.

## 5. Data and migrations

- Use parameterized queries and transaction boundaries appropriate to the operation.
- Review schema changes for locking, compatibility, data retention and rollback.
- Ensure financial or usage ledgers preserve traceability and consistent reconciliation.
- Test migrations against the intended database and confirm previously applied migration history.
- Do not run destructive data operations without explicit authorization and a recovery plan.

## 6. Code conventions

- Follow language-specific conventions and established patterns in each repository.
- Use available formatters, linters, static analysis and dependency checks.
- Keep commits focused; suggested prefixes include `feat:`, `fix:`, `docs:`, `refactor:`, `test:` and `chore:`.
- Document new dependencies, important trade-offs and breaking contract changes.
- Never add credentials, customer data or internal operational secrets to public documentation.

## 7. Testing and verification

- Run the project's applicable build, lint and test commands.
- Cover changed business rules with unit tests and external integrations with isolated integration tests.
- Verify authorization, concurrency, failure recovery and idempotency for critical workflows.
- For AI flows, test denied actions, exceeded budgets, disabled providers, ambiguous outcomes and duplicate attempts.
- Distinguish unit-test evidence, CI success, staging deployment and authenticated end-to-end operational evidence.
- Do not invent pass/fail results or claim validation without execution evidence.

Numerical coverage targets and required CI checks are defined by each product repository, not by this document.

## 8. Pull requests and reviews

- Use dedicated branches and link the relevant issue or operational checkpoint.
- Document scope, changed contracts, tests, risks, deployment considerations and rollback.
- Require independent review for security-sensitive and financially sensitive changes when the project policy calls for it.
- Preserve concurrent work; reconcile branch heads and deployment SHAs before modifying active workflows.
- Do not merge with failing mandatory checks or unresolved critical risks.

## 9. Deployment and operations

- Prefer staged, reproducible deployment processes and environment-specific configuration.
- Reconcile source commit, CI result, image or artifact version, deployment and runtime health.
- Confirm identity, database and dependent service readiness through real checks.
- Monitor logs, metrics and error rates without exposing personal data or secrets.
- Maintain incident notes, checkpoints and recovery procedures in authorized locations.

## 10. Documentation hierarchy

Approved security policies, product-specific runbooks and active operational restrictions override these general recommendations. A guideline documented here is not automatically an enabled GitHub rule, CI gate or deployed runtime control.
