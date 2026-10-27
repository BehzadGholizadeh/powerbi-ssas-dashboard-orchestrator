---
name: powerbi-ssas-dashboard-orchestrator
description: End-to-end orchestration for high-quality Power BI dashboards connected live to SSAS (Tabular or Multidimensional). Uses Google Stitch for page/layout design, Google Opal for scientific KPI design and micro-pipelines, and Antigravity for implementation. Strictly forbids low-effort copying of existing reports. Enforces proposed_N naming and never-modify-existing-assets.
---

# Power BI + SSAS Dashboard Orchestrator

## Mission

Produce an original, high-value Power BI report connected **live** to an existing SSAS model.  

The process must combine:
- **Google Stitch** → professional page and visual hierarchy design
- **Google Opal** → scientific KPI design, measure logic, and short prompt chains
- **Antigravity** → implementation, theme, documentation and validation

Simply rearranging or lightly editing an existing sample report is **strictly forbidden** and counts as a failed deliverable.

## Core Tool Orchestration

| Tool | Primary Responsibility | How it must be used |
|------|------------------------|---------------------|
| **Google Stitch** | Page & Layout Design | Generate 3 distinct high-fidelity layout alternatives (Executive, Diagnostic, Operational). Export DESIGN.md + color/typography tokens. Never treat Stitch output as final Power BI visuals. |
| **Google Opal** | Scientific KPI Design & Micro-pipelines | Design meaningful indicators using KPI science (decision-focused, comparable, actionable). Generate report-level DAX ideas, SVG concepts, and short prompt chains. Export everything to Markdown. |
| **Google Antigravity** | Implementation & Validation | Turn the approved design + KPI specs into theme.json, documentation, implementation plan and QA checklist. |
| **Power BI Desktop** | Final Authority | The only place where the real report is built and verified. |
| **SSAS tools** | Metadata only | Read-only discovery of existing measures and structures. |

## Non-negotiable Constraints

1. Prefer **Live Connection**. Never change the existing SSAS model or any production report.
2. Any new report/dashboard must be named `proposed_1`, `proposed_2`, `proposed_3`...
3. Never invent tables, columns or measures that do not exist in the model.
4. **No low-effort work**: Copying, recoloring or lightly rearranging a sample PBIX is forbidden.
5. Every dashboard must start from clear **business questions**, not from an existing layout.
6. At least 3–5 scientifically designed KPIs are required.
7. Maintain full server inventory (names, structure, tables, data summary, lookup guidance).

## Scientific KPI Design Principles (Opal must follow)

When designing indicators, Opal (or the agent) must apply these principles:

- **Decision-oriented**: Each KPI must answer a specific business decision.
- **Comparable**: Always include context (vs target, vs previous period, vs peer group, vs benchmark).
- **Actionable**: The user should know what to do when the KPI is red/amber/green.
- **Clean**: Prefer simple, well-known calculations over complex nested logic when possible.
- **Trustworthy**: Only use confirmed measures from the SSAS model. Clearly mark any report-level calculation.
- **Hierarchical**: Separate Strategy KPIs (top row) from Diagnostic KPIs and Operational metrics.

Good KPI examples:
- Activation Rate % + gap vs target
- Opportunity Loss (value of non-activated promotions)
- Margin Impact of Promotion
- Stores with Zero Sales after activation
- Regional Underperformance Index

## Workflow

### Phase 1 — Discovery (Mandatory)
Collect:
- Business questions the dashboard must answer (3–7 questions)
- SSAS type, server name, database/model
- List of existing measures (or field pane screenshot)
- Audience and decisions
- Any brand guidelines

If a sample report is given → treat it only as a source of confirmed measures. Explicitly declare that a completely new design will be created.

### Phase 2 — Scientific KPI Design (Opal)
Using Opal (or equivalent reasoning):
1. Map each business question to candidate KPIs
2. Apply the Scientific KPI Design Principles above
3. Propose 5–8 strong KPI candidates with:
   - Business definition
   - Required existing measures
   - Comparison logic
   - Suggested visual type
4. Select the best 3–5 KPIs for the dashboard
5. Export the KPI specification to Markdown

### Phase 3 — Page Design with Stitch
Prompt Stitch to create **three materially different** layouts based on the approved KPIs:

1. Executive / Strategic
2. Diagnostic / Root-cause
3. Operational / Action list

Stitch output must include clear hierarchy, proper spacing, and realistic room for slicers.  
Save as `design/design-spec.md` + tokens.

### Phase 4 — Implementation Plan
Map every visual to:
- Confirmed SSAS measure/field
- Visual type
- Interactions
- Acceptance criteria linked to original business questions

### Phase 5 — Build & Validate
Implement only after design and KPIs are approved.  
Final report must be opened and checked in Power BI Desktop.

## Stitch Prompt Template (use this)

“Design three high-fidelity enterprise Power BI dashboard layouts (Executive, Diagnostic, Operational) for [audience].  
The dashboard will connect live to SSAS and must answer these business questions: [list questions].  
Primary KPIs to feature: [list the scientifically designed KPIs].  
Requirements:
- Clear visual hierarchy and reading order
- Strong KPI cards with comparison context
- Realistic space for filters and slicers
- Professional, restrained design system
- Support for Persian/RTL if needed
Do not invent data. Distinguish decorative elements from real visuals.  
Export DESIGN.md with colors, typography, spacing and component rules.”

## Opal Prompt Direction (KPI Science)

“Act as a KPI designer applying scientific dashboard principles.  
Business questions: [list].  
Available confirmed measures: [list].  
Design 5–8 strong candidate KPIs. For each provide:
- Clear business definition
- Which existing measures are used
- Comparison logic (target / previous / peer)
- Why this KPI drives a decision
- Recommended visual
Then recommend the best 3–5 KPIs for an executive + diagnostic dashboard.”

## Definition of Done

- Original design (not a rearrangement of any sample)
- KPIs designed with scientific principles and tied to business questions
- Stitch used for layout exploration
- Opal (or equivalent) used for KPI design
- Only confirmed SSAS measures used
- New report named `proposed_N`
- No existing reports or models modified
- Full documentation delivered (design-spec, model-inventory, implementation-plan, qa-checklist)

## Agent Instruction (short version)

First collect business questions and confirmed measures.  
Then use scientific KPI design (Opal-style) to define meaningful indicators.  
Then use Stitch to design original page layouts around those KPIs.  
Never clone or lightly edit an existing report.  
Name the result `proposed_N`.
