# Orchestration Architecture — How Design Tools Are Wired

How the supervisor's orchestration machinery routes design work through specialized subagents, with MCP permission layering keeping the supervisor's context clean.

## The Architecture

```
┌─────────────────────────────────────────┐
│              SUPERVISOR                  │
│     (DeepSeek V4 Pro, text-only)         │
│                                          │
│  Owns: project mgmt, delegation          │
│  Design MCPs: DENIED (21st, open-design) │
│  Visual MCPs: KEPT (playwright, devtools)│
│                                          │
│  "Is this design?" → @designer           │
└──────────────┬──────────────────────────┘
               │ spawns via Task tool
               ▼
┌─────────────────────────────────────────┐
│              @DESIGNER                   │
│        (Grok 4.5, multimodal)            │
│                                          │
│  Owns: ALL UI/UX/design work            │
│  MCPs: playwright, chrome-devtools,      │
│        21st, open-design, a11y-contrast  │
│  Skills: loads taste, ui-styling,        │
│          design-system, motion-design     │
│  Pattern: capture → analyze → edit →     │
│           recapture → report              │
│                                          │
│  Spawns: @designer-mule for subtasks     │
└──────────────┬──────────────────────────┘
               │ spawns via Task tool
               ▼
┌─────────────────────────────────────────┐
│           @DESIGNER-MULE                 │
│        (Grok 4.3, leaf node)             │
│                                          │
│  Owns: bounded design subtasks           │
│  Same MCPs as designer                  │
│  task: deny (cannot spawn further)       │
└─────────────────────────────────────────┘
```

## Permission Layering

Design-specific MCPs use a three-layer gate (following the existing `open-design_*` pattern):

| Layer | File | twenty-first_* | open-design_* | a11y-color-contrast_* |
|---|---|---|---|---|
| Global | opencode.json `permission` | deny | deny | allow |
| Supervisor | opencode.json `agent.supervisor.permission` | deny | deny | — |
| Designer | agents/designer.md frontmatter | allow | allow | allow |
| Designer-mule | agents/designer-mule.md frontmatter | allow | allow | allow |

`playwright_*` and `chrome-devtools_*` remain globally allowed — many agents use them.

## The Surgical Hook

A single line in `agent/supervisor.md` Pre-Implementation Triage table:

> UI/UX design, visual styling, component design, wireframes, mockups, layout, animation, accessibility styling → Spawn `designer`

No other supervisor.md changes needed for routing. The supervisor still uses playwright for non-design screenshots.

## Tool Count Safety

Grok has a 200-tool limit. The designer only sees MCPs explicitly allowed in its markdown:
- playwright (~20) + chrome-devtools (~30) + 21st (~35) + a11y-contrast (~3) + open-design (~15) + ~12 builtins = **~110 tools**
- Denied MCPs (elevenlabs, firecrawl, railway, screenpipe, etc.) never appear in registry
- Well under 200. Safe.

## Agent Specs

| Agent | Model | Steps | Color | Spawn? |
|---|---|---|---|---|
| designer | xai/grok-4.5 | 45 | #EC4899 (pink) | Yes — can spawn designer-mule |
| designer-mule | xai/grok-4.3 | 30 | #F472B6 (light pink) | No — task: deny |

## Files Involved

| File | Action |
|---|---|
| `~/.config/opencode/agents/designer.md` | Create |
| `~/.config/opencode/agents/designer-mule.md` | Create |
| `~/.config/opencode/opencode.json` | Add twenty-first MCP, a11y-color-contrast MCP, enable open-design, add permission blocks |
| `~/.config/opencode/agent/supervisor.md` | Add triage row + toolbox row + visual verification reference |
