---
name: quest-ade-decisions
type: spec
description: Accepted, provisional and rejected decisions governing Quest ADE
---

# Quest ADE Decisions

Status values: **accepted** (agreed and in force), **provisional** (recorded, not
yet ratified), **superseded** (replaced; retained as history), **rejected**
(considered and refused, with the reason kept).

A decision states what is in force. The reasoning behind a decision lives in the
Amber source it cites.

## D1 — Native harnesses first; no cross-harness protocol

**Accepted.** Copilot, Codex and Claude integrate natively: one MCP declaration
per adapter gives every harness the same tools, the shared hook contract gives
them one durable cross-harness state channel, and any harness can start another
as a subprocess. Handoff between sessions routes through specifications, source
Git and durable evidence rather than a message bus.

The single genuine gap — no native push into a *running* session of another
harness — is not a requirement in the accepted model. A messaging protocol
(QN-011) is therefore **not planned**. The `agent-bridge` seat ships the verdict
plus falsification evidence, and two tests refuse the addition of a protocol
until the evidence changes.

Source: `armory/extensions/agent-bridge/docs/protocol-gate.md`.

## D2 — Quest ADE is a separate organisation

**Accepted (proposed-implementation).** Quest ADE is its own GitHub organisation
with its own local root, holding reusable and open-source agentic development
infrastructure. Eikuro keeps private application and research specifications;
Opbi keeps generic developer configuration and language templates.

Source: `amber/proposals/ORG-AREA-WORKSPACE-REORG-2026-10.md` §2.

## D3 — Amber is the canonical writable private registry

**Accepted.** Amber holds Eikuro's private project contracts and accepted
decisions, and is the **only** writable specification registry for that corpus.
Quest ADE owns independently publishable interfaces and examples, and may
optionally consume an authorised Amber adapter.

**Private Eikuro specifications must never become a runtime requirement of a
public extension or CLI.**

Source: `amber/proposals/AMBER-SPEC-AUTHORITY.md`.

## D4 — No second requirements authority and no second task ledger

**Accepted.** Implementation repositories own their interfaces, schemas and
algorithms. Attempts, retries, budgets and results are owned by the execution
repository; a viewer projects them and never stores its own copy.

This is why the nine destinations are defined as **projections over a shared
revision-aware graph**, not as repositories, packages, databases or mandatory
workflow stages.

Source: `amber/runes/quest/EXTENSIONS.md`, shared invariants table.

## D5 — Area maps to GitHub organisation by default

**Accepted.** For this operator the default top-level semantic Area is a GitHub
organisation with a matching local organisation directory.

The mapping is a **configurable relation**, not a universal rule. Personal Areas
need not be GitHub organisations and must not be public. Stable identifiers remain
independent of GitHub names and physical paths.

Source: `amber/proposals/ORG-AREA-WORKSPACE-REORG-2026-10.md` §2.

## D6 — One organisation root, switched by Area

**Accepted.** Open one organisation root as one VS Code folder; switch Area by
opening the other root. No giant default multi-root workspace. An on-demand,
narrowly scoped `.code-workspace` may be generated for proven cross-organisation
work only.

Source: `amber/proposals/ORG-AREA-WORKSPACE-REORG-2026-10.md` §3.

## D7 — Keep native VS Code surfaces; add small contributions

**Accepted.** Keep the native Explorer, Source Control, editor, diff, terminal,
Problems, Testing and Chat. Add small discoverable contributions in the existing
sidebars. Open a graph or detail view as a lazy editor tab only when complexity
justifies it.

**Rejected by this decision:** forking VS Code; rebuilding a chat IDE; a
permanently open dashboard; nine always-active webviews or Activity Bar
destinations; a second writable copy of authored specifications; silently
converting an idea into execution.

Source: `amber/proposals/QUEST-VSCODE-LIFT.md`, `amber/runes/quest/EXTENSIONS.md`.

## D8 — An identifier is not an authorisation

**Accepted.** A selection or Markdown heading may name a task; it does not
convey permission to execute it. Every surface calls the **same** resolver and
admission boundary, and previews owner, scope, exclusions, prerequisites,
expected changes, harness, verification oracle, budget and external-effect
permissions before dispatch.

If a heading is not independently executable, offer **Create Task Draft** rather
than silently inventing missing acceptance criteria.

Source: `amber/runes/quest/EXECUTION-CONTRACT.md`.

## D9 — `aurora-copilot-plus` is the merged status-bar package

**Accepted (shipped).** Four status-bar extensions — keep-awake, browser, envoy
and RAM — were merged into one package at 0.1.100, alongside provider routing,
latency, sidebar width and workspace commit. The standalone directories remain as
porting reference and are retirement candidates.

Source: `armory/extensions/aurora-copilot-plus/package.json`.

## D10 — One VSIX per theme family pair, one repository recipe

**Accepted (shipped).** `aurora-themes` packages all six themes (Aurora, Neon,
Paper × Light, Dark) into a single VSIX, generated from Jsonnet sources. Theme
appearance is operator configuration and is **not** a Quest ADE extraction
candidate.

Source: `armory/themes/package.json`.

## D11 — Armory is a mixed repository; split case by case

**Accepted.** Armory bundles reusable extensions *and* Eikuro-specific editor
settings. Dispositions are recorded per content group in [AREAS.md](AREAS.md).

**Explicitly rejected:** moving all current Board, Squire or Armory code
unchanged into Quest ADE. Each move requires the audit in
[ROADMAP.md](ROADMAP.md) ORG-01/ORG-02/ORG-03 and a verified clean checkout on
the new path.

Source: `amber/proposals/ORG-AREA-WORKSPACE-REORG-2026-10.md` §2.

## D12 — The legacy QX queue is not executable

**Accepted.** The 24-task QX queue in `amber/runes/quest/ROADMAP.md` is
Board/Squire-centric and historical. It is retained as evidence and is not
reactivated for new work. New commissions come from the area-first roadmap.

Source: `amber/runes/quest/AREA-FIRST-ROADMAP.md` header.

## D13 — `EXTENSIONS.md` is superseded for new work

**Accepted.** The nine-destination contracts in
`amber/runes/quest/EXTENSIONS.md` remain useful as a **compatibility inventory**
and as the definition of the destinations, but no implementation may proceed from
it without re-admission through the current roadmap.

Source: `amber/runes/quest/EXTENSIONS.md` status block.

## D14 — `.specs` is the Quest ADE specification authority

**Accepted, 2026-10-26.** This repository is the Quest ADE equivalent of Amber:
a standalone registry of visions, features, roadmap, concepts, decisions and
conventions, authored independently of any implementation repository.

The extraction was directed by the operator on **2026-10-25** and settled on
**2026-10-26**. The four questions D14 left open were answered on the surface
recorded as `tmp/ask-decisions/quest-decisions.json`:

| Question | Resolution |
| --- | --- |
| Extraction scope | **All of Armory**, not the ADE-specific subset. `armory/` moved whole as a holding step; the target shape is its dissolution, recorded in D18. |
| History | **Moved with Git.** The repository keeps its commits, its branch and its `origin`; nothing was re-initialised or copied. |
| Target shape | **One organisation root** at `/Users/zhenyulin/Desktop/code/quest`, which is not itself a Git repository. Members are independent repositories. |
| Repository name | **`.specs`**, matching Amber's convention for a specification registry. |

Two consequences of the chosen shape are recorded alongside the decision. They
are properties read from the realised layout, **not** answers the operator gave —
neither was put to any question surface:

- The Quest org root **links** the shared agent tree and editor configuration
  rather than owning them: `quest/.agents` and `quest/.vscode` are symlinks into
  the Aurora checkout. Quest therefore inherits Aurora's settings composition
  until it owns a base of its own — see [WORKSPACE.md](WORKSPACE.md).
- `armory/porter.yaml` therefore reaches back across the org boundary for its
  `$schema` and its composed `config.base`. Those two paths are the boundary, not
  an accident of layout.

Source: operator answers on `tmp/ask-decisions/quest-decisions.json`, 2026-10-26.
The surface this entry originally cited, `tmp/ask-decisions/quest-extract.json`,
**timed out** — exit 3 after 1800 s with no submission: the page still read
`data-state="unanswered"` with `window.__answer = null`, and the four values it
appeared to return were each radio group's pre-checked default. The scope row was
corrected the same day by `tmp/ask-decisions/quest-reeval.json`; see D18.

## D15 — Five separate events, not one

**Accepted.** An accepted requirement revision, a real diff, deterministic
checks, independent verifier evidence, and the integration result are **five
separate events**. A worker exit, a green self-test or a chart does not mark a
project accepted. A reviewer accepts a verified revision explicitly, and the
task derives its status from that evidence without rewriting its original
acceptance criteria.

Source: `amber/proposals/ORG-AREA-WORKSPACE-REORG-2026-10.md` §5.

## D16 — Evidence over estimate

**Accepted.** A capability claim requires an artifact, a measurement or a
reproducible check. Where none exists the answer is `unavailable`, never an
estimate.

This repository applies the rule to itself: [FEATURES.md](FEATURES.md) separates
shipped artifacts from planning documents, and [NOTE.md](NOTE.md) records what
could not be evidenced at extraction time.

## D17 — Progressive release gates

**Accepted.** Capabilities advance through sketch → bicycle → car → supercar
gates. Shipping at sketch is permitted; describing a sketch as a car is not.

Source: `amber/runes/quest/AREA-FIRST-ROADMAP.md`.

## D18 — Armory dissolves into the Quest org root, behind the D11 audit

**Accepted, 2026-10-26.** Armory is a holding shape, not the target. Its
contents become the org root's own members — the theme repository and each
extension package — so `armory/` is flattened and retired rather than kept as
one repository.

Execution is **gated, not deferred**: each child moves only after the audit in
[ROADMAP.md](ROADMAP.md) ORG-01/ORG-02/ORG-03 and a verified clean checkout on
its new path. D11 already names that gate and already says the split is case by
case, so D11 is the mechanism for this dissolution rather than a decision against
it.

**Coupled obligation — citations move with the code.** The same pass that moves a
path updates every citation naming it, so no citation outlives its path: D1's
`armory/extensions/agent-bridge/docs/protocol-gate.md`, D9's
`armory/extensions/aurora-copilot-plus/package.json`, D10's
`armory/themes/package.json`, and the evidence and verification tables in
[FEATURES.md](FEATURES.md) and [NOTE.md](NOTE.md), whose paths are already
labelled historical. Until the move runs those citations stay as written, because
`armory/` is still the org root's member. D11 needs no path edit: what D18
supersedes is D11's premise that `armory/` is one repository, and D11's own Source
is a proposal outside the tree.

**Deferred, not decided.** A `porter.type` VS Code extension is the operator's
intended future clue for whether a change requires a rebuild and reinstall. It is
not built and nothing depends on it; it is recorded here so that the
delivery-detection question has a named home instead of being inferred from a
path again.

The shared agent tree is already brought into line with this shape: its `armory/…`
references named a repository by directory, which the tree's own accepted
decision *Shared resources stay organisation-neutral* forbids, so they now name
the repository by role and an extension by its own directory. No
`quest/agent-skills` repository is created for this — that rule's home is
`.agents/specs/DECISIONS.md`.

Source: `tmp/ask-decisions/quest-reeval.json` (2026-10-26), answers
`armory-shape: flatten-gated` and `source-citations: update-with-move`; the
rewording came from the free-form answer recorded there as `quest-skills`.
