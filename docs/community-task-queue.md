# Community Task Queue

**Updated:** 2026-07-31
**Milestone:** real-map import and the client/server Script Runtime loop

This queue divides the current compatibility effort into bounded work items. Contributors should claim one task at a time, keep changes inside the stated scope, and report unknown behavior as an evidence classification instead of guessing.

## Shared Rules

- Never include private map exports, raw scripts, captures, credentials, browser state, token-bearing URLs, or unpublished assets in public issues, branches, fixtures, logs, or reports.
- Keep evidence, generated reports, and executable implementation separate.
- Add focused conformance coverage for runtime behavior changes.
- Do not refactor the preserved Player. Add narrow adapters at an explicit boundary when integration is required.
- Run the narrowest useful validation first and report the exact command.

## Ready

### RT-001 — Generate a Sanitized Real-Map Compatibility Gap Report

**Owner:** unassigned
**Allowed scope:** `runtime-compat/` sanitized evidence import, report generator, focused tests, and deterministic public report output.
**Forbidden scope:** private map exports, raw scripts, payloads, token-bearing URLs, Player rewrites, and unrelated runtime changes.

**Goal:** Compare sanitized real-map API usage with the current runtime ABI and rank missing behavior by observed usage.

**Acceptance criteria:**

- The tracked report contains no source text, payload values, private identity, or private paths.
- Unsupported and uncertain APIs use evidence-based classifications.
- Focused validation proves deterministic output for approved sanitized input.

**Blocks:** RT-002 and the final implementation order.

## Queued

### RT-002 — Select the First Remote-Channel or UI Slice

**Owner:** runtime lead
**Allowed scope:** a decision record and one approved runtime contract.

**Goal:** Select exactly one highest-value executable behavior from RT-001 results.

**Acceptance criteria:** document client/server ownership, known evidence, unknowns, focused tests, visible demo proof, and explicit deferrals.

**Depends on:** RT-001.

### IMP-001 — Import Public Recovered Project Structure

**Owner:** importer engineer
**Allowed scope:** `demo-map/` importer code and focused importer tests.

**Goal:** Map approved public core project fields into the `nea-map/v1` import format.

**Acceptance criteria:** validate input; preserve unavailable fields as evidence-blocked or deferred; never infer missing historical values.

**Depends on:** RT-001 confirmation of the public/redacted field set.

### RT-003 — Add Bidirectional Remote-Channel Conformance

**Owner:** runtime transport engineer
**Allowed scope:** `runtime-compat/conformance/`, focused tests, and the smallest `demo-map/` adapter seam.

**Goal:** Prove client-to-server and server-to-client remote events with an explicit packet contract.

**Acceptance criteria:** test malformed packets, startup ordering, tick validation, listener cleanup, and failure behavior.

**Depends on:** RT-002.

### RT-004 — Add Directed and Broadcast Server-to-Client Delivery

**Owner:** delivery-semantics engineer
**Allowed scope:** one isolated delivery module, focused conformance fixtures, and tests.

**Goal:** Add target-one and target-all delivery only where the contract is evidenced.

**Acceptance criteria:** test recipient selection, no-recipient handling, disconnect cleanup, ordering, and authorization boundaries.

**Depends on:** RT-003.

### UI-001 — Prove Client-Script-Owned UI and Input

**Owner:** client runtime engineer
**Allowed scope:** client runtime/UI adapter and a visible `demo-map/` proof.

**Goal:** Let one client script create UI, receive one input/event, and emit one approved remote event.

**Acceptance criteria:** capability gates deny undeclared UI/input APIs, and the preserved Player path visibly demonstrates the approved behavior.

**Depends on:** RT-002 and RT-003.

### INT-001 — Integrate the Preserved Player Bridge

**Owner:** integration engineer
**Allowed scope:** `demo-map/` launch/bridge code and narrowly scoped `local-player/` adapters.

**Goal:** Run one real map through the preserved Player with connected client and server Script Runtimes.

**Acceptance criteria:** a single-player session establishes the bridge, emits actionable diagnostics, and shuts down cleanly without rewriting the Player.

**Depends on:** IMP-001, RT-003, RT-004, and UI-001.

### QA-001 — Add a Sanitized End-to-End Real-Map Smoke Fixture

**Owner:** QA and evidence engineer
**Allowed scope:** public fixture, focused smoke test, and validation documentation.

**Goal:** Make import, both Script Runtimes, transport, and Player-visible output reproducible through one safe local smoke path.

**Acceptance criteria:** the fixture contains no private data and documents the exact focused command plus expected observable result.

**Depends on:** INT-001.
