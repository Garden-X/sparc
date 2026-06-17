## META

name: design.tpl.md
type: template
for: DESIGN.md
updated: 2026-06-17 03:55:16 UTC+00:00
version: 1.1

## USE

`DESIGN.md` is the live design-system contract for one application.

Recommended path:

```txt
<docs-root>/<app-name-en>/design/DESIGN.md
```

It gives humans and agents a persistent, structured understanding of the app's
visual identity, design tokens, rationale, component rules, and guardrails.

It is used when creating, updating, validating, or preserving UI, UX, layout,
visual, brand, accessibility, component, and interaction rules.

It does not override application or platform logic.

## RULES

`DESIGN.md` must describe current design truth only.

### Source Format

Primary source standard:

```txt
google-labs-code/design.md
https://github.com/google-labs-code/design.md
https://github.com/google-labs-code/design.md/blob/main/docs/spec.md
```

The `google-labs-code/design.md` format is the source for file structure.

Agents do not need to open external references for simple reading of an existing
`DESIGN.md`.

Agents should use the source links when creating, updating, or validating
`DESIGN.md`, or when the local design contract has gaps.

If an agent has an applicable design skill, that skill may stand in for opening
the external source unless the owner asks for source verification.

### File Structure

`DESIGN.md` has two layers:

1. YAML front matter with machine-readable design tokens.
2. Markdown body with human-readable rationale and guidance.

`DESIGN.md` is a structured exception to the default live contract format.

It may use YAML front matter and design-system sections before SPARC sections.

The YAML token layer is normative.

The markdown prose explains why tokens exist and how to apply them.

YAML front matter is optional only when no tokens are known yet. If tokens are
known, include it at the top of the file between `---` fences.

Token groups may include:

- `version`
- `name`
- `description`
- `theme`
- `colors`
- `typography`
- `rounded`
- `spacing`
- `components`

Token values should use:

- hex sRGB colors such as `"#1A1C1E"`;
- dimensions with `px`, `em`, or `rem`;
- token references such as `{colors.primary}`;
- typography objects with font family, size, weight, line height, and spacing.

### Markdown Section Order

Markdown sections should use this order when present:

1. `Overview` or `Brand & Style`
2. `Colors`
3. `Typography`
4. `Layout` or `Layout & Spacing`
5. `Elevation & Depth` or `Elevation`
6. `Shapes`
7. `Components`
8. `Do's and Don'ts`

`DESIGN.md` may also include SPARC sections after the design-system sections:

- `## META`
- `## PURPOSE`
- `## GAPS`

`## META` must include `theme`. If the project has only one theme, use the
canonical theme name, such as `default`.

### May Contain

`DESIGN.md` may contain:

- source reference and local overrides;
- brand personality and target audience;
- color palettes and semantic color roles;
- typography levels and rationale;
- layout, spacing, and responsive rules;
- elevation, depth, and hierarchy rules;
- shape and radius language;
- component tokens and variants;
- component usage rules;
- accessibility constraints;
- Do's and Don'ts;
- links to design chunks.

### Component Tokens

Component tokens may define:

- `backgroundColor`
- `textColor`
- `typography`
- `rounded`
- `padding`
- `size`
- `height`
- `width`

Component variants may be separate related keys, such as
`button-primary-hover` or `button-primary-active`.

### Validation

Unknown sections should be preserved.

Duplicate section headings are invalid.

Token references must resolve.

Color contrast should meet the project's accessibility target, normally WCAG AA
for standard UI text unless the owner defines a stricter rule.

When available, validate with:

```txt
npx @google/design.md lint DESIGN.md
```

The external lint command is optional. Do not require it for simple reading.

When comparing or exporting design tokens, the canonical CLI commands are:

```txt
npx @google/design.md diff DESIGN.md DESIGN-v2.md
npx @google/design.md export --format json-tailwind DESIGN.md
npx @google/design.md export --format css-tailwind DESIGN.md
npx @google/design.md export --format dtcg DESIGN.md
npx @google/design.md spec
```

On Windows, if the `.md` binary name conflicts with file associations, use the
`designmd` alias from a package script.

### Must Not Contain

`DESIGN.md` must not contain:

- business logic;
- permissions;
- persistence rules;
- folder maps;
- task lists;
- TODOs;
- runtime orchestration;
- agent coordination rules.

### Conflict Rules

If design conflicts with application behavior, `LOGIC.md` wins.

If design conflicts with platform rules, `PLATFORM-LOGIC.md` wins.

Unknown design decisions must be listed in `GAPS`.

## EXAMPLE

```md
---
version: alpha
name: Example App
description: Calm operational UI for structured work.
theme: default
colors:
  primary: "#1A1C1E"
  secondary: "#6C7278"
  tertiary: "#B8422E"
  neutral: "#F7F5F2"
typography:
  h1:
    fontFamily: Public Sans
    fontSize: 48px
    fontWeight: 600
    lineHeight: 1.1
  body-md:
    fontFamily: Public Sans
    fontSize: 16px
    fontWeight: 400
    lineHeight: 1.6
rounded:
  sm: 4px
  md: 8px
spacing:
  xs: 4px
  sm: 8px
  md: 16px
  lg: 32px
components:
  button-primary:
    backgroundColor: "{colors.tertiary}"
    textColor: "{colors.neutral}"
    rounded: "{rounded.sm}"
    padding: 12px
---

# DESIGN.md

## Overview

The app should feel calm, structured, and editorial, with strong hierarchy and
minimal decorative noise.

## Colors

- Primary is deep ink for headlines and core text.
- Secondary is slate for borders, captions, and metadata.
- Tertiary is the main action color.
- Neutral is the page foundation.

## Typography

- Headlines use Public Sans Semi-Bold.
- Body text uses Public Sans Regular for readability.

## Layout

- Use a responsive grid with stable spacing tokens.
- Keep dense operational surfaces readable before decorative.

## Elevation & Depth

- Prefer tonal layers and borders over heavy shadows.

## Shapes

- Use small radii for operational controls.
- Use larger radii only for intentionally expressive surfaces.

## Components

- Primary buttons use `components.button-primary`.
- Form fields must include labels, helper text when needed, and error states.

## Do's and Don'ts

- Do use the primary action color for the most important action.
- Do maintain accessible color contrast.
- Don't mix unrelated radius systems in the same view.
- Don't introduce one-off colors when a token exists.

## META

project: example-app
theme: default
updated: 2026-05-25 00:00:00 UTC+00:00
version: 1.0

## PURPOSE

Current design-system contract for UI and interaction decisions.

## GAPS

None.
```
