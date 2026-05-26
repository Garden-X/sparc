## META

name: platform-logic.tpl.md
version: 1.0
type: template
for: PLATFORM-LOGIC.md

## USE

`PLATFORM-LOGIC.md` is the live contract for platform-wide rules.

Recommended path:

```txt
/docs/PLATFORM-LOGIC.md
```

It is used when a rule applies across applications or overrides an individual
application contract.

For projects with multiple applications, `PLATFORM-LOGIC.md` is shared and
created once. App-level contracts defer to it on platform concerns.

`PLATFORM-LOGIC.md` describes global invariants.

It does not describe one app's internal behavior unless that behavior is a
platform rule.

## RULES

`PLATFORM-LOGIC.md` must describe platform-level truth only.

### May Contain

It may contain:

- global invariants;
- security rules;
- authentication rules;
- billing rules;
- shared data rules;
- API rules;
- persistence rules;
- cross-application constraints.

### Must Not Contain

It must not contain:

- app-specific feature details;
- folder maps;
- one-off implementation notes;
- task lists;
- TODOs;
- runtime orchestration;
- agent coordination rules.

Platform rules override app-level `LOGIC.md` when there is a conflict.

Conflicts or unknown precedence must be listed in `GAPS`.

## EXAMPLE

```md
# PLATFORM-LOGIC.md

## META

platform: example-platform
version: 1.0
last_updated: 2026-05-25

## PURPOSE

Global platform behavior and invariants.

## CURRENT

### Invariants

- Authentication is centralized.
- Application APIs must not trust client-provided user identifiers.
- Billing events must be recorded before user-visible entitlement changes.

### Overrides

Platform authentication rules override app-level permission shortcuts.

## GAPS

None.
```
