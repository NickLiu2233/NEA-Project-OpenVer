# Evidence Model

OpenVer makes compatibility claims only when a publishable source supports them. This document defines how contributors classify those claims and how public evidence is handled.

## Source Classes

| Source class | What it can establish | What it cannot establish alone |
| --- | --- | --- |
| Historical declaration or documentation | API names, signatures, documented intent | Runtime timing, error behavior, engine-side side effects |
| Preserved client or server bundle | Recovered control flow, serialisation shape, call sites | Behavior hidden behind unavailable services or data |
| Transport capture metadata | Message presence, direction, framing, and reproducibility limits | Meaning of unobserved fields or account-specific values |
| Local runtime implementation | Current OpenVer behavior and explicit adaptation policy | Historical behavior that the implementation merely assumes |
| Sanitized real-script usage summary | Priority, surface usage, and observed call patterns | Original source text, identities, payloads, or unobserved branches |

## Compatibility Classifications

| Classification | Meaning |
| --- | --- |
| `compatible` | The supported behavior is backed by evidence and validated through the current runtime path. |
| `partial` | A defined subset is implemented; missing behavior is named rather than implied away. |
| `recovered-only` | The behavior is present in a recovered artifact but is not yet proven through the current executable path. |
| `declared-only` | The surface is known from documentation or declarations, without runtime proof. |
| `evidence-deferred` | The project intentionally does not implement the behavior because available evidence is insufficient. |
| `evidence-blocked` | A needed source exists only in a non-publishable or unavailable form, so public implementation cannot proceed. |

## Rules For Public Fixtures

Every new evidence fixture or summary must state:

1. Its source class.
2. Whether it is redacted and what information was removed.
3. Whether the source is public, private, or reproduced from an approved public artifact.
4. Its reproducibility limits, including unavailable services, missing captures, or environment-dependent conditions.

Do not publish raw browser state, account material, private maps, private scripts, captured payload values, or token-bearing URLs. A fixture that cannot meet these requirements remains local and is represented publicly only by an honest blocked/deferred classification.

## From Evidence To Implementation

1. Locate the smallest source that directly supports the proposed behavior.
2. Add or update a neutral fixture or generator input only if it can be published safely.
3. Define the runtime contract at the correct boundary: client, server, transport, authoritative runtime, or Player adapter.
4. Add focused conformance coverage for the supported subset.
5. Generate reports from the evidence and implementation; do not edit generated output to improve appearance or counts.
6. Record unresolved fields, timing behavior, and edge cases as partial or deferred.

## Review Questions

- Does the evidence support this exact behavior, or only a similarly named API?
- Is the observed side and delivery direction explicit?
- Could a reviewer reproduce the public result without private data?
- Does the proposed code preserve the distinction between historical fact and local compatibility policy?
- If behavior is unknown, does the diagnostic identify the boundary without exposing sensitive input?
