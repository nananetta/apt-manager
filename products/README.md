# Products Directory

In a standalone project repository, all product work lives under `products/<product-slug>/`, using lowercase kebab-case. Keep company-wide policy and reusable templates outside product folders.

The company repository maintains shared rules and the project registry, not new product implementations. Follow `playbooks/project-initiation.md` to create a separate repository. Root `project.yaml` identifies the single product and pinned company source revision. Existing legacy product folders are not automatically moved or deleted.

## Naming and Placement Rules

- Each project repository contains one product folder, for example `products/customer-portal/`.
- Use lowercase words separated by hyphens for the product slug; do not use spaces or uppercase letters.
- Keep all product-specific context, requirements, designs, code, tests, deployment material, and handoffs inside that product folder, rather than at the repository root or in shared template folders.
- Keep the agreed deliverable filenames shown below. The architecture and implementation specifications intentionally share a filename but live in different phase folders.

## Product Layout

```text
products/<product-slug>/
├── README.md                         # Stable purpose, goals, and link to STATUS.md
├── STATUS.md                         # Single current product summary, owned by PM
├── context/                          # CEO brief and references
├── planning/
│   ├── ceo-presentation.html
│   └── functional-spec.html
├── architecture/
│   ├── ceo-tech-presentation.html
│   └── technical-spec.html
├── implementation/
│   └── technical-spec.html           # Shared frontend/backend implementation reference
├── qa/                               # Tests, defects, and validation evidence
├── ops/                              # Build, deployment, and runtime material
└── handoffs/                         # Role handoff history
    └── approvals/                    # Version-specific CEO decision records
```

Implementation code and supporting assets also stay within the product folder. Create deliverables when their authorized phase begins; the layout is not evidence that artifacts exist or gates are approved.

## Purpose of Each Location

| Location | What belongs here |
|---|---|
| `README.md` | Stable product summary, goals, and a link to current status. |
| `STATUS.md` | PM-owned current phase, assignments, blockers, next action, artifact versions, approval references, and local/live state. |
| `context/` | CEO brief, source material, research, business background, and references. |
| `planning/` | Scope, user stories, business rules, functional/non-functional requirements, acceptance criteria, and the two requirements HTML deliverables. |
| `architecture/` | Solution design, component/data/API decisions, diagrams, and the two architecture HTML deliverables. |
| `implementation/` | Tech Lead implementation specification, work breakdown, assignments, build notes, and product code or references to its location within the product folder. |
| `qa/` | Test plans, test results, defects, validation evidence, and release-readiness assessments. |
| `ops/` | Build/deployment configuration, environment setup, startup instructions, release evidence, and operational/recovery guidance. |
| `handoffs/` | Markdown records of historical role-to-role transfers, input/output references, decisions, and outstanding questions, using the handoff template. |
| `handoffs/approvals/` | Version-specific CEO approval records and retained artifact snapshots when required. |

PM starts STATUS.md from `templates/product-status-template.md`. Use `templates/approval-record-template.md` for decisions and `templates/handoff-template.md` for role transfers. Follow `playbooks/product-tracking.md` for update ownership, artifact identity, and approval history; approved snapshots may live beneath the corresponding approval ID when Git does not retain the reviewed content.

Document content and formats are defined in `playbooks/document-standards.md`; phase order is defined in `playbooks/delivery-lifecycle.md`. README describes the product; STATUS.md reports current work. Do not maintain separate current-status sections in README or handoff files.
