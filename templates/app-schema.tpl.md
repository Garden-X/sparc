## META

name: app-schema.tpl.md
type: template
for: SCHEMA.ts
updated: 2026-06-17 23:39:24 UTC+00:00
version: 2.0

## USE

`SCHEMA.ts` is the live typed data-shape contract of one application.

Recommended path:

```txt
<docs-root>/<app-name-en>/schema/SCHEMA.ts
```

It is used to understand application entities, tables, fields, enums,
constraints, indexes, relations, cross-application references, public dataset
views, schema compatibility gaps, and runtime schema artifacts.

`SCHEMA.ts` describes how application data is shaped. It does not describe
application behavior or where files are located.

`SCHEMA.ts` replaces `SCHEMA.md` as the canonical SPARC schema contract. Do not
keep `SCHEMA.md` as a parallel authority. If an older binding has `SCHEMA.md`,
treat it as legacy material to migrate into `SCHEMA.ts`.

## RULES

`SCHEMA.ts` must be a self-contained, side-effect-free TypeScript data
contract.

It must export:

- a `SparcSchemaContract` type;
- a `schema` object using `as const satisfies SparcSchemaContract`.

It may export supporting TypeScript types used by `SparcSchemaContract`.

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

- imports from runtime, database, framework, generated, or application modules;
- side effects, executable startup work, DB clients, migrations, or runtime
  orchestration;
- user flows;
- feature behavior;
- permission policy except where permission fields are part of stored shape;
- folder maps;
- implementation diary entries;
- task lists;
- TODOs;
- agent coordination rules.

If a data-shape decision is unclear, list it in `gaps` instead of inventing it.

If behavior in `LOGIC.md` implies data shape not represented in `SCHEMA.ts`,
record the conflict or update the responsible live contract with owner
approval.

If a platform rule overrides app data shape, reference
`<docs-root>/PLATFORM-LOGIC.md`.

Runtime schema files implement or mirror the data contract. They do not replace
the SPARC `SCHEMA.ts` contract.

## EXAMPLE

```ts
export type SparcSchemaScalar =
  | "uuid"
  | "string"
  | "text"
  | "integer"
  | "number"
  | "boolean"
  | "datetime"
  | "date"
  | "json"
  | "enum"
  | "reference"
  | "unknown";

export type SparcSchemaField = {
  type: SparcSchemaScalar;
  required: boolean;
  description?: string;
  enumValues?: readonly string[];
  references?: {
    entity: string;
    field?: string;
  };
  default?: string;
  generated?: boolean;
  primaryKey?: boolean;
  unique?: boolean;
};

export type SparcSchemaEntity = {
  storage?: string;
  description?: string;
  fields: Record<string, SparcSchemaField>;
  constraints?: readonly string[];
  indexes?: readonly string[];
};

export type SparcDatasetView = {
  description?: string;
  fields: readonly string[];
};

export type SparcSchemaContract = {
  meta: {
    type: "app schema contract";
    project: string;
    updated: string;
    version: string;
  };
  purpose: string;
  runtimeArtifacts?: readonly {
    path: string;
    description?: string;
  }[];
  entities: Record<string, SparcSchemaEntity>;
  datasetViews?: Record<string, SparcDatasetView>;
  crossApplicationReferences?: readonly string[];
  compatibility?: readonly string[];
  gaps: readonly string[];
};

export const schema = {
  meta: {
    type: "app schema contract",
    project: "example-app",
    updated: "2026-05-25 00:00:00 UTC+00:00",
    version: "1.0",
  },
  purpose: "Canonical typed data-shape contract for the application.",
  runtimeArtifacts: [
    {
      path: "src/db/schema.ts",
      description: "ORM table declarations.",
    },
    {
      path: "src/dataset-schema.ts",
      description: "Public compact and full dataset views.",
    },
  ],
  entities: {
    note: {
      storage: "notes",
      fields: {
        id: {
          type: "uuid",
          required: true,
          primaryKey: true,
          description: "Primary key.",
        },
        owner_id: {
          type: "uuid",
          required: true,
          references: {
            entity: "user",
            field: "id",
          },
          description: "User that owns the note.",
        },
        title: {
          type: "string",
          required: false,
          description: "Optional display title.",
        },
        body: {
          type: "text",
          required: true,
          description: "Main note content.",
        },
        status: {
          type: "enum",
          required: true,
          enumValues: ["draft", "active", "archived"],
        },
        created_at: {
          type: "datetime",
          required: true,
          generated: true,
        },
        updated_at: {
          type: "datetime",
          required: true,
          generated: true,
        },
      },
      constraints: ["primary key: id"],
      indexes: ["owner_id", "status"],
    },
  },
  datasetViews: {
    compact: {
      fields: ["id", "title", "status"],
    },
    full: {
      fields: ["id", "title", "status", "body", "created_at", "updated_at"],
    },
  },
  gaps: [],
} as const satisfies SparcSchemaContract;
```
