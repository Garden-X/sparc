# Specification Protocol for Agent Runtime Contracts (SPARC)

updated: 2026-06-16 23:37:13 UTC+00:00
Specification Protocol for Agent Runtime Contracts (SPARC) is a minimal
file-contract specification for keeping project context stable, explicit, and
readable for humans and AI agents.

It defines where project truth lives, what each contract file owns, and how
templates create or update those contracts.

Specification Protocol for Agent Runtime Contracts (SPARC) is not an executor,
task queue, scheduler, runtime, or agent coordination system. Those concerns
belong to PACT or another execution layer.

## Status

Version: `01.02`

Status: minimal specification package.

## Why It Exists

AI-assisted projects lose context when structure, behavior, design rules, and
change history are scattered across chats and files.

Specification Protocol for Agent Runtime Contracts (SPARC) keeps those concerns
in a small, inspectable contract set.

SPARC is declarative and structural. It provides deterministic file-driven
discovery for project context, not workflow execution.

`MAP.md` is the first structural entry point for an app. It records the main
file inventory and points to attached modules, plugins, integrations, extension
points, and any split map files.

## Repository Contents

| Path | Purpose |
|---|---|
| [SPARC.md](SPARC.md) | Entry point for the SPARC specification |
| [INSTALL.md](INSTALL.md) | How to attach SPARC to a project |
| [templates/](templates/) | Templates for live project contracts |
| [license/](license/) | Repository legal and notice files |

## What It Provides

Specification Protocol for Agent Runtime Contracts (SPARC) gives a project:

- a stable place for platform rules;
- a stable place for app structure and relevant project file inventory;
- a stable place for app behavior;
- a stable place for app data shape and schema contracts;
- a stable place for design-system rules;
- a two-layer app log: accepted summaries and request-level daily entries;
- templates for creating those files consistently.

## System Boundaries

SPARC is project-agnostic.

PACT is agent-agnostic.

Applications are implementation-specific.

SPARC standardizes context.

PACT standardizes execution.

Projects provide meaning.

| System | Agnostic To | Responsibility |
|---|---|---|
| SPARC | project | contracts and context |
| PACT | agent | execution and coordination |
| Project | none | actual business and application logic |

`README.md`, `SPARC.md`, `INSTALL.md`, and repository legal files are static
package files. Project-specific truth is written into generated live contracts
under the mapped documentation root. In the Agent OS layout, that root is
`/ai/docs`.

## Agent OS Placement

SPARC may be placed inside a broader Agent OS layout:

```txt
/ai
├── pact/
├── raw/
├── sparc/
└── docs/
```

In that layout, `/ai` is the agent-system root, `/ai/sparc/` contains SPARC
files, `/ai/docs/` contains SPARC-described app documentation, `/ai/pact/`
belongs to PACT or another execution layer, and `/ai/raw/` stores examples,
raw data, and imported source material.

This does not make SPARC an executor. SPARC still owns only its package,
templates, and generated live contracts.

## Quick Start

1. Read [SPARC.md](SPARC.md) as the entry point for the specification.
2. Read [INSTALL.md](INSTALL.md) for project attachment and setup.
3. Use the files in [templates/](templates/) to create or update live contracts.
4. Keep runtime and coordination files outside SPARC core unless another system
   explicitly owns them.

For agents, use [SPARC.md](SPARC.md) as the input file.

## SPARC And PACT

PACT means **Protocol for Agent Coordination and Tasks**.

Specification Protocol for Agent Runtime Contracts (SPARC) says where project
truth lives.

PACT says who does what, when, and under which execution rules.

SPARC can serve as PACT's expected-result standardization layer. It defines
where current truth, expected result, gaps, conflicts, and accepted result logs
live while PACT coordinates execution.

PACT is developed separately from the SPARC core package.

## Help

Use [SPARC.md](SPARC.md) first for specification questions and [INSTALL.md](INSTALL.md)
for project attachment questions.

After this project is published on GitHub, use repository issues for questions,
bugs, and proposed changes.

## Maintainer

Maintained by the repository owner.

## License

Specification Protocol for Agent Runtime Contracts (SPARC) is released under a
source-available dual license model.

This project should not be described as open source unless the license model is
changed to an OSI-compatible open-source license.

Free use is allowed for Free Projects under the Specification Protocol for
Agent Runtime Contracts (SPARC) Community License.

Commercial, paid, client, SaaS, consulting, internal business, or monetized use
requires a separate commercial license.

In short: free for free projects, paid for paid projects.

See:

- [license/LICENSE.md](license/LICENSE.md)
- [license/COMMERCIAL-LICENSE.md](license/COMMERCIAL-LICENSE.md)
- [license/NOTICE.md](license/NOTICE.md)
