# INSTALL

> For: Specification Protocol for Agent Runtime Contracts (SPARC) 01.00
> Purpose: attach Specification Protocol for Agent Runtime Contracts (SPARC) to a project

## PURPOSE

`INSTALL.md` is the directive for attaching Specification Protocol for Agent
Runtime Contracts (SPARC) to a project.

Installation means:

- identify the project structure and context;
- verify the Specification Protocol for Agent Runtime Contracts (SPARC) package
  is complete;
- create or verify project contract files;
- bind SPARC into existing agent configuration files;
- give SPARC authority inside its own contract-file scope;
- update the app structural map with the installed contract topology.

INSTALL does not define runtime execution, task orchestration, agent
coordination, locks, retries, schedulers, run loops, or autopipelines.

## INSTALLATION SCOPE

Specification Protocol for Agent Runtime Contracts (SPARC) governs project
contract files.

SPARC does not govern agent behavior outside SPARC contract handling.

Agent configuration files may define how an agent behaves.

PACT or another execution layer may define task execution and coordination.

## EXTERNAL BOOTSTRAP

Specification Protocol for Agent Runtime Contracts (SPARC) may be installed
directly or as a prerequisite of another system such as PACT.

An external installer, for example `INSTALL-PACT.md`, may:

1. reference the SPARC repository;
2. place the SPARC package under `/ai/`, normally `/ai/sparc_01.00/`;
3. run the SPARC installation procedure defined by this `INSTALL.md`;
4. continue with its own non-SPARC installation steps.

Running SPARC installation means following this file to attach SPARC contracts
to the target project. It does not mean executing PACT task coordination.

External bootstrap files must not rewrite static SPARC package files or
`templates/*.tpl.md` for the target project.

External bootstrap files must not add task execution, agent queues, locks,
retries, schedulers, or runtime state to SPARC contracts.

## REQUIRED SPARC PACKAGE

Before installing SPARC into a project, verify that the SPARC package contains:

```txt
README.md
SPARC.md
INSTALL.md

license/
  LICENSE.md
  COMMERCIAL-LICENSE.md
  NOTICE.md

templates/
  platform-logic.tpl.md
  app-map.tpl.md
  app-logic.tpl.md
  app-log.tpl.md
  design.tpl.md
```

If any required SPARC file is missing, installation must stop.

Do not create project contract files from an incomplete SPARC package.

`README.md`, `SPARC.md`, `INSTALL.md`, and files under `license/` are static
package files. During installation, read them and copy or reference them as
package files, but do not rewrite them for the target project.

## TARGET PROJECT STRUCTURE

Identify before installation:

- project root;
- SPARC package path, for example `/ai/sparc_01.00/`;
- documentation root, normally `/docs/`;
- application English name or stable English slug;
- existing project structure;
- existing behavior or logic documentation;
- platform-level rules, if any;
- design rules and design source, if any;
- project timezone;
- existing agent configuration files.

For projects with multiple applications, identify all app names and assign each
a stable English slug before installation. `PLATFORM-LOGIC.md` is created once.
The app-level contract structure is created separately for each app.

Recommended installed shape:

```txt
/ai/
  sparc_01.00/
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
      platform-logic.tpl.md
      app-log.tpl.md
      design.tpl.md

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
    design/
      DESIGN.md
```

Required installed files:

```txt
/docs/PLATFORM-LOGIC.md
/docs/<app-name-en>/map/MAP.md
/docs/<app-name-en>/logic/LOGIC.md
/docs/<app-name-en>/changes/LOG.md
/docs/<app-name-en>/design/DESIGN.md
```

Required installed folders:

```txt
/docs/<app-name-en>/changes/daily/
```

Daily log files are created only when request-level work is recorded.

## PREFLIGHT CHECK

Before creating or updating project contracts:

1. Verify the SPARC package is complete.
2. Verify `SPARC.md` is readable.
3. Verify all required templates are readable.
4. Choose the app folder name.
5. Choose or confirm the project timezone.
6. Identify existing agent configuration files.

Do not proceed if the SPARC package is incomplete.

## AGENT CONFIG BINDING

If the project contains agent configuration files, SPARC must be referenced
there.

Common agent configuration files include:

```txt
GEMINI.md
AGENTS.md
CLAUDE.md
CODEX.md
.cursor/rules/*
.windsurfrules
```

Add a SPARC contract binding block to each relevant agent configuration file.

Use the actual installed SPARC path and app folder name.

Recommended binding block:

```md
## SPARC CONTRACT BINDING

This project uses SPARC as its contract specification layer.

For SPARC file handling, template usage, contract updates, conflicts, gaps, and
boundaries, follow:

- `/ai/sparc_01.00/SPARC.md`
- `/ai/sparc_01.00/templates/*.tpl.md`

For current project truth, read:

- `/docs/PLATFORM-LOGIC.md`
- `/docs/<app-name-en>/map/MAP.md`
- `/docs/<app-name-en>/logic/LOGIC.md`
- `/docs/<app-name-en>/changes/LOG.md`
- `/docs/<app-name-en>/design/DESIGN.md`

Agent behavior files may define execution behavior.

They must not silently override SPARC contract files within SPARC scope.
```

Do not add PACT execution semantics to this binding.

## AUTHORITY BY SCOPE

SPARC has authority inside its own scope.

Agent configuration files govern agent behavior.

`SPARC.md` governs:

- SPARC file handling;
- template usage;
- project contract file structure;
- project contract file updates;
- contract conflict handling;
- contract gap handling;
- SPARC/PACT boundary rules.

Project contract files govern current project truth.

No layer should silently override another layer outside its scope.

Agent configuration must not silently override SPARC contracts.

SPARC contracts must not define task execution behavior.

## CONTRACT FILE CREATION

Use templates only when creating, updating, or validating live contract files.

Only generated live contract files in `/docs` are created, updated, or appended
during installation and project work.

Do not write project-specific truth into:

```txt
README.md
SPARC.md
INSTALL.md
license/LICENSE.md
license/COMMERCIAL-LICENSE.md
license/NOTICE.md
templates/*.tpl.md
```

```txt
templates/platform-logic.tpl.md -> /docs/PLATFORM-LOGIC.md
templates/app-map.tpl.md        -> /docs/<app-name-en>/map/MAP.md
templates/app-logic.tpl.md      -> /docs/<app-name-en>/logic/LOGIC.md
templates/app-log.tpl.md        -> /docs/<app-name-en>/changes/LOG.md
templates/app-log.tpl.md        -> /docs/<app-name-en>/changes/daily/YYYY-MM-DD.log.md
templates/design.tpl.md         -> /docs/<app-name-en>/design/DESIGN.md
```

Create `/docs/<app-name-en>/changes/daily/` as a folder.

Do not create `daily/YYYY-MM-DD.log.md` during initial installation unless the
owner explicitly requires installation history to be recorded.

If no platform rules are known yet, `PLATFORM-LOGIC.md` should still exist and
record the gap.

If no design rules are known yet, `DESIGN.md` should still exist and record the
gap.

## PROJECT MAP UPDATE

After SPARC installation, update the app structural map:

```txt
/docs/<app-name-en>/map/MAP.md
```

This is the app/project map, not a web SEO `sitemap.xml`.

The map must include the installed documentation contract structure.

The map must remain the app structural index and relevant project file
inventory.

Recommended map entry:

```md
### Documentation Contracts

- `/docs/PLATFORM-LOGIC.md` - global platform logic.
- `/docs/<app-name-en>/map/*` - app structural map layer.
- `/docs/<app-name-en>/logic/LOGIC.md` - app behavior contract.
- `/docs/<app-name-en>/changes/LOG.md` - accepted summary ledger.
- `/docs/<app-name-en>/changes/daily/*.log.md` - request-level daily work logs.
- `/docs/<app-name-en>/design/DESIGN.md` - design contract.
```

This update is part of installation bootstrap.

It must not create a daily request log.

It must not create an accepted change entry in `LOG.md`, unless the owner
explicitly requires installation history to be recorded.

## LOGGING RULE

SPARC installation does not create daily request logs by default.

Do not create:

```txt
/docs/<app-name-en>/changes/daily/YYYY-MM-DD.log.md
```

only because SPARC was installed.

Do not append to:

```txt
/docs/<app-name-en>/changes/LOG.md
```

only because SPARC was installed.

Logs are created for app-level project work, not for initial SPARC bootstrap,
unless explicitly requested by the owner.

## VALIDATION CHECKLIST

After installation, verify:

### Package Checks

- [ ] The SPARC package passed preflight.
- [ ] `SPARC.md` is readable.
- [ ] All required templates are readable.

### Contract Checks

- [ ] `/docs/PLATFORM-LOGIC.md` exists.
- [ ] `/docs/<app-name-en>/map/MAP.md` exists.
- [ ] `/docs/<app-name-en>/logic/LOGIC.md` exists.
- [ ] `/docs/<app-name-en>/changes/LOG.md` exists.
- [ ] `/docs/<app-name-en>/changes/daily/` exists.
- [ ] `/docs/<app-name-en>/design/DESIGN.md` exists.

### Map Checks

- [ ] `MAP.md` records the documentation contract topology.
- [ ] `MAP.md` does not enumerate individual daily log files.
- [ ] `MAP.md` uses `changes/daily/*.log.md` for daily logs.

### Agent Config Checks

- [ ] Existing relevant agent config files contain a SPARC contract binding.

### Log Checks

- [ ] No daily request log was created only for bootstrap.
- [ ] No `LOG.md` entry was created only for bootstrap unless explicitly requested.

### Content Checks

- [ ] Static package files were not rewritten for the target project.
- [ ] No template contains project-specific current truth.
- [ ] No live contract contains template-only writing rules.

If any required contract is missing, SPARC is not fully attached.

## FORBIDDEN CONTENT

INSTALL must not define:

```txt
task execution
request processing lifecycle
runTask
agent queues
locks
retries
schedulers
autopipelines
implementation workflow
agent coordination semantics
```

Those concerns belong to PACT or another execution system.
