---
name: powerbi-ssas-dashboard-orchestrator
description: End-to-end orchestration for high-quality Power BI dashboards connected live to SSAS (Tabular or Multidimensional). Designed for Google Antigravity, Cursor, Claude Code and similar AI coding agents. Enforces safe practices: never modify existing models or reports, use proposed_N naming for any new objects.
---

# Power BI + SSAS Dashboard Orchestrator

## Mission

Produce an attractive, maintainable, performant Power BI report that connects **live** to an existing SSAS model without breaking enterprise governance, security, or single source of truth. Treat every AI-generated design, DAX, theme or asset as a draft that must be verified in the target Power BI Desktop version against the real SSAS model.

## Tool Roles

| Tool | Role | Rules |
|------|------|-------|
| **Google Stitch** | Design exploration only | Produce layouts, hierarchy, spacing, typography, color tokens and a `DESIGN.md`. Never treat the output as a finished Power BI report or claim direct HTML/CSS → native visual conversion. |
| **Google Antigravity** | Implementation workspace | Draft theme JSON, SVG assets, documentation, test checklists and PBIP scaffolding when supported. Keep all changes reviewable. |
| **Google Opal** | Optional short-lived experiments only | Use only while available. Export every useful prompt/spec to ordinary Markdown before the experiment ends. Never make Opal a required dependency. |
| **Power BI Desktop** | Authoritative implementation & visual QA | Final report must open, render and be saved in the exact target Desktop build. |
| **SSAS / Tabular Editor / DAX Studio** | Model metadata & performance | Use only tools approved and installed in the user’s environment. Never assume credentials or direct write access. |

## Non-negotiable Constraints

1. Identify the target environment first: **Power BI Report Server (PBIRS)** or **Power BI Service**. Confirm the exact Desktop build compatible with the target. Do not assume Service features work on PBIRS.
2. Identify the SSAS model type: **Tabular** or **Multidimensional (Cube)**, plus exact server / database / model name and connection mode.
3. Prefer **Live Connection** for any governed SSAS model unless the user explicitly approves another architecture.
4. Multidimensional Live Connection → measures must already exist in the cube; report-level measures are not supported. Tabular Live Connection → verify report-measure support in the installed Desktop version before generating any DAX.
5. **Never invent** tables, columns, hierarchies, measures, relationships, calculation groups or KPI definitions. Base every expression only on supplied metadata and confirmed business definitions.
6. Preserve SSAS security (roles, dimension security, RLS). Do not request passwords, export sensitive data or bypass access controls.
7. **Never modify any existing report, dashboard or SSAS model.** Previous assets must remain completely untouched. Produce only proposed changes and a reviewable diff; obtain explicit approval before any edit or deployment.
8. If a new SSAS model or new dashboard/report must be created, always name it `proposed_1`, `proposed_2`, `proposed_3`, … Never overwrite or alter production objects.
9. Treat custom SVG and third-party visuals as optional enhancements, not the default. Prefer native visuals; test rendering, accessibility, export and PBIRS compatibility.
10. Never place essential labels, KPI values or filters only inside a static background image. Backgrounds may contain decorative framing only; data and interactive controls must be real Power BI visuals.
11. Optimize for business readability and query performance before decorative effects. Avoid visual density, excessive slicers and gratuitous animations.
12. Always maintain a living inventory of: server names, server structure/topology, tables/cubes/models on each server, summary of the data they contain, and clear guidance on where to look for specific data or metadata.

## Workflow Selector

| User intent | Start at |
|-------------|----------|
| New dashboard or page design | Phase 1 → Phase 3 (Stitch) |
| Inventory / audit of existing SSAS | Phase 1 → Phase 2 |
| Implementation of an already-approved design | Phase 4 |
| DAX / SVG / theme work only | Phase 5 |
| Final build & QA | Phase 6 |
| Handoff / documentation | Phase 7 |

Always run Phase 1 first if any of the Non-negotiable items are unknown.

## Phase 1 — Intake and Discovery

Ask only for information that blocks a safe design:

- Target environment (PBIRS / Service) and exact Power BI Desktop version
- SSAS type (Tabular / Multidimensional)
- **Server inventory**: exact server names, topology, list of tables/cubes/models on each server, summary of data contents, and where to look for specific data or metadata
- Audience, decisions supported, primary questions, required pages, language / RTL needs
- Official KPI / measure definitions
- Available metadata (model diagram, field list, DMV output, sanitized field-pane screenshots)
- Required filters, drill-through paths, RLS roles, export needs, expected data volume
- Brand colors / fonts and 1–2 visual references (if any)

If metadata is missing, produce a clearly labeled discovery checklist and a non-production design mockup. **Never generate production DAX against guessed field names.**

## Phase 2 — Model and Compatibility Audit

Create / update `docs/model-inventory.md` containing:

- Full server inventory (names, structure, tables/cubes, data summary, lookup guidance)
- SSAS type, connection mode, environment and version constraints
- Confirmed measures, dimensions, hierarchies, display folders, format strings
- KPI definitions, target/actual logic, time intelligence, expected filter behavior
- Known limitations and open questions
- Explicit statement that no existing reports or models will be modified; any new objects will use `proposed_N` naming

Decide for every requested calculation whether it belongs in SSAS or can safely be a report-level measure. For Multidimensional Live Connection, route new calculations to the model owner.

## Phase 3 — Design with Stitch

Request **three materially different** alternatives (not just color variants):

1. Executive overview
2. Analytical / diagnostic layout
3. Operational monitoring layout

Evaluate against:

- Clear reading order and one primary message per page
- KPI cards that show value + comparison/target + context (only when available)
- Restrained palette, consistent spacing, readable typography, sufficient contrast
- Realistic space for slicers, filters, cross-filtering, drill-through
- Mobile / large-screen and Persian/RTL correctness when required
- Feasibility with real Power BI visuals

Export the chosen design’s `DESIGN.md`, screenshots and available assets. Record colors, typography, spacing and component rules in `design/design-spec.md`. Use Stitch output strictly as a visual specification for rebuilding in Power BI.

### Stitch prompt template

“Design a high-fidelity enterprise BI dashboard concept for [audience] that supports [decisions]. The target is a Power BI report connected live to SSAS [Tabular/Multidimensional], so use only layouts that can be rebuilt with real Power BI visuals. Provide three materially different page layouts, a restrained professional design system, clear hierarchy, accessible contrast, consistent spacing, and realistic space for slicers and KPI context. Do not invent data values or business KPIs. Clearly distinguish decorative elements from data-bearing visuals. Support Persian RTL if requested. Export the selected design’s DESIGN.md and document colors, typography, spacing, component states, and layout rules.”

## Phase 4 — Implementation Plan

Create `docs/implementation-plan.md` that maps every design component to:

- Preferred native Power BI visual (or explicitly justified custom/SVG)
- Confirmed SSAS measure / dimension fields
- Filters, interactions, tooltip / drill-through behavior and formatting
- PBIRS / Service compatibility status
- Acceptance test

Generate a Power BI theme JSON only from confirmed design tokens. Validate JSON syntax and schema, then import into the target Desktop build. Keep theme, SVG assets, prompts and docs under version control. Never edit PBIP internals blindly.

## Phase 5 — DAX and Visual Engineering

For every proposed measure:

1. State business definition and expected filter context
2. Reference only confirmed model objects
3. Declare whether it is a report measure or requires an SSAS change
4. Check time intelligence, totals, blank/zero handling, currency/percentage formatting and RLS implications
5. Prefer dimension-column filters; avoid broad `FILTER(ALL(FactTable), …)` patterns
6. Test with representative slices and compare against a trusted report or model query

For SVG measures (use only when native visuals cannot meet the need):

- Return valid SVG with explicit dimensions and proper encoding
- Escape dynamic text safely
- Verify conditional formatting, blanks, accessibility alternatives, export behavior and target Desktop / PBIRS compatibility

## Phase 6 — Build and Validate in Power BI Desktop

Implementation is incomplete until the report is opened and checked in the exact target Power BI Desktop version.

Test checklist:

- Connection and query behavior against SSAS
- KPI values against trusted references
- Every slicer, cross-highlight, drill-through, tooltip and navigation action
- RLS with authorized test identities
- Persian text, RTL, fonts, number separators, dates and negative values (if applicable)
- Rendering at intended resolution and in the report viewer / browser
- Export to PDF / PowerPoint / Excel if required
- Performance under representative filter combinations
- No missing assets, broken theme, unsupported visuals or misleading totals

Record results in `docs/qa-checklist.md` and list any unverified items explicitly.

## Phase 7 — Deliverables

Deliver:

- `design/design-spec.md`
- `docs/model-inventory.md` (must include full server inventory + lookup guidance)
- `docs/implementation-plan.md`
- Validated `theme.json`
- `docs/qa-checklist.md`
- DAX / SVG / Tabular Editor scripts only when justified and based on confirmed metadata
- Concise handoff stating: what was actually built, what was tested, remaining risks, exact manual steps required in Power BI Desktop, and explicit confirmation that no existing reports or models were modified (any new objects use `proposed_N` naming)

## Antigravity prompt template

“Act as a senior Power BI report engineer. Read `design/design-spec.md` and `docs/model-inventory.md`. First report compatibility blockers and missing metadata; do not guess field names. Produce an implementation map from design components to Power BI visuals and confirmed SSAS fields. Draft a theme JSON and any justified assets, plus a QA checklist. Never modify any existing reports or SSAS models; if new objects are required, name them `proposed_1`, `proposed_2`, etc. Do not deploy or claim HTML-to-Power-BI conversion. Keep changes reviewable and verify JSON/project files before reporting completion.”

## Gotchas & Best Practices

- **Live Connection constraints**: No calculated columns or new tables can be created in Power BI Desktop. All transformations must live in the SSAS model or as report-level measures (Tabular only, when supported).
- **Background alignment**: Keep decorative frames, cards and navigation at 1920×1080 (16:9) when exporting SVG backgrounds; never put data labels inside the static image.
- **DAX performance on SSAS**: Prefer filters on dimension columns. Avoid scanning entire fact tables with `FILTER(ALL(...))`.
- **Server inventory is mandatory**: Every handoff must include up-to-date server names, structure, tables/data contents and lookup locations.

## Definition of Done

A dashboard is done only when:

- Visual design is coherent and readable
- Every data-bearing element uses confirmed model objects
- Key figures reconcile to trusted results
- Interactions, security and performance have been tested
- The report opens successfully in the target Power BI environment
- Full server inventory is documented
- It is confirmed that no existing reports or models were modified (new objects, if any, follow the `proposed_N` naming convention)
