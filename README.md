# KYE Protocol™ — OpenAPI Contracts

The patent-safe **API contract surface** of KYE Protocol™: OpenAPI 3.1
descriptions of every externally reachable KYE™ API, plus the compiled
agent-native tool packs derived from them.

This repository is a **mirror**. It is generated from the `public/openapi` tree
of the KYE Protocol master repository and re-synced on change; edits made here
are overwritten. Report problems via
[Discussions](https://github.com/KYE-Protocol/Discussions).

## Layout

| Path | What |
|---|---|
| `core.openapi.yaml` | Core API — entity hierarchy, principals, delegations, decisions |
| `data-governance.openapi.yaml` | Data Governance Pack™ endpoints |
| `state.openapi.yaml`, `state-library.openapi.yaml` | Authority-state surfaces |
| `reality-coupling.openapi.yaml`, `scenario-testing.openapi.yaml` | Reality Coupling™ + Scenario Testing™ |
| `consultant-programme.openapi.yaml` | Consultant programme surface |
| `native-engines.openapi.yaml` | Native engine surface |
| `site.yaml`, `app.yaml`, `app-partner.yaml`, `admin.yaml`, `sandbox.yaml`, `status.yaml` | Per-surface API descriptions |
| `agent-native/` | Compiled `.kye-tool` packs — a compact, token-efficient projection of the specs above for agent consumption, with an `index.json` manifest |

Request and response bodies reference the JSON Schemas published at
[KYE-Protocol/schemas](https://github.com/KYE-Protocol/schemas), whose canonical
`$id`s resolve under `https://kyeprotocol.com/schemas/`.

## Status of the agent-native packs

The `.kye-tool` files in `agent-native/` are **development-signed**. Each pack
carries `@kid kye:key:agent-tool-signing:dev` and `@sig
DEV-NOT-FOR-PRODUCTION`, and several declare a placeholder `@base
https://kye.example`.

Treat them as a **structural preview of the pack format**, not as a
signature you can verify or a base URL you can call. They are published because
the mirror is faithful to `public/openapi` rather than curated — hiding them
would misrepresent what the public surface contains. Production-signed packs
will replace them under a real key id; until then, do not build a trust
decision on their signature line.

The `.yaml` OpenAPI documents alongside them are unaffected by this and are the
authoritative contract.

## What is here — and what is deliberately not

These documents define **interface**: paths, operations, parameters, request
and response shapes, authentication schemes, error codes.

They do **not** define **mechanism**. How an authority decision is reached, how
evidence is canonicalised and sealed, how a replay proof is derived — none of
that is published here or anywhere else in the open. Knowing the endpoint that
returns a decision tells you nothing about how the decision was made. That
split is deliberate and permanent.

## Using them

```bash
git clone https://github.com/KYE-Protocol/open-api
cd open-api
npx @redocly/cli lint core.openapi.yaml
npx @redocly/cli preview-docs core.openapi.yaml
```

## Licence

Apache-2.0 — see [LICENSE](LICENSE). KYE™, KYE Protocol™ and the KYE product
names are trademarks of KYE Protocol; the licence covers the contract files,
not the marks.
