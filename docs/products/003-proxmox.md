# Product 003 — Ideavelo for Proxmox

**Ownership:** internal | **Category:** plugin | **Repository:** `Ideavelo/internal-plugin-proxmox` | **Status:** approved for development (owner decision, 2026-11-13, internal-platform-core#137).

## Value proposition

Operate Proxmox VE hosts from an AI assistant (ChatGPT first) with the same safety model as the Coolify plugin: OAuth sign-in, per-environment roles, access schedules and expiry, and an activity log. Aimed at small teams that run their own virtualization without a dedicated operations team.

## Initial scope

1. Connection per Proxmox host or cluster with an API token (privilege separation on); the token's role is the ceiling, the portal can only narrow it.
2. Read: overview, nodes, guests (VMs and containers), storage, tasks, snapshots, backups.
3. Operate: start, shutdown, reboot, hard stop (with confirmation), snapshot, backup now.
4. Write: snapshot rollback and deletion, both with confirmation.
5. Out of the first version: guest creation and deletion, configuration changes, consoles, users and permissions, firewall, storage and cluster changes. Proxmox Backup Server comes later.

## Security

Proxmox has no native MCP endpoint and no OAuth for its API, so the plugin implements its own tools over the REST API. Tokens are entered only in the portal and kept in Vault; the plugin receives them per call from Core and never logs them. TLS uses the public chain or exactly the pinned certificate fingerprint; hosts must resolve to public addresses. Design: `internal-platform-core/docs/architecture/proxmox-plugin.md`.

## MVP acceptance criteria

An authorized user connects a Proxmox host in the portal, the connection is verified, the assistant lists guests and runs an operate action allowed by the role, the action appears in the activity log, and a viewer is refused. Tests cover role refusal, confirmation for destructive actions, TLS pinning and organization isolation.

## Launch

Commercial launch together with at least Coolify and GitHub (owner decision, 2026-11-13). Testing uses a separate small VPS running Proxmox VE.
