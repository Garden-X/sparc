## META

name: app-log.tpl.md
version: 1.1
type: template
for: LOG.md and daily/YYYY-MM-DD.log.md

## USE

`LOG.md` is the append-only accepted summary ledger of meaningful accepted
changes for one application.

Daily logs record request-level work.
`daily/YYYY-MM-DD.log.md` is the request-level daily work log.

Recommended paths:

```txt
<docs-root>/<app-name-en>/changes/LOG.md
<docs-root>/<app-name-en>/changes/daily/YYYY-MM-DD.log.md
```

`LOG.md` is used to understand what accepted changes became part of the project.

`daily/YYYY-MM-DD.log.md` is used to understand request-level work for one day.

Neither log layer is the current source of application logic.

Do not confuse either log layer with `LOGIC.md`.

## RULES

The app change log has two layers:

1. `LOG.md` - accepted summary ledger.
2. `daily/YYYY-MM-DD.log.md` - request-level daily work log.

Both layers must be append-only.

### LOG.md Rules

`LOG.md` entries inside `## CURRENT` may contain only:

- date;
- accepted change summary.

`LOG.md` summary entries must use this date-based format:

```md
### YYYY-MM-DD

- Change summary.
```

No actor, time, request, verification, or related-log fields belong in `LOG.md`.
Those details belong in the daily log.

### Daily Log Rules

Daily entries must contain:

- actor that wrote the entry;
- time;
- original request or accepted change trigger;
- changed content summary;
- old documented truth;
- new documented truth;
- verification result;
- follow-up.

Do not add extra per-entry fields unless the owner explicitly extends the log
standard.

Daily log entries must use this format:

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

The date value is mandatory in the daily filename:

```txt
daily/YYYY-MM-DD.log.md
```

Dates and daily log filenames must use the project timezone. If the project
timezone is not declared, use UTC. The timezone should be declared in the
relevant `META` section.

Write `None` when there is no old behavior or follow-up.

Write `Not run` when verification was not run.

The body fields are the canonical request-level log data.

`Actor` records the agent, human, script, or tool that wrote the entry.

`Time` records when the change was made.

`Request` records the owner request, accepted decision, or change trigger.

`Changed` summarizes what was changed.

`Old` records the previous documented truth or `None` for new behavior.

`New` records the new documented truth after the change.

`Verified` records the check that proves the change or `Not run`.

`Follow-up` records remaining work or `None`.

### Forbidden in Both Layers

Neither log layer may contain:

- current canonical logic that belongs in `LOGIC.md`;
- current structure that belongs in `MAP.md`;
- platform invariants that belong in `PLATFORM-LOGIC.md`;
- task queues;
- TODOs;
- runtime orchestration;
- agent coordination rules.

Do not edit old change entries except to fix formatting or broken links.

### Write Sequence

When a change alters current truth:

1. Update the responsible live contract.
2. Append a request-level entry to the current daily log.
3. When the change is accepted, promote a concise summary into `LOG.md`.

## EXAMPLE

```md
# LOG.md

## META

project: example-app
version: 1.0
last_updated: 2026-05-25

## PURPOSE

Append-only history of meaningful accepted app changes.

## CURRENT

### 2026-05-25

- Notes can now be archived, restored, or deleted with confirmation.

## GAPS

None.
```

```md
# 2026-05-25.log.md

## META

project: example-app
date: 2026-05-25
timezone: Europe/Warsaw
type: daily request log

## PURPOSE

Request-level work log for one day.

## CURRENT

### Request: add reversible note removal

- Actor: Codex
- Time: 13:40:33
- Request: add reversible note removal.
- Changed: added archive and restore behavior for notes.
- Old: notes could be deleted only.
- New: notes can be archived, restored, or deleted with confirmation.
- Verified: `LOGIC.md` updated with archive and restore invariants.
- Follow-up: None.

## GAPS

None.
```
