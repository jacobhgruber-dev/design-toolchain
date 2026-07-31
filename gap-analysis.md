# Design Tooling Gap Analysis

**Date:** 2026-07-31
**Scope:** Compare installed tools (skills, MCPs, global npm packages) against research docs at `mcp-servers.md`, `ai-skills-tools.md`, `apis-platforms.md`.

---

## What We Have (by category)

| Category | Installed & Active | Installed but Disabled | On Disk (unregistered skill) |
|---|---|---|---|
| **Design Intelligence** | ui-ux-pro-max (skill), 21st MCP | Southleft Design Systems MCP, Open Design MCP | taste (anti-slop design methodology) |
| **Components** | 21st MCP (shadcn/React search+install) | Flowbite MCP, Magic UI MCP, TailwindCSS MCP | — |
| **Accessibility** | — | a11y-mcp (axe-core), a11y-color-contrast-mcp, Lighthouse MCP, WCAG MCP | — |
| **Animation** | — | — | gsap (core API), motion-design (design theory) |
| **Testing (Visual)** | Playwright MCP (screenshots) | — | — |
| **Design-to-Code** | 21st MCP, Apify MCP (disabled remote) | — | — |
| **Icons/Assets** | design skill (icon gen via Gemini), brand skill (logo gen) | — | — |
| **Color/Typography** | ui-ux-pro-max (palettes + font pairings DB), brand skill (extract-colors.cjs) | Design Token Bridge MCP | — |
| **Linting** | stylelint, svgo (global npm) | — | — |
| **Design Systems** | design-system skill (token architecture), brand skill | Design Token Bridge MCP, Open Design MCP | — |
| **Collaboration/Handoff** | — | — | — |
| **Wireframing** | — | — | — |

**Summary:** 6 of 11 categories have at least one active tool. Accessibility, animation, collaboration, and wireframing have zero active tools. 10 MCP servers are configured but disabled.

---

## Fillable Gaps (tool exists — we could install/enable)

### Trivial (already npm-installed, just flip `enabled: true`)

| Tool | Category | What It Does | Why It Matters | Disk Impact |
|---|---|---|---|---|
| **a11y-mcp** | Accessibility | axe-core accessibility audit via MCP. Tests URLs/HTML for WCAG 2.0/2.1/2.2 violations. | Only zero-config way to audit generated UI in-agent. Catches color contrast, ARIA, keyboard traps before commit. | 0 (already installed) |
| **a11y-color-contrast-mcp** | Accessibility | Pairwise color contrast checker (AA/AAA). `are-colors-accessible`, `use-light-or-dark` tools. | Quick check when picking colors — prevents contrast violations at design time. | 0 (already installed) |
| **Lighthouse MCP** | Accessibility/Perf | Google Lighthouse wrapper: performance, accessibility, SEO, Core Web Vitals. | One-shot audit covering perf + a11y + SEO. Complements a11y-mcp with perf dimension. | 0 (already installed) |
| **Design Token Bridge MCP** | Design Systems | Translates tokens between Tailwind, CSS, Figma Variables, W3C DTCG, Material 3, SwiftUI. WCAG contrast validation built in. | Bridges design-system skill output to actual framework tokens. Eliminates manual translation. | 0 (already installed) |
| **Flowbite MCP** | Components | 60+ Tailwind components. Includes Figma-to-code conversion. | Expands component palette beyond shadcn. Figma→Tailwind pipeline is uniquely valuable. | 0 (already installed) |
| **Magic UI MCP** | Components | Animated React components (Magic UI library). Searchable, installable. | Only animation-aware component source in your toolchain. Fills animation gap partially. | 0 (already installed) |
| **TailwindCSS MCP** | Components | Tailwind utilities, docs, conversion tools, template generation. | Makes the agent Tailwind-literate without hunting docs. Reduces hallucinated classes. | 0 (already installed) |
| **Southleft Design Systems MCP** | Design Intelligence | Vector search across 200+ design system entries: W3C, WCAG 2.2, ARIA, Material Design 3, Fluent, Carbon, Polaris. | Design spec lookup without leaving the agent. Reduces context-switching to docs. | 0 (remote) |

### Moderate (not installed, but tool exists)

| Tool | Category | What It Does | Why It Matters | Install Difficulty | Disk Impact |
|---|---|---|---|---|---|
| **Framelink MCP for Figma** | Design-to-Code | Reads Figma layout, spacing, color tokens, typography, screenshots. 15.5k stars, MIT. | Market leader for Figma→code. Closes the design handoff gap entirely. | `npm i -g figma-developer-mcp` + add to opencode.json | ~20 MB |
| **Figma Official MCP** | Design-to-Code | Read design context AND write back to Figma canvas (frames, components, variables). | Bidirectional — agent can both read designs and create/update them. Requires Figma seat. | Remote URL config | 0 (remote) |
| **Storybook MCP** | Components/Testing | Component docs, code generation reusing existing components, component/accessibility tests, self-healing. | Deepest component library integration. If your project has Storybook, this is transformative. | `npm i -g @storybook/mcp` | ~15 MB |
| **Apify MCP** | Design-to-Code | "Screenshot to HTML/Code" tool. Converts UI screenshots → HTML, Tailwind, React. | Already configured but disabled. Bridges visual inputs to code generation. | 0 (already in config) | 0 (remote) |
| **shadcn-ui MCP Server** | Components | shadcn/ui v4 components, blocks, demos for React, Svelte 5, Vue, React Native. | Better shadcn coverage than 21st alone. Covers Svelte/Vue/RN variants. | `npx @shadcn/ui-mcp` or npm install | ~10 MB |
| **mcp-image-compare-server** | Visual Regression | Pixel-perfect comparison via Pixelmatch. Compares two images or screenshots of two URLs. | Fills the visual regression gap with zero platform dependency. Diff image output. | `npm i -g mcp-image-compare-server` | ~5 MB |
| **tints-cli** | Color | Rust CLI generating 11-shade Tailwind palettes from hex. Perceptually uniform (HSLuv). | Generates design-system-ready palettes from a single accent color. Agent-friendly CLI. | `npm i -g tints-cli` or `cargo install` | ~3 MB (Rust binary) |
| **fonttrio** | Typography | Curated font pairing registry for shadcn/ui. 49 combos, single-command install. | Removes font pairing guesswork. Single-command install into shadcn config. | `npx fonttrio` (no global install) | 0 |
| **screenshot-to-code** | Design-to-Code | Converts screenshots/designs → HTML/Tailwind/React/Vue. Supports local models (Ollama). | Self-hosted alternative to v0/Anima. Works with your local Ollama models. | `git clone` + `pip install` | ~200 MB (models) |

### Hard (significant setup or commercial)

| Tool | Category | What It Does | Why It Matters | Install Difficulty | Notes |
|---|---|---|---|---|---|
| **Figma MCP (thirdstrandstudio)** | Design Systems | Full Figma REST API wrapper — 31 tools: users, files, comments, teams, components, styles, webhooks. | Deepest Figma integration available. Programmatic access to entire Figma file structure. | Requires Figma API token + config | Best if you manage Figma org |
| **Penpot MCP** | Design-to-Code | Open-source design platform MCP. Design↔code↔design roundtrip. | Free self-hosted Figma alternative. Full design-to-code roundtrip. | Requires Penpot instance | Best for FOSS design workflow |
| **Applitools MCP** | Visual Regression | AI-powered visual testing. Computer vision detects meaningful changes. Ultrafast Grid. | Industry leader. Smarter than pixel diffs — catches what humans notice. | Commercial ($99–$199/mo) | Overkill unless shipping production UI |
| **Carbon MCP (IBM)** | Design Systems | Makes AI agents IBM Carbon experts: React, Web Components, Icons, Charts. | Only if using IBM Carbon. Otherwise irrelevant. | Remote, free | Niche |
| **MUI MCP** | Components | Natural language → React + MUI code. `useMuiDocs`, `fetchDocs`, `generateReactCode`. | Only if using MUI. Otherwise skip. | `npm i -g @mui/mcp` | Niche |
| **Canva MCP** | Assets | Generate/edit/search designs, manage assets/brands, export. Remote MCP. | If you use Canva for asset creation. | Remote URL + auth | Niche |
| **Frame0 MCP** | Wireframing | Create/modify wireframes via natural language. Balsamiq alternative. | Non-existent wireframing capability. Unique. | Requires Frame0 v1.7.0+ | Nascent (low adoption) |

### On-Disk Skills to Register (zero install — just add to config)

| Skill | Category | What It Does | Why It Matters |
|---|---|---|---|
| **taste** (design-taste-frontend) | Design Intelligence | Anti-slop methodology: infers design brief, sets DESIGN_VARIANCE/MOTION_INTENSITY/VISUAL_DENSITY dials, avoids AI defaults. | Single highest-impact skill to add. Prevents generic AI aesthetics across every design output. 1206 lines. |
| **gsap** (gsap-core) | Animation | Official GSAP API: `to()`, `from()`, `fromTo()`, easing, stagger, ScrollTrigger, matchMedia. | Industry-standard animation library. Free since Webflow acquisition (April 2025). |
| **motion-design** | Animation | LottieFiles-authored motion design principles: emotional targets, Disney principles for UI, stagger patterns, choreography rules. | Design-theory layer for animation. Pairs with gsap (theory + implementation). |

---

## Unfillable Gaps (no tool exists yet)

| Gap | Category | Why It Matters | Likelihood of Being Filled |
|---|---|---|---|
| **Integrated design QA pipeline** | Testing | No single MCP combines a11y audit + visual regression + brand consistency + responsive testing in one pass. Workflow today is manual: run a11y-mcp → Playwright screenshots → manual review → repeat. | Low — tooling is fragmenting, not consolidating. AI agents may eventually orchestrate this themselves. |
| **AI design critique agent** | Design Intelligence | No tool reviews AI-generated UIs against design principles (hierarchy, balance, rhythm, consistency) and suggests improvements. Taste skill is the closest but is a methodology, not an auditor. | Medium — Gemini/Claude vision models are close to being able to do this. Expect a skill or MCP in 6–12 months. |
| **Brand consistency enforcement** | Brand/Design Systems | Brand skill has asset validation scripts but no automated check that generated UI respects brand tokens, voice, spacing rules. Needs to compare output against DESIGN.md or brand config. | Medium — Open Design's DESIGN.md contract is a step in this direction. Likely emerges from Open Design ecosystem. |
| **Lottie/After Effects → React conversion MCP** | Animation | Designers create animations in After Effects, export Lottie JSON. No MCP converts Lottie → React components with proper event handling and responsive behavior. | Low — LottieFiles has a React player but no MCP for agent-driven conversion. motion-skills partially addresses this. |
| **Real-time collaboration awareness** | Collaboration | Liveblocks, Yjs, PartyKit exist as libraries but no MCP gives AI agents awareness of collaborative state (who's editing what, merge conflict resolution, CRDT sync). | Low — collaboration MCPs require deep real-time infrastructure. Not a priority for the ecosystem. |
| **Comprehensive responsive testing MCP** | Testing | Playwright does viewport capture but no MCP validates layout at every breakpoint, checks for overflow, tests touch targets on mobile. Gap between "capture screenshot" and "validate responsive behavior." | Low — Playwright MCP + custom scripts can approximate this. Unlikely to get a dedicated MCP. |
| **Icon/asset pipeline MCP** | Icons/Assets | Iconify has a REST API, but no MCP integrates icon search + SVG optimization + sprite generation + component wrapping. Currently manual via svgo + copy-paste. | Medium — Iconify API + svgo wrapper would be straightforward. Someone will build this. |
| **Design token diff/versioning** | Design Systems | Style Dictionary handles transforms but no MCP diffs token changes between versions, generates changelogs, or validates breaking changes in token APIs. | Medium — Design Token Bridge MCP has the foundation. Versioning likely comes from the W3C DTCG ecosystem. |

---

## Top 5 Recommendations (ranked by impact)

### 1. Register `taste` skill — highest impact, zero cost
Currently on disk at `~/.opencode/skills/taste/` but not in the `available_skills` registry. Prevents every AI-generated UI from looking like default AI slop. 1206 lines of design methodology. Complements ui-ux-pro-max (which provides the database, taste provides the judgment).

### 2. Enable `a11y-mcp` + `a11y-color-contrast-mcp` — closes the accessibility gap
Both are npm-installed, already configured in opencode.json, just disabled. Zero-disk-impact. Turn on the accessibility category: catching WCAG violations at generation time prevents rework.

### 3. Install `Framelink MCP for Figma` — closes the design handoff gap
15.5k stars, MIT license, actively maintained. Single largest missing category: the bridge between Figma designs and AI-generated code. `npm i -g figma-developer-mcp` + add to opencode.json. Moderate effort, transformative impact.

### 4. Enable `Magic UI MCP` + register `gsap` and `motion-design` skills — closes the animation gap
Animation is a zero-coverage category right now. Magic UI MCP provides animated components (install side). gsap + motion-design skills provide animation implementation + design theory. Three zero-to-low-effort additions that together make animation a first-class capability.

### 5. Install `Storybook MCP` — future-proofs component workflow
If your projects use Storybook, this is the deepest component integration available: docs, code generation, testing. If you don't use Storybook yet, skip this and prioritize Framelink MCP instead.

---

## Post-Implementation Update (July 2026)

All fillable gaps from the original analysis have been addressed. The final state:

- **All fillable gaps closed.** Every tool in the "Trivial" and "Moderate" tiers has been either installed, enabled, or intentionally skipped with a documented reason.
- **framelink MCP** was installed then removed — Figma's free tier is too restrictive for API access, making the MCP unusable without a paid seat.
- **higgsfield** was installed then removed — upstream dependency deadlock made it unviable.
- **Final counts:** 30 MCPs evaluated total (15 installed, 6 always-on/enabled), 10 skills registered.
- **Remaining unfillable gaps unchanged.** The 8 gaps identified in the original analysis (integrated QA pipeline, AI design critique agent, brand consistency enforcement, Lottie→React conversion, real-time collaboration awareness, comprehensive responsive testing, icon/asset pipeline, design token diff/versioning) remain unfillable — no tools exist yet that address them.
