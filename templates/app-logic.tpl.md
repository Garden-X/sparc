## META

name: app-logic.tpl.md
version: 1.1
type: template
for: LOGIC.md

## USE

`LOGIC.md` is the live behavior contract of one application.

Recommended path:

```txt
<docs-root>/<app-name-en>/logic/LOGIC.md
```

It is used to understand application rules, flows, permissions, invariants, and
edge cases.

`LOGIC.md` describes what the application does.

It does not describe where files are located.

## RULES

`LOGIC.md` must describe current application behavior only.

### May Contain

It may contain:

- domain rules;
- core behavior;
- user flows;
- permissions;
- validation rules;
- data lifecycle rules;
- invariants;
- edge cases;
- links to structural files when needed.

### Must Not Contain

It must not contain:

- folder maps;
- module ownership maps;
- implementation diary entries;
- task lists;
- TODOs;
- runtime orchestration;
- agent coordination rules;
- historical change logs.

If a behavior is unclear, list it in `GAPS` instead of inventing it.

If a platform rule overrides app behavior, reference
`<docs-root>/PLATFORM-LOGIC.md`.

## EXAMPLE

```md
# LOGIC.md

## META

project: example-app
version: 1.0
last_updated: 2026-05-25

## PURPOSE

Canonical application behavior contract.

## CURRENT

### Core Behavior

Users can create, edit, archive, and restore notes.

### Invariants

- Archived notes are hidden from the default list.
- Restoring a note returns it to the default list.
- Deleting a note requires explicit confirmation.

### Flow: Create Note

1. User creates a draft note.
2. The application assigns an identifier.
3. The note remains editable until archived or deleted.

## GAPS

None.
```
