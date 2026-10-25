---
name: quest-ade-concepts
type: spec
description: Vocabulary for Quest ADE — Areas, Projects, Specs, Resources, seats, destinations and entity identity
---

# Quest ADE Concepts

The shared vocabulary. Derived from `amber/CONCEPTS.md`,
`amber/runes/quest/IDENTITY.md`, `amber/runes/quest/EXTENSIONS.md` and
`amber/proposals/ORG-AREA-WORKSPACE-REORG-2026-10.md`.

## Organisation and workspace

| Term | Meaning |
| --- | --- |
| **Organisation** | A GitHub organisation and its matching local organisation directory. Holds a set of member repositories. |
| **Organisation root** | The local directory opened as one VS Code folder. It is not itself a Git repository. |
| **Area** | The top-level semantic grouping. For this operator the default Area *is* an organisation, but the mapping is configurable and is not a universal rule. |
| **Project** | A logical unit of work. One Project may span several repositories or consume Resources from another Area. |
| **Resource** | A reusable artefact a Project consumes: a package, a template, a data source, a specification. |
| **Seat** | A repository's declared place in the workspace, registered in the component registry so navigation does not depend on a physical sibling path. |

## Specification identity

| Term | Meaning |
| --- | --- |
| **Spec** | An authored, revision-bearing statement of intent, requirement or contract. |
| **Stable ID** | An identifier that survives heading rename, reorder and reparent. IDs are never recycled for a different task. |
| **Entity reference** | `{ownerRepoOrProvider, repositoryId?, nodeId, documentUri?, sourceRevision?, environment?}` — the canonical way to name a spec node across surfaces. |
| **Spec revision** | The pinned revision of an authored specification. Independent of the code revision. |
| **Code revision** | The pinned revision of the implementation. A spec revision and a code revision are separate and both are recorded. |
| **Typed edge** | A validated relation between nodes. `contains` is hierarchy; `depends_on` is a validated DAG edge; `relates_to`, `implemented_by`, `verified_by` and `observed_by` are distinct relations. |
| **Provenance class** | Whether a link is *authored*, *inferred* or *observed*. The three are kept visibly separate. |

## Execution

| Term | Meaning |
| --- | --- |
| **Commission** | A bounded, revision-pinned task derived from a spec node, carrying scope, acceptance, dependencies and a verification oracle. |
| **Admission** | The gate that decides whether a commission is executable. An identifier alone is not authorisation. |
| **Attempt** | One execution of a commission by a worker. Owned by the execution repository, never by a viewer. |
| **Receipt** | The evidence an attempt produces: commands, outputs, environment, revision. |
| **Harness** | A native agent client: Copilot, Codex or Claude. |
| **Worker** | A fresh-context agent executing one bounded commission. |
| **Marshal** | The supervising role that derives a session DAG, dispatches eligible nodes and integrates results. |
| **Verifier** | An independently dispatched agent that proves a result against the accepted specification. A verifier is not the author. |

## Surfaces

| Term | Meaning |
| --- | --- |
| **Destination** | One of the nine conceptual Quest surfaces: Inbox, Specs, Sprint, Now, Graph, Goal, Distributed, Pipeline, System. A destination is a *projection* over a shared revision-aware graph — not a repository, a package, a database or a mandatory workflow stage. |
| **View** | A concrete VS Code contribution: a tree, a webview, a status-bar item or a custom editor. Several views may serve one destination; one package may serve several destinations. |
| **Graph** | The unified visualization and query tool with two targets: **Canvas** for architecture and flow, **Anatomy** for exploratory network and analytics. |
| **Lazy tab** | An editor tab opened on demand rather than a permanently mounted sidebar destination. |

## Discipline

| Term | Meaning |
| --- | --- |
| **Vertical slice** | One whole realistic path run end to end, rather than one module finished in isolation. |
| **Progressive release gate** | Sketch demonstrates the desired journey; bicycle runs one whole realistic path; car adds real usage and robustness; supercar is performance work tied to a proven metric. |
| **Evidence** | An artifact, a measurement or a reproducible check. Where none exists the answer is `unavailable`, never an estimate. |
| **Independent verification** | Proof obtained by an agent or procedure that did not produce the change. |

## Not concepts here

Two things that look like concepts and are not:

- **A second task ledger.** Attempts, retries, budgets and results are owned by
  the execution repository. A viewer projects them; it does not store them.
- **A second specification authority.** Implementation repositories own their
  interfaces, schemas and algorithms. Quest ADE owns the cross-repository
  contract, not a copy of every internal decision.
