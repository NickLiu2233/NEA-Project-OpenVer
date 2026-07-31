# NEA Project OpenVer

NEA Project OpenVer is a source-available preservation and compatibility project for the discontinued `dao3.fun` game runtime. It is an evidence-first local implementation: preserved packages, Script Runtime behavior, MuDB transport, and the authoritative runtime are kept as separate layers rather than treated as one opaque Player binary.

> **OpenVer scope:** this repository contains publishable implementation code and vetted preservation evidence. Private captures, browser state, credentials, private maps, and personal archives stay local and are never part of the open version.

## What This Repository Is

OpenVer is not a drop-in replacement for every historical DAO3 service. It is a self-hostable compatibility path that reconstructs only behavior supported by publishable evidence. The near-term product goal is concrete: run an editable map locally through both Client and Server Script Runtimes, MuDB transport, the authoritative runtime, and the preserved Player browser client.

The project deliberately separates:

- **Preserved evidence** from new executable compatibility code.
- **Declared API surfaces** from observed runtime behavior.
- **Client and server script ownership** from transport and Player integration.
- **Compatible behavior** from partial, recovered-only, declared-only, and evidence-deferred behavior.

## Start Here

| Goal | Start with |
| --- | --- |
| Understand the repository | [Repository layout](docs/repository-layout.md) |
| Understand the runtime boundaries | [Runtime architecture](docs/runtime-architecture.md) |
| Work with the open version safely | [Open version policy](docs/open-version.md) |
| Contribute code or evidence | [Contributing](CONTRIBUTING.md) |
| Follow the current delivery order | [Development roadmap](docs/development-roadmap.md) |
| Find a bounded contribution | [Community task queue](docs/community-task-queue.md) |
| Learn how compatibility claims are made | [Evidence model](docs/evidence-model.md) |
| Browse all engineering documentation | [Documentation index](docs/README.md) |
| Inspect ABI coverage and known limits | `runtime-compat/generated/gap-report.md` |
| Run the importable demo | `demo-map/` |

## Repository Map

| Path | Purpose |
| --- | --- |
| `demo-map/` | Reference project, map importer, client publication, and local server Script Runtime. |
| `runtime-compat/` | Machine-readable API/ABI catalogs, evidence generators, compatibility reports, and conformance fixtures. |
| `local-player/` | Recovered Player hosting, compatibility backend, launch tools, and Player-side adapters. |
| `preservation-dump/` | Bounded capture/export tooling. Its private output remains under ignored paths. |
| `works/` | Public work catalog; recovered/private work sources remain ignored. |
| `dao3-docs-mirror/`, `origin/`, `mudb/`, `dump/` | Vetted documentation, transport, bundle, and historical evidence. They are inputs to compatibility conclusions, not replacement application architecture. |
| `docs/` | Repository-wide governance, layout, and architecture documentation. |
| `tools/` | Small maintenance helpers, including the required patch wrapper. |

## Architecture

The executable path is deliberately layered:

```text
Project package
  -> Client Script Runtime / Server Script Runtime
  -> MuDB transport
  -> Authoritative Game Runtime
  -> Preserved Player browser client
```

Compatibility conclusions are generated from local declarations, historical bundles, preserved runtime behavior, capture metadata, and real script usage. When evidence is absent, the project records an explicit gap instead of synthesizing an API.

## Quick Start

Prerequisites: a supported Node.js runtime, the tracked repository assets, and network access for the pinned MuDB compiler on the first clean start.

```powershell
npm --prefix demo-map start
```

The default demo is then available at:

```text
http://127.0.0.1:4322/play/nea-script-lab?contentId=100110008
```

The command must stay running: it starts both the Server Script Runtime and the Player compatibility backend. Starting `local-player/backend/box3-server.cjs` by itself only serves the Player shell and does not run map scripts. For a clean-clone walkthrough, expected logs, port-conflict recovery, and Capability Manifest troubleshooting, see [Cold Start Guide](docs/cold-start.md).

For repository validation, run the documented package commands when you are ready:

```powershell
npm --prefix runtime-compat run build
npm --prefix runtime-compat test
npm --prefix demo-map run build
npm --prefix demo-map test
```

Run only the narrowest command needed while developing. Full package checks are useful before a pull request, but are not a substitute for a focused conformance test that proves the changed runtime behavior.

## Expected Local Result

At the current milestone, a successful local run means:

1. The map package is imported through the public project format.
2. Client and Server Script Runtimes start as separate execution realms.
3. The Player compatibility backend and the authoritative runtime establish the expected local transport path.
4. A visible demo behavior is delivered through the preserved Player without inventing unsupported historical API behavior.

It does **not** mean that every historical game mode, account feature, multiplayer room, physics detail, or public API is implemented. Read the [development roadmap](docs/development-roadmap.md) before planning work against unsupported behavior.

## Current Compatibility Posture

- Client and server Script Runtimes are separate execution realms with declared transport boundaries.
- The current local ABI and compatibility classifications are generated under `runtime-compat/abi/` and `runtime-compat/generated/`.
- Runtime-created entities can project only through captured, validated mesh bindings; unknown meshes remain script-local rather than receiving fabricated geometry.
- Historical posture body-shape values that have no local evidence remain `null`; the runtime preserves the current collider instead of guessing dimensions.
- Full physics/posture reconstruction, complete API parity, and a Player rewrite are intentionally out of scope until evidence and the real-map runtime loop justify them.

## How To Contribute Safely

1. Choose one task from the [community task queue](docs/community-task-queue.md), or create a bounded task with an observable acceptance condition.
2. Read the owning package documentation and its focused tests before editing.
3. Identify direct evidence and state what remains unknown. Missing evidence is a result, not a reason to fabricate behavior.
4. Keep the patch inside one runtime boundary and add focused validation.
5. Report exact commands run, generated files changed, and unresolved compatibility limits in the pull request.

See [CONTRIBUTING.md](CONTRIBUTING.md) for submission rules and [docs/evidence-model.md](docs/evidence-model.md) for the claim vocabulary.

## Community

- GitHub open-version repository: <https://github.com/ForgottenArch/NEA-Project-OpenVer>
- QQ group ? **???? - dao4.fun ??????**: <https://qm.qq.com/q/Mixf3L5xeO>

Please do not post browser profiles, cookies, credentials, token-bearing URLs, private maps, or private captures in issues, pull requests, or the group.

For substantial work, open an issue or draft pull request that names the task ID, allowed scope, evidence class, validation plan, and one reviewer-needed question. This keeps community effort aligned with the real-map client/server runtime loop instead of dispersing it across speculative API completion.

## License

This repository is source-available under the [PolyForm Noncommercial License 1.0.0](LICENSE.md). Commercial use is not permitted under that license.
