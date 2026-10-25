---
name: quest-ade-options
type: spec
description: Candidate tooling, vendors and prior art with their evaluation state
---

# Quest ADE Options

Options under consideration, with what is known and what is still open. An option
listed here is **not** a decision. Decisions are in [DECISIONS.md](DECISIONS.md).

## Editor host

| Option | State | Notes |
| --- | --- | --- |
| Native VS Code extensions | **In use** | Ten shipped packages. Keeps native Explorer, SCM, editor, diff, terminal, Problems, Testing and Chat. |
| Standalone Quest IDE | **Rejected for V1** | An optional future client of the same contracts, not a prerequisite. |
| Forked VS Code / SideX fork | **Open — research only** | Bounded feasibility in [ROADMAP.md](ROADMAP.md) SIDEX-01: RAM and startup under load, extension-host API support, browser and CDP route, auth isolation, maintainership and upgrade cost. Go/no-go before any permanent fork. |
| Optional multi-root `.code-workspace` | **Deferred, on demand** | Generated via `workspace.jsonnet` only for proven cross-organisation use. Not the default. |

## Model providers

| Option | State | Notes |
| --- | --- | --- |
| GitHub-hosted Copilot models | **In use** | Default path. |
| BYOK providers via `languageModelChatProviders` | **In use** | Six vendor registrations ship in `aurora-copilot-plus`. |
| Delegating router over registered providers | **Open** | A router vendor delegating to other registered models is feasible; the stable API cannot delegate system messages or thinking parts, so it requires a host launch flag and a full quit to apply. Not yet shipped as a separate product. |
| Pre-checking a BYOK provider's quota | **Unavailable** | No provider exposes a balance to another extension. Only reaction to a `LanguageModelError.Blocked` is possible, and a fallback is safe only before any content part is emitted. |

## Cross-harness integration

| Option | State | Notes |
| --- | --- | --- |
| Native MCP tool declarations per harness | **In use** | One declaration per adapter; every harness sees the same tools. |
| Shared hook contract | **In use** | One durable cross-harness state channel. |
| Harness-as-subprocess dispatch | **In use** | Any harness can start another. |
| Native push into a running other-harness session | **Unavailable** | The one genuine gap. Not a requirement in the accepted model. |
| Cross-harness messaging protocol | **Rejected pending evidence** | The `agent-bridge` seat records the verdict and its falsification tests. Reopening requires a real case, not a preference. |

## Specification and task storage

| Option | State | Notes |
| --- | --- | --- |
| Amber Markdown and Spell corpus | **In use** | Canonical writable private registry for Eikuro. |
| `.kanban/` card store with `.quest/quest.db` | **In use** | Current execution store; read path only, projected. |
| Squire attempt ledger | **In use** | Owns attempts, retries, budgets and results. |
| A Quest-owned task database | **Rejected** | Would duplicate the execution owner's ledger. |
| `folder.yaml` / `ignore.yaml` as registration inputs | **Open** | Candidate repository-selection and exclusion inputs across all three roots. Confirm real location and schema before adding a compiler binding; they were not present at the previously probed root paths. |

## Visualisation

| Option | State | Notes |
| --- | --- | --- |
| Canvas target | **Partial** | Architecture and flow rendering exists as static HTML. |
| Anatomy target | **Partial** | Exploratory network and analytics rendering exists as static HTML. Two HTML renderers currently overlap. |
| Lazy graph editor tab | **Planned** | Read-only projections over real attempts, dependencies and receipts. Build only to close an observed native UI gap. |

## Session provenance

| Option | State | Notes |
| --- | --- | --- |
| Git and GitHub native provenance | **In use** | Commit trailers and PR links. |
| Session-linked commit provenance | **Planned** | QN-015: reversible, compatible with Git and GitHub, with a removal path that rewrites no history. |
| Automatic session rewriting on squash merge | **Rejected** | A squash merge flattens provenance; the record must be re-attachable rather than auto-rewritten. |

## Verification

| Option | State | Notes |
| --- | --- | --- |
| Extension Host tests | **Partial** | Declared by some packages only. |
| Native browser and Playwright | **Planned** | QN-013. |
| Notebook routes | **Planned** | QN-013. |
| Fresh-worker evidence receipt | **Planned** | QN-013. |

## Open questions

- Which Armory packages are genuinely reusable versus operator-specific?
- Does the extracted content move with Git history, or is it referenced in place?
- Does Quest ADE start as one organisation root or one repository?
- Which Porter and Tab surfaces belong to Opbi rather than Quest ADE, and in what
  order can they move without breaking a clean checkout?
