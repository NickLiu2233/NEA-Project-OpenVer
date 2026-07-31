# Development Roadmap

**Current priority:** prove the real-map client/server Script Runtime loop before broad gameplay compatibility, full physics coverage, or frontend polish.

## Product Outcome

The target local path is:

```text
Project package
  -> Client Script Runtime and Server Script Runtime
  -> MuDB transport
  -> Authoritative Game Runtime
  -> Preserved Player browser client
```

A milestone is complete only when its focused validation passes or its remaining gap is explicitly documented with an evidence classification.

## Milestones

### M0 — Repeatable Local Start

**Outcome:** a contributor can start the public demo from a clean clone and understand expected logs, ports, and common failures.

**Status:** largely available; maintain startup guidance as runtime bootstrap changes.

### M1 — Real-Map Import and Gap Report

**Outcome:** a sanitized real-map usage report is compared against the current ABI, and public project structure is imported without private data.

**Exit criteria:**

- Sanitized usage data ranks real API demand without storing source text or payloads.
- The compatibility report classifies supported, partial, and deferred behavior.
- The importer accepts approved public core project fields and preserves unknowns honestly.

### M2 — Client/Server Script Loop

**Outcome:** a visible demo proves separate client/server scripts, remote events in both directions, server-to-client delivery, and one client-owned UI/input interaction.

**Exit criteria:**

- Remote-channel packet framing and lifecycle have focused conformance coverage.
- Directed and broadcast delivery are implemented only for evidenced semantics.
- The preserved Player displays a behavior driven by the executable map path.
- Capability gates deny undeclared or unsupported runtime surfaces.

### M3 — High-Value Gameplay Compatibility

**Outcome:** implement the next highest-value behavior based on the real-map gap report.

**Priority order:** remote-channel edge cases; UI/input; world events; entity lifecycle; voxel/storage behavior; player state; collision and physics replication.

Each feature needs a dedicated task, evidence statement, focused test, and explicit statement of unsupported edge cases.

### M4 — Public Release Hygiene

**Outcome:** contributors can reproduce public reports, understand limits, and audit the public/private boundary.

**Exit criteria:**

- Reports are deterministic and regenerated from reviewed inputs.
- Fixtures identify source class, redaction status, and reproducibility limits.
- Documentation describes startup, architecture, task ownership, and current limitations.
- Public branches contain no private capture, credentials, browser state, or unclear assets.

## Current Delivery Sequence

1. Generate the sanitized real-map compatibility gap report (`RT-001`).
2. Select one evidence-backed remote-channel or UI slice (`RT-002`).
3. Import the approved public project structure (`IMP-001`).
4. Add bidirectional remote-channel conformance (`RT-003`).
5. Add directed and broadcast server-to-client delivery (`RT-004`).
6. Prove client-script-owned UI and input (`UI-001`).
7. Integrate the preserved Player bridge (`INT-001`).
8. Freeze the path with a sanitized end-to-end smoke fixture (`QA-001`).

See the [community task queue](community-task-queue.md) for allowed scopes, dependencies, and acceptance criteria.

## Explicit Non-Goals

- Rewriting the recovered Player instead of extending the bridge incrementally.
- Claiming complete historical API parity from declarations alone.
- Implementing posture/physics values without safe, direct evidence.
- Publishing private real-map exports, raw script source, browser state, or captured account material.
- Performing repository-wide moves while references, ignore rules, generators, reports, and provenance remain unaudited.

## Planning A New Task

Use one task ID, one observable outcome, one declared write scope, and one primary validation path. A good task begins with the runtime boundary it owns and ends with a result a reviewer can reproduce. If a task discovers missing evidence, close it as evidence-deferred or evidence-blocked rather than expanding it into speculative implementation.
