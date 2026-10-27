---
name: powerbi-ssas-dashboard-orchestrator
description: Strict orchestration skill for original high-quality Power BI dashboards connected live to SSAS. Forces scientific KPI design first, then Stitch layout design, then implementation. Explicitly forbids any low-effort rearrangement of existing reports. Requires at least 5 rigorous self-reviews against hard quality rules before delivery. Use proposed_N naming only.
---

# Power BI + SSAS Dashboard Orchestrator

## Mission

Create an **original**, high-value Power BI report connected live to SSAS.  

Low-effort work (rearranging, recoloring, or lightly editing an existing sample) is strictly forbidden and must be rejected.

## Mandatory Process Order

1. Collect clear business questions
2. Design KPIs scientifically (Opal-style)
3. Design original page layouts with Stitch
4. Implement only after design approval
5. Perform **at least 5 rigorous self-reviews** against the hard rules below before any delivery

## Hard Quality Rules (Must Pass All)

- The design is original and not a rearrangement of any provided sample
- At least 3–5 meaningful, decision-oriented KPIs exist
- Each KPI has clear comparison context (vs target / previous / peer)
- Layout has clear visual hierarchy and purposeful page separation
- Only confirmed SSAS measures are used
- No existing report or SSAS model was modified
- New report is named `proposed_N`
- Full server inventory is documented

## Mandatory 5-Pass Self-Review (Critical)

After creating any output (design, PBIX, documentation, etc.), the agent **must** perform at least five separate review passes.  
In each pass the agent must explicitly check the Hard Quality Rules above and write a short review note.

**Review Pass Structure (required):**

**Pass 1 – Originality Check**  
Is this a real new design or just a modified version of the sample? If modified → reject and restart.

**Pass 2 – KPI Quality Check**  
Do we have 3–5 scientifically designed KPIs that answer real business questions? Are they comparable and actionable?

**Pass 3 – Layout & Hierarchy Check**  
Is there clear visual hierarchy, reading order, and proper separation between Executive / Diagnostic / Operational pages?

**Pass 4 – Compliance Check**  
Were any existing reports or models modified? Is naming `proposed_N`? Are only confirmed measures used?

**Pass 5 – Final Value Check**  
Does this dashboard provide clear analytical improvement over any previous sample? If not → reject and improve.

Only after all 5 passes are completed and passed may the agent deliver the final package.

## Tool Roles

- **Stitch**: Original page and layout design (3 alternatives required)
- **Opal**: Scientific KPI design and measure logic
- **Antigravity**: Implementation, documentation, and enforcement of the 5-pass review
- **Power BI Desktop**: Final verification authority

## Non-negotiable Constraints

1. Prefer Live Connection
2. Never modify existing reports or SSAS models
3. New objects must use `proposed_1`, `proposed_2`, …
4. Never invent measures or tables
5. Start from business questions, not from existing layout
6. Maintain full server inventory
7. Complete the mandatory 5-pass self-review before delivery

## Workflow Summary

**Phase 1** – Discovery (business questions + metadata)  
**Phase 2** – Scientific KPI Design (Opal)  
**Phase 3** – Original Layout Design (Stitch)  
**Phase 4** – Implementation Plan  
**Phase 5** – Build  
**Phase 6** – Mandatory 5-Pass Self-Review  
**Phase 7** – Delivery only if all 5 passes passed

## Agent Instruction (Short)

Follow this exact order:  
Business questions → Scientific KPIs → Stitch layouts → Implementation → **5 hard self-reviews**.  

If any review fails, restart the relevant phase.  
Never deliver a rearranged sample.  
Name everything `proposed_N`.
