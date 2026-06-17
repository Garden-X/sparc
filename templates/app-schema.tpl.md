## META

name: app-schema.tpl.md
type: template
for: SCHEMA.md
updated: 2026-06-17 03:55:16 UTC+00:00
version: 1.0

## USE

`SCHEMA.md` is the live data-shape contract of one application.

Recommended path:

```txt
<docs-root>/<app-name-en>/schema/SCHEMA.md
```

It is used to understand application entities, tables, fields, enums,
constraints, indexes, relations, cross-application references, public dataset
views, and schema compatibility gaps.

`SCHEMA.md` describes how application data is shaped.

It does not describe application behavior or where files are located.

## RULES

`SCHEMA.md` must describe current data shape only.

### May Contain

It may contain:

- entity, table, collection, document, or resource definitions;
- field names, types, nullability, defaults, and generated values;
- enum values and value meanings when they affect stored data;
- primary keys, unique constraints, indexes, and relation rules;
- cross-application references, including owner system and stored reference
  shape;
- public dataset schema views such as compact and full views when the project
  exposes them;
- schema version and compatibility notes;
- links to runtime schema files such as `schema.ts`, `dataset-schema.ts`,
  migrations, validation schemas, DTOs, or API schema files;
- known data-shape gaps.

### Must Not Contain

It must not contain:

- user flows;
- feature behavior;
- permission policy except where permission fields are part of stored shape;
- folder maps;
- implementation diary entries;
- task lists;
- TODOs;
- runtime orchestration;
- agent coordination rules.

If a data-shape decision is unclear, list it in `GAPS` instead of inventing it.

If behavior in `LOGIC.md` implies data shape not represented in `SCHEMA.md`,
record the conflict or update the responsible live contract with owner
approval.

If a platform rule overrides app data shape, reference
`<docs-root>/PLATFORM-LOGIC.md`.

Runtime schema files implement or mirror the data contract. They do not replace
`SCHEMA.md` as the human-readable SPARC schema contract.

## EXAMPLE

```md
# SCHEMA.md

## META

type: app schema contract
project: example-app
updated: 2026-05-25 00:00:00 UTC+00:00
version: 1.0

## PURPOSE

Canonical data-shape contract for the application.

## CURRENT

### Runtime Schema Artifacts

- `src/db/schema.ts` - ORM table declarations.
- `src/dataset-schema.ts` - public compact and full dataset views.

### Entity: note

Storage: `notes`

Fields:

| Field | Type | Required | Notes |
|---|---|---|---|
| `id` | uuid | yes | Primary key. |
| `owner_id` | uuid | yes | User that owns the note. |
| `title` | string | no | Optional display title. |
| `body` | text | yes | Main note content. |
| `status` | enum | yes | `draft`, `active`, or `archived`. |
| `created_at` | datetime | yes | Generated on create. |
| `updated_at` | datetime | yes | Updated on write. |

Constraints and indexes:

- Primary key: `id`.
- Index: `owner_id`.
- Index: `status`.

### Dataset Views

Compact fields:

- `id`
- `title`
- `status`

Full fields:

- all compact fields
- `body`
- `created_at`
- `updated_at`

## GAPS

None.
```
