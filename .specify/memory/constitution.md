<!--
Sync Impact Report
Version change: [TEMPLATE] → 1.0.0 (initial ratification)
Modified principles: n/a (first concrete ratification; template placeholders replaced)
Added sections:
  - Core Principles I-VI (Spec-Driven Workflow, Infrastructure as Code,
    Lab-First Validation, Documentation as a Deliverable, Observability by
    Default, Reproducibility & Idempotency)
  - Domain & Technology Scope
  - Development Workflow
  - Governance
Removed sections: none (placeholder scaffold only)
Templates requiring updates:
  - .specify/templates/plan-template.md: ⚠ pending manual check (not modified by
    this command; verify its Constitution Check section still maps to the six
    principles below)
  - .specify/templates/spec-template.md: ⚠ pending manual check
  - .specify/templates/tasks-template.md: ⚠ pending manual check
Follow-up TODOs: none
-->

# Network Engineering Lab Constitution

## Core Principles

### I. Spec-Driven Workflow (NON-NEGOTIABLE)
Every non-trivial change — a new fabric design, automation role, lab topology,
or dashboard — MUST go through the Spec Kit flow (`/speckit-specify` →
`/speckit-clarify` → `/speckit-plan` → `/speckit-tasks` → `/speckit-implement`)
before it is treated as done. Ad hoc edits to fabric/automation code without a
backing spec are permitted only for quick throwaway experiments in a scratch
branch; anything meant to persist in the repo MUST be traced back to a spec.
Rationale: this repo exists to capture *why* a design or automation pattern
works, not just the artifact — skipping the spec loses the learning.

### II. Infrastructure as Code
Device configuration, fabric/topology definitions, and automation (Ansible
playbooks/roles, AVD inputs, NDFC/CVP definitions, VXLAN-as-code, Python
tooling) MUST be expressed as version-controlled code or declarative
templates. Manual CLI changes on lab devices are allowed for exploration, but
MUST be reconciled back into code before a change is considered complete —
the repo, not a device's running-config, is the source of truth.

### III. Lab-First Validation
A new design or automation pattern MUST be exercised in a virtual/lab
environment (containerlab, netboxlab, or an equivalent sandbox) before it is
documented as validated. Nothing is marked "known good" on the basis of
reading vendor docs or theory alone — it must have been run.

### IV. Documentation as a Deliverable
Each domain area (`ai-fabric/`, `ansible/`, `automation/`, `avd/`,
`containerlab/`, `cvp/`, `evpn-fabric/`, `ndfc/`, `netboxlab/`,
`observability-stack/`, `python-tools/`, `vxlan-as-code/`) MUST carry a
README (or equivalent doc) stating its purpose, current topology/architecture,
and validated state. A feature is not complete until what was learned is
written down where the next session (human or agent) will find it.

### V. Observability by Default
Where a lab or automation change can reasonably emit metrics, logs, or
traces, it SHOULD be wired into `observability-stack/` (Prometheus, Grafana,
Loki, Tempo, or the relevant collector/exporter) rather than being validated
only through one-off manual CLI checks. Ad hoc `show` commands are fine for
quick debugging, but repeatable validation belongs in the observability
stack.

### VI. Reproducibility & Idempotency
Automation MUST be safely re-runnable from a clean state: Ansible playbooks
and roles must be idempotent, and lab environments must be scripted so they
can be torn down and rebuilt without manual cleanup steps. If a lab can't be
rebuilt from the repo alone, it isn't finished.

## Domain & Technology Scope

This repository is a personal network-engineering learning lab, not a
production-consumed toolkit. Its working areas are: AI-driven fabric
experiments (`ai-fabric/`), configuration management (`ansible/`),
general automation and scripting (`automation/`), Arista Validated Design
inputs (`avd/`), virtual topologies (`containerlab/`), Arista CloudVision
(`cvp/`), EVPN fabric designs (`evpn-fabric/`), Cisco Nexus Dashboard Fabric
Controller (`ndfc/`), NetBox-based source-of-truth labs (`netboxlab/`),
monitoring/telemetry (`observability-stack/`), Python helper tooling
(`python-tools/`), and VXLAN-as-code (`vxlan-as-code/`). Because this is a
learning environment, rigor is calibrated for clarity and reproducibility
over production hardening: prefer the simplest automation that correctly
demonstrates the pattern, and prefer clear documentation over exhaustive
test suites — but the Core Principles above are still mandatory, not
optional.

## Development Workflow

1. Start every feature or lab exercise with `/speckit-specify`, then resolve
   ambiguities with `/speckit-clarify` before planning.
2. Run `/speckit-plan` and `/speckit-tasks` to produce an implementation plan
   and dependency-ordered task list; both MUST be checked against the Core
   Principles above (a "Constitution Check" step) before implementation
   starts.
3. Execute with `/speckit-implement`, validating in a lab environment per
   Principle III as tasks complete, not only at the end.
4. Before marking a feature done, update the relevant domain README
   (Principle IV) and confirm any automation involved is idempotent and
   re-runnable (Principle VI).
5. Use `/speckit-analyze` for a cross-artifact consistency pass on larger
   features (spec, plan, tasks) before implementation, and
   `/speckit-converge` to catch any unbuilt work left behind.
6. Since this is a solo lab, "review" means a deliberate self-check of the
   diff and docs against this constitution before considering work merged —
   there is no separate reviewer gate, but the standard is not optional.

## Governance

This constitution supersedes ad hoc practice for everything under this
repository's Spec Kit workflow. Amendments are made by re-running
`/speckit-constitution`, which MUST update the version per semantic
versioning (MAJOR: incompatible principle removal/redefinition; MINOR: new
principle or materially expanded guidance; PATCH: clarification or wording
fix), refresh `Last Amended`, and record the change in a Sync Impact Report
comment at the top of this file. Every `/speckit-plan` run MUST include an
explicit Constitution Check against the six Core Principles; unjustified
deviations block moving on to `/speckit-tasks`. Complexity (e.g., skipping
lab validation, hand-editing device state, leaving docs stale) must be
justified in the spec/plan or removed.

**Version**: 1.0.0 | **Ratified**: 2026-09-20 | **Last Amended**: 2026-09-20
