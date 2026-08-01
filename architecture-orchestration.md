# Design Tool Orchestration Architecture

**Date:** 2026-07-31
**Context:** Post-audit of the Annulment Advocate Assistant UI/UX design effort. The supervisor agent has 30 MCP servers and 10 skills installed but fails to orchestrate them effectively. This document proposes concrete changes to bridge the "installed vs. used" gap.

---

## Summary

The supervisor needs a **Design Orchestration Skill** — a SKILL.md that loads on design-related keywords and serves as the supervisor's "design playbook." It is not a general-purpose design skill (like `taste` or `ui-ux-pro-max`); it is a **bridge layer** that tells the supervisor which of the 10 skills and 30 MCPs to invoke in which situation, and in what sequence. Additionally, six targeted fixes close the specific gaps identified in the audit.

---

## Mode

**Cross-cutting concern design** — orchestrating an existing toolchain, not building new tools.

---

## Design Forces

| Force | Weight | Implication |
|---|---|---|
| Supervisor context budget | High | The orchestration skill must be lean — it is loaded into the already-crowded supervisor prompt |
| Supervisor is text-only | High | Visual review must be a structured process, not an afterthought |
| Supervisor delegates to junior agents | High | The orchestration skill must work when a subagent (not the supervisor directly) holds the design task |
| Skills auto-activate on keywords | Medium | We can control activation by adjusting skill descriptions |
| MCP servers are always-on or toggleable | Medium | The supervisor needs to know which are enabled (6 always-on, 24 toggleable) |
| 10 skills installed, 30 MCPs configured | High | There are too many tools for the supervisor to discover organically — curation is essential |
| Design work spans multiple tool categories | High | A landing page might use taste + ui-ux-pro-max + 21st + Open Design + Playwright + @observer |

---

## Approaches Considered

### Option A: Expand AGENTS.md / supervisor.md with design tool references

Add a "Design Toolchain Reference" section to the supervisor's system prompt listing every tool and when to use it.

- **Pros:** Simple, no new files, works immediately
- **Cons:** Bloating the supervisor prompt with 30+ entries the supervisor rarely needs. The supervisor already has 419 lines of instructions. Context is the scarcest resource. Would be pruned during compaction. Would not activate on design-specific keywords — the supervisor would need to remember it exists.

### Option B: Create a "Design Supervisor Skill" (SKILL.md)

A new skill at `~/.opencode/skills/design-orchestration/SKILL.md` that auto-activates on broad design keywords. It loads the full design playbook — decision trees, tool inventory, pipeline sequences, visual review loop — all in one file.

- **Pros:** Activates only when design work is detected (keyword-gated, stays out of context for non-design tasks). Can be comprehensive without bloating the supervisor. Can be updated independently of supervisor.md. Works within the existing skill framework — no new infrastructure needed.
- **Cons:** 1200+ line SKILL.md may exceed context budget. Subagents (junior-workers) may not auto-load skills. The supervisor still needs to know to spawn the right subagent type for visual work.

### Option C: Multiple small, single-purpose skills

Create separate skills: `design-visual-review`, `design-component-pipeline`, `design-system-generator`, etc. Each activates on narrower keywords.

- **Pros:** Very focused, minimal context waste
- **Cons:** No single "orchestrator" view. The supervisor would need to load 4+ skills to understand the full toolchain. Keyword activation would be unreliable — a task might trigger one skill but not another. Fragmentation makes the exact problem we're solving (supervisor doesn't know what's available).

### **Recommendation: Option B + targeted fixes to Option A**

A single **Design Orchestration Skill** as the primary mechanism, plus a lightweight reference in supervisor.md that points to it. Option C's fragmentation defeats the purpose. Option A alone bloats beyond reason. Option B gives us curation + activation + independence.

---

## Recommendation in Detail

### 1. Create the Design Orchestration Skill

**File:** `~/.opencode/skills/design-orchestration/SKILL.md`

This is the "bridge" file. It does not contain design principles (those belong to `taste`, `ui-ux-pro-max`, etc.) — it contains **routing logic**:

#### Structure

```
---
name: design-orchestration
description: |
  Design tool orchestrator for the supervisor. Activates on any design/UI task.
  Routes to the right skill + MCP for each design sub-task: components (21st),
  design systems (Open Design), anti-slop (taste), visual review (Playwright→@observer),
  accessibility (a11y + Lighthouse), animation (GSAP + motion-design), and more.
---

# Design Orchestration Playbook

## Quick Reference: What Tool When

| Situation | Tool | Why |
|---|---|---|
| Need a React/shadcn component | 21st MCP → search → retrieve → adapt | 35 tools for component marketplace |
| "Make it look beautiful" / "This looks generic" | Load taste skill FIRST | Anti-slop methodology, prevents AI defaults |
| Starting a new design system | Open Design MCP (enable it first) | 150+ design system packages, DESIGN.md contracts |
| Need color palette / font pairing / UX guidelines | ui-ux-pro-max skill → CLI search | 84 styles, 192 palettes, 74 fonts, 98 UX guidelines |
| After any UI code change | Visual Review Loop (see below) | Playwright screenshot → @observer analysis |
| Need accessibility audit | a11y MCP (enable it) + Lighthouse MCP | axe-core WCAG audit + Lighthouse perf/a11y/SEO |
| Need animation | motion-design skill (theory) + gsap skill (implementation) | Disney principles + GSAP API |
| Design system token work | design-system skill + Design Token Bridge MCP | Three-layer tokens + cross-format translation |
| Brand identity / logos | brand skill + design skill | 55 logo styles, brand guidelines |
| "Fix this button/input" | a11y-color-contrast MCP | WCAG contrast checking |
| Figma design handoff | Flowbite MCP (enable it) | Figma→code conversion |
| Animated React components | Magic UI MCP (enable it) | 150+ animated React components |
| Tailwind utilities/docs lookup | TailwindCSS MCP (enable it) | Makes agent Tailwind-literate |
| Design spec lookup | Southleft Design MCP (enable it) | 200+ design system entries |
| Screenshot → code | Apify MCP (enable it) | Screenshot to HTML/Tailwind/React |
| Visual regression testing | image-compare MCP (enable it) | Pixel-perfect diff comparison |
| Mathematical/programmatic animation | Manim MCP | Already enabled |

## Decision Flowcharts

### Starting Design Work
```
User asks for UI/design work
  ├── First time this project? → Open Design MCP: init DESIGN.md
  ├── New UI from scratch? → Load taste skill → set dials → load ui-ux-pro-max for keywords
  ├── Adding components? → 21st MCP pipeline (search → retrieve → adapt → install)
  ├── Improving existing UI? → Capture before → taste pre-flight audit → fix → capture after
  └── Any UI change complete? → Visual Review Loop (mandatory)
```

### Component Pipeline (21st.dev)
```
1. SEARCH: 21st MCP search tool with the component description
2. RETRIEVE: 21st MCP retrieve tool with the component ID from search results
3. ADAPT: Modify the retrieved component to match the project's design tokens (colors, fonts, spacing)
4. INSTALL: npx shadcn@latest add or manual file placement
   → NEVER stop at step 1. Always complete the pipeline.
```

### Visual Review Loop (mandatory for any UI change)
```
1. playwright screenshot (before change, if modifying existing UI)
2. Make code changes
3. Build/run/reload
4. playwright screenshot (after change)
5. @observer Mode F (comparison) with both screenshots
   Alternative: gemini-worker (multimodal) for visual analysis
6. If issues found → fix → loop back to step 3
7. Report: "Verified visually — N/N checks passed"
```

### Pre-Flight Quality Gates
After any design output, run these before declaring done:
1. a11y-color-contrast on primary/secondary colors
2. Lighthouse accessibility audit on the deployed/built page
3. taste pre-flight checklist (37 mechanical checks)
4. Visual review loop with @observer

## MCP Server Status

### Always-On (enabled, no action needed)
- 21st (component marketplace)
- a11y-color-contrast (WCAG contrast)
- Lighthouse (perf/a11y/SEO audit)
- Manim (animation rendering)
- Playwright (browser automation)
- OCR Pipeline (document processing)

### Toggleable (need `enabled: true` in opencode.json → restart OpenCode)
- a11y (WCAG axe-core audit)
- Flowbite (Tailwind components + Figma→code)
- Magic UI (animated React components)
- TailwindCSS (Tailwind utilities/docs)
- Design Token Bridge (cross-format tokens)
- WCAG (digital librarian)
- Image Compare (visual regression)
- Apify (screenshot→code)
- Southleft Design (design spec search)
- **Open Design** (design system CLI — 150+ packages)

### When to Enable Which Toggleable Server
- Starting a project with design system needs: Open Design + Design Token Bridge
- Need accessibility audit: a11y + WCAG
- Need animated components: Magic UI
- Need Tailwind reference: TailwindCSS
- Need Figma integration: Flowbite
- Need visual regression: Image Compare
- Need screenshot→code: Apify
- Need design spec reference: Southleft Design

## Skill Activation Keywords

The following skills auto-activate on keyword detection. Load them PROACTIVELY when relevant:

| Skill | Current Triggers | Sneak Paths (also load for) |
|---|---|---|
| taste | landing page, portfolio, redesign, frontend, design | "UI overhaul", "beautify", "make it look better", "improve the look", "polish", "pretty", "stunning", "eye-catching", "visual refresh", "retheme" |
| ui-ux-pro-max | design, UI, UX, styling, colors, fonts, layout, product type | (triggers are already broad — no change needed) |
| design-system | design tokens, design system, CSS variables, spacing scale, typography scale | "token architecture", "theme configuration" |
| motion-design | animation, motion, transition, micro-interaction, loading | "animated", "smooth", "dynamic" |
| gsap | GSAP, tween, timeline, ScrollTrigger, animate | "scroll animation", "parallax", "pin" |
```

#### Key Design Decisions for the Skill

- **It references other skills by name** but does not duplicate their content. It tells the supervisor *which* skill to load, not what that skill contains.
- **It tracks MCP server status** (always-on vs. toggleable) so the supervisor knows whether a tool is available without checking config.
- **It encodes full pipelines**, not just tool names. The 21st.dev pipeline says "step 1→2→3→4, never stop at step 1."
- **It includes the visual review loop as a standard process**, not an afterthought.
- **It augments the taste skill's keyword triggers** to catch "beautify" and other non-technical design requests.

### 2. Lightweight supervisor.md Addition

Add to `~/.config/opencode/agent/supervisor.md`, in the Visual Verification section (around line 130), before the "@observer" table:

```markdown
### Design Toolchain

When the user asks for any UI, design, frontend, styling, layout, or visual work:
- **Load the `design-orchestration` skill FIRST.** It is your design playbook — it tells you which skills and MCPs to invoke for each design sub-task.
- **Never reach for default shadcn/Tailwind without running the design pipeline.** The pipeline is: taste (anti-slop) → ui-ux-pro-max (design keywords) → 21st (components) → Open Design (system) → visual review.
- **After any UI-affecting code change, run the Visual Review Loop** (capture → @observer → fix → repeat). Never ship UI you haven't seen.
```

This is ~5 lines and ensures the supervisor always loads the orchestrator when design work is detected. It stays in context after compaction since it's part of the supervisor's system prompt.

### 3. Expand taste Skill Keyword Triggers

The taste skill at `/Users/jacobgruber/.opencode/skills/taste/SKILL.md` currently activates on:
```
landing page, portfolio, redesign, frontend, design
```

This misses common non-technical design requests. Update the `description` frontmatter (line 3 of the file) to:

```yaml
description: Anti-slop frontend skill for landing pages, portfolios, and redesigns. The agent reads the brief, infers the right design direction, and ships interfaces that do not look templated. Real design systems when applicable, audit-first on redesigns, strict pre-flight check. Activates on: landing page, portfolio, redesign, frontend, design, UI overhaul, beautify, make it look better, improve the UI, polish, pretty, stunning, eye-catching, visual refresh, retheme, rebrand, visual upgrade.
```

OpenCode's skill loader uses substring matching on the description. Adding these keywords ensures taste loads when the user says "make this page prettier" or "do a visual refresh."

**File to modify:** `/Users/jacobgruber/.opencode/skills/taste/SKILL.md`, line 3

### 4. Fix the 21st.dev Pipeline

The 21st.dev MCP has 35 tools. The four-step pipeline (search → retrieve → adapt → install) stopped at step 1 because the supervisor didn't know steps 2-4 existed. Two fixes:

**A) Add to the Design Orchestration Skill** (already done in the skill design above — the "Component Pipeline" section explicitly lists all 4 steps).

**B) Add a reference to the supervisor's AGENTS.md** (already done in point #2 above — "Never reach for default shadcn/Tailwind without running the design pipeline").

**C) Practical fix — what the 21st pipeline actually looks like:**

```
Step 1: SEARCH — use the 21st search tool with a component description
  Example: "a pricing card with three tiers, monthly/annual toggle, feature list, CTA button"
  
Step 2: RETRIEVE — use the 21st retrieve tool with the component ID from search results
  This returns the full component code (React/shadcn), not just a preview
  
Step 3: ADAPT — modify the retrieved code to match project tokens
  - Replace colors with project's CSS variables or Tailwind config
  - Replace font families with project's font config
  - Adjust spacing to match project's spacing scale
  - Add any project-specific props or variants
  
Step 4: INSTALL — place the component in the project
  - For shadcn projects: add to components/ui/ directory
  - For other projects: add to the appropriate components directory
  - Ensure all dependencies are in package.json
```

The supervisor (or the design orchestration skill) should enforce that ALL four steps complete before declaring the component task done.

### 5. Enable Key Toggleable MCP Servers by Default

Six MCP servers are always-on. Ten more are configured but disabled. Of those ten, five are high-value for design work and should be enabled by default:

| Server | Reason to Enable |
|---|---|
| **Open Design** | Foundation for all design system work. 150+ packages, DESIGN.md contracts. Currently disabled. |
| **TailwindCSS** | Makes the agent Tailwind-literate. Prevents hallucinated classes. Low overhead. |
| **a11y** | Only zero-config way to audit generated UI for WCAG violations. Complements Lighthouse. |
| **Magic UI** | Only animation-aware component source. 150+ animated React components. |
| **Design Token Bridge** | Eliminates manual token translation between formats. |

**File to modify:** `/Users/jacobgruber/.config/opencode/opencode.json`

Change these entries from `"enabled": false` to `"enabled": true`:
- `open-design` (line 100)
- `tailwindcss` (line 307)
- `a11y` (line 263)
- `magic-ui` (line 302)
- `design-token-bridge` (line 282)

These five have zero disk impact (already installed) and minimal runtime overhead. They expand the supervisor's available tool surface without any configuration burden.

### 6. Automate the Visual Review Loop

The Playwright → @observer pattern was discovered late in the Annulments project and proved incredibly effective (8+ issues found in one pass). It needs to be:

**A) Encoded in the Design Orchestration Skill** (already designed above — see "Visual Review Loop" section).

**B) Added as a post-commit hook pattern.** After any commit that changes UI files (`.tsx`, `.css`, `.jsx`), the supervisor should run the visual review loop before declaring the batch complete. This is a discipline change, not a code change — it goes in the supervisor's workflow section.

**C) The specific tool chain:**

```
For web UIs:
  1. playwright_browser_navigate(url="http://localhost:PORT")
  2. playwright_browser_snapshot() → accessibility tree (text, no image needed)
  3. playwright_browser_take_screenshot(filename="before.png") → screenshot
  4. Make code changes
  5. Reload: playwright_browser_navigate(url="http://localhost:PORT")
  6. playwright_browser_take_screenshot(filename="after.png") → screenshot
  7. Spawn @observer in Mode F (UI Comparison) with both screenshots
     OR: spawn gemini-worker ("Analyze this UI screenshot for design issues...")
  8. Parse issues, fix, loop

For native macOS apps:
  1. macos-use capture
  2. @observer analyze
  3. Fix, recapture, loop
```

**D) Add to supervisor.md's "After Work Complete" checklist** (around line 356):

```markdown
- [ ] Visual review loop completed (if UI was changed): capture → @observer → fix → loop → "N/N checks passed"
```

### 7. Open Design MCP: Activation and Initialization

Open Design MCP is configured at `/Users/jacobgruber/.config/opencode/opencode.json` (lines 94-106) but disabled. It runs a daemon at `/Users/jacobgruber/Projects/Design/open-design/apps/daemon/dist/cli.js` with `OD_DATA_DIR` pointing to `.od/`.

Once enabled, the supervisor should:

```
First use in a project:
  1. Enable the Open Design MCP server
  2. Run: od init (creates DESIGN.md for the project)
  3. DESIGN.md becomes the "brand contract" — all subsequent UI respects it
  
Ongoing:
  - od design-system → generates design tokens
  - od component → generates components against DESIGN.md
  - od prototype → generates prototypes
```

The Design Orchestration Skill should include this initialization flow as a "First Time Setup" section.

However, there's a critical permission issue: `opencode.json` line 324 has `"open-design_*": "deny"`. This must be changed to `"allow"` for the supervisor to use Open Design tools.

**File to modify:** `/Users/jacobgruber/.config/opencode/opencode.json`, line 324: change `"deny"` to `"allow"`.

### 8. Subagent Design Tool Awareness

When the supervisor spawns a junior-worker or junior-architect to do design work, the subagent does NOT inherit the supervisor's loaded skills. The supervisor must:

- **Tell the subagent to load the relevant skill** in the subagent prompt: "Before writing any code, use the `skill` tool to load `taste` and `ui-ux-pro-max`."
- **Include the design orchestration context** in the subagent prompt: "Available design tools: 21st MCP (component marketplace), Playwright (screenshots), a11y-color-contrast (WCAG checks). Use them."
- **Pre-capture visual state** if the subagent needs it: The supervisor captures screenshots with Playwright, analyzes with @observer, and includes the text analysis in the subagent prompt. Subagents (except debuggers/workers) cannot access macos-use; mules cannot access visual tools at all.

Add to supervisor.md's Subagent Prompt Checklist (around line 256), a new item:

```markdown
- [ ] For design/UI tasks: tell the subagent to load `taste`, `ui-ux-pro-max`, and `design-orchestration` skills. List available design MCPs in the prompt. Pre-capture any visual state the subagent needs.
```

---

## Risks & Mitigations

| Risk | Severity | Mitigation |
|---|---|---|
| Design Orchestration Skill exceeds context budget (could be 1200+ lines like taste) | Medium | Keep the orchestration skill to routing logic only — don't duplicate design principles. If it grows, split into a "quick reference" top section + "detailed" appendix. |
| Subagent doesn't load the orchestration skill | Medium | Add to supervisor.md's subagent checklist. Test with a junior-worker: "Build a pricing page" → verify it uses taste + 21st. |
| Enabling 5 more MCP servers increases startup time or memory | Low | All are local, zero-disk-impact. Magic UI is the heaviest (150+ component index). Monitor with `ps aux | grep mcp` after restart. |
| Open Design MCP fails to initialize (daemon dependency) | Medium | Test with `od --version` first. The daemon at `apps/daemon/dist/cli.js` requires Node 24 + pnpm. If the build is stale, run `pnpm --filter @open-design/daemon build` in the open-design repo. |
| `open-design_*: deny` blocks the supervisor despite MCP being enabled | High | Change the permission BEFORE enabling the MCP. Order: 1) change deny→allow, 2) enable MCP, 3) restart OpenCode. |
| taste skill keyword expansion causes false activations | Low | "beautify", "polish", "pretty" are specific enough. Monitor. If taste loads during a backend-only task, add context checks in taste's Section 0. |
| Visual review loop adds latency to every UI change | Medium | Use @observer Mode G (Quick State) by default, only escalate to Mode F (comparison) for final review. For trivial CSS changes (single color value), skip the loop. The design orchestration skill should define thresholds. |

---

## Implementation Order

| Priority | Change | File(s) | Effort |
|---|---|---|---|
| **P1** | Create Design Orchestration Skill | New file: `~/.opencode/skills/design-orchestration/SKILL.md` | Medium (write ~800-line SKILL.md) |
| **P1** | Expand taste skill triggers | `~/.opencode/skills/taste/SKILL.md` line 3 | Trivial (one-line edit) |
| **P1** | Fix `open-design_*` permission | `~/.config/opencode/opencode.json` line 324 | Trivial (one-word edit) |
| **P1** | Enable 5 key MCP servers | `~/.config/opencode/opencode.json` (5 entries) | Trivial (5 boolean flips) |
| **P2** | Add design toolchain reference to supervisor.md | `~/.config/opencode/agent/supervisor.md` | Small (~5 lines) |
| **P2** | Add visual review step to "After Work Complete" checklist | `~/.config/opencode/agent/supervisor.md` | Trivial (1 checkbox) |
| **P2** | Add design subagent prompt checklist item | `~/.config/opencode/agent/supervisor.md` | Trivial (1 line) |
| **P3** | Test the full pipeline end-to-end | Annulments or any test project | Medium (manual testing) |

---

## What Success Looks Like

After all changes are implemented, the following should happen automatically:

1. User says: "Make this page prettier" → supervisor loads `design-orchestration` skill (keyword match on "prettier" from expanded taste triggers) → loads `taste` skill → runs design read → sets dials

2. User says: "Add a pricing component" → supervisor loads `design-orchestration` → runs 21st.dev pipeline (search → retrieve → adapt → install) → completes all 4 steps

3. Any UI code change → supervisor runs visual review loop: Playwright screenshot → @observer analysis → fix issues → recapture → report "Verified visually — N/N checks passed"

4. User says: "Build a design system for my SaaS" → supervisor loads `design-orchestration` → enables Open Design MCP → runs `od init` → generates DESIGN.md → generates tokens → generates components

5. No more blind shipping of UI that "looks bad" because the supervisor never saw it.
