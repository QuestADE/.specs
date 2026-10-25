---
name: quest-ade-features
type: spec
description: Quest ADE feature ledger — every shipped capability marked done and every planned capability marked open
---

# Quest ADE Features

The behavioural ledger for Quest ADE: what exists and can be observed today, and
what is planned but not built. Purpose and boundaries are in
[VISIONS.md](VISIONS.md); delivery order is in [ROADMAP.md](ROADMAP.md);
vocabulary is in [CONCEPTS.md](CONCEPTS.md).

## How to read this ledger

- `[x]` — **shipped.** The capability is observable in the delivered artifact
  named on the line: an installed extension package, a packaged theme, a
  materialised configuration file, or a repository recipe.
- `[ ]` — **planned, not built.** No artifact exists. A planning document is not
  an artifact: `amber/runes/quest/ROADMAP.md` states outright that "no task is
  implemented merely by this document".

Both parts carry their evidence inline. Part 1 is derived from the extension
manifests, the theme package manifest and the repository recipes actually read on
2026-10-25. Part 2 is derived from `amber/runes/quest/AREA-FIRST-ROADMAP.md` and
`amber/proposals/ORG-AREA-WORKSPACE-REORG-2026-10.md` in the Eikuro Amber
registry.

A `[x]` line records that the surface ships. It does **not** record that the
capability was accepted as correct, measured, or verified end to end. Where the
evidence contradicts the claim, the contradiction is stated on the line.

---

## Part 1 — Shipped

### 1.1 Editor extensions

Ten directories under `armory/extensions/` carry a `package.json` and ship a
VSIX. Two further directories (`agent-bridge`, `agent-now`) are documentation
seats with no manifest and no build.

#### `agent-inbox` — 0.1.31

Quick-capture inbox for ideas, over the workspace `.INBOX.md` backlog.

- [x] Quick capture of an item into `.INBOX.md` (`agentInbox.addTodo`)
- [x] Two-level scopes: add a scope and move an item between scopes (`addScope`, `moveTodo`)
- [x] Feature entries inside a scope (`addFeature`)
- [x] Inline editing of a captured item (`editTodo`)
- [x] Completion toggle (`toggleTodo`)
- [x] Archive and restore (`archiveTodo`)
- [x] Kick an item into a Copilot chat session as a manual handoff (`kickTodo`)
- [x] Promote a note to a spec (`promoteNoteToSpec`)
- [x] Link a note to an existing spec (`linkNoteToSpec`)
- [x] Reveal an item in the backlog file (`reveal`)
- [x] Open the backlog file and its Markdown preview, routed through the host custom editor (`openFile`, `openPreview`)
- [x] Collapse / expand all (`toggleAll`)
- [x] Search and folding over the backlog (`search`)
- [x] Refresh and a diagnostic log (`refresh`, `showLog`)
- [x] Keyboard organisation and context-menu commands (`keybindings`, `menus`)
- [x] Drag-and-drop reorder
- [x] Safe persistence over the Markdown store
- [x] Secondary Side Bar container `agentInbox` with webview view `agentInbox`

#### `agent-todo` — 0.1.2

Local-first personal task workspace.

- [x] Rich-text notes on a task
- [x] Nested tasks
- [x] Two-level scopes
- [x] Priority ordering
- [x] Drag-and-drop organisation
- [x] Secondary Side Bar container `agentTodo` with view `agentTodo.tasks`
- [x] `agentTodo.open` and `agentTodo.capture`

#### `agent-schedule` — 0.1.60

Recurring agent sessions, gated on Copilot being idle.

- [x] Recurring job definition and scheduling in an open window
- [x] Copilot-idle gating before a job runs
- [x] Add a job (`addJob`)
- [x] Configure a job (`configureJob`)
- [x] Enable or disable a job (`toggleJob`)
- [x] Run a job immediately (`runJob`)
- [x] Job details view (`showJob`)
- [x] Run log (`showLog`)
- [x] Export schedules to files (`exportSchedules`)
- [x] Refresh and reveal the Schedule view (`refresh`, `showView`)
- [x] Secondary Side Bar container `agentSchedule` with a webview view

#### `agent-guide` — 0.2.37

Local `.agents` guidance browser with no remote catalog.

- [x] Browse local `.agents` guidance as a tree
- [x] Activity Bar container `agentGuide` with tree view `agentGuide`
- [x] Refresh (`agentGuide.refresh`)
- [x] Zero-cost activation (empty `activationEvents`; the container activates it)

#### `agent-quest` — 0.1.0

Heading-to-commission resolver.

- [x] Resolve a stable `ROADMAP.md` heading ID at the cursor into one revision-bound commission (`resolveCommission`)
- [x] Copy the section identity (`copySectionIdentity`)
- [x] Open a commission (`openCommission`)
- [x] Preview a commission (`previewCommission`)

> **Known drift.** The installed identity is `workspace-local.agent-quest` 0.2.38
> produced by `board`, which declares only 2 commands; this package declares 4.
> A rebuild would install a second extension beside the current one rather than
> replacing it. Recorded as a gap, not a capability.

#### `agent-specs` — 0.1.3

Turn a selected Markdown or `.sp` heading into a revision-pinned, copyable
commission that never authorises a merge.

- [x] Preview an agent commission from a selection (`previewCommission`)
- [x] Copy the commission (`copyCommission`)
- [x] Run the agent commission (`runAgentCommission`)
- [x] Refusal to authorise a merge, encoded as the package contract

#### `agent-area` — 0.1.1

Compact seat navigator inside the existing Explorer.

- [x] Resolve seats from the Amber component registry
- [x] Compact navigator view in the Explorer: `agentArea.seats`
- [x] Open a seat's locus (`agentArea.openSeatLocus`)

#### `agent-resume` — 0.1.0

Hook-based failure classification with conditional, idempotent resumption.

- [x] Inspect a failure and classify it (`inspectFailure`)
- [x] Prepare a handoff (`prepareHandoff`)
- [x] Resume only if the failure class supports it (`resumeIfSupported`)
- [x] Cancel a pending retry (`cancelRetry`)

#### `aurora-copilot-plus` — 0.1.100

The merged successor of `agent-awake`, `agent-browser`, `agent-envoy` and
`agent-ram`: 27 commands, status-bar only, no views.

- [x] Keep-awake via installed hooks: install and remove Claude Code hooks, install and remove Copilot Chat hooks
- [x] Session estimates and ETA (`agentAwake.showSessionEstimates`, `agentEta.show`)
- [x] Telegram bridge configuration and toggle (`agentEnvoy.configure`, `agentEnvoy.toggle`)
- [x] Agent browser: toggle and open a URL (`agentBrowser.toggle`, `agentBrowser.openUrl`)
- [x] Memory and process usage, with dangling-process cleanup (`agentRam.show`, `agentRam.cleanDangling`)
- [x] Provider latency display and on-demand probe (`agentLatency.show`, `agentLatency.probe`)
- [x] Sidebar width control: show, resize both, resize primary, resize secondary, set a custom width (`agentWidth.*`)
- [x] Workspace commit and sync across repositories (`agentCommit.syncWorkspace`)
- [x] Open the extension's settings (`auroraCopilotPlus.openSettings`)
- [x] BYOK model routing: configure, plus Codex sign-in/sign-out and profile add/switch/delete
- [x] Six `languageModelChatProviders` vendor registrations
- [x] Configuration defaults contributed to the host (`configurationDefaults`)

#### `aurora-vscode` — 0.1.97

Editor and workspace integration surface: 8 commands, no views.

- [x] Filter the built-in Folders tree (`auroraVscode.refresh`, `selectFilters`)
- [x] Open or close Source Control repositories (`selectScmRepositories`)
- [x] Porter configuration action (`porterConfig`)
- [x] Compile a manifest's managed outputs (`porter.compileOutputs`)
- [x] Markdown custom editor for `*.md` and `*.markdown` (`markdownPreview`, `markdownSource`, `markdownToggle`)
- [x] Add Markdown to Copilot Chat from the rendered view (`markdownAddToChat`)
- [x] Continue inline comments across configured languages

#### Superseded and orphaned packages

- [x] `aurora-copilot-plus` retains the four merged status-bar features as one package; the standalone `agent-awake`, `agent-browser`, `agent-envoy` and `agent-ram` directories remain only as porting reference
- [x] `agent-resources` is retained as a retired predecessor of `agent-guide`
- [ ] `agent-explorer` has no source directory; its `refresh`/`selectFilters` ids overlap `aurora-vscode` and are treated as one surface to extend, not two
- [ ] `agent-project` 0.1.2 is orphaned: a VSIX exists with no source directory and no successor command family

### 1.2 Themes — `aurora-themes` 0.2.21

- [x] Aurora Light (`vs`)
- [x] Neon Light (`vs`)
- [x] Paper Light (`vs`)
- [x] Aurora Dark (`vs-dark`)
- [x] Neon Dark (`vs-dark`)
- [x] Paper Dark (`vs-dark`)
- [x] Theme JSON generated from Jsonnet sources (`theme-template.libsonnet`, `theme-helpers.libsonnet`)
- [x] One VSIX packaging both theme families

### 1.3 Shared editor configuration

- [x] Shared editor, extension and agent settings composed by language repositories rather than copied
- [x] Materialised root hygiene and editor configuration: `.gitignore`, `.editorconfig`, `cspell.config.yaml`, `.markdownlint.yaml`
- [x] Porter `config`-repository role with TabJS declared as the configuration base
- [x] Workspace-wide `settings/` fragments consumed by TabPy, TabJS and the shared agent tree

### 1.4 Delivery tooling

- [x] `just refresh-extension <extension>` — version bump, package, install, diff-verify
- [x] `just dev-host <extension> [port]` — Extension Development Host, default port 9333
- [x] `just package` — themes packaged into one VSIX
- [x] Theme generation and drift checks (`just generate`, `just check`)

### 1.5 Documentation seats

- [x] `agent-bridge` seat ships a protocol-gate verdict, its falsification evidence, and two tests that re-derive the verdict and refuse the addition of a protocol
- [x] `agent-now` seat ships design documentation and tests

### 1.6 Headless Quest surfaces owned outside this repository

Listed because the ADE is not only the editor surface.

- [x] `squire` CLI: `run`, `stats`, `quota`, plus the quest verbs `open`, `declared-status`, `field`, `next`, `review-ids`, `claim`, `transition`, `repair`, `requeue`, `runtime`, `annotate`, `sections`
- [x] `board` ingest writes and queries the `.quest/quest.db` store from `.kanban/` cards
- [x] `board` read-only workbench and the `spec-plus` (`*.sp`) language in source
- [x] `anatomy` static HTML views built from `ONTOLOGY.json`

---

## Part 2 — Planned, not built

### 2.1 Destination coverage

The nine destinations from `EXTENSIONS.md` §E1–E7. Measured against installed
manifests and tracked source: **1 exists, 8 partial, 0 absent.**

- [x] **E1 Inbox** — exists: `agent-inbox` 0.1.31 capture/todo/session-link surface with preview through the host custom editor
- [ ] **E1 enhancement** — `Promote to Specs` / `Link to existing node` with a conflict-safe diff preview and `Open in Specs` after success
- [ ] **E0 Headless shared Quest service** — partial: a `.quest/quest.db` read path exists; the canonical resolver, entity/edge query, command gateway and change event do not
- [ ] **E2 Specs** — partial: `spec-plus` and its preview command exist in `board` source only, absent from the installed build; no Explorer tree
- [ ] **E3 Sprint / roadmap** — partial: `.kanban` stages render read-only; no sprint tree, approval gate or DAG
- [ ] **E4 Now** — partial: host/agent state only; no quest-state row, attempt id, pinned revision or review queue
- [ ] **E5 Graph** — partial: two HTML renderers exist; no lazy graph editor tab
- [ ] **E6 Goal** — partial: a `goal` clause kind exists on `spec`; no goal matrix, hypothesis, experiment plan or evaluation receipt
- [ ] **E7a Distributed** — partial: cross-checkout inventory carries remote/branch/head; no worker capability, heartbeat, placement or trusted CI state
- [ ] **E7b Pipeline** — partial: `provider.pullRequests`/`issues` are `never[]` and `available` is hard-coded `false`; no PR/check/build/deploy join
- [ ] **E7c System** — partial: host process sampling only; no service/environment lens or telemetry receipt

### 2.2 Planned extension packages

Named in `EXTENSIONS.md`; none has a directory, a manifest or a registered
identifier.

- [ ] `questCore` — canonical source resolver and revision snapshot, typed entity/edge query, graph slicing, incremental invalidation, command and lifecycle admission gateway, one outward change event
- [ ] `agent-sprint` — sprint tree, approval gate and DAG rendering over the existing card store
- [ ] `agent-now` — lazy per-session DAG tab, read-only projection, no persistent task board
- [ ] `agent-graph` — unified Graph tool with Canvas and Anatomy visualization targets
- [ ] `agent-goal` — goal matrix, hypothesis, experiment plan and evaluation receipt
- [ ] `agent-distributed` — worker capability, heartbeat and placement
- [ ] `agent-pipeline` — PR, check, build and deploy join
- [ ] `agent-system` — service and environment lens with telemetry receipts

### 2.3 Area-first transition tasks (QN)

From `amber/runes/quest/AREA-FIRST-ROADMAP.md`. IDs are stable.

- [x] **QN-001** (P0) — grounded inventory of shipped Board, Specs and native session features and their consumer dependencies. *Delivered as `amber/runes/quest/INVENTORY.md` (observed 2026-10-24); not yet accepted.*
- [ ] **QN-002** (P0) — define Area/Project/Spec/Resource stable IDs and the project relationship contract
- [ ] **QN-003** (P0) — enforce spontaneous-session spec reconciliation and the provisional user-feedback loop in `.agents`
- [ ] **QN-004** (P0) — Marshal supervisor, fresh Squire worker and verifier profiles
- [ ] **QN-005** (P0) — native `agent-specs` resolves and previews canonical Amber nodes with no Board service dependency
- [ ] **QN-006** (P0) — pilot one spontaneous idea through observable result, user feedback, Amber diff and independent review
- [ ] **QN-007** (P1) — `agent-area` compact Areas/Projects navigator in the existing Explorer
- [ ] **QN-008** (P1) — optional `agent-now` lazy per-session DAG tab, only if a native UI gap is proven
- [ ] **QN-009** (P1) — optional `agent-resume` hook-based diagnosis with conditional retry and resume
- [ ] **QN-010** (P2) — retire Board integrations and the heavy Quest UI after a compatibility audit
- [ ] **QN-011** (P2) — optional cross-harness `agent-bridge` protocol, only if native session messaging fails a real case
- [ ] **QN-012** (P2) — user study measuring iterative spec quality and accepted throughput
- [ ] **QN-013** (P0) — verification infrastructure: native browser/Playwright, Extension Host and notebook routes with a fresh-Squire evidence receipt
- [ ] **QN-014** (P1) — minimal outcome/trace/error telemetry plus a profiling decision gate
- [ ] **QN-015** (P1) — reversible Entire session/commit provenance pilot with Git/GitHub compatibility
- [ ] **QN-016** (P1) — daily goal-alignment skill and shared `.agents` schedule validation
- [ ] **QN-017** (P2) — risk-weighted source-review sampling and evaluation

### 2.4 Cross-organisation and workspace tasks

From `amber/proposals/ORG-AREA-WORKSPACE-REORG-2026-10.md`. These are planning
commissions, not completed work.

- [ ] **LIFE-01** (P0) — record the operator's values, goals and autonomy constraints at a non-sensitive level
- [ ] **ORG-01** (P0) — inventory repositories, GitHub organisations, registration files, remotes, package names, licences, links, CI, symlink consumers and shipped VS Code features
- [ ] **ORG-02** (P0) — controlled Porter/Tab/TabPy/TabJS migration plan and smoke tests preserving history and import continuity
- [ ] **ORG-03** (P0) — verify QuestADE tool access and catalogue what to extract, leave or retire; no private Amber content in public exports
- [ ] **WS-01** (P0) — organisation-root workspace prototype with compiled `.vscode` defaults and bounded local links
- [ ] **WS-02** (P0) — single-root switching and repo-level focus acceptance tests
- [ ] **DAG-01** (P0) — baseline the current `agent-orchestrate` / Marshal / Squire session DAG: graph shape, serial host, conflicted writes, early unblock, verification/retry, token/time/RSS and context costs
- [ ] **DAG-02** (P0) — portable validated task/receipt protocol, provider capability discovery, safe admission, and headless Codex/Claude adapter proofs
- [ ] **DAG-03** (P1) — incremental ready-set and critical-path dispatch with bounded concurrency; retry only failed nodes
- [ ] **APP-01** (P1) — one real end-to-end vertical slice exercising spec → parallel implementation → independent evidence → human acceptance
- [ ] **LIFE-02/03** (P1) — weekly ideas/goals/commitments portfolio review with existing authorised tools
- [ ] **PORTER-UI** (P1) — CodeLens/actions on `porter.yaml`: `config --dry --json` preview and diff, explicit compile, source→consumer cascade and reverse provenance
- [ ] **AREA-01** (P1) — small `agent-area` navigator and `agent-specs` browser for Area → Project → canonical spec with version-safe previews
- [ ] **GRAPH-01** (P2) — lazy DAG/Graph/Now visualization of real attempts, dependencies and receipts as read-only projections
- [ ] **SIDEX-01** (P2) — bounded SideX build/fork feasibility: RAM/startup under load, extension-host API support, browser/CDP route, auth isolation, maintainership cost
- [ ] **LIFE-04/05** (P2+) — one reversible authorised cross-app action with receipt, recovery and cancellation before recurring delegated stewardship
- [ ] **WS-03** (P2) — generate narrowly scoped `*.code-workspace` via `workspace.jsonnet` only for proven cross-org use
- [ ] **KNOW-01** (continuous) — capture problem → hypotheses → experiments → evidence → decision → limits as reviewed records
- [ ] **OSS-01** (continuous) — publish generic non-core modules only when independently installable, licensed, tested and safe from proprietary configuration

### 2.5 Retirements and open gaps

- [ ] Retire the standalone `agent-awake`, `agent-browser`, `agent-envoy` and `agent-ram` directories once the merged features are accepted in `aurora-copilot-plus`
- [ ] Retire the `agent-resources` and `agent-explorer` packaged-only VSIXes
- [ ] Resolve the `agent-quest` source/installed identity drift (2 declared commands installed, 4 in this package, package name `agent-board` in `board`)
- [ ] Add `npm run test:host` to new Armory extension packages as part of implementation
- [ ] Add a `test` script to `anatomy`, which ships `tests/features.test.mjs` with no script
- [ ] Correct `armory/README.md`, which lists four extensions while ten directories carry a manifest
- [ ] Declare `agentEnvoy.getState` in the installed manifest; it is registered but undeclared
- [ ] Record host startup time, Extension Host idle RAM and CPU; all three are currently `unavailable`
- [ ] Read and render `squire stats`/`quota`; runner data currently has only a prompt reference and no UI
- [ ] Promote an Inbox item into a card; zero cards have reached review, so no idea-to-review instance is recorded

---

## Provenance

| Part | Source | Read |
| --- | --- | --- |
| 1.1 | `armory/extensions/*/package.json` | 2026-10-25 |
| 1.2 | `armory/themes/package.json` | 2026-10-25 |
| 1.3 | `armory/README.md`, `armory/specs/features.spx` | 2026-10-25 |
| 1.4 | `armory/extensions/justfile`, `armory/themes/justfile` | 2026-10-25 |
| 1.6, 2.1 | `amber/runes/quest/INVENTORY.md` | 2026-10-24 (observed) |
| 2.2 | `amber/runes/quest/EXTENSIONS.md` | 2026-10-23 |
| 2.3 | `amber/runes/quest/AREA-FIRST-ROADMAP.md` | 2026-10-24 |
| 2.4 | `amber/proposals/ORG-AREA-WORKSPACE-REORG-2026-10.md` | 2026-10-25 |

Counts stated here are counted from those sources, not estimated. Where a source
records an honest gap, the gap is carried into §2.5 rather than smoothed away.
