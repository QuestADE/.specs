---
name: readme
type: spec
description: Quest ADE specification index, repository contract and relationship to Amber
---

# Quest ADE Specifications

`.specs` is the **specification authority for Quest ADE**: the portable agentic
development environment — its reusable editor surfaces, its headless execution
contracts, its verification discipline and its cross-harness adapters.

It is the Amber-equivalent for this organisation: a standalone registry of
visions, features, roadmap and decisions, authored independently of any
implementation repository.

## Status

**Accepted, 2026-10-26.** The specification authority itself is ratified: this
repository is the Quest ADE equivalent of Amber and owns the requirements in it.
The extraction that populated it was directed by the operator on 2026-10-25 from
the Eikuro Amber registry (`amber/`) and settled on 2026-10-26 — see
[D14](DECISIONS.md).

Ratifying the authority does not ratify every claim inside it. Documents here were
extracted rather than re-derived, so each one cites the Amber source it came from;
where Amber records a gap, an unavailable measurement or an unbuilt surface, this
repository reproduces the gap rather than asserting the capability. A section is
ratified when it carries an accepted revision of its own.

## Reading order

| Task | Document |
| --- | --- |
| Review every shipped and planned capability as a checklist | [FEATURES.md](FEATURES.md) |
| Reconstruct the Armory editor, theme and configuration capabilities | [FEATURES.md](FEATURES.md#reconstruction-target) |
| Understand what Quest ADE is and what it refuses to be | [VISIONS.md](VISIONS.md) |
| Review delivery order, gates and the executable task queue | [ROADMAP.md](ROADMAP.md) |
| Learn the vocabulary: Area, Project, Spec, Resource, Seat, Destination | [CONCEPTS.md](CONCEPTS.md) |
| Review accepted and provisional decisions | [DECISIONS.md](DECISIONS.md) |
| Understand Area ownership and organisation mapping | [AREAS.md](AREAS.md) |
| Understand the workspace, root and settings contract | [WORKSPACE.md](WORKSPACE.md) |
| Apply authoring and delivery conventions | [CONVENTIONS.md](CONVENTIONS.md) |
| Review candidate tooling, vendors and prior art | [OPTIONS.md](OPTIONS.md) |
| Review repository-specific lessons | [NOTE.md](NOTE.md) |
| Review repository metadata and registrations | [components.yaml](components.yaml) |

## Relationship to Amber

Amber remains the canonical writable registry for **Eikuro**'s private
application and research specifications, including the trading platform. Quest
ADE does not duplicate that corpus.

The split the organisation plan selects:

| Concern | Owner |
| --- | --- |
| Cross-repository contracts, private application/research specs, accepted decisions | Amber (Eikuro) |
| Reusable agentic infrastructure, native-harness adapters, DAG planning and dispatch, verification, optional IDE client | Quest ADE (this organisation) |
| Generic developer configuration, compiler and language templates | Opbi |
| Shared agent instructions and workflow tooling | `.agents` |
| Reviewed reusable knowledge and the manuscript | Saga |

Amber's Quest material — `amber/runes/quest/` and the Quest proposals under
`amber/proposals/` — is the **source** of this repository's content. Amber keeps
that material as historical evidence and as Eikuro's semantic/acceptance record;
it must not become a second executable task queue for Quest ADE.

## Boundaries

- **No private Amber content.** Nothing derived from Eikuro's private corpus may
  become a runtime requirement of a public extension or CLI. Quest ADE may
  consume an authorised Amber adapter; it may not export Amber's corpus.
- **No second authority.** Implementation repositories own their interfaces,
  schemas and algorithms. A spec here states observable behaviour; it does not
  restate a module's internals.
- **No invented capability.** A planning document is not an artifact. `[x]` in
  [FEATURES.md](FEATURES.md) requires a manifest, a package or a file that
  exists.

## Conventions

Authored Markdown carries YAML frontmatter with `name` first and `description`
last. Prose follows the organisation's Markdown conventions: one fact per line
where a list carries facts, tables for registers, and no restatement of a source
document's argument. See [CONVENTIONS.md](CONVENTIONS.md).
