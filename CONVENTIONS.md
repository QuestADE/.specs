---
name: quest-ade-conventions
type: spec
description: Authoring, specification and delivery conventions for Quest ADE
---

# Quest ADE Conventions

## Specification authoring

- **Frontmatter on every authored Markdown file.** `name` first, `description`
  last, identity keys between them. Root-level keys only — never a nested
  `metadata` mapping.
- **One fact per line** where a list carries facts. Tables are for registers
  (owners, dispositions, provenance), not for prose.
- **Cite the source.** A document derived from Amber names the file it derives
  from. A claim that cannot be cited is marked provisional.
- **State status.** A specification carries an explicit status: provisional,
  accepted, superseded or rejected. Silence is read as provisional.
- **Do not restate the source's argument.** A specification states what is in
  force and points at the evidence; it does not reproduce the deliberation.

## Naming

- Repository names are lower-case and hyphenated.
- Task identifiers are stable and never recycled for a different task. An
  identifier that appears in a source document is preserved verbatim so the two
  remain cross-referenceable.
- Extension package names are lower-case, hyphenated, and prefixed by domain
  (`agent-` for agent surfaces, `aurora-` for host integration).
- A package name describes the surface it contributes, not the internal module
  that happens to implement it.

## Extension delivery

Changing an extension is not complete until the running copy matches the source.

1. Change source, then run the package's own tests, including Extension Host
   tests where the package declares them.
2. Run the owning repository recipe **once** at the end: `just refresh-extension
   <extension>` performs the version bump, package, install and diff-verify.
3. Verify the **installed** artifact, not only the source tree.
4. Report any required host reload rather than assuming it happened.

Do not stop after source tests. Do not install a package whose manifest identity
differs from the installed one without recording the resulting duplicate.

## Theme delivery

`just package` builds all six themes into one VSIX. Theme JSON is generated from
Jsonnet sources; regenerate rather than hand-editing generated output, and run
the drift check before committing.

## Configuration ownership

In a consumer repository with a root `porter.yaml`, Porter-managed configuration
is **manifest-owned**. Put repository-specific customisation in `porter.yaml`
rather than editing a materialised file, which the compiler will overwrite.

## Evidence

- State exact commands and their results.
- Distinguish **unavailable** from **zero**. A measurement that was not taken is
  unavailable, not zero.
- Record a known gap as a gap. Do not smooth a contradiction out of a ledger
  entry.

## Boundaries

- Never place private Eikuro content — specifications, paths, credentials or
  configuration — in this repository.
- Never add a runtime dependency on a sibling checkout to a publishable package.
- Never make a public extension or CLI require an Amber adapter; the adapter is
  optional and authorised.

## Agent memory and durable knowledge

An assistant's built-in memory store is a **cache**, not a home. On this machine
it sits outside every repository and outside Git:

| Scope | Path | Lifetime |
| --- | --- | --- |
| User memory | `~/Library/Application Support/Code/User/globalStorage/github.copilot-chat/memory-tool/memories/` | every workspace on this machine |
| Repository memory | `~/Library/Application Support/Code/User/workspaceStorage/<hash>/GitHub.copilot-chat/memory-tool/memories/repo/` | one registration of one workspace, keyed by a storage hash |

Neither is reviewed in a pull request, shared with a collaborator, or readable
by another harness, and the second disappears when that workspace storage is
cleared. A fact that matters therefore has to be written somewhere else.

Route it to the document that owns it:

- **Quest ADE intent, contracts, decisions and known gaps** — this repository.
- **Implementation facts about a package** — that package's own README, or its
  `docs/` directory, in the repository that owns it.
- **A reusable agent technique** — the skill in the shared agent tree that owns
  that technique, never this repository.
- **Session working state** — the org root's ignored `tmp/`, which is disposable
  and is not a record.

A memory entry that matters is a prompt to write one of the above.

## Markdown rendering

Checklists use nested bullet lists with `- [x]` and `- [ ]`, not tables. GitHub
does not render a checkbox inside a table cell, and a ledger whose states do not
render is not a ledger.

## Plan pages

`.quest/` holds the delivery-plan page family: `index.html` (the plan of
releases), `milestones.html` (one row per release), `slice-0N-<id>.html` (one page
per vertical slice) and `plan.json` (the derived data the pages read).

- **`data.js` is the single source and `_build.mjs` writes every generated page.**
  Edit the data or the builder, then run `node _build.mjs` from inside `.quest`.
  Hand-editing a generated page loses the change on the next build.
- **Hand-authored alongside it**: `review.html`, `extensions-mockup.html`,
  `quest-mock.html`, `codicon.css`, `dag.css`, `dag.js`. The builder does not
  overwrite these.
- **A card's colour is its container's class**, read through
  `window.QUEST_CONTAINERS[REPOS[id].repo].cls` — never `REPOS[id].cls`. A legend
  row that names a per-card class a container does not have matches no card.
- **Tag vocabulary** is empty, `new`, `deferred`, `superseded` and `done`; `done`
  marks a delivered card. The builder validates no tag string, and the graph and
  the register both render tags in the browser, so verify a tag change by
  rendering the page rather than by grepping the generated HTML.
- **The build is a gate, not a convenience**: it exits non-zero on an unknown
  card, a missing milestone, a missing slice, a duplicate card and a forward
  dependency, and it prints the milestone sizes, cumulative totals and maximum
  round for comparison against the previous run.

`.quest/` is not a tracked member of any repository at present: the org root is
not a Git repository ([DECISIONS.md](DECISIONS.md) D14), and no member tracks the
directory. Its durability is therefore the same as any other uncommitted local
file until a member adopts it.
