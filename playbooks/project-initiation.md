# Project Initiation and Repository Ownership

## Company and Project Contexts

The company repository is the source of truth for shared roles, playbooks, agent entry points, skills, and templates. It also owns the project registry and provisioner. New software projects use separate GitHub repositories with independent Git history; do not create a new product inside the company repository or nest another Git repository inside it.

Each project repository contains its own shared instruction snapshot, `project.yaml`, and exactly one `products/<product-slug>/` folder. Keep the existing product paths and deliverable conventions from `products/README.md`. Existing product folders are not automatically migrated; moving a product requires a separate scoped task that preserves its history, artifacts, and approval evidence.

Before acting, determine the context from `project.yaml`: a project repository delivers its identified product; the company repository provisions and registers projects. A project agent should propose another project through company initiation rather than create another product folder locally. Repository separation does not change delivery, decision, or publication rules.

## Initiation Procedure

PM identifies the CEO brief, lowercase kebab-case slug, destination outside the company checkout, intended GitHub account/organization, explicit `private` or `public` visibility, and responsible PM. Request only information that is missing or ambiguous. A CEO request to create the specified repository authorizes that creation; no routine extra approval gate is required. An instruction to implement company provisioning infrastructure does not itself authorize creating a real product repository.

Use `scripts/create-project.sh` from the company checkout. Its normal source is committed `HEAD`; shared bootstrap files must be committed and clean so their recorded source revision reproduces the copied content. Do not commit unrelated user changes to satisfy this prerequisite. `templates/software-project/README.md` defines the copied snapshot and generated scaffold.

Creation requires a POSIX environment (macOS or Linux), Python 3, Git, and a resolvable Git author/committer identity. Remote creation also requires the GitHub CLI (`gh`), authentication to GitHub.com, and permission to create a repository for the chosen owner. The provisioner checks these before creating files. Dry-run validates the local plan without authenticating to GitHub; success does not establish remote access. This provisioner targets GitHub.com, not GitHub Enterprise hosts.

Preview a planned creation without changing files or GitHub:

```sh
./scripts/create-project.sh --slug customer-portal \
  --destination /path/outside/company/customer-portal \
  --owner YOUR_GITHUB_OWNER --visibility private \
  --pm product-manager --dry-run
```

With an authorized repository creation request, omit `--dry-run` to create and push the independent repository, then register it. Use `--local-only` to create only the local project scaffold and Git history; owner and visibility remain required to identify the intended remote, but `repository_url` stays null and the project is not registered. Local-only creation does not authorize later remote creation. The script does not start agents or deploy the product. `--pm` defaults to `Product Manager` when omitted; that role label does not identify or start a running agent session.

After creation, PM places the CEO brief under the product's `context/`, checks the initialized `STATUS.md`, and proceeds through `delivery-lifecycle.md`. Scaffold placeholders and an initial commit are not requirements, design, QA, or release approval. Do not claim the delivery phases have run.

## Shared Policy Versions and Upgrades

Each project receives versioned copies of the shared instructions, profiles, skill, and templates so local agents can resolve their repository-relative references. `project.yaml` records project identity, intended repository, and the exact company source commit. The registry records that same company revision. A link to the company repository is provenance, not an instruction-loading mechanism.

Policy upgrades are deliberate project changes. Compare the recorded company revision with the proposed committed revision, review the relevant changes and project-specific adaptations, and update the affected shared files and provenance together. Never overwrite project content, retained approval snapshots, or historical decisions while refreshing policy. PM reconciles active state and evidence under `product-tracking.md`; changed policy does not retroactively grant or revoke an artifact approval. Material product changes still follow the existing decision rules. Report unresolved compatibility before dependent work proceeds.

## Completion and Recovery

Creation is complete only when the local repository has the intended independent history and source revision, the expected GitHub repository and pushed revision have been verified, and the company registry contains the matching project entry. Report partial completion accurately. A local-only result ends at local initialization.

On failure, preserve the destination and any created remote for diagnosis; do not delete repositories or retry into an unrelated existing directory. The provisioner records its own identity and progress under `.git/company-provision.json`. Use `--resume` with the same creation arguments only for a matching recorded provisioner operation. Original parameters, including local-only mode, are immutable. Resume validates recorded identity and the GitHub repository ID before pushing and registering; it does not force push or overwrite an unrelated project. Existing remote repositories are refused during creation. Any attempted creation without a recorded remote ID is treated as uncertain, including a failed creation command: stop and resolve its result manually rather than adopt an unverified repository or automatically retry creation. For a recorded, verified remote, correct a reported access problem and resume the matching operation to retry push or registration. Registry failure after a successful push remains incomplete registration, not a failed or absent remote. Never fabricate registration or silently create a second remote to bypass recovery.

A local-only scaffold cannot be promoted by changing mode through `--resume`. Later remote creation is a separate authorized, scoped task that must reconcile project metadata and verified registry identity; the current script does not implement that promotion.

The registry contract and multi-project reads are owned by `portfolio-supervision.md`. Machine-specific checkout locations stay in local configuration, outside the shared registry.
