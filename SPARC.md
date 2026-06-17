# Specification Protocol for Agent Runtime Contracts (SPARC) Specification

> Version: 01.02
> Updated: 2026-06-17 03:55:16 UTC+00:00
> Status: minimal specification package
> Purpose: file contracts for stable project context

## Definition

**Specification Protocol for Agent Runtime Contracts (SPARC)**.

Use the full name in public, legal, and repository-facing references when
practical. The acronym `SPARC` may be used after the full name is established,
and remains the package acronym, file-prefix convention, and short technical
identifier.

`SPARC.md` is the entry point of the SPARC specification.

It describes:

- what SPARC is;
- which files are included in the SPARC package;
- which project contract files SPARC creates or updates;
- how templates map to generated live contracts;
- which rules govern reading, writing, conflicts, gaps, logs, and boundaries.

SPARC defines the files that hold canonical project context:

- what each file is for;
- what each file may contain;
- what each file must not contain;
- where current truth is stored;
- when a template must be read;
- how live contracts are updated;
- how SPARC stays separate from execution and coordination systems.

SPARC is a contract specification.

SPARC is not an execution system.

SPARC is declarative and structural. It provides deterministic file-driven
discovery for project context, not workflow execution.

## SPARC And PACT

**PACT** - **Protocol for Agent Coordination and Tasks**.

PACT is the execution and coordination layer. PACT may define agents, tasks,
task states, queues, locks, retries, schedulers, `runTask` flows, pipelines,
handoffs, worker routing, input interfaces, and runtime state.

SPARC does not define any of that.

SPARC defines the contracts that PACT or another execution system may read.

SPARC can serve as the expected-result standardization layer for PACT. In that
role, SPARC defines where the expected result, current truth, structural map,
logic, design, gaps, conflicts, and accepted-result logs live.

This does not make PACT part of SPARC. PACT remains the execution and
coordination layer.

```txt
SPARC says where project truth lives.
PACT says who does what, when, and under which execution rules.
```

They are related, but not interchangeable.

PACT or another external installer may use SPARC as a prerequisite. In that
case, the external installer may reference the SPARC repository, place the
SPARC package under `/ai/`, and then follow `INSTALL.md` to attach SPARC to the
target project.

That bootstrap order does not make PACT part of SPARC. SPARC still governs only
the specification package, templates, and generated live contract files.

## Agent OS Placement

SPARC may be installed inside a broader Agent OS layout:

```txt
/ai
├── pact/
├── raw/
├── sparc/
└── docs/
```

`/ai` itself is not SPARC. It is the broader agent-system root.

`/ai/pact/` is PACT or execution-system territory.

`/ai/raw/` is imported source material, examples, and raw data, not live SPARC
contract truth.

`/ai/sparc/` is SPARC package territory.

`/ai/docs/` is SPARC-described app documentation territory. It must contain app
documentation described by SPARC, and no PACT state, raw source material,
agent workflow files, scripts, adapters, or cache files.

This placement does not change SPARC's scope. SPARC remains the declarative
contract/result standardization layer. It must not absorb agent workflow rules,
task coordination, runtime state, adapters, queues, locks, retries, or
schedulers from the surrounding Agent OS.

## System Boundaries

SPARC is project-agnostic.

SPARC defines reusable structural contracts for context. It does not know the
business meaning, runtime implementation, or application-specific behavior of a
target project.

SPARC discovery must be explicit and deterministic. Agents must not infer hidden
inheritance, implicit merge behavior, or unstated authority from folder shape
alone.

PACT is agent-agnostic.

PACT may define reusable execution coordination. It does not depend on one
specific AI model, agent identity, or agent personality.

Projects are implementation-specific.

Projects define actual business logic, application behavior, runtime code,
domain data, and user-facing meaning.

```txt
SPARC standardizes context.
PACT standardizes execution.
Projects provide meaning.
```

| System | Agnostic To | Responsibility |
|---|---|---|
| SPARC | project | contracts and context |
| PACT | agent | execution and coordination |
| Project | none | business and application implementation |

## Authority

Owner instructions may authorize a contract change.

Accepted project truth must be written into the responsible live contract.

Until written into a live contract, chats, notes, imported specs, raw material,
and model outputs remain source material.

Installed SPARC package files define the contract rules.

If source material describes task execution or agent coordination, keep it out
of SPARC contracts and preserve it in a PACT-owned source location or another
external companion document.

## Included Package Files

The minimal SPARC package is:

```txt
README.md
SPARC.md
INSTALL.md

license/
  LICENSE.md
  COMMERCIAL-LICENSE.md
  NOTICE.md

templates/
  app-map.tpl.md
  app-logic.tpl.md
  app-schema.tpl.md
  platform-logic.tpl.md
  app-log.tpl.md
  design.tpl.md
```

`README.md` is the repository presentation page for GitHub and humans.

`SPARC.md` is the specification entry point and rule set.

`INSTALL.md` explains how to attach SPARC to a project.

`license/LICENSE.md`, `license/COMMERCIAL-LICENSE.md`, and
`license/NOTICE.md` define repository legal and notice terms, including the
source-available dual license model. They are not SPARC templates or live
contracts.

`README.md`, `SPARC.md`, `INSTALL.md`, and files under `license/` are static
package files during project installation and project work. They are read as
package files and must not be rewritten for a target project.

`templates/*.tpl.md` define how to create or update one matching live contract.

There is no separate `templates/README.md`. The template system is defined in
this specification to avoid extra files that agents would have to load anyway.

## Generated Project Contracts

When SPARC is installed into a project, it creates or updates live contract
files.

In the Agent OS layout, the documentation root is `/ai/docs/`:

```txt
/ai/docs/
  PLATFORM-LOGIC.md

  <app-name-en>/
    map/
      MAP.md
    logic/
      LOGIC.md
    schema/
      SCHEMA.md
    changes/
      LOG.md
      daily/
        YYYY-MM-DD.log.md
    design/
      DESIGN.md
```

Standalone installations may use another mapped documentation root, such as
`/docs/`, as long as that root contains only SPARC-described app
documentation.

Standalone generated docs shape:

```txt
/docs/
  PLATFORM-LOGIC.md

  <app-name-en>/
    map/
      MAP.md
    logic/
      LOGIC.md
    changes/
      LOG.md
      daily/
        YYYY-MM-DD.log.md
    design/
      DESIGN.md
```

`<app-name-en>` must be an English application name or stable English slug.

Lowercase kebab-case is recommended.

`PLATFORM-LOGIC.md` belongs at docs root because it can override multiple
applications.

App-level files live under the app folder because `MAP.md`, `LOGIC.md`,
`SCHEMA.md`, `LOG.md`, daily logs, and `DESIGN.md` are scoped app inputs.

Dated daily log files are created only when request-level work is recorded.

## Generated Files

SPARC distinguishes templates from real contract files.

```txt
README.md, SPARC.md, INSTALL.md = static specification package files
license/*.md = static legal and notice files
templates/*.tpl.md = instructions for creating or updating a contract
*.md               = live contract file with current project truth
```

During project installation or project work, only live contract files in the
mapped documentation root are created, updated, or appended according to
templates. In the Agent OS layout, that root is `/ai/docs/`.

Static specification package files are changed only when maintaining or
releasing SPARC itself.

Required live contracts in the mapped documentation root:

```txt
PLATFORM-LOGIC.md
<app-name-en>/map/MAP.md
<app-name-en>/logic/LOGIC.md
<app-name-en>/schema/SCHEMA.md
<app-name-en>/changes/LOG.md
<app-name-en>/changes/daily/
<app-name-en>/design/DESIGN.md
```

If a project has no platform rules yet, `PLATFORM-LOGIC.md` still exists and
records the gap.

If a project has no known design rules yet, `DESIGN.md` still exists and
records the gap.

## Responsibilities

| File | Source of truth for |
|---|---|
| `PLATFORM-LOGIC.md` | global platform rules that override app-level logic |
| `MAP.md` | first structural entry point, relevant project file inventory, attached parts, map-layer structure, responsibility zones |
| `LOGIC.md` | app behavior, rules, flows, permissions, invariants |
| `SCHEMA.md` | app data shape: entities, fields, enums, constraints, indexes, relations, references, public dataset views |
| `LOG.md` | app changelog: date and accepted change summary |
| `daily/YYYY-MM-DD.log.md` | request-level daily work log with actor and time |
| `DESIGN.md` | design-system contract: `google-labs-code/design.md` format, tokens, rationale, local UI/UX rules |

`MAP.md` is the canonical structural index and first structural entry point of
the app. It lists the map layer, split map files, relevant project file
inventory, attached parts, responsibility zones, and structural gaps.

Attached parts are app components that should be discoverable from the
structural map before an agent edits the project. Examples include modules,
plugins, integrations, route systems, UI subsystems, service layers, data
layers, extension points, and other independently meaningful app parts.

`MAP.md` must list attached parts directly when the list is compact. If an
attached part becomes too detailed, split its structural details into a named
map-layer file under `<docs-root>/<app-name-en>/map/` and list that file in
`MAP.md`.

`MAP.md` must not enumerate individual daily log files. Use
`changes/daily/*.log.md`.

`LOGIC.md` is current behavior.

`SCHEMA.md` is current data shape. It records the application schema contract
for humans and agents: entities, storage structures, fields, types, enums,
constraints, indexes, relations, cross-application references, and public
dataset views when the project exposes them. Runtime files such as
`schema.ts`, `dataset-schema.ts`, `APP-SCHEMA.ts`, migrations, DTOs, and
validation schemas implement or mirror this contract; they do not replace the
SPARC schema contract.

`LOG.md` is the app changelog. It contains only the date and what changed.

`daily/YYYY-MM-DD.log.md` records request-level work. The entry records actor
and time.

Daily entries must identify the actor, time, and changed content. `Time` uses
`HH:mm:ss`.

Dates and daily log filenames must use the project timezone. If the project
timezone is not declared, use UTC. The timezone should be declared in the
relevant `META` section.

`DESIGN.md` uses the `google-labs-code/design.md` format as the primary source
format: YAML front matter for design tokens and Markdown body for human-readable
rationale and guidance.

`DESIGN.md` must identify its theme in `META`. If the project has only one
theme, use `default`.

`DESIGN.md` is a structured exception to the default live contract format. It
may use YAML front matter and design-system sections before SPARC sections.
When present, YAML design tokens are normative for design values.

The source links are stored inside `DESIGN.md`. Agents do not need to visit
them for simple reading when `DESIGN.md` already contains current design truth
or an applicable design skill is available.

## Non-Core Companion Files

SPARC 01.02 does not require task, agent, draft, runtime-state, contract-code,
or implementation-plan files.

Examples of non-core files:

```txt
TODO.md
TASKS.md
STATE.md
APP-LOGIC-DRAFT.md
AGENTS.md
AGENTS-INSTALL.md
APP-CONTRACT.ts
IMPLEMENTATION-PLAN.md
```

Projects or PACT may add those files later.

If they exist, they are external companions owned by the project, PACT, or
another execution system. They must not override SPARC live contracts.

When present, `AGENTS.md` is a PACT-owned workflow rules container for agents,
not a SPARC live contract.

External companion files such as `AGENTS.md` and `AGENTS-INSTALL.md` are not
SPARC cascade children.

## File Layers

SPARC has four file groups.

### Specification Package

```txt
README.md
SPARC.md
INSTALL.md
templates/*.tpl.md
```

These files define SPARC itself.

### Repository Legal And Notice Files

```txt
license/LICENSE.md
license/COMMERCIAL-LICENSE.md
license/NOTICE.md
```

These files define repository use, distribution, copyright, and notice terms.
They are static package files, not templates and not live contracts.

### Platform Contract

```txt
<docs-root>/PLATFORM-LOGIC.md
```

This file defines platform-wide rules and invariants.

### App Input Contracts

```txt
<docs-root>/<app-name-en>/map/MAP.md
<docs-root>/<app-name-en>/logic/LOGIC.md
<docs-root>/<app-name-en>/schema/SCHEMA.md
<docs-root>/<app-name-en>/changes/LOG.md
<docs-root>/<app-name-en>/changes/daily/YYYY-MM-DD.log.md
<docs-root>/<app-name-en>/design/DESIGN.md
```

These files define app-scoped current truth.

## Mutability Rules

SPARC package files are not project working files.

During project installation and project work, do not rewrite:

```txt
README.md
SPARC.md
INSTALL.md
license/LICENSE.md
license/COMMERCIAL-LICENSE.md
license/NOTICE.md
```

Use those files as stable specification inputs.

Use `templates/*.tpl.md` as writing instructions.

Templates are package instructions, not project working files. Do not write
project-specific truth into templates.

Create, update, or append only the generated live contract files in the mapped
documentation root.

Live contracts must follow their matching templates.

## Read Rules

Use `SPARC.md` as the agent entry point for this specification.

Read `SPARC.md` when deciding how to work with SPARC files.

Do not require `README.md` for agent work. `README.md` is optional repository
presentation, not the source of SPARC rules.

Read `INSTALL.md` when attaching SPARC to a project.

Read `license/LICENSE.md`, `license/COMMERCIAL-LICENSE.md`, and
`license/NOTICE.md` for repository use, distribution, and licensing questions.
They are not needed for ordinary SPARC contract-file updates.

Read `<docs-root>/PLATFORM-LOGIC.md` for platform-wide rules.

Read `<docs-root>/<app-name-en>/map/MAP.md` for app structure and relevant project
file inventory.

Read `<docs-root>/<app-name-en>/logic/LOGIC.md` for app behavior.

Read `<docs-root>/<app-name-en>/schema/SCHEMA.md` for app data shape and schema
contracts.

Read `<docs-root>/<app-name-en>/changes/LOG.md` for accepted change summaries.

Read `<docs-root>/<app-name-en>/changes/daily/YYYY-MM-DD.log.md` for request-level
daily work details.

Read `<docs-root>/<app-name-en>/design/DESIGN.md` for design constraints.

Do not read a template for simple understanding of an existing live contract.

`DESIGN.md` may reference the `google-labs-code/design.md` format as its source
format. Do not open the external source for simple reading if `DESIGN.md`
already contains current design truth or an applicable design skill is
available. Use the source link when creating, updating, validating, or resolving
gaps in `DESIGN.md`.

## Template System

Template files use this naming pattern:

```txt
<contract-name>.tpl.md
```

Template mapping:

```txt
templates/platform-logic.tpl.md -> <docs-root>/PLATFORM-LOGIC.md
templates/app-map.tpl.md        -> <docs-root>/<app-name-en>/map/MAP.md
templates/app-logic.tpl.md      -> <docs-root>/<app-name-en>/logic/LOGIC.md
templates/app-schema.tpl.md     -> <docs-root>/<app-name-en>/schema/SCHEMA.md
templates/app-log.tpl.md        -> <docs-root>/<app-name-en>/changes/LOG.md
templates/app-log.tpl.md        -> <docs-root>/<app-name-en>/changes/daily/YYYY-MM-DD.log.md
templates/design.tpl.md         -> <docs-root>/<app-name-en>/design/DESIGN.md
```

Each template uses:

```md
## META

## USE

## RULES

## EXAMPLE
```

`META` identifies the template.

Template META fields use this order:

```txt
name
type
...
for
updated
version
```

The final three fields are always `for`, `updated`, and `version` in that
order. Additional template metadata, when needed, belongs between `type` and
`for`.

`USE` explains what the target contract file is for.

`RULES` defines how the target contract file must be created or updated.

`EXAMPLE` shows a small valid target contract file.

Template rules belong in templates. They should not be copied into live
contract files unless they are actual project truth.

## Live Contract Format

Real contract files should stay compact. They should contain current truth, not
template instructions.

Live contract files generally use:

```md
## META

## PURPOSE

## CURRENT

## GAPS
```

`META` identifies the document, version, and update stamp.

Live contract `META` should include:

```txt
updated: YYYY-MM-DD HH:mm:ss UTC+00:00
```

Use only `UTC+00:00` for update stamps. Do not write local timezone names,
IANA timezone names, city names, or other location-bearing timezone labels.

`PURPOSE` states what the document is responsible for.

`CURRENT` contains the current canonical content.

`GAPS` lists missing, unclear, unmapped, or unresolved areas. If there are no
known gaps, write `None.`

## Write Rules

Update the file responsible for the truth that changed.

If app structure, relevant project file inventory, attached parts, modules,
plugins, integrations, extension points, or map-layer split files change,
update `MAP.md`.

If app behavior changes, update `LOGIC.md`.

If app data shape, persistence shape, schema version, data references, public
dataset views, or runtime schema artifacts change, update `SCHEMA.md`.

If a platform invariant changes, update `PLATFORM-LOGIC.md`.

If a request changes app truth, append the request-level record to the current
daily log.

If a meaningful app change is accepted, promote a summary into `LOG.md`.

If design tokens, design rules, source references, or local overrides change,
update `DESIGN.md`.

When a change affects current truth and history, update the current contract
first, append the daily entry, then promote accepted summary into `LOG.md`.

When a meaningful Markdown content change is made, refresh that file's
`updated` stamp. Do not refresh `updated` for mirror-only, sync-only, or file
metadata changes.

Daily log entries must use the standard request-level format:

```md
### Request: short request title

- Actor:
- Time:
- Request:
- Changed:
- Old:
- New:
- Verified:
- Follow-up:
```

`Actor`, `Time`, and `Changed` are mandatory and must not be empty.

`Actor` identifies who wrote the log entry. It may be an agent, human, script,
or tool. It does not assign work or define coordination.

`Time` must use `HH:mm:ss`.

The date is provided by the daily filename: `YYYY-MM-DD.log.md`.

Dates and daily log filenames must use the project timezone. If the project
timezone is not declared, use UTC. The timezone should be declared in the
relevant `META` section.

Write `None` when there is no old behavior or follow-up. Write `Not run` when
verification was not run.

`LOG.md` is the accepted summary ledger, like an app changelog.

`LOG.md` summary entries inside `## CURRENT` must contain only the date and
what changed:

```md
### YYYY-MM-DD

- Change summary.
```

Do not put actor, time, request, verification, or related-log fields in
`LOG.md`. Those details belong in the daily log.

## Size Rules

Keep SPARC contracts compact and readable.

If a live contract grows beyond 800 lines, review whether it should be split by
meaningful responsibility.

If a live contract grows beyond 1000 lines, split it unless there is a clear
reason not to.

When splitting a non-map contract, use an index file and numbered chunks:

```txt
LOGIC.md
LOGIC-01.md
LOGIC-02.md
```

The required live contract file remains the entry point and must link to the
chunks.

For `MAP.md`, additional map files use the separate map split policy: name
split map files by meaning instead of sequence unless order is meaningful.
Follow `app-map.tpl.md` for map split rules.

## Conflict Rules

`PLATFORM-LOGIC.md` overrides app-level contracts.

`LOGIC.md` and `SCHEMA.md` own different scopes. If behavior and data shape
appear to conflict, expose the conflict and update the responsible live
contract instead of silently merging them.

`LOGIC.md` overrides `DESIGN.md` when behavior and design conflict.

`MAP.md` must not override behavior. It only maps structure.

`LOG.md` must not override current truth. It records accepted summaries.

Daily logs must not override current truth. They record request-level work.

If precedence is unclear, list the issue in `GAPS` and expose the ambiguity.

SPARC does not provide implicit merge semantics. If two files appear to define
the same truth and no explicit precedence rule applies, record a conflict or
gap instead of merging by interpretation.

## Gap Rules

If required context is missing, do not invent it.

Record missing, unclear, unmapped, or unresolved areas in `GAPS`.

If there are no known gaps, write:

```txt
None.
```

## Forbidden Mixing

SPARC files must not define PACT concerns:

```txt
tasks
task states
agent assignment
queues
locks
retries
schedulers
runTask
execution pipelines
workflow orchestration
```

Discovery is not execution. SPARC files must remain declarative, structural,
and discoverable; they must not become workflow runners or task state machines.

SPARC may say which contract file contains the truth.

SPARC must not say which agent should execute which task or how execution is
coordinated.

SPARC 01.02 also does not define `TASKS.md`, `TODO.md`, `STATE.md`,
`APP-LOGIC-DRAFT.md`, `AGENTS.md`, `AGENTS-INSTALL.md`, `APP-CONTRACT.ts`, or
`IMPLEMENTATION-PLAN.md`. Those may exist in PACT or in project-specific
systems, but they are not SPARC core contracts.

## Versioning

The authoritative SPARC package version is declared in this specification.

`README.md` may display the package version for repository visitors, but agents
do not need to read it.

Each template has its own template version.

Each maintained SPARC Markdown file should declare its own privacy-safe
`updated` stamp:

```txt
updated: YYYY-MM-DD HH:mm:ss UTC+00:00
```

Change the package version only when the contract model changes. Small wording
fixes inside examples do not require a new package version.

Version fields remain compatibility and template-drift markers. They are
secondary to `updated` when a human needs to know which file was touched most
recently.
