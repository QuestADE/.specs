---
name: quest-ade-roadmap
type: spec
description: Delivery order, gates and the executable task queue for Quest ADE
---

# Quest ADE Roadmap

Feature status lives in [FEATURES.md](FEATURES.md). This document owns **order,
dependencies and gates**: what is worked next, what must exist first, and what
evidence closes each stage.

## Delivery principle

Migrate safely, and prove **one reliable, verifiable cross-harness workflow**
before expanding IDE surfaces. A large surface built on an unproven dispatch
contract is the failure mode this roadmap is written to avoid.

Two queues are deliberately excluded:

- The legacy **QX** queue (24 tasks, Board/Squire-centric) is not executable for
  new work. It is retained in Amber as history.
- `amber/runes/quest/EXTENSIONS.md` is superseded for new work. Do not implement
  from it without re-admission.

## Stage gates

Progressive release gates, applied per capability rather than per repository:

| Gate | Required |
| --- | --- |
| **Sketch** | The desired journey is demonstrated. No claim of general correctness. |
| **Bicycle** | One whole realistic path runs end to end, including its failure path. |
| **Car** | Real usage: repeat runs, robustness, and a named user relying on it. |
| **Supercar** | Performance work tied to a measured metric, not to an intuition. |

A capability may sit at a lower gate than its neighbours indefinitely. Shipping
at Sketch is permitted; describing a Sketch as a Car is not.

## P0 exit criterion

The operator can work in one organisation root **or** one direct repository, and:

- links, paths and private boundaries survive an Opbi migration rehearsal;
- one concrete task is independently verified through a supported VS Code-native
  path **and** at least one CLI/headless path;
- that verification carries actual timing, cost and reliability evidence.

No large standalone IDE and no permanent SideX fork is required to reach P0.

## Phase 1 — Grounding and identity

Closes the gap between "we have code" and "we know what it is".

| Task | Depends on | Deliverable |
| --- | --- | --- |
| **QN-001** | — | Grounded inventory of shipped Board, Specs and native session features with consumer dependencies. *Artifact delivered as `amber/runes/quest/INVENTORY.md`; awaiting acceptance.* |
| **ORG-01** | — | Inventory of repositories, organisations, registration files, remotes, package names, licences, links, CI, symlink consumers and shipped VS Code features, marked current vs target ownership. |
| **QN-002** | QN-001 | Stable Area/Project/Spec/Resource IDs and the project relationship contract. |
| **ORG-03** | ORG-01 | QuestADE tool access verified; shared agent tools, Board/Squire/Armory implementations catalogued and designated extract, leave or retire. |

**Exit:** every shipped surface has an owner and a stated disposition; no
reference in the inventory points at a repository that does not exist.

## Phase 2 — Dispatch and verification baseline

Prove the execution contract before building any surface on it.

| Task | Depends on | Deliverable |
| --- | --- | --- |
| **DAG-01** | ORG-03 | Baseline of the current `agent-orchestrate` / Marshal / Squire session DAG: graph shape, serial host behaviour, conflicted writes, early unblock, verification and retry, plus token, time, RSS and context cost. Planned versus actually supported host features are distinguished. |
| **DAG-02** | DAG-01 | Portable validated task/receipt protocol, provider capability discovery, safe admission and independence constraints; headless Codex/Claude adapter proofs carrying the same acceptance contract. |
| **QN-013** | DAG-01 | Verification infrastructure — native browser/Playwright, Extension Host and notebook routes — with a fresh-worker evidence receipt. |
| **QN-003** | QN-002 | Spontaneous-session spec reconciliation and the provisional user-feedback loop, enforced in `.agents`. |
| **QN-004** | QN-003 | Marshal supervisor, fresh worker and verifier profiles. |

**Exit:** one task is dispatched, executed and independently verified with a
receipt, and the same acceptance contract holds in at least one headless path.

## Phase 3 — One real vertical slice

| Task | Depends on | Deliverable |
| --- | --- | --- |
| **APP-01** | WS-01, DAG-02 | One real end-to-end vertical slice — a point-in-time research result with notebook and tests — exercising spec → parallel implementation → independent evidence → human acceptance. |
| **QN-005** | QN-002, DAG-02 | Native `agent-specs` resolves and previews canonical Amber nodes with no Board service dependency. |
| **QN-006** | QN-005, QN-013 | Pilot one spontaneous idea through observable result, user feedback, Amber diff and independent review. |
| **DAG-03** | DAG-02 | Incremental ready-set and critical-path dispatch with bounded concurrency; retries touch only failed nodes. |

**Exit:** the slice is optimised for outcome, not infrastructure size. Wall time
to accepted result, repair rate, tokens, cost and peak process-tree RSS are
recorded against a sequential baseline.

## Phase 4 — Workspace contract

| Task | Depends on | Deliverable |
| --- | --- | --- |
| **ORG-02** | ORG-01 | Controlled Porter/Tab/TabPy/TabJS migration plan and smoke tests preserving Git history and import/package continuity. |
| **WS-01** | ORG-01, ORG-02 | Organisation-root workspace prototype with compiled `.vscode` defaults and bounded local links; one root opens and all relevant commands and hooks resolve. |
| **WS-02** | WS-01 | Single-root switching and repository-level focus acceptance tests: Area selection, Project selection, active-session safety, cross-Area context attachment, hook and primary-cwd behaviour, direct-repo mode. |
| **QN-007** | WS-02, QN-002 | `agent-area` compact Areas/Projects navigator in the existing Explorer. |
| **AREA-01** | WS-02, ORG-03 | Small `agent-area` navigator and `agent-specs` browser for Area → Project → canonical spec, with version- and permission-safe previews. |

**Exit:** switching Area does not require reopening the editor for a Project
switch; no private path or specification leaks into a public repository.

## Phase 5 — Surface expansion, only against proven gaps

Each task here requires an observed native UI gap. Build only what closes one.

| Task | Depends on | Deliverable |
| --- | --- | --- |
| **PORTER-UI** | ORG-02, WS-01 | CodeLens and actions on `porter.yaml`: `config --dry --json` preview and diff, then explicit compile; source→consumer cascade and reverse provenance. No guessed provenance and no silent overwrites. |
| **QN-008** | DAG-03 | Optional `agent-now` lazy per-session DAG tab. |
| **QN-009** | QN-013 | Optional `agent-resume` hook-based diagnosis with conditional retry and resume. |
| **GRAPH-01** | DAG-03, AREA-01 | Lazy DAG/Graph/Now visualization of real attempts, dependencies and receipts, as read-only projections. |
| **QN-014** | APP-01 | Minimal outcome/trace/error telemetry plus a profiling decision gate. |
| **QN-015** | DAG-02 | Reversible session/commit provenance pilot compatible with Git and GitHub. |
| **QN-016** | QN-003 | Daily goal-alignment skill and shared `.agents` schedule validation. |
| **WS-03** | WS-02 | Generate a narrowly scoped `*.code-workspace` via `workspace.jsonnet` only for proven cross-organisation use. |

## Phase 6 — Measurement, retrenchment and publication

| Task | Depends on | Deliverable |
| --- | --- | --- |
| **QN-010** | QN-007 | Retire Board integrations and the heavy Quest UI after a compatibility audit. |
| **QN-012** | QN-006 | User study measuring iterative spec quality and accepted throughput. |
| **QN-017** | QN-014 | Risk-weighted source-review sampling and evaluation. |
| **KNOW-01** | APP-01, DAG-01 | Continuous capture of problem → hypotheses → experiments → evidence → decision → limits as reviewed records. |
| **OSS-01** | ORG-02, ORG-03 | Publish generic non-core modules only when independently installable, licensed, tested and free of proprietary configuration. Track external adoption and maintenance burden. |
| **QN-011** | — | Optional cross-harness `agent-bridge` protocol, **only** if native session messaging fails a real case. Currently unplanned: the seat's tests refuse a protocol until the evidence changes. |
| **SIDEX-01** | DAG-02 | Bounded SideX build/fork feasibility: RAM and startup under load, extension-host API support, browser/CDP route, auth isolation, maintainership and upgrade cost. Go/no-go before any permanent fork. |
| **LIFE-01** | — | Record the operator's values, goals and autonomy constraints at a non-sensitive, user-approved level. |
| **LIFE-02/03** | LIFE-01 | Weekly read-only ideas/goals/commitments portfolio review with existing authorised tools; recommend explicit, uncertain trade-offs without creating another task system. |
| **LIFE-04/05** | LIFE-03 | One reversible authorised cross-app action with receipt, recovery and cancellation before recurring delegated stewardship. Permission-gated. |

## Continuous rules

- **Parallelism only at genuine seams:** established interfaces, distinct write
  scopes or proven isolation, real host concurrency, no overlapping mutable
  lockfiles, and explicit reviewer/integration ownership.
- **Compare before claiming:** sequential versus 2–3 workers on identical
  fixtures, reporting wall time to accepted result, success and repair rate,
  input/output tokens, cost, parent interventions and peak process-tree RSS. Do
  not presume more agents are faster.
- **Measure the workspace too:** single root versus direct repository versus
  focused optional multi-root, with identical extension profiles and real
  startup, idle RSS/CPU, language-server and watcher behaviour. Path exclusions
  are not proof of language-server suppression.
- **Migration safety:** no automated mass transfer. Export and check refs and
  links before and after each selected migration, verify a clean checkout with
  tests or CI on the new path, and prepare a revert or redirect plan. Never
  change a protected or public remote, licence, secret or private visibility by
  inference.
- **Correctness first:** an accepted requirement revision, a real diff,
  deterministic checks, independent verifier evidence and the integration result
  are five separate events.

## Provenance

Derived from `amber/runes/quest/AREA-FIRST-ROADMAP.md` (2026-10-24) and
`amber/proposals/ORG-AREA-WORKSPACE-REORG-2026-10.md` (2026-10-25). Task IDs are
preserved verbatim so Amber remains cross-referenceable.
