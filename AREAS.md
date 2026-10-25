---
name: quest-ade-areas
type: spec
description: Area ownership, organisation mapping and migration disposition for Quest ADE
---

# Quest ADE Areas

Derived from `amber/proposals/ORG-AREA-WORKSPACE-REORG-2026-10.md` (status
`proposed-implementation`, 2026-10-25) and `amber/components.yaml`.

## The three organisations

For this operator the default top-level semantic **Area** is a GitHub
organisation with a matching local organisation directory. The mapping is a
configurable relation, not a universal rule that every Quest ADE user's Area must
be a GitHub organisation.

| Area / organisation | Ownership | Members and disposition |
| --- | --- | --- |
| **Eikuro** | Internal application Areas and Projects, plus research. **Amber is the canonical writable private registry**; Saga is the curated learning and manuscript home. | Amber, Flume and the trading platform, and other product/research repositories. Private project contracts and accepted decisions stay here. |
| **Opbi** | Generic, non-agent-specific developer configuration, compiler and language templates. | **Move** Porter, Tab, TabPy and TabJS after dependency and release audits. The Porter configuration UI belongs with this product. |
| **Quest ADE** | Reusable and open-source agentic development infrastructure, native-harness adapters, DAG planning and dispatch, verification, and an optional IDE or extension client. | Extract shared development-agent functionality, cross-harness adapters and agent-facing utilities from current Eikuro ownership as contracts stabilise. |

## Classification rules

- **Own by independent product purpose**, not by the first internal consumer.
  Eikuro may consume versioned Opbi and Quest ADE packages without hosting their
  source.
- **Do not export Amber's private corpus.** Quest ADE owns independently
  publishable interfaces, examples and specs, and may optionally consume an
  authorised Amber adapter. Private Eikuro specifications must never become a
  runtime requirement of a public extension or CLI.
- **Inspect mixed repositories before moving them.** Armory bundles reusable
  extensions *and* Eikuro-specific editor settings; Squire and Board contain both
  historical and current experiments. Split, preserve or retire case by case. Do
  **not** claim that all current Board, Squire or Armory code should move
  unchanged. The shared agent tree's current location is transition state, not
  permanent ownership.
- **Keep `components.yaml` as a current-state inventory** until transfers and
  checkout/import updates are verified. Register Eikuro-owned components only at
  that point, record cross-organisation references as external dependencies, and
  do not remove entries early and lose discoverability.
- **Keep GitHub history and redirects intact** where transfer is supported. Audit
  package names, install scripts, symlinks, import paths, remote URLs, branch
  protection, Actions secrets, issue and PR links, README backlinks, licences and
  CI in each move. **A directory move is never a GitHub transfer.**

## Personal Areas

Personal Areas — wellbeing, relationships, education, family, administration —
need not be GitHub organisations and must not be public. They sit above the
engineering Areas in importance, not below them.

A future private Butler or personal layer is a plausible coordinator, but its
architecture and data store remain uncommitted. Reuse managed connectors and
proven third-party tools before building new universal personal infrastructure,
and keep private records out of public Quest ADE repositories.

## Armory disposition

Armory is the clearest mixed case and therefore the first audit target.

| Armory content | Disposition |
| --- | --- |
| Reusable extension packages (`agent-inbox`, `agent-todo`, `agent-schedule`, `agent-guide`, `agent-quest`, `agent-specs`, `agent-area`, `agent-resume`) | **Extract** to Quest ADE as their contracts stabilise. |
| `aurora-copilot-plus` (status-bar host integration, BYOK routing, browser, envoy, RAM) | **Split.** Host-integration and provider-routing parts are Quest ADE; operator-specific defaults are Eikuro. |
| `aurora-vscode` (Folders and SCM filters, Porter actions, Markdown custom editor) | **Split.** The Porter actions belong with Opbi; the Markdown custom editor and SCM filtering are Quest ADE candidates. |
| `aurora-themes` (six themes) | **Leave or retire.** Editor appearance is operator configuration, not reusable agentic infrastructure. |
| Shared editor configuration and materialised root hygiene | **Move** with Porter to Opbi, as the compiler that materialises them. |
| Documentation seats (`agent-bridge`, `agent-now`) | **Extract.** Their verdicts and falsification tests are reusable knowledge. |

No row here authorises a move. Each requires the audit named in
[ROADMAP.md](ROADMAP.md) **ORG-01**, **ORG-02** and **ORG-03**, and a verified
clean checkout on the new path before the old copy is removed.

## Registration state

Quest ADE has been registered by the operator but is **not yet among the GitHub
connector installations visible in this review**. Access must be verified before
creating or moving its repositories.

An OpenAI or GitHub connector not listing an organisation is **not** evidence
that the organisation does not exist. Absence from a connector listing is a
connector fact, not an organisational one.
