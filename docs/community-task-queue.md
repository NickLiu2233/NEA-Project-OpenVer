# Community Task Queue

**Updated:** 2026-07-31
**Milestone:** M1 real-map import and M2 client/server Script Runtime loop

This queue splits the current compatibility work into small, evidence-first tasks for community contributors. Each contributor may claim only one task ID at a time. Do not copy private map exports, script source, captures, credentials, browser state, tokens, or unpublished assets into issues, branches, fixtures, logs, or reports.

## Dispatch Rules

- Start only the tasks listed as ready. Treat all other tasks as queued until their dependencies pass.
- Keep implementation, evidence, and generated reports separate.
- Use `compatible`, `partial`, `recovered-only`, `declared-only`, or `evidence-deferred` for compatibility claims. Do not guess historical behavior.
- Limit each change to the declared scope and add focused conformance coverage for runtime changes.
- Do not refactor the preserved Player implementation. Add narrow adapters at a documented boundary when integration is required.

## Ready

### RT-001 — Generate a Sanitized Real-Map Compatibility Gap Report

**Owner:** unassigned
**Allowed scope:** `Middleware/runtime-compat/` sanitized evidence import, report generator, focused tests, and deterministic public report output.
**Forbidden scope:** private map exports, raw scripts, payloads, token-bearing URLs, Player rewrites, and unrelated runtime changes.

**Goal:** Compare sanitized real-map API usage with the current runtime ABI and rank missing behavior by observed usage.

**Acceptance criteria:**

- The tracked report contains no source text, payload values, private identity, or private paths.
- Each unsupported or uncertain API has an evidence-based classification and a reproducibility limit.
- Focused validation proves the report is deterministic for the approved sanitized input.

**Blocks:** RT-002 and the final ordering of runtime implementation work.

## Queued

### RT-002 — Select the First Remote-Channel or UI Slice

**Owner:** runtime lead
**Allowed scope:** a decision record and one approved runtime contract.
**Goal:** Select exactly one highest-value executable behavior from RT-001 results.

**Acceptance criteria:** Document client/server ownership, known evidence, unknowns, focused tests, visible demo proof, and explicit deferrals.

**Depends on:** RT-001.

### IMP-001 — Import Public Recovered Project Structure

**Owner:** importer engineer
**Allowed scope:** `Frontend/demo-map/` importer code and focused importer tests.
**Goal:** Map approved public core project fields into the `nea-map/v1` import format.

**Acceptance criteria:** Validate external input; preserve unavailable fields as evidence-blocked or deferred; never infer absent historical values.

**Depends on:** RT-001 confirmation of the public and redacted field set.

### RT-003 — Add Bidirectional Remote-Channel Conformance

**Owner:** runtime transport engineer
**Allowed scope:** `Middleware/runtime-compat/conformance/`, focused conformance tests, and the smallest `Frontend/demo-map/` adapter seam.
**Goal:** Prove client-to-server and server-to-client remote events with an explicit packet contract.

**Acceptance criteria:** Test malformed packets, startup ordering, tick validation, listener cleanup, and failure behavior. Unsupported historical semantics remain evidence-deferred.

**Depends on:** RT-002.

### RT-004 — Add Directed and Broadcast Server-to-Client Delivery

**Owner:** delivery-semantics engineer
**Allowed scope:** one isolated delivery module, focused conformance fixtures, and tests.
**Goal:** Add target-one and target-all delivery only where the contract is evidenced.

**Acceptance criteria:** Test recipient selection, no-recipient handling, disconnect cleanup, ordering, and authorization boundaries.

**Depends on:** RT-003.

### UI-001 — Prove Client-Script-Owned UI and Input

**Owner:** client runtime engineer
**Allowed scope:** client runtime/UI adapter and a visible `Frontend/demo-map/` proof.
**Goal:** Let one client script create UI, receive one input/event, and emit one approved remote event.

**Acceptance criteria:** The capability gate denies undeclared UI/input APIs, and the preserved Player path visibly demonstrates the approved behavior.

**Depends on:** RT-002 and RT-003.

### INT-001 — Integrate the Preserved Player Bridge

**Owner:** integration engineer
**Allowed scope:** `Frontend/demo-map/` launch and bridge code plus narrowly scoped `Backend/local-player/` adapters.
**Goal:** Run one real map through the preserved Player with connected client and server Script Runtimes.

**Acceptance criteria:** A single-player session establishes the bridge, emits actionable diagnostics, and shuts down cleanly without rewriting the Player.

**Depends on:** IMP-001, RT-003, RT-004, and UI-001.

### QA-001 — Add a Sanitized End-to-End Real-Map Smoke Fixture

**Owner:** QA and evidence engineer
**Allowed scope:** public fixture, focused smoke test, and validation documentation.
**Goal:** Make import, both Script Runtimes, transport, and Player-visible output reproducible through one safe local smoke path.

**Acceptance criteria:** The fixture contains no private data and documents the exact focused command plus expected observable result.

**Depends on:** INT-001.

## Development Sequence

1. Complete RT-001.
2. Complete RT-002 and select one evidence-backed behavior.
3. Prepare IMP-001 field inventory and RT-003 test design without implementation overlap.
4. Implement RT-003, then RT-004 and UI-001.
5. Integrate through INT-001 and lock the behavior with QA-001.
6. Only after the loop is proven, evaluate later gameplay work in this order: world events, entity lifecycle, voxel/storage, player state, collision, and physics replication.

## Deferred Work

- Full physics and posture compatibility remain evidence-deferred.
- Broad historical API completion remains out of scope without demonstrated real-map usage.
- Player rewrites and repository-wide directory moves are not community tasks until their dependencies and provenance are audited.
