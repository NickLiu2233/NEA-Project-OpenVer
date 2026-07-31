# Engineering Documentation

This directory describes the publishable OpenVer implementation and the rules for extending it safely. Historical mirrors and preserved artifacts are evidence inputs; they are not the primary place to learn how to change the current runtime.

## Start By Role

| Role | Read first | Then read |
| --- | --- | --- |
| New contributor | [Repository layout](repository-layout.md) | [Contributing](../CONTRIBUTING.md) and [Evidence model](evidence-model.md) |
| Runtime implementer | [Runtime architecture](runtime-architecture.md) | [Development roadmap](development-roadmap.md) and package tests |
| Evidence reviewer | [Open version policy](open-version.md) | [Evidence model](evidence-model.md) |
| Demo/integration maintainer | [Cold start guide](cold-start.md) | [Development roadmap](development-roadmap.md) |
| Community contributor | [Community task queue](community-task-queue.md) | [Contributing](../CONTRIBUTING.md) |

## Documents

- [Cold start guide](cold-start.md): local startup, expected behavior, and recovery steps.
- [Community task queue](community-task-queue.md): bounded work items, dependencies, and acceptance criteria.
- [Development roadmap](development-roadmap.md): delivery milestones and explicit non-goals.
- [Evidence model](evidence-model.md): sources, classifications, and publication rules.
- [Open version policy](open-version.md): public/private boundary and publication checklist.
- [Repository layout](repository-layout.md): ownership of top-level packages and evidence inputs.
- [Runtime architecture](runtime-architecture.md): client/server runtime, transport, authoritative runtime, and Player boundaries.

## Documentation Rules

- Engineering documentation is written in English.
- Describe known limits directly; do not replace missing evidence with plausible technical detail.
- Keep generated reports separate from explanatory documentation. Update a report through its generator, not by editing output.
- Link to an owning package, conformance fixture, or reproducible command whenever documentation makes an implementation claim.
