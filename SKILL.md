---
name: powerbi-ssas-dashboard-orchestrator
description: End-to-end orchestration for high-quality Power BI dashboards connected live to SSAS (Tabular or Multidimensional). Designed for Google Antigravity, Cursor, Claude Code and similar AI coding agents. Enforces safe practices, real design thinking, meaningful KPIs, and never-modify-existing-assets rule with proposed_N naming.
---

# Power BI + SSAS Dashboard Orchestrator

## Mission

Produce an attractive, maintainable, performant Power BI report that connects **live** to an existing SSAS model without breaking enterprise governance, security, or single source of truth.  

**Critical quality rule:** Every deliverable must demonstrate real design thinking and analytical value. Simply rearranging, recoloring, or lightly editing an existing sample report is **forbidden** and considered a failed output.

Treat every AI-generated design, DAX, theme or asset as a draft that must be verified in the target Power BI Desktop version against the real SSAS model.

## Tool Roles

| Tool | Role | Rules |
|------|------|-------|
| **Google Stitch** | Design exploration only | Produce layouts, hierarchy, spacing, typography, color tokens and a `DESIGN.md`. Never treat the output as a finished Power BI report or claim direct HTML/CSS → native visual conversion. |
| **Google Antigravity** | Implementation workspace | Draft theme JSON, SVG assets, documentation, test checklists and PBIP scaffolding when supported. Keep all changes reviewable. |
| **Google Opal** | Optional short-lived experiments only | Use only while available. Export every useful prompt/spec to ordinary Markdown. Never make Opal a required dependency. |
| **Power BI Desktop** | Authoritative implementation & visual QA | Final report must open, render and be saved in the exact target Desktop build. |
| **SSAS / Tabular Editor / DAX Studio** | Model metadata & performance | Use only tools approved and installed in the user’s environment. Never assume credentials or direct write access. |

## Non-negotiable Constraints

1. Identify the target environment first: **Power BI Report Server (PBIRS)** or **Power BI Service**. Confirm the exact Desktop build compatible with the target.
2. Identify the SSAS model type: **Tabular** or **Multidimensional (Cube)**, plus exact server / database / model name and connection mode.
3. Prefer **Live Connection** for any governed SSAS model unless the user explicitly approves another architecture.
4. Multidimensional Live Connection → measures must already exist in the cube; report-level measures are not supported. Tabular Live Connection → verify report-measure support before generating any DAX.
5. **Never invent** tables, columns, hierarchies, measures, relationships, calculation groups or KPI definitions. Base every expression only on supplied metadata and confirmed business definitions.
6. Preserve SSAS security (roles, dimension security, RLS). Do not request passwords or bypass access controls.
7. **Never modify any existing report, dashboard or SSAS model.** Previous assets must remain completely untouched. Produce only proposed changes; obtain explicit approval before any edit or deployment.
8. If a new SSAS model or new dashboard/report must be created, always name it `proposed_1`, `proposed_2`, `proposed_3`, … Never overwrite production objects.
9. Treat custom SVG and third-party visuals as optional. Prefer native visuals.
10. Never place essential labels, KPI values or filters only inside a static background image.
11. Optimize for business readability and query performance before decorative effects.
12. Always maintain a living inventory of: server names, structure/topology, tables/cubes/models, data summary, and lookup guidance.

### Quality & Anti-Low-Effort Rules (Mandatory)

13. **No copy-paste or light editing of existing reports.** Taking an existing PBIX/sample and only rearranging visuals, changing colors, or adding 1–2 cards is strictly forbidden. This is considered a failed deliverable.
14. Every new dashboard must start from **business questions**, not from an existing layout. If the user provides a sample, treat it only as a reference for data/measures, never as a template to clone.
15. At least **3–5 meaningful KPIs** with clear business definitions must be designed or selected. KPIs must answer real decisions (e.g. opportunity loss, activation gap, margin impact, regional underperformance).
16. Layout must show clear visual hierarchy, reading order, and purposeful page separation (Executive / Diagnostic / Operational). Random placement of cards is not acceptable.
17. If the agent cannot produce a design that is clearly superior in analytical value and usability to any provided sample, it must stop and ask for more business context instead of delivering a weak version.

## Workflow Selector

| User intent | Start at |
|-------------|----------|
| New dashboard or page design | Phase 1 → Phase 3 |
| Inventory / audit of existing SSAS | Phase 1 → Phase 2 |
| Implementation of an already-approved design | Phase 4 |
| DAX / SVG / theme work only | Phase 5 |
| Final build & QA | Phase 6 |
| Handoff / documentation | Phase 7 |

Always run Phase 1 first if any Non-negotiable item is unknown.

## Phase 1 — Intake and Discovery

**Mandatory first step:** Collect the primary business questions the dashboard must answer. Without clear questions, do not proceed to design.

Ask for:

- Target environment (PBIRS / Service) and exact Power BI Desktop version
- SSAS type (Tabular / Multidimensional)
- **Server inventory**: server names, topology, tables/cubes, data summary, lookup guidance
- Audience and the **3–7 key decisions / questions** the dashboard must support
- Official KPI / measure definitions (if they exist)
- Available metadata (field list, DMV, screenshots of field pane)
- Required filters, drill-through, RLS, export needs
- Brand guidelines (if any)

If a sample report is provided, explicitly state:  
“Sample will be used only as a source of confirmed measures and data shapes. A completely new design will be created.”

If metadata or business questions are missing → produce a discovery checklist and stop. Do not generate a production report.

## Phase 2 — Model and Compatibility Audit

Create / update `docs/model-inventory.md` with:

- Full server inventory
- SSAS type, connection mode, version constraints
- Confirmed measures, dimensions, hierarchies, format strings
- Mapping of business questions → candidate measures
- Known limitations
- Explicit statement that no existing reports/models will be modified; new objects use `proposed_N`

## Phase 3 — Design (Real Design Thinking Required)

Do **not** start from any existing report layout.

Request or produce **three materially different** alternatives:

1. Executive / Strategic overview
2. Analytical / Diagnostic (root-cause focused)
3. Operational / Action-oriented

Each alternative must include:

- Clear primary message per page
- 3–5 high-value KPI cards with comparison (vs target / previous period / peer)
- Logical visual hierarchy and reading order
- Purposeful use of space (not crowded, not sparse)
- Realistic filter placement

Document the chosen design in `design/design-spec.md`.

**Rejection criteria:** Any design that is essentially a re-skin or rearrangement of a provided sample must be rejected and redone.

## Phase 4 — Implementation Plan

Create `docs/implementation-plan.md` mapping every component to:

- Native visual type (preferred)
- Confirmed SSAS fields / measures
- Interactions and filters
- Compatibility notes
- Acceptance criteria tied to the original business questions

## Phase 5 — DAX and Visual Engineering

For every proposed measure:

1. Business definition and the decision it supports
2. Only confirmed model objects
3. Report-level vs model-level decision
4. Blank/zero, totals, formatting, RLS checks
5. Performance-conscious patterns

## Phase 6 — Build and Validate

Implementation is incomplete until opened and tested in the target Power BI Desktop version.

Must verify:

- Connection and correct numbers against trusted sources
- Every interaction
- That the dashboard answers the original business questions better than any previous sample
- No existing assets were modified

## Phase 7 — Deliverables

- `design/design-spec.md`
- `docs/model-inventory.md`
- `docs/implementation-plan.md`
- Validated `theme.json`
- `docs/qa-checklist.md`
- Any justified DAX/SVG
- Handoff note confirming:  
  – No existing reports/models were modified  
  – New objects use `proposed_N`  
  – Design is original and answers the stated business questions

## Antigravity / Agent Prompt Template

“Act as a senior Power BI report engineer specializing in SSAS Live Connection.  
First confirm business questions and available metadata.  
Never clone or lightly edit an existing report.  
Create an original design with clear hierarchy and meaningful KPIs that answer the business questions.  
Use only confirmed measures.  
Name any new report `proposed_N`.  
Produce design-spec, model-inventory, implementation-plan and QA checklist.  
Stop and ask for more context if you cannot deliver clear analytical improvement over any provided sample.”

## Definition of Done

A dashboard is done only when:

- It is an original design (not a rearrangement of a sample)
- It answers the stated business questions with clear, meaningful KPIs
- All data-bearing elements use confirmed model objects
- Key figures reconcile to trusted results
- Interactions, security and performance are tested
- No existing reports or models were modified
- Full server inventory is documented
- Naming follows `proposed_N` convention
