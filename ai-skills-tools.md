# AI Skills & Tools for UI/UX Design — Reference

An opinionated catalog of AI skills, CLI tools, and GitHub repos for UI/UX design work that integrate with AI coding assistants (Claude Code, Cursor, OpenCode, Codex, Gemini CLI).

---

## Installation Status

Status of skills and tools from this catalog as of July 2026.

### Skills — 10 Installed

| Skill | Status |
|---|---|
| ui-ux-pro-max | ✅ Installed — 84 UI styles, 192 palettes, 74 font pairings, 98 UX guidelines |
| taste (design-taste-frontend) | ✅ Installed — anti-slop design methodology, prevents generic AI aesthetics |
| brand | ✅ Installed — brand voice, visual identity, asset management, messaging |
| design | ✅ Installed — logos (55 styles), icons, CIP mockups, presentations |
| slides | ✅ Installed — strategic HTML presentations with Chart.js + design tokens |
| banner-design | ✅ Installed — social/ads/web/print banners (22 styles) |
| ui-styling | ✅ Installed — shadcn/ui components + Tailwind CSS + canvas design |
| gsap-core | ✅ Installed — GSAP animation API: tweens, timelines, ScrollTrigger |
| motion-design | ✅ Installed — timing, easing, choreography, Disney principles for UI |
| design-system | ✅ Installed — three-layer token architecture, component specs |

### CLI Tools

| Tool | Status |
|---|---|
| Open Design CLI | ✅ Cloned at `~/Projects/open-design` — agent-agnostic design system |
| screenshot-to-code | ⏭️ Skipped — redundant; Apify MCP covers screenshot-to-code |
| figma-to-code (bernaferrari) | ⏭️ Skipped — requires Figma API access (free tier too restrictive) |
| OpenPencil CLI | ⏭️ Skipped — design token extraction covered by Design Token Bridge MCP |
| Builder CLI | ⏭️ Skipped — requires Builder.io Figma plugin |
| Google Stitch MCP | ⏭️ Skipped — Google-specific design platform |
| tints-cli | ⏭️ Skipped — ui-ux-pro-max palette database covers color generation |
| fonttrio | ⏭️ Skipped — ui-ux-pro-max font pairing database covers this |
| axe-core CLI / Pa11y / Lighthouse CLI | ⏭️ Skipped — covered by MCP equivalents (a11ymcp + Lighthouse MCP) |

### Component Libraries

| Library | Status |
|---|---|
| Eldora UI | ⏭️ Skipped — project-level dependency, not installed globally |
| Aceternity UI | ⏭️ Skipped — project-level dependency, not installed globally |
| shadcn/ui | ⏭️ Skipped — installed per-project via CLI; MCP coverage via 21st |
| Magic UI | ⏭️ Skipped — installed per-project; MCP provides search + install |
| Vercel AI Elements | ⏭️ Skipped — project-level dependency |
| Shadway | ⏭️ Skipped — project-level, covered by 21st generation |

---

## AI Design Skills & Repos

| Tool | Description | License | Status |
|------|-------------|---------|--------|
| [ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) | AI skill with searchable database: 84 UI styles, 192 color palettes, 74 font pairings, 192 product types, 98 UX guidelines, 16 GSAP motion presets. Built-in BM25 search engine. | — | ✅ Installed |
| [Taste Skill](https://github.com/Leonxlnx/taste-skill) | Open-source SKILL.md to prevent generic/AI-slop frontend designs. Aesthetic constraints for layout, typography, spacing, motion, responsiveness. Portable across Claude Code, Cursor, Codex, Gemini CLI. | — | Active (2026) |
| [ai-ui-design-skills](https://github.com/dhananjaym182/ai-ui-design-skills) | Production-ready AI skills for SaaS UI/UX, typography systems, and brand asset generation. Compatible with Claude Code, Cursor, Windsurf, Codex, OpenCode. | — | Active |
| [Open Design](https://github.com/nexu-io/open-design) | Local-first, agent-agnostic design system CLI. Wraps coding agents in a curated skill library (150+ design system packages, 250+ skills). Uses `DESIGN.md` as brand contract. 57,400+ stars in 8 weeks. Rapidly growing (2026). | Apache-2.0 | ✅ Cloned |
| [Swiss Design System](https://github.com/maxbogo/awesome-ai-tools-for-ui) | Teaches AI agents Swiss design principles — typography, grids, color patterns — to enforce systematic design. Part of awesome-ai-tools-for-ui list. | — | — |

> **Note:** Open Design is already cloned at `/Users/jacobgruber/Projects/open-design`.

---

## Design-to-Code Tools & CLIs

| Tool | Description | License | Status |
|------|-------------|---------|--------|
| [screenshot-to-code](https://github.com/abi/screenshot-to-code) | Converts UI screenshots/design images into HTML/Tailwind/React/Vue. Supports local models (Ollama). CLI + API surfaces. Well-maintained. | MIT | Active |
| [figma-to-code (React + Tailwind)](https://github.com/bernaferrari/FigmaToCode) | Free CLI (released Jan 2026). Converts Figma frame → React + Tailwind code including components, layout, assets. | — | Active |
| [OpenPencil](https://github.com/open-pencil/open-pencil) | Open-source Figma alternative. Native `.fig` file support. AI design via chat, 90+ node tools. Headless CLI for export to JSX/Tailwind. Real-time WebRTC collaboration. ~7 MB Tauri app. July 2026 update. | MIT | Active |
| [Builder CLI](https://www.builder.io/c/docs/cli) | Works with Builder Figma plugin. Imports designs, generates customizable code. Supports prompts to influence output. | — | Active |
| [Google Stitch MCP](https://github.com/google/stitch-mcp) | Open-source CLI to build production React components from Google Stitch designs. Integrates with Claude Code, Cursor. | Apache-2.0 | Active |

---

## Component Generators

| Tool | Description | License | Status |
|------|-------------|---------|--------|
| [21st.dev Magic](https://21st.dev) | AI component marketplace & registry. Generate React/shadcn components from natural language. Multiple variants, remix existing, refine via chat. | — | ✅ MCP installed |
| [ai-components-generator](https://github.com/hanzili/ai-components-generator) | CLI tool creating React components from text descriptions. Supports natural language modification of existing components. | — | Active |
| [shadcn/ui (CLI v4)](https://github.com/shadcn-ui/ui) | Project-aware context for AI assistants. `--dry-run` and `--diff` flags. Mar 2026. | MIT | Active |
| [Vercel AI Elements](https://vercel.com/ai/elements) | Component library + custom registry on shadcn/ui for AI-native apps. Pre-built React components for conversations, messages. CLI installation. | — | Active |
| [Shadway](https://shadway.com) | AI-powered generation of production React/Next.js UI using shadcn components. | — | Active |

---

## Accessibility Testing Tools

| Tool | Description | License | Status |
|------|-------------|---------|--------|
| [axe-core CLI](https://github.com/dequelabs/axe-core-npm) | Deque's industry-standard accessibility engine. Zero false positives. WCAG 2.0/2.1/2.2 (A/AA/AAA). `--exit` flag for CI failure. Versions 4.10–4.11.3 in 2025–2026. | MPL-2.0 | Active |
| [Pa11y](https://github.com/pa11y/pa11y) | Automated accessibility testing suite. CLI + Node.js API. Supports CSV, HTML, JSON, TSV reporters. **pa11y-ci** for CI/CD (URL lists, sitemaps). Can use axe-core as alternative engine. | LGPL-3.0 | Active |
| [Lighthouse CLI](https://github.com/GoogleChrome/lighthouse) | Google's auditing tool. Accessibility audits powered by axe-core subset. **Lighthouse CI** for continuous monitoring, GitHub Actions integration. | Apache-2.0 | Active |

---

## Design System Generators

| Tool | Description | License | Status |
|------|-------------|---------|--------|
| [Open Design](https://github.com/nexu-io/open-design) | Agent-agnostic design system CLI. `DESIGN.md` as brand contract. Generates consistent artifacts (prototypes, dashboards, landing pages, email templates) using any coding agent. 57K+ stars. | Apache-2.0 | ✅ Cloned |
| [Source Foundation CLI](https://github.com/source-foundation/cli) | NPM package generating color palettes + typography tokens from `source.config.json`. Creates CSS variables for colors, typography, radii, spacing. | — | Active |
| [OpenPencil](https://github.com/open-pencil/open-pencil) | Extract design tokens (colors, typography, spacing). Convert between formats. Analyze clusters. CLI-driven design token management. | MIT | Active |

---

## Visual AI Tools

| Tool | Description | License | Status |
|------|-------------|---------|--------|
| [VisionTest.ai](https://github.com/jstuart0/visiontest-ai-oss) | Open-source AI visual regression. 4-stage diff cascade: SSIM → LPIPS → DINOv2 → VLM analysis. Natural language test creation. Self-healing selectors. | — | Active |
| [Applitools Eyes](https://applitools.com) | Enterprise AI visual testing. Computer vision to identify meaningful changes (not pixel-level). Viewport grid testing. Figma Plugin (Jan 2026). Storybook Addon. Industry leader. | Proprietary | Active |
| [Percy (BrowserStack)](https://percy.io) | AI-powered visual review agent. Auto-filters anti-aliasing, sub-pixel, OS font false positives. CI/CD integration. | Proprietary | Active |
| [Lost Pixel](https://github.com/lost-pixel/lost-pixel) | Open-source visual regression testing. Free + cloud options. AI-driven UI verification. | — | Active |
| [Chromatic](https://www.chromatic.com) | Storybook-integrated visual regression + cross-browser testing. UI component review. | Proprietary | Active |

---

## Color & Typography Tools

### Color

| Tool | Description | License | Status |
|------|-------------|---------|--------|
| [tints-cli](https://github.com/crabby-utils/tints-cli) | Rust CLI generating 11-shade Tailwind-style palettes (50–950) from hex color. Optimized for coding agents — token-efficient CLI. HSLuv for perceptually uniform lightness. | — | Active |
| [Colorizer.rs](https://github.com/colorizer-rs/colorizer) | Rust CLI for palettes + semantic color schemes (Base16/Base24) from accent color. Terminal/PNG visualization. | — | Active |
| [Colorpedia](https://github.com/joeyespo/colorpedia) | Python CLI for color lookup, shades, and predefined palettes (molokai, facebook). Supports HEX, RGB, HSL, HSV, CMYK. | — | Active |

### Typography

| Tool | Description | License | Status |
|------|-------------|---------|--------|
| [fonttrio](https://www.fonttrio.xyz) | Curated font pairing registry for shadcn/ui. 49 combinations (heading + body + monospace). Single-command install via shadcn CLI. Launched May 2026. | — | Active |
| [font-pairing](https://github.com/Eckankar/font-pairing) | Python tool generating visual previews of font combos. Auto-downloads from Google Fonts. Light/dark themes. | — | Active |
| [FontGet](https://github.com/ronniedroid/fontget) | Cross-platform CLI font manager. Discovers/installs from Google Fonts, Nerd Fonts, Font Squirrel. | — | Active |
| [gfcli](https://github.com/aitchkhan/gfcli) | Node.js CLI for Google Fonts — search, download, install. No API key needed. | — | Active |

---

## Animation & Motion Design Tools

| Tool | Description | License | Status |
|------|-------------|---------|--------|
| [Motion (formerly Framer Motion)](https://github.com/motiondivision/motion) | MIT-licensed animation library for React/JS/Vue. AI Kit: agent-compatible docs, saved transitions, 410+ premium examples. MotionScore for Agents: audits animation performance (2026). | MIT | Active |
| [GSAP + GSAP Skills](https://github.com/greensock/gsap-skills) | Entire GSAP toolkit became 100% free (April 2025, Webflow acquisition). Official AI skills teach agents correct API usage, ScrollTrigger, timelines, plugins. Works with Cursor, Claude Code. | Proprietary → Free | Active |
| [motion-skills](https://github.com/nexu-io/motion-skills) | Open-source skills teaching AI agents to create motion graphics, kinetic typography, data-driven charts, TikTok/Reels content. | — | Active |
| [motion-anything](https://github.com/nexu-io/motion-anything) | Chat-native motion engine — generate/edit animated pages and videos from natural language. Open source. | — | Active |
| [LottieFiles Motion Design Skill](https://github.com/LottieFiles/motion-design-skill) | Universal motion design principles for AI agents. Covers timing, easing, choreography, Disney animation principles adapted for UI. | — | Active |
| [GSAPify](https://gsapify.com) | AI tool generating and optimizing GSAP code from natural language prompts — timelines, tweens, ScrollTrigger. Framework-agnostic. | — | Active |

---

## Responsive Design Testing

| Tool | Description | License | Status |
|------|-------------|---------|--------|
| [Playwright](https://github.com/microsoft/playwright) | Built-in viewport testing + screenshot comparison. Cross-browser (Chromium, Firefox, WebKit). CLI + CI/CD. | Apache-2.0 | ✅ MCP installed |
| [Cypress](https://github.com/cypress-io/cypress) | `cy.viewport()` for responsive testing. CLI runner. GitHub CI integration. | MIT | Active |
| [Galen Framework](https://github.com/galenframework/galen) | Layout testing with specification language for responsive design validation. | Apache-2.0 | Active |

---

## What's Already Installed

| Tool | Status |
|------|--------|
| UI UX Pro Max Skill | ✅ Installed via `uipro init --ai opencode` |
| 21st.dev MCP | ✅ Configured in `opencode.json` |
| Playwright MCP | ✅ Already configured |
| Open Design | ✅ Cloned at `/Users/jacobgruber/Projects/open-design` |
| Brand, Design, Slides, Banner, UI-Styling skills | ✅ Came with UI UX Pro Max install |

---

## Notable Gaps

Tools worth evaluating that are not yet installed:

| Tool | Why | Effort |
|------|-----|--------|
| [Taste Skill](https://github.com/Leonxlnx/taste-skill) | Prevents AI-slop UI designs. Simple SKILL.md install. | Low |
| [a11ymcp](https://github.com/orgs/a11ymcp) | axe-core accessibility testing via MCP. Integrates directly with your assistant. | Low |
| [tints-cli](https://github.com/crabby-utils/tints-cli) | Agent-optimized palette generation. Token-efficient, perceptually uniform (HSLuv). | Low |
| [fonttrio](https://www.fonttrio.xyz) | Font pairing registry for shadcn/ui. Single-command install. | Low |
| Frame0 MCP | Open-source wireframing with natural language. MCP integration. | Medium |
| Apify MCP | Screenshot-to-code via MCP. Bridges visual inputs to code generation. | Medium |
