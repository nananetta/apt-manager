# Portfolio Supervision

## Project Discovery

`registry/projects.yaml` in the company repository locates independent projects. It contains `schema_version: 1` and a `projects` list. Maintain it in JSON syntax, which is compatible with YAML: the provisioner uses the standard-library JSON parser and does not accept general YAML syntax or comments. The registry is not a second current-status file; each project's PM-owned `STATUS.md` remains authoritative under `product-tracking.md`.

| Entry field | Meaning |
|---|---|
| `id` | Unique lowercase kebab-case project/product slug. |
| `repository_url` | Verified GitHub repository URL. |
| `pm` | Responsible project PM identity or role label; not proof a session is running. |
| `status_path` | Repository-relative path `products/<id>/STATUS.md`. |
| `company_source_revision` | Exact company commit used for the project's shared policy snapshot. |
| `dependencies` | List of registered project IDs this project depends on; empty when none. |

Register only a verified remote project. Keep generated `project.yaml` and the registry entry consistent; manual corrections require verification against the actual repository and source revision. Do not include credentials or machine-specific checkout paths. Review dependency changes with affected PMs and record the actual interface, required versions, and blocking work in product artifacts rather than expanding the registry into a duplicate task tracker. Cycles and unknown dependency IDs require clarification; they are not a valid execution order.

The provisioner serializes registry writes using `registry/.projects.lock`. Respect an active lock rather than bypassing it with a concurrent manual edit. A stale lock requires investigation of the owning process before recovery.

## Observation and Coordination

Supervisor is an opt-in portfolio role governed by `roles/supervisor.md`. PM remains the default responding orchestrator under `communication-rules.md`; selecting or assigning Supervisor does not replace the PM in each project.

For an assigned portfolio review, Supervisor reads the registry, identifies repository access, and reads each requested project's instructions, `STATUS.md`, relevant artifacts, and decision evidence. Record the repository identity, branch/ref and commit read, observation time, and status update time when available. Distinguish observed state from a PM report. An accessible old branch, stale status, missing timestamp, inaccessible repository, or uncertain live release must be described explicitly; mark unverifiable current facts as unknown. No universal freshness interval is assumed: compare observations to the requested decision and flag potentially stale evidence before depending on it.

Produce a concise portfolio view of verified progress, blockers, dependency impact, owners, and decisions needed, with links and revision/time provenance. This is an observation for the assigned task, not another maintained current-state document. When status and artifacts disagree, request PM reconciliation rather than silently editing product state from the company repository.

Coordinate bounded assignments through project PMs, naming the target repository, product, inputs and revision, authorized scope, output location, dependency acceptance condition, and next handoff. Existing routing, delegation, delivery gates, decision ownership, and handoff formats remain canonical in their owning playbooks. Escalate material cross-project priority, cost, timeline, scope, or release trade-offs to the CEO with affected PM recommendations.

## Access and Execution Boundaries

Markdown contracts and a registry do not grant repository access, credentials, tool capability, or permission to message another chat. Read and write only within the available environment and authorized assignment. Actual cross-chat messages require explicit human authorization under the tool's rules; neither a registry PM label nor a Supervisor assignment alone supplies that authorization. When messaging tools or authorization are absent, provide the concrete handoff for the human or work in authorized local agent contexts.

Supervisor cannot approve requirements/design, treat another project's approval as local approval, impersonate a project PM, infer publication authorization, or claim an agent ran because a profile exists. Report inaccessible repositories and unavailable capabilities as blockers while continuing independent authorized work. Each project's PM consolidates its status and evidence; Supervisor consolidates portfolio observations and coordination results.
