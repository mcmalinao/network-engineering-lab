# Network Engineering Lab

A personal, Spec-Kit driven lab for designing, automating, and validating
network engineering patterns — data center fabrics, automation pipelines,
and observability — before they're trusted anywhere else.

This repo is a learning environment, not a production-consumed toolkit.
Every design or automation pattern here is meant to be run in a lab, proven,
and documented — see [`.specify/memory/constitution.md`](.specify/memory/constitution.md)
for the principles that govern how work happens in this repo.

## Structure

| Directory | Purpose |
|---|---|
| [`ai-fabric/`](ai-fabric/) | AI-driven fabric experiments |
| [`ansible/`](ansible/) | Configuration management playbooks and roles |
| [`automation/`](automation/) | General automation and scripting |
| [`avd/`](avd/) | Arista Validated Design (AVD) inputs |
| [`containerlab/`](containerlab/) | Virtual network topologies |
| [`cvp/`](cvp/) | Arista CloudVision Portal (CVP) automation |
| [`evpn-fabric/`](evpn-fabric/) | EVPN fabric designs |
| [`ndfc/`](ndfc/) | Cisco Nexus Dashboard Fabric Controller (NDFC) |
| [`netboxlab/`](netboxlab/) | NetBox-based source-of-truth labs |
| [`observability-stack/`](observability-stack/) | Metrics, logs, and traces (Prometheus, Grafana, Loki, Tempo, and collectors/exporters) |
| [`python-tools/`](python-tools/) | Python helper tooling |
| [`vxlan-as-code/`](vxlan-as-code/) | VXLAN fabric definitions as code |
| [`docs/`](docs/) | Cross-cutting documentation |
| [`specs/`](specs/) | Spec Kit feature specs, plans, and tasks |
| [`tasks/`](tasks/) | Standalone task tracking |

Each domain directory carries its own README describing its purpose,
current topology/architecture, and validated state as work lands there.

## Workflow

This repo uses [Spec Kit](https://github.com/github/spec-kit) to drive work
end to end:

1. `/speckit-specify` — describe the feature or lab exercise
2. `/speckit-clarify` — resolve ambiguities before planning
3. `/speckit-plan` — produce an implementation plan (checked against the
   constitution)
4. `/speckit-tasks` — break the plan into dependency-ordered tasks
5. `/speckit-implement` — execute, validating in a lab environment as work
   completes
6. `/speckit-analyze` / `/speckit-converge` — cross-check consistency and
   catch unbuilt work on larger features

See the constitution for the full principles (spec-driven workflow,
infrastructure as code, lab-first validation, documentation as a
deliverable, observability by default, and reproducibility/idempotency).
