# Independent Project Bootstrap

`bootstrap.json` is the explicit file allowlist for a new project repository. It selects committed company rules, role profiles, PM skill, and reusable artifact templates; it excludes the portfolio supervisor's agent profile, company audit, project/customer data, registry, provisioning scripts, Git history, and local files. The supervisor role contract remains available so shared policy links resolve. Extend the allowlist deliberately when adding shared files.

`README.template.md` becomes the new repository's root README. The provisioner generates `project.yaml` (JSON-compatible YAML) with `schema_version`, `repository_context`, `id`, `repository_url`, `pm`, `product_path`, and `company_source` (`repository_url` and exact `revision`). Local-only projects have a null repository URL. Each repository gets one `products/<slug>/README.md` and a truthful initial `STATUS.md`; delivery artifacts and approvals are not pre-created.

See [project initiation](../../playbooks/project-initiation.md) for commands, clean committed source requirements, and recovery. The company's provisioner is not copied into projects. Shared rules are versioned snapshots; upgrades are explicit PM-coordinated changes.
