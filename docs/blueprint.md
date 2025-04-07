# GitHub Architecture Blueprint for Epec Engineered Technologies

This document defines how we organize, name, structure, and manage GitHub repositories for engineering work involving battery and cable testing systems.

---

## 1 | Organization‑level Layout

| Unit         | Purpose                         | Naming Rule                | Examples                                      |
| ------------ | ------------------------------- | -------------------------- | --------------------------------------------- |
| **Repos**    | Deliverables that ship together | <product>-<domain>-<type>  | phoenix-battery-ui, copperhead-cable-firmware |
| **Teams**    | Access control groups           | <dept>-<scope>             | ee-lab, qa-automation                         |
| **Projects** | High‑level roadmap views        | proj-<customer>-<codename> | proj-tesla-phoenix                            |

---

## 2 | Repository Classes

| Type                  | Used for                                         | Notes                                  |
| --------------------- | ------------------------------------------------ | -------------------------------------- |
| **Product Repo**      | Software or firmware that runs on test rigs      | Full CI/CD, protected branches         |
| **Fixture / Tooling** | Stand‑alone scripts, 3‑D models, wiring diagrams | Lightweight CI, permissive access      |
| **Shared‑Library**    | Code reused across products                      | Strict semver tags, release publishing |

---

## 3 | Branching Strategy

Trunk‑based development with short‑lived feature branches:

    main   ← protected
    │
    ├─ feat/<ticket-id>-<slug>   ← deleted after merge
    └─ release/vX.Y              ← optional long‑term support

Tags follow semantic versioning: v1.0.0, v1.0.1, etc.

---

## 4 | Repository Folder Layout

    .
    ├── docs/                 # Documentation (markdown)
    ├── src/                  # Source code
    ├── tests/                # Unit & integration tests
    ├── hardware/             # Schematics, 3‑D models
    ├── ci/                   # CI scripts
    ├── scripts/              # Utility tools
    ├── .github/              # Actions, templates, issue/PR forms
    ├── README.md
    ├── CHANGELOG.md
    └── LICENSE

---

## 5 | README Template (stored in .github/templates/README_TEMPLATE.md)

    # <Project title>

    > One‑sentence elevator pitch.

    ## Table of contents
    - Quick start
    - Hardware requirements
    - Repository layout
    - Branch & release model
    - Contributing
    - License

---

## 6 | Access and Teams

- core-maintainers – admin on all repos
- tech-writers – write access to docs
- qa-automation – write access to tests

CODEOWNERS example:

    *       @core-maintainers
    /docs/  @tech-writers

---

## 7 | CI/CD Setup

| Purpose       | Tool                  | Notes                                         |
| ------------- | --------------------- | --------------------------------------------- |
| Build & Test  | GitHub Actions        | Linux runners + self‑hosted Windows (LabVIEW) |
| HIL           | Azure Pipelines       | Triggered via REST from Actions               |
| Releases      | GitHub Releases       | Tag, build, upload binaries                   |
| Documentation | GitHub Pages + MkDocs | Auto‑publish from docs/ folder                |

---

## 8 | Onboarding Guidelines

1. Clone → create feature branch → open PR → squash merge
2. Use Conventional Commits: type(scope): message
3. Run pre-commit install for linting hooks
4. New hires pair for first three PRs
5. Seniors rotate writing documentation PRs

---

## 9 | Scaling as Team Grows

| Headcount | Action                                                               |
| --------- | -------------------------------------------------------------------- |
| > 25 devs | Split maintainers into domain‑specific teams                         |
| > 40 devs | Require 2 approvals, enable review‑rotation bot                      |
| > 50 devs | Auto‑scale CI runners, lock down repo creation to architecture board |

---

## 10 | Why This Works for Epec

- Projects combine software, firmware, and hardware → clear folder layout keeps assets together but organized.
- Regulated customers demand traceability → release branches + GitHub Releases provide immutable binaries and change logs.
- CI enforces code quality without manual policing.
- Simple naming rules and CODEOWNERS scale cleanly as the team expands.

---
