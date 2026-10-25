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

## Markdown rendering

Checklists use nested bullet lists with `- [x]` and `- [ ]`, not tables. GitHub
does not render a checkbox inside a table cell, and a ledger whose states do not
render is not a ledger.
