---
name: quest-ade-workspace
type: spec
description: Physical workspace layout, root contract, settings authority and configuration materialisation
---

# Quest ADE Workspace

Derived from `amber/proposals/ORG-AREA-WORKSPACE-REORG-2026-10.md` §3.

## Target layout

One organisation root per Area. No parent Git repository is required.

```text
Workspace/
  eikuro/          # Amber, application and research checkouts
    .agents        # ignored, locally materialised shared agent entry
    .vscode        # compiled organisation-root settings
    tab            # optional declared local link or pack, not a hidden dependency
    amber/
    flume/
  opbi/            # Porter, Tab, TabPy, TabJS
    .agents
    .vscode
    porter/
    tab/
    tabpy/
    tabjs/
  questade/        # public agent tools and future ADE clients
    .agents
    .vscode
    <agent-tools>/
```

## Realised root

One of the three roots above exists: **Quest ADE**, created 2026-10-26 at
`/Users/zhenyulin/Desktop/code/quest` — `quest`, not the `questade/` this plan
proposed. It holds `.specs` and `armory` as independent repositories and is **not
itself a Git repository**, which is the "no parent Git repository is required"
rule in force. `armory` is a **holding member, not the target shape**: its
dissolution into the root is [D18](DECISIONS.md#d18--armory-dissolves-into-the-quest-org-root-behind-the-d11-audit),
gated behind the ORG-01/ORG-02/ORG-03 audit in [ROADMAP.md](ROADMAP.md).

Three members are transitional rather than owned, and all are recorded here because
they contradict a requirement further down:

- `.agents` and `.vscode` are **symlinks into the Aurora checkout**. That is the
  "locally materialised shared agent entry" the target layout names, but reached
  by link rather than by compilation, so the root inherits Eikuro's settings
  composition — including `search.exclude` entries derived from
  `amber/components.yaml`, which lists Aurora's members, not Quest's.
- `.claude` and `.codex` are the **native harness entry points**, linked through
  the `.agents` link in exactly the form the shared tree's manifest declares
  (`.claude: .agents/harnesses/claude`, `.codex: .agents/harnesses/codex`).
  Porter materialises these at a consumer root; this root is not a Porter
  consumer, so they are created by hand. They are not optional: the shared MCP
  adapters launch through a repository-root-relative path
  (`.claude/../../tools/jev-mcp`), which resolves only where that entry point
  exists, so an org root without it reports `No such file or directory` and exits
  127 for every shared MCP server.
- `armory/porter.yaml` reaches back across the org boundary for its `$schema`
  (`../../aurora/porter/schemas/manifest.json`) and its composed `config.base`
  (`../../aurora/tabjs`). That contradicts the **"must work without sibling
  checkouts"** requirement under Configuration materialisation; removing it needs
  a Quest-owned editor-config base.

## Root contract

**Default: open one organisation root as one VS Code folder.** That root *is* the
active Area. Switch Area by opening the other root — preferably in a new window
when agents or tasks are running. Switch Project within an Area semantically,
without reopening the workspace. Work on an individual repository directly when
focused language-server performance or repository-local `.vscode` settings
matter.

**No giant default multi-root workspace.** An optional, on-demand multi-root
`.code-workspace` may be generated for genuinely simultaneous cross-Area editing,
diffing, search or Git work, with narrow membership. Multi-root is not required
merely for occasional cross-Area agent context.

Do not treat `@` as a universal repository-discovery mechanism. Copilot's `@`
addresses participants and agents; file and folder context uses the context
picker, and this differs by client and version.

## Settings authority

- One **organisation-root `.vscode` settings output** serves single-root
  operation.
- Each nested repository **retains its own independent `.vscode/settings.json`**
  for when it is opened directly.
- VS Code does **not** automatically apply a nested repository's folder settings
  when only the parent organisation root is opened. This is a host fact, not a
  configuration oversight, and it must not be worked around by duplicating
  settings into the root.
- Keep editor-wide **profile** settings distinct from **workspace** and **folder**
  settings.

## Configuration materialisation

Porter, through declared inputs, materialises local-only `.agents`, `.vscode` and
optional Tab or configuration links and outputs.

Requirements:

- compile and check deterministically;
- detect conflicts;
- never silently replace a real file;
- hooks and instructions still need the **native harness entry points**, tested
  per Copilot, Codex and Claude — a symlink alone is not sufficient;
- explicit versioned dependencies or clean-checkout copying must work **without
  sibling checkouts**;
- do not bake Eikuro-relative `../tab` or `../.agents` imports into published
  Opbi packages.

## Registrations

`folder.yaml` and `ignore.yaml` are candidate inputs for local repository
selection and exclusion across all three roots. Confirm their real locations and
schema, and their current ownership, **before** adding a compiler binding — they
were not present at the previously probed repository root paths.

Normalise to **one repository catalogue** serving both agent/context navigation
and optional Jsonnet workspace generation. Keep `workspace.jsonnet` →
`.code-workspace` **deferred and on demand**, not the default.

## Distinctions that must not be collapsed

| Setting family | Applies to |
| --- | --- |
| `files.exclude` | Explorer visibility |
| `search.exclude` | Search scope |
| `files.watcherExclude` | File watching |
| Git repository detection | Source Control |
| Active root selection | Which folder is primary |

Neither Git ignore syntax nor glob syntaxes may be copied blindly between them.
Do not promise a performance improvement without a measurement.

## Agent configuration

Single-root operation reduces ambiguous hook discovery and file anchoring, but
the following need regression tests rather than assumption:

- primary-folder hook semantics;
- direct-repository behaviour;
- cross-Area context selection;
- headless path resolution.

Avoid recursive symlink scans and duplicate agent trees. Private configuration
and credentials must not leak into public repositories.

## Agent Area selector

Two stages, deliberately separated:

- **Stage A** mirrors physical navigation: Area → organisation root, Project →
  one or more repositories, invoking public VS Code folder-opening APIs. It must
  not require a private Project Manager extension API.
- **Stage B** resolves the canonical semantic Project, spec and context, and
  optionally attaches other repositories to a native agent session.

A workspace switch is **not** a guaranteed agent-session migration. Keep four
things explicitly distinct at all times: the active Area, the primary execution
directory, attached context, and the current spec revision.
