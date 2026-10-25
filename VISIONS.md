---
name: quest-ade-visions
type: spec
description: What Quest ADE is, what it refuses to be, and the north star above it
---

# Quest ADE Visions

Derived from `amber/runes/quest/AREA-FIRST-ARCHITECTURE.md`,
`amber/proposals/QUEST-AIDE.md`, `amber/proposals/QUEST-VSCODE-LIFT.md` and
`amber/proposals/ORG-AREA-WORKSPACE-REORG-2026-10.md`.

## V1 — A portable agentic development environment

Quest ADE is the reusable agentic development environment: native-harness
adapters, DAG planning and dispatch, verification discipline, and optional
editor clients. It is deliberately **not** one product. It is the set of
contracts and small surfaces that let a human direct agents across harnesses and
still see, verify and accept what changed.

Its success measure is **verified accepted outcomes per human attention hour** —
not commits, worker count, lines of code or repository count.

## V2 — The human stays in the loop at the seams that matter

Accepted requirement revision, real diff, deterministic checks, independent
verifier evidence and integration result are **separate events**. A worker exit,
a green self-test or a chart does not mark a project accepted. Only a reviewer
accepts a verified revision.

Corollary: an identifier is not an authorisation. A Markdown heading may name a
task; it does not convey permission to execute it.

## V3 — Native harnesses first, no second bus

Harnesses already talk natively: one MCP declaration per adapter gives every
harness the same tools, the shared hook contract gives them one durable
cross-harness state channel, and any harness can start another as a subprocess.
The one genuine gap — no native push into a *running* session of another harness
— is not a requirement in the accepted model, which routes handoff through
specifications, source Git and durable evidence.

Consequence: a cross-harness messaging protocol is **not** planned. The
`agent-bridge` seat exists to record that verdict and the evidence under it, and
its tests refuse the addition of a protocol.

## V4 — Small composable surfaces, not a second IDE

Keep VS Code's native Explorer, Source Control, editor, diff, terminal,
Problems, Testing and Chat. Add small discoverable contributions in the existing
sidebars. Open a graph or detail view as a lazy editor tab only when its
complexity justifies it.

Refused by design:

- forking VS Code, or rebuilding a chat IDE;
- a permanently open dashboard;
- nine always-active webviews or Activity Bar destinations;
- a second writable copy of authored specifications;
- a second task ledger beside the execution owner's;
- silently converting an idea into execution;
- a second requirements authority.

## V5 — Areas, Projects, Specs and Resources

The default top-level semantic **Area** is a GitHub organisation and a matching
local organisation directory. The mapping is a configurable relation, not a
universal rule: personal Areas such as wellbeing, relationships, education and
administration need not be GitHub organisations and must not be published.

A logical **Project** may span several repositories, or use resources from
another Area. Stable Area/Project/spec identifiers survive heading renames,
reordering and reparenting, and remain independent of GitHub names and physical
paths.

## V6 — One organisation root, switched by Area

Open **one organisation root** as one VS Code folder; that root is the active
Area. Switch Area by opening the other root, preferably in a new window when
agents or tasks are running. Switch Project within an Area semantically, without
reopening the workspace.

A giant default multi-root workspace is refused. An on-demand, narrowly scoped
`.code-workspace` may be generated for genuinely simultaneous cross-Area work.

## V7 — Evidence before claim

Every delivered capability should be evidenced by an artifact, a measurement or
a reproducible check, and where none exists the answer is `unavailable` rather
than an estimate. This repository applies the rule to itself: [FEATURES.md](FEATURES.md)
distinguishes shipped artifacts from planning documents, and
[NOTE.md](NOTE.md) records what could not be evidenced.

## North star above the organisations

The higher aim is not a faster ADE. It is a **human-governed agent** helping the
operator manage life and work: evaluate and organise ideas, allocate scarce
attention, time, money, compute and agent capacity, delegate authorised work, and
learn from real outcomes.

This is a multi-objective, values-constrained portfolio problem, not a single
productivity metric. Eikuro, Opbi and Quest ADE are engineering Areas mapped to
GitHub organisations; they sit *below* that goal. Decisions, budgets, consent and
overrides stay human-controlled, and private records stay out of public
repositories.
