---
name: quest-ade-notes
type: note
description: Repository-specific notes, extraction provenance and known gaps
---

# Quest ADE Notes

## Extraction provenance

Every document in this repository was written on **2026-10-25** from material read
in `/Users/zhenyulin/Desktop/code/aurora`. Nothing here was inferred from a
directory name or a plan title.

| Source | Contributed to |
| --- | --- |
| `armory/extensions/*/package.json` | [FEATURES.md](FEATURES.md) §1.1 |
| `armory/themes/package.json` | [FEATURES.md](FEATURES.md) §1.2 |
| `armory/README.md`, `armory/specs/features.spx` | [FEATURES.md](FEATURES.md) §1.3 |
| `armory/extensions/justfile`, `armory/themes/justfile` | [FEATURES.md](FEATURES.md) §1.4, [CONVENTIONS.md](CONVENTIONS.md) |
| `armory/extensions/agent-bridge/docs/protocol-gate.md` | [DECISIONS.md](DECISIONS.md) D1 |
| `amber/runes/quest/INVENTORY.md` | [FEATURES.md](FEATURES.md) §1.6, §2.1, §2.5 |
| `amber/runes/quest/EXTENSIONS.md` | [FEATURES.md](FEATURES.md) §2.1–2.2, [CONCEPTS.md](CONCEPTS.md), [DECISIONS.md](DECISIONS.md) D4, D7, D13 |
| `amber/runes/quest/AREA-FIRST-ROADMAP.md` | [FEATURES.md](FEATURES.md) §2.3, [ROADMAP.md](ROADMAP.md) |
| `amber/proposals/ORG-AREA-WORKSPACE-REORG-2026-10.md` | [AREAS.md](AREAS.md), [WORKSPACE.md](WORKSPACE.md), [ROADMAP.md](ROADMAP.md), [DECISIONS.md](DECISIONS.md) D2, D5, D6, D11, D15 |
| `amber/proposals/AMBER-SPEC-AUTHORITY.md` | [DECISIONS.md](DECISIONS.md) D3 |
| `amber/components.yaml` | [components.yaml](components.yaml) |

The table records where content was **read from on 2026-10-25**, when Armory
still sat at `aurora/armory`. Those paths are historical; `armory/` is now
`quest/armory/`.

## Acceptance and relocation

The extraction was accepted on **2026-10-26** ([D14](DECISIONS.md)), which also
settled where the implementation repositories live. Four facts from that step are
easy to get wrong later:

- **The Quest org root is not a Git repository.**
  `/Users/zhenyulin/Desktop/code/quest` holds independent repositories as direct
  children — `.specs` and `armory`. There is no root commit to check out and no
  root remote.
- **The shared agent tree and editor configuration are linked, not owned.**
  `quest/.agents` and `quest/.vscode` are symlinks into the Aurora checkout, so
  Quest inherits Aurora's settings composition — including the `search.exclude`
  entries derived from `amber/components.yaml`, which lists Aurora's members, not
  Quest's. See [WORKSPACE.md](WORKSPACE.md).
- **Armory reaches back across the org boundary.** `armory/porter.yaml` resolves
  its `$schema` to `../../aurora/porter/schemas/manifest.json` and its composed
  `config.base` to `../../aurora/tabjs`, because neither is a sibling of the Quest
  org root. A Quest-owned editor-config base would remove both references.
- **Armory's `README.md` links inside it were repointed, not copied.** Its local
  `.editorconfig`, `.markdownlint.yaml` and `cspell.config.yaml` are untracked
  symlinks to `../../aurora/tabjs/`, so the repository tree itself stayed clean.

## Deliberately not mirrored

Amber carries four files that have no Quest ADE equivalent, and creating empty
twins would imply authority this repository does not have:

- **`BOOK.md`** — the manuscript. Reviewed reusable knowledge and the book belong
  to Saga, not to the ADE's specification authority.
- **`SPELL.md`** — Spell language conventions. Those are Eikuro tooling
  conventions and stay with the corpus they describe.
- **`plan/`** and **`proposals/`** — working proposals. Quest ADE records
  *decisions* and *plans of record*; an in-flight proposal belongs with its
  authoring Area until it is settled.
- **`runes/`** — per-project runes. Quest ADE has no project corpus of its own
  until QN-002 defines Area/Project identity.

## Implemented baseline — `quest-core`, 2026-10-26

`quest-core` is the org root's pipeline repository and carries nine delivered
commissions. It is an npm-workspaces monorepo of nine TypeScript ESM packages
that run on Node's native type stripping — no build step and no runtime
dependency. Its gate is `npm run check` (`tsc --noEmit`, then `node --test`):
**359 tests, clean, observed 2026-10-26**.

| Package | Commission |
| --- | --- |
| `@quest/identity` | QN-002 |
| `@quest/dag-baseline` | DAG-01 |
| `@quest/contracts` | QADE-CORE-01 |
| `@quest/protocol` | DAG-02 |
| `@quest/verification` | QN-013 |
| `@quest/run-store` | QADE-RUN-01 |
| `@quest/scheduler` | DAG-03 |
| `@quest/adapters` | PEER-01 |
| `@quest/soul` | SO-01 |

QADE-CORE-01, QADE-RUN-01, PEER-01 and SO-01 are commissions from the area-first
plan and have no row in [FEATURES.md](FEATURES.md) §2.3 or §2.4; their evidence
is the package and its `docs/` entry in `quest-core`.

Three gaps were found by independent verification and are carried, not smoothed
out:

- **`@quest/soul` labels the live `.agents` tree entirely authored.** That tree
  ships no `soul.manifest.json`, and the reader does not apply Porter's
  `manifest.yaml` symlink declarations, so 109 of 109 nodes read `authored`
  while several are materialised mounts. The label is honest for the
  declarations it reads; it is not yet useful for that tree.
- **`@quest/scheduler` enforces its concurrency width in `nextWave`, not in
  `applyEvent`.** A caller that records `start` directly can exceed the bound,
  and the next plan reports `capacity: 0` rather than a refusal.
- **`@quest/adapters`' headless candidate is a fixture stub.** The bake-off
  proves that one contract carries two adapters; it does not prove a Codex or
  Claude integration.

## What could not be evidenced

These gaps are carried in [FEATURES.md](FEATURES.md) §2.5 rather than resolved
here, because resolving them requires measurement, not writing.

- **Host startup time, Extension Host idle RAM and idle CPU are unavailable.**
  No measurement was taken. This is `unavailable`, not zero.
- **No end-to-end surface instance exists.** Nine core-slice commissions are
  delivered and verified in `quest-core` (see the baseline above), but all of
  them are headless libraries: no Inbox → card promotion and no editor surface
  exists, so no idea-to-review path has been walked by a person. The blocker
  remains the missing Inbox → card promotion, which is the E1 `Promote to
  Specs` gap.
- **Source and installed builds differ.** `agent-quest` 0.1.0 in Armory declares
  four commands; the installed identity is 0.2.38 produced by `board` with two.
  A rebuild would install a second extension rather than replacing the first.
- **Packaged-only VSIXes exist.** Fifteen VSIXes are present under
  `armory/extensions`; six match an installed identity. The remainder —
  including `agent-resources`, `agent-explorer` and `agent-project` — have no
  source directory, so they cannot be rebuilt or reviewed.
- **`armory/README.md` is stale.** It lists four extensions while ten
  directories carry a manifest.
- **`agentEnvoy.getState` is registered but undeclared** in the installed
  manifest.
- **`anatomy` ships `tests/features.test.mjs` with no `test` script.**
- **Runner data has no UI.** Only a prompt reference exists; `squire stats` and
  `squire quota` are not read or rendered anywhere.

## Reading discipline

Two rules that prevented over-claiming during extraction, and should hold for
future edits:

1. **A planning document is not an artifact.** `amber/runes/quest/ROADMAP.md`
   states outright that no task is implemented merely by that document. Every
   `[x]` in [FEATURES.md](FEATURES.md) names a manifest, a package or a file
   that exists.
2. **A count is counted.** Where a number appears — commands, extensions,
   destinations — it was counted from the source in the provenance table, not
   estimated from a description.

## Open questions blocking acceptance

The four questions in [DECISIONS.md](DECISIONS.md) D14 remain open. Until they
are answered, [FEATURES.md](FEATURES.md) Part 2 is the most volatile document
here: its task identifiers are stable, but the boundary between "Quest ADE owns
this" and "Eikuro or Opbi owns this" is not settled.
