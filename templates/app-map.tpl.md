## META

name: app-map.tpl.md
type: template
for: MAP.md
updated: 2026-06-17 03:55:16 UTC+00:00
version: 1.1

## USE

`MAP.md` is the live structural index, first structural entry point, and
relevant project file inventory for one application.

Recommended path:

```txt
<docs-root>/<app-name-en>/map/MAP.md
```

It is used to understand the app map layer, project file inventory, important
structural zones, entrypoints, attached parts, and unmapped areas.

`MAP.md` describes where things are.

It does not describe what the application should do.

## RULES

`MAP.md` is the canonical structural index of the app.

It must contain:

- the structure of the map layer itself;
- all split map files;
- the complete relevant project file inventory;
- attached parts such as modules, plugins, integrations, extension points,
  route systems, UI subsystems, service layers, and data layers;
- high-level responsibility zones;
- known structural gaps.

Relevant project file inventory means all files an agent or engineer needs to
know to safely work with the codebase.

Relevant files include:

- source files;
- configuration files;
- documentation files;
- contract files;
- manually maintained scripts;
- important public assets.

Files that are generated, fetched, or managed automatically are generally not
part of the relevant inventory.

### Excluded From Inventory

`MAP.md` must not enumerate:

- dependencies such as `node_modules/`;
- generated build output such as `dist/`, `.next/`, or `build/`;
- caches;
- runtime logs;
- `.git/`;
- temporary files.

### Content Restrictions

`MAP.md` must not contain:

- business logic;
- feature rules;
- user flows;
- permissions;
- platform invariants;
- change history;
- task lists;
- TODOs;
- implementation plans;
- runtime orchestration;
- agent coordination rules.

Every important path should have a clear responsibility.

If an important area exists but is not mapped, list it in `GAPS`.

`MAP.md` may link to `LOGIC.md` when behavior is relevant, but must not
duplicate application logic.

### Attached Parts Rule

`MAP.md` is the first structural entry point for attached parts.

Attached parts are app components that should be discoverable before an agent
edits the project. Examples include modules, plugins, integrations, extension
points, route systems, UI subsystems, service layers, and data layers.

If no attached parts exist, `MAP.md` should say so explicitly.

If an attached part is compact, list it directly in `MAP.md`.

If an attached part becomes large, detailed, or independently maintained, split
its structural details into a named map-layer file and list that file in
`MAP.md`.

### Split Rule

`MAP.md` may be split into additional map files when a structural area becomes
too large, too detailed, or semantically independent.

Additional map files must be placed inside:

```txt
<docs-root>/<app-name-en>/map/
```

Each additional map file must be named by the meaning of the structure it
describes.

Examples:

- `routes.md`
- `models.md`
- `services.md`
- `ui.md`
- `api.md`
- `database.md`
- `auth.md`
- `integrations.md`
- `docs.md`

Do not name split files by sequence unless order is meaningful.

Bad:

- `map-01.md`
- `part-2.md`
- `misc.md`

Good:

- `routes.md`
- `controllers.md`
- `billing.md`
- `editor-flow.md`

Split map files expand detail.

The main `MAP.md` remains the structural index.

`MAP.md` must still list every split map file.

### Map Layer Inventory Rule

`MAP.md` must list all map-layer files in the `Map Structure` section.

The `Map Structure` section is the canonical place where split map files are
listed.

Map-layer files should not be duplicated with full detail in the general
project file inventory.

### Log Inventory Rule

`MAP.md` must list the change log structure, but must not enumerate every daily
log file.

Use:

```txt
changes/daily/*.log.md
```

Do not list:

```txt
changes/daily/2026-05-25.log.md
changes/daily/2026-05-26.log.md
changes/daily/2026-05-27.log.md
```

Daily logs grow over time. `MAP.md` must reference them by pattern.

## EXAMPLE

```md
# MAP.md

## META

type: app structural map
app: example-app
updated: 2026-05-25 00:00:00 UTC+00:00
version: 1.0

## PURPOSE

Canonical structural map of the application.

This file describes the app map layer and provides the complete relevant
project file inventory.

Detailed structural sections may be split into additional map files when
needed.

## CURRENT

### Map Structure

This section lists all files that belong to the app map layer.

- `map/MAP.md` - main structural map and relevant project file inventory.
- `map/routes.md` - route structure and page entrypoints.
- `map/models.md` - models, schemas, DTOs, and validation files.
- `map/services.md` - services, adapters, and external integrations.
- `map/ui.md` - view and component structure.

### Attached Parts

This section lists app modules, plugins, integrations, extension points, and
other independently meaningful structural parts.

- `routes` - page and route entrypoint structure; details in `map/routes.md`.
- `services` - service and integration boundaries; details in
  `map/services.md`.
- `ui` - view and component structure; details in `map/ui.md`.

### Project File Inventory

This section lists relevant project files.

#### Root

- `package.json`
- `README.md`
- `next.config.ts`
- `tsconfig.json`

#### App

- `app/page.tsx`
- `app/layout.tsx`
- `app/api/chat/route.ts`

#### Source

- `src/models/user.ts`
- `src/models/message.ts`
- `src/services/chat-service.ts`
- `src/views/chat-panel.tsx`

#### Documentation Contracts

- `/ai/docs/PLATFORM-LOGIC.md`
- `/ai/docs/example-app/map/*`
- `/ai/docs/example-app/logic/LOGIC.md`
- `/ai/docs/example-app/schema/SCHEMA.md`
- `/ai/docs/example-app/changes/LOG.md`
- `/ai/docs/example-app/changes/daily/*.log.md`
- `/ai/docs/example-app/design/DESIGN.md`

### Responsibility Zones

- `app/` contains application routes and framework entrypoints.
- `src/models/` contains data contracts and validation.
- `src/services/` contains integration boundaries and side effects.
- `src/views/` contains presentation components.
- `/ai/docs/example-app/map/` contains app structural maps.
- `/ai/docs/example-app/schema/SCHEMA.md` contains app data-shape truth.

### Excluded From Inventory

- `node_modules/`
- `.git/`
- `.next/`
- `dist/`
- `build/`
- `coverage/`
- cache and temporary files

## GAPS

None.
```
