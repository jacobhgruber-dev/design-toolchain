# Designer Subagent — Architecture Blueprint

## Summary

Add two new subagents to the opencode agent roster — `designer` (Grok 4.5, spawn-capable) and `designer-mule` (Grok 4.3, leaf) — scoped to ALL UI/UX/design work. The `designer` is a peer to `grok-worker` in the agent hierarchy: a high-capacity subagent with design-specific system prompt, MCP access (playwright, 21st, chrome-devtools, open-design, a11y tools), and subdelegation capability. A surgical one-line hook in the supervisor's Pre-Implementation Triage table routes all design work to it. The supervisor retains existing visual tools for quick orientation checks but delegates substantive design work.

## Mode

Scoping + cross-cutting concern design. Adding a new agent role to an existing multi-tier agent system.

---

## Design Forces

1. **Model tier clarity** — The `designer` uses Grok (xAI), which is a separate provider tier from junior (DeepSeek), mid (Claude Sonnet), and senior (Claude Opus). It does NOT fit the junior/mid/senior naming convention. It follows the `grok-worker` addon pattern: a named agent with its own model tier.
2. **Supervisor permission model** — MCP tool access is per-agent via YAML frontmatter `permission` blocks. The supervisor's block is in `opencode.json`. Subagent blocks are in their `.md` files. The supervisor can deny itself tools to ensure they're exclusively delegated.
3. **Existing visual infrastructure** — The supervisor already has playwright, chrome-devtools, and @observer for visual tasks. The `designer` must complement (not break) this existing infrastructure.
4. **21st MCP reliability** — Previously failed with Gemini. Grok should handle it, but we need a fallback pattern.
5. **Skill ecosystem** — Multiple design skills already exist (`design`, `ui-styling`, `ui-ux-pro-max`, `design-system`, `banner-design`, `motion-design`, etc.). The `designer` loads them on demand rather than duplicating their content.
6. **Subdelegation safety** — `designer-mule` follows the mule invariant (`task: {"*": "deny"}`), structurally guaranteed to never spawn further agents.

---

## Approaches Considered

### Option A: Designer as a named skill (no new subagent)

Load a `design-orchestration` skill via the supervisor's skill tool. The supervisor stays the single orchestrator.

- **Pros**: Zero new agent files, no permission changes
- **Cons**: Supervisor is text-only (DeepSeek V4 Pro); cannot see mockups, screenshots, or rendered output. Design work requires visual feedback loops. The skill would just be instructions for a text-only model that can't execute them. **Rejected.**

### Option B: Designer as a variant of grok-worker (shared agent file)

Add design-specific instructions to `grok-worker.md` and route design work there.

- **Pros**: Fewer files, simpler
- **Cons**: Conflates general-purpose Grok work with design work. Different permission needs (21st, open-design, etc.). Different system prompts. The `grok-worker` already has its own identity. **Rejected.**

### Option C: Dedicated `designer` + `designer-mule` agents (separate files, separate identity)

Two new agent files. The `designer` has its own system prompt, permission block, MCP access, and subdelegation rules. The `designer-mule` mirrors the mule pattern for bounded design sub-tasks.

- **Pros**: Clean separation of concerns. Design-specific MCP access isolated to the designer. Clear delegation path. Follows existing patterns (`grok-worker` / `grok-mule`).
- **Cons**: Two new files, slight config growth. **Accepted — this is the right pattern.**

---

## Recommendation

**Option C — dedicated `designer` + `designer-mule`.** Two new agent markdown files in `~/.config/opencode/agents/`, one surgical edit to `supervisor.md`, and minor `opencode.json` permission updates.

### What the codebase looks like after

```
~/.config/opencode/agents/
├── designer.md          ← NEW — Grok 4.5, spawn-capable, design system prompt
├── designer-mule.md     ← NEW — Grok 4.3, leaf, bounded design tasks
├── ... (existing 44 agents unchanged)
```

**`opencode.json`** — Two changes:
1. Add `agent.designer.permission` block (MCP tools designer can access)
2. Add design MCP servers that aren't yet configured (21st, etc.)

**`agent/supervisor.md`** — Three changes:
1. Add row to Pre-Implementation Triage table
2. Add `designer` and `designer-mule` to Subagent Toolbox table
3. Update Visual Verification section to reference `@designer` as preferred path

---

## 1. Exact Agent Configs

### `agents/designer.md`

```yaml
---
description: Design subagent for UI/UX work — wireframes, mockups, visual styling, design systems, component design, layout, animation, accessibility. Fully empowered — writes code, runs dev servers, captures screenshots, verifies visually. Powered by Grok 4.5. Spawn at will for ANY design task.
mode: subagent
model: xai/grok-4.5
variant: max
steps: 45
color: "#EC4899"
permission:
  task:
    "*": allow
  edit: allow
  bash: allow
  webfetch: allow
  websearch: allow
  playwright_*: allow
  chrome-devtools_*: allow
  twenty-first_*: allow
  open-design_*: allow
  a11y-color-contrast_*: allow
---
```

**Design decisions:**
- **model: `xai/grok-4.5`** — User's requested model. The xAI provider is confirmed available (`@ai-sdk/xai` v4.0.2 in package.json). If the exact model ID differs (e.g. `xai/grok-4.5-beta`), adjust in implementation.
- **steps: 45** — Higher than `grok-worker`'s 40 because design work involves visual capture → analyze → edit → recapture loops that consume steps.
- **color: `#EC4899`** (Tailwind pink-500) — Distinct from all existing agent colors. Pink is unused in the current palette.
- **Permission `twenty-first_*`** — The 21st MCP tool family. The MCP server name in opencode.json must be `"twenty-first"` to match this prefix.
- **`task: {"*": "allow"}`** — Designer can spawn mules for parallel sub-tasks (e.g., spawn `designer-mule` for a component implementation while it researches design patterns).

### `agents/designer-mule.md`

```yaml
---
description: "Design leaf agent — bounded UI/UX implementation, component styling, visual fixes, CSS/Tailwind work. Mule tier: structurally cannot spawn subagents. Powered by Grok 4.3."
mode: subagent
model: xai/grok-4.3
variant: max
steps: 30
color: "#F472B6"
permission:
  task:
    "*": deny
  edit: allow
  bash: allow
  webfetch: allow
  websearch: allow
  playwright_*: allow
  chrome-devtools_*: allow
  twenty-first_*: allow
  open-design_*: allow
  a11y-color-contrast_*: allow
---
```

**Design decisions:**
- **model: `xai/grok-4.3`** — Cheapest Grok model for bounded leaf work. Consistent with `grok-mule`.
- **steps: 30** — Standard mule budget.
- **color: `#F472B6`** (Tailwind pink-400) — Lighter shade of designer's pink, visual kinship.
- **`task: {"*": "deny"}`** — Mule invariant: cannot spawn further agents.
- **Same MCP access as designer** — Mules need the same tools to execute design subtasks.

### Designer System Prompt (body of `designer.md`)

The system prompt should cover:

1. **Role definition** — "You are a design subagent. You handle ALL UI/UX/design work across any framework or project type."
2. **Design workflow** (visual-first loop):
   - Capture current state (playwright or chrome-devtools screenshot)
   - Analyze visually (Grok can see images directly — no @observer needed)
   - Make changes
   - Recapture and verify
   - Report with before/after evidence
3. **Tool guidance** — When to use playwright vs chrome-devtools, when to load design skills
4. **Skill loading** — "Load relevant design skills via the `skill` tool when needed: `design` for brand identity/tokens, `ui-styling` for shadcn/ui + Tailwind, `design-system` for token architecture, `motion-design` for animations, `gsap-core` for GSAP, `banner-design` for social/ads, `design-taste-frontend` for landing pages."
5. **Accessibility** — Always check contrast (a11y-color-contrast), run lighthouse audits on navigation, flag a11y issues in reports
6. **21st workflow** — "Use `twenty-first_*` tools to search for and retrieve UI components. If 21st returns errors, fall back to manual implementation."
7. **Subdelegation rules** — Same mule orchestration pattern as `grok-worker`
8. **Pre-completion checks** — Visual before/after, lighthouse, contrast, responsive breakpoints
9. **Visual Needs section** — "As a subagent with native image vision, you can see screenshots directly. Use playwright or chrome-devtools to capture state. You do NOT need @observer."

---

## 2. opencode.json Changes

### 2a. Add MCP server configs for design tools

Add to the `mcp` block. These are servers that don't currently exist but the designer needs:

```json
"twenty-first": {
  "command": ["npx", "-y", "@21st-dev/mcp"],
  "enabled": true,
  "type": "local"
},
"a11y-color-contrast": {
  "command": ["npx", "-y", "@a11y-color-contrast/mcp"],
  "enabled": true,
  "type": "local"
}
```

**`open-design`** already exists in `opencode.json` but is `"enabled": false`. Change to `"enabled": true` for the designer.

### 2b. Add agent-level permission blocks

Add a `designer` entry to the `agent` block:

```json
"agent": {
  "supervisor": { ... },
  "media": { ... },
  "designer": {
    "permission": {
      "twenty-first_*": "allow",
      "open-design_*": "allow",
      "a11y-color-contrast_*": "allow"
    },
    "options": {}
  }
}
```

**Why this is needed:** The `agent.designer.permission` block in `opencode.json` is the *global* gate for these MCP tools. The designer's own `.md` file also lists them, but both layers must allow. This follows the existing pattern: the supervisor has `open-design_*: "deny"` in both its `opencode.json` block AND the global permission block.

### 2c. Add global permission rules

Add to the top-level `permission` block:

```json
"permission": {
  "chrome-devtools_*": "allow",
  "elevenlabs_*": "allow",
  "macos-use_*": "allow",
  "open-design_*": "deny",
  "screenpipe_search-content": "allow",
  "screenpipe_export-video": "deny",
  "pentest-ai_*": "deny",
  "macos-automator_*": "allow",
  "gemini-api-docs_*": "allow",
  "vercel_*": "allow",
  "twenty-first_*": "deny",
  "a11y-color-contrast_*": "allow"
}
```

**Key decision:** `twenty-first_*` is globally `"deny"` (supervisor can't use it, only designer). `a11y-color-contrast_*` is globally `"allow"` (supervisor can use it for quick checks if needed — it's lightweight and read-only).

### 2d. Supervisor permission update

In `agent.supervisor.permission`, explicitly deny design-only tools so the supervisor is forced to delegate:

```json
"agent": {
  "supervisor": {
    "permission": {
      "chrome-devtools_*": "allow",
      "elevenlabs_*": "allow",
      "open-design_*": "deny",
      "pentest-ai_*": "deny",
      "macos-use_*": "allow",
      "screenpipe_search-content": "allow",
      "screenpipe_export-video": "allow",
      "macos-automator_*": "allow",
      "gemini-api-docs_*": "allow",
      "vercel_*": "allow",
      "twenty-first_*": "deny"
    }
  }
}
```

### Summary of opencode.json diff

| Change | Location | Detail |
|--------|----------|--------|
| Add MCP server | `mcp.twenty-first` | `@21st-dev/mcp`, enabled: true |
| Add MCP server | `mcp.a11y-color-contrast` | `@a11y-color-contrast/mcp`, enabled: true |
| Enable existing | `mcp.open-design.enabled` | false → true |
| Add agent block | `agent.designer` | Permission block for 21st, open-design, a11y-contrast |
| Add global deny | `permission.twenty-first_*` | `"deny"` (designer-only tool) |
| Add global allow | `permission.a11y-color-contrast_*` | `"allow"` (safe for anyone) |
| Add supervisor deny | `agent.supervisor.permission.twenty-first_*` | `"deny"` |

---

## 3. The Surgical Hook (supervisor.md Changes)

### 3a. Pre-Implementation Triage table — new row

Insert after the existing rows (after the `junior-security` row):

```markdown
| UI/UX design, visual styling, component design, wireframes, mockups, layout, animation, accessibility styling | Spawn `designer` |
```

**Full updated table:**

```markdown
| Situation | Action before implementing |
|---|---|
| Symptom unclear; bug behavior not fully understood | Spawn `junior-debugger` for root-cause investigation |
| Project docs don't clearly point to the right approach, or the area involves evolving standards (libraries, security, modern API patterns, accessibility, etc.) | Spawn `junior-researcher` *before* architecting — cheap insurance against reinventing or using stale patterns |
| Needs unfamiliar APIs, library behavior, or current best practices | Spawn `junior-researcher` |
| Multiple valid approaches; refactor scope unclear | Spawn `junior-architect` for a tradeoff analysis |
| Large work; unclear sequence | Spawn `junior-planner` for an ordered breakdown |
| Security-sensitive area (auth, secrets, payments, input handling) | Spawn `junior-security` *after* implementation, *before* committing |
| UI/UX design, visual styling, component design, wireframes, mockups, layout, animation, accessibility styling | Spawn `designer` |
```

### 3b. Subagent Toolbox table — new rows

Add after the `grok-worker` row:

```markdown
| `designer` | UI/UX design, visual styling, component design, accessibility, animations | `designer-mule` | Bounded design implementation, component styling, CSS/Tailwind work. | Supervisor tool (always available) |
```

**Full updated toolbox section:**

```markdown
| Subagent | Use for | Mule variant | Mule use for | Supervisor access |
|---|---|---|---|---|
| ... (existing rows unchanged) ... |
| `grok-worker` | High-powered max-capacity worker. Grok 4.3 with 1M context, strong coding, creative reasoning. Spawn at will. | — | — | Supervisor tool (always available) |
| `designer` | UI/UX design, visual styling, component design, accessibility, animations | `designer-mule` | Bounded design implementation, component styling, CSS/Tailwind work. | Supervisor tool (always available) |
```

### 3c. Visual Verification section — reference @designer

In the **Decision Flow for Visual Tasks** section (line ~150), add a new priority item above the existing list:

```markdown
### Decision Flow for Visual Tasks

When the user asks for anything involving visual state, follow this priority:

0. **If the task is design work (styling, layout, components, mockups)** → delegate to `@designer`. The designer has native image vision (Grok 4.5) and can capture, analyze, edit, and verify in a tight loop without @observer. This is the preferred path for ALL design tasks.
1. **If the user pasted an image** → @observer plugin auto-injects, handle the analysis
2. **If you need to see a web app for non-design reasons** → playwright screenshot → @observer analyze
3. **If you need to see a native macOS app** → macos-use capture → @observer analyze
4. **If you need to verify a UI change** → full loop: capture → @observer analyze → compare → fix → repeat
```

### 3d. After Work Complete checklist — visual verification gate

Add to the checklist (after the "Manual smoke check" line):

```markdown
- [ ] Visual verification for UI-affecting changes:
  - Design work: designer confirmed before/after visual match in report
  - Non-design UI changes: @observer Mode F comparison passed
```

---

## 4. MCP Enablement Decisions

| MCP Server | Currently | Action | Justification |
|---|---|---|---|
| `playwright` | enabled: true | **Keep enabled** | Already used by supervisor, grok-worker, and others. Designer gets `playwright_*` in its permission block. |
| `chrome-devtools` | enabled: true | **Keep enabled** | Already used. Provides `lighthouse_audit` — the designer uses this for perf/a11y audits. |
| `open-design` | enabled: false | **Enable (true)** | Design system CLI. Currently denied to supervisor. Enable globally but keep supervisor deny — only designer uses it. |
| `twenty-first` (`@21st-dev/mcp`) | *Not in config* | **Add + enable** | Component retrieval. The user wants this for the designer. Add with `enabled: true`, deny globally and to supervisor, allow only in designer's permission blocks. |
| `a11y-color-contrast` | *Not in config* | **Add + enable** | WCAG contrast checking. Lightweight, read-only, safe for anyone. Allow globally. |
| `lighthouse` | *Not in config* | **Do NOT add separately** | `chrome-devtools` already provides `chrome-devtools_lighthouse_audit`. Adding a separate `lighthouse` MCP would be redundant. |
| `tailwindcss` | *Not in config* | **Do NOT add** | Tailwind docs MCP. The designer can use `webfetch` for docs or load the `ui-styling` skill. Low value as a separate MCP. |
| `magic-ui` | *Not in config* | **Do NOT add** | Animated React components. Niche. Designer can use `webfetch` + `firecrawl` if needed. |
| `flowbite` | *Not in config* | **Do NOT add** | Same reasoning as magic-ui. |
| `design-token-bridge` | *Not in config* | **Do NOT add** | Token translation tool. Niche. Can be added later if needed. |
| `wcag` | *Not in config* | **Do NOT add** | WCAG librarian. Redundant with `chrome-devtools_lighthouse_audit` + `a11y-color-contrast`. |
| `southleft-design` | *Not in config* | **Do NOT add** | Design system search. Overlaps with 21st + open-design. |

**Bottom line:** Add only `twenty-first` and `a11y-color-contrast`. Enable `open-design`. The rest are either redundant, already covered, or too niche to justify the config surface area.

---

## 5. 21st MCP Handling

**Problem:** User previously turned 21st off because Gemini couldn't handle the tool names/schemas. The designer uses Grok, which should handle it. But the 21st MCP isn't even in `opencode.json` currently.

**Solution — three-layer gate:**

1. **Layer 1 (global `permission`):** `"twenty-first_*": "deny"` — No agent can call 21st tools unless explicitly allowed.
2. **Layer 2 (`agent.supervisor.permission`):** `"twenty-first_*": "deny"` — Supervisor cannot use it. Supervisor delegates design work to @designer.
3. **Layer 3 (`agent.designer.permission` + designer.md frontmatter):** Both allow `twenty-first_*` — Only the designer can use it.

This follows the existing `open-design_*` pattern exactly (globally denied, supervisor denied, media agent allowed).

**Fallback in designer system prompt:** The designer should handle 21st failures gracefully: "If 21st tools return errors, fall back to manual implementation or use playwright to browse 21st.dev directly." The user's prior issues were Gemini-specific (model couldn't parse the tool output), not a tool crash — so Grok should handle it. The fallback covers the case where it's actually a tool issue, not just a model issue.

**MCP config to add:**

```json
"twenty-first": {
  "command": ["npx", "-y", "@21st-dev/mcp"],
  "enabled": true,
  "type": "local"
}
```

If the 21st MCP requires an API key, it goes in the `environment` block of the MCP config (not in the agent config).

---

## 6. Design-Orchestration Skill

**Decision: No separate `design-orchestration` skill. The designer's system prompt IS the single source of truth for design workflow.**

**Rationale:**

- The existing design skills (`design`, `ui-styling`, `design-system`, `motion-design`, etc.) are *tool-specific* — they teach how to use shadcn/ui, design tokens, GSAP, etc.
- The `designer`'s system prompt is *role-specific* — it teaches the designer how to THINK about design work: the visual loop, when to capture vs when to edit, how to structure reports, what to verify.
- Mixing role instructions into a skill creates confusion about what's the designer's identity vs what's a tool guide.

**Scope boundaries:**

| What lives in the designer's system prompt | What lives in skills (loaded on demand) |
|---|---|
| Design-first workflow (capture → analyze → edit → verify) | `design` — brand identity, tokens, logos, banners |
| When to use playwright vs chrome-devtools for screenshots | `ui-styling` — shadcn/ui + Tailwind patterns |
| Accessibility requirements and verification gates | `design-system` — token architecture, component specs |
| 21st MCP usage and fallback patterns | `motion-design` — animation principles and CSS/Framer techniques |
| Visual report format (before/after screenshots, checklist) | `gsap-core` — GSAP API reference |
| Subdelegation rules for design mules | `design-taste-frontend` — anti-slop landing page patterns |
| Pre-completion checklist (lighthouse, contrast, responsive) | `banner-design` — social media banner specs |
| Skill loading guidance (which skill for which situation) | `slides` — presentation design |

This follows the `grok-worker` pattern: the agent's `## Strengths` section and workflow guidance live in the agent file, while specialized knowledge loads via skills.

---

## 7. Visual Review Loop

### Current state (supervisor.md line ~160)

The supervisor has a "Verification Loop Protocol" that uses @observer for visual verification. This works for non-design UI changes (e.g., a bug fix that happens to affect layout) but is inefficient for design work.

### New state

**The `designer` handles visual verification internally.** Grok 4.5 has native image vision — it can see screenshots directly without @observer. This eliminates the supervisor → @observer roundtrip for design tasks.

**Designer's internal loop:**
1. Capture current UI state (playwright screenshot or chrome-devtools)
2. Visually analyze the screenshot (Grok's native vision)
3. Make code changes
4. Restart/reload the app
5. Recapture
6. Compare before/after visually
7. Report: "Verified visually — [N]/[N] design checks passed"

**Supervisor's role:** The supervisor receives the designer's report (which includes before/after evidence and verification results). The supervisor does NOT re-verify design work visually — it trusts the designer's report. The supervisor's "After Work Complete" checklist gains a visual verification gate for design work (see section 3d above).

**For non-design UI changes** (e.g., a debugger fixing a layout bug), the existing @observer path remains unchanged.

### Updated "After Work Complete" checklist addition

```markdown
- [ ] Visual verification gate:
  - Design work: designer's report includes before/after screenshots and confirms visual match
  - Non-design UI changes: @observer Mode F comparison passed (or designer spawned for quick visual review if complex)
```

---

## 8. Migration of Existing Design Tooling

**Decision: The supervisor KEEPS existing visual tool access. No tool migration.**

| Tool | Supervisor keeps? | Reasoning |
|---|---|---|
| `playwright_*` | **Yes** | Used for non-design visual verification (debugging, @observer screenshots, smoke checks). Also needed for the supervisor's Visual Verification section which handles non-design UI tasks. |
| `chrome-devtools_*` | **Yes** | Used for lighthouse audits in non-design contexts (performance debugging). Also a fallback when playwright fails. |
| `macos-use_*` | **Yes** | Desktop automation — not a design tool. Used for system-level tasks. |
| `a11y-color-contrast_*` | **Yes** (allowed globally) | Lightweight, read-only. Supervisor can use for quick checks without spawning designer. |
| `open-design_*` | **No** (already denied) | Already denied in current config. Leave as-is. |
| `twenty-first_*` | **No** (newly denied) | Designer-only. Component retrieval doesn't make sense for supervisor. |

**The pattern is:** The supervisor retains general-purpose visual tools for its own use. Design-specific tools (21st, open-design) are gated to the designer. The surgical hook in supervisor.md (section 3) is the mechanism that routes work — not tool denial. The supervisor COULD technically still do design work with playwright, but the triage table tells it not to.

---

## Implementation Order

1. **Create `agents/designer.md`** — Frontmatter + full system prompt
2. **Create `agents/designer-mule.md`** — Frontmatter + system prompt
3. **Edit `opencode.json`** — Add MCP servers (twenty-first, a11y-color-contrast), enable open-design, add permission blocks
4. **Edit `agent/supervisor.md`** — Three changes (triage table row, toolbox table rows, visual verification reference)
5. **Restart opencode** to pick up new agents and MCP configs
6. **Smoke test** — "Design a login page" — verify designer spawns, captures, edits, and reports

---

## Risks & Mitigations

| Risk | Likelihood | Mitigation |
|---|---|---|
| `xai/grok-4.5` model ID is wrong | Medium | The xAI SDK may use a different ID format (e.g. `xai/grok-4.5-beta`, `xai/grok-4.5-latest`). Verify by checking the `@ai-sdk/xai` v4.0.2 supported models before finalizing. Fall back to `xai/grok-4.3` if 4.5 isn't available yet. |
| 21st MCP still fails (not just a Gemini issue) | Low | Designer system prompt includes fallback: "If 21st tools error, browse 21st.dev directly via playwright or implement manually." |
| Designer step limit (45) insufficient for complex design work | Medium | Design loops (capture → edit → recapture) are step-hungry. If 45 is too low, increase to 55. Monitor first few real tasks. |
| `a11y-color-contrast` MCP package name is wrong | Low | The npm package might be `@a11y-color-contrast/mcp`, `a11y-color-contrast-mcp`, or similar. Verify on npm before adding. |
| Color clash with existing agent colors | Low | `#EC4899` (pink) is unused. `#F472B6` (lighter pink for mule) is also unused. Verified against all 44 existing agent colors. |
| Designer loads skills that conflict with its system prompt | Low | Skills are additive (they inject instructions, don't override). The designer's system prompt takes precedence as the base context. |
