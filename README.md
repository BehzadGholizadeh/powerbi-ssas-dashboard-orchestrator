# Power BI + SSAS Dashboard Orchestrator

**AI Agent Skill** for designing and implementing high-quality Power BI reports that connect **live** to SQL Server Analysis Services (SSAS) — Tabular or Multidimensional.

Compatible with:
- Google Antigravity
- Cursor
- Claude Code
- GitHub Copilot / other agents that support the open `SKILL.md` format

## Key Safety Rules

- **Never modify** existing reports or SSAS models
- Any new object must be named `proposed_1`, `proposed_2`, `proposed_3`, …
- Always document server inventory (names, structure, tables, data contents, lookup guidance)
- Prefer Live Connection and native Power BI visuals
- Treat every AI output as a draft that must be verified in Power BI Desktop

## Installation

### Google Antigravity

**Project scope (recommended):**
```bash
mkdir -p .agents/skills/powerbi-ssas-dashboard-orchestrator
curl -o .agents/skills/powerbi-ssas-dashboard-orchestrator/SKILL.md \
  https://raw.githubusercontent.com/BehzadGholizadeh/powerbi-ssas-dashboard-orchestrator/main/SKILL.md
```

**Global scope:**
```bash
mkdir -p ~/.gemini/config/skills/powerbi-ssas-dashboard-orchestrator
# or
mkdir -p ~/.gemini/antigravity/skills/powerbi-ssas-dashboard-orchestrator
# then copy SKILL.md into the folder
```

### Other agents
Copy the `SKILL.md` file into the skills directory used by your agent (usually `.agents/skills/`, `.claude/skills/`, etc.).

## How to use

Just describe your dashboard need. Example prompts:

- “Use the powerbi-ssas-dashboard-orchestrator skill and design an executive dashboard for our SSAS Tabular model”
- “Create a model inventory and implementation plan for a live-connected Power BI report”

The skill will guide the agent through discovery, design (Stitch), implementation planning, DAX/SVG work, and final QA checklist.

## License

MIT – free to use, modify and share.
