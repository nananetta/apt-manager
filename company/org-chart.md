# Org Chart

## Leadership

- **CEO**: Human owner of the company vision, priorities, budget, and final approval
- **Supervisor** (opt-in): Coordinates an explicitly assigned portfolio across project PMs; see `roles/supervisor.md`

## Product and Planning

- **Product Manager**
- **Business Analyst**

## Engineering Leadership

- **Solution Architect**
- **Tech Lead**

## Delivery

- **Java Spring Backend Developer**
- **Frontend Developer**

## Quality and Operations

- **QA / Test Engineer**
- **DevOps / Platform Engineer**

## Reporting Lines

```text
CEO
├── Supervisor (when explicitly assigned; portfolio coordination)
├── Product Manager
├── Business Analyst
├── Solution Architect
├── Tech Lead
│   ├── Java Spring Backend Developer
│   └── Frontend Developer
├── QA / Test Engineer
└── DevOps / Platform Engineer
```

## Practical Collaboration Model

- PM is the default recipient of CEO messages and the main orchestrator; explicit CEO role or agent assignments take precedence
- Supervisor observes an assigned multi-repository portfolio and coordinates dependencies through project PMs; it does not replace PM as the default or assume project delivery/approval authority
- PM owns product direction and consolidates specialist handoffs into a response to the CEO
- BA improves clarity and documentation
- Architect owns technical shape
- Tech Lead owns execution coordination
- Developers own implementation
- QA owns validation
- DevOps owns build and deployment readiness

## Repository Responsibility

- Company-wide operating rules stay in top-level folders such as `company/`, `roles/`, `playbooks/`, and `templates/`
- The company repository owns the shared policy source, project registry, and provisioning; new projects use separate repositories under `playbooks/project-initiation.md`
- Each project receives a versioned shared-policy snapshot and stores its single product's artifacts under `products/<product-slug>/` inside its own repository
- The product folder is the default home for context, planning, architecture, implementation notes, QA evidence, ops notes, and handoff records
- The project PM owns its authoritative `STATUS.md`; portfolio observations and registry behavior follow `playbooks/portfolio-supervision.md`
