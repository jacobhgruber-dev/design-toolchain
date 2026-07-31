# Design Toolchain for OpenCode

A complete UI/UX design toolchain integrated with the [OpenCode](https://opencode.ai) AI coding assistant — component marketplaces, accessibility auditing, visual testing, design systems, animation, brand identity, and design-to-code pipelines. This repo catalogs every tool, documents what's wired in, and provides a blueprint for replicating the setup.

## Using This Repo as a Template

1. **Clone the repo** — `git clone <repo-url> && cd Design`
2. **Read the README** (this file) for the big picture — what's installed, what each category covers, and what skills auto-activate
3. **Follow [`SETUP.md`](./SETUP.md) step by step** — replace `$HOME` and `$NPM_GLOBAL` placeholders with your actual paths before running any commands
4. **Reference the catalogs** — [`mcp-servers.md`](./mcp-servers.md), [`ai-skills-tools.md`](./ai-skills-tools.md), and [`apis-platforms.md`](./apis-platforms.md) document tools beyond the defaults. Use them to evaluate what to add next.

The repo works as a reference even if you don't install everything — the catalog docs are standalone value. Pick and choose what fits your workflow.

## What's Here

| Document | Content |
|----------|---------|
| [`mcp-servers.md`](./mcp-servers.md) | Catalog of 60+ MCP servers for UI/UX — design systems, components, accessibility, visual regression, design-to-code, prototyping |
| [`ai-skills-tools.md`](./ai-skills-tools.md) | Catalog of 40+ AI skills, CLIs, and repos — design intelligence, design-to-code, color/typography, animation |
| [`apis-platforms.md`](./apis-platforms.md) | Catalog of 50+ APIs and platforms — color/font/icon/illustration APIs, design handoff, collaboration |
| [`gap-analysis.md`](./gap-analysis.md) | Coverage audit: what we have installed vs. what's missing, ranked recommendations |
| [`SETUP.md`](./SETUP.md) | Step-by-step replication guide (planned) |

## Toolchain Overview

| Category | What's Installed | Always-On | Key Capabilities |
|----------|-----------------|-----------|------------------|
| **Component Marketplace** | 21st MCP | Yes | Search, generate, retrieve React/shadcn components; multiple variants per query |
| **Component Libraries** | Flowbite MCP (60+ Tailwind), Magic UI MCP (150+ animated React) | No | Tailwind components + Figma-to-code; animated React components |
| **Accessibility** | a11y-color-contrast MCP, a11y MCP (axe-core), Lighthouse MCP, WCAG MCP | a11y-color-contrast + Lighthouse | WCAG contrast checking, full axe-core audits, Lighthouse perf/a11y/SEO, WCAG spec librarian |
| **Visual Testing** | Playwright MCP, image-compare MCP | Playwright | Browser screenshots + accessibility snapshots; pixel-perfect diff comparison |
| **Design Intelligence** | ui-ux-pro-max (skill), taste (skill), Southleft Design Systems MCP, Open Design MCP | No (skills auto-activate) | 84 UI styles, 192 palettes, 74 fonts, 98 UX guidelines; anti-slop enforcement; vector search across 200+ design system entries; agent-agnostic design system CLI |
| **Design Systems & Tokens** | design-system (skill), design-token-bridge MCP, brand (skill) | No | Primitive→semantic→component token architecture; Tailwind↔CSS↔Figma↔Material 3↔SwiftUI translation; brand identity guidelines |
| **Design-to-Code** | 21st MCP, Apify MCP | 21st | Component generation; screenshot→HTML/Tailwind/React conversion |
| **Animation** | manim MCP, motion-design (skill), gsap (skill) | manim | Mathematical/programmatic animation; Disney principles for UI; GSAP tweens/timelines/ScrollTrigger |
| **UI Styling** | ui-styling (skill) | No (auto-activate) | shadcn/ui components, Tailwind CSS, accessible theming, dark mode |
| **Brand & Identity** | brand (skill), design (skill), banner-design (skill) | No (auto-activate) | Brand voice + visual identity; logo design (55 styles), icons (15 styles), CIP mockups; social/ads/hero banners (22 styles) |
| **Presentations** | slides (skill) | No (auto-activate) | Strategic HTML presentations with Chart.js |
| **Document Processing** | ocr-pipeline MCP | Yes | Multi-engine OCR for documents, images, audio, handwriting |

## MCP Servers

30 MCP servers total: 6 always-on, 24 toggleable (disabled by default in `opencode.json`).

### Always-On (6)

| Server | Type | Description |
|--------|------|-------------|
| **21st** | Remote (`https://21st.dev/api/mcp`) | Component marketplace: search, generate, retrieve React/shadcn components. 35+ tools. |
| **a11y-color-contrast** | Local (`a11y-color-contrast-mcp`) | WCAG color contrast checking: `get-color-contrast`, `are-colors-accessible` (AA/AAA), `use-light-or-dark`. 3 tools. |
| **Lighthouse** | Local (`lighthouse-mcp-server`) | Google Lighthouse wrapper: performance, accessibility, SEO, best-practices, Core Web Vitals. 13+ tools. |
| **Manim** | Local (`manim-mcp-server`) | Mathematical and programmatic animation rendering. 2 tools. |
| **Playwright** | Local (`@playwright/mcp`) | Full browser automation: screenshots, accessibility snapshots, PDF generation, vision-based interactions. Chromium, Firefox, WebKit. |
| **OCR Pipeline** | Local | Multi-engine document OCR: PDF, EPUB, DOCX, images, audio, handwriting. Preexisting server. |

### Toggleable Design MCPs

Flip `enabled: true` in `opencode.json` to activate. All are already configured — just disabled.

| Server | Type | Description |
|--------|------|-------------|
| **a11y** | Local (`a11y-mcp`) | axe-core full WCAG accessibility audits via Puppeteer. Tests URLs/HTML for WCAG 2.0/2.1/2.2 violations — color contrast, ARIA, keyboard traps. |
| **Flowbite** | Local (`flowbite-mcp`) | 60+ Tailwind components plus Figma-to-code conversion pipeline. |
| **Magic UI** | Local (`@magicuidesign/mcp`) | 150+ animated React components (Tailwind + Motion). Searchable and installable from AI editors. |
| **TailwindCSS** | Local (`tailwindcss-server`) | Tailwind utilities, docs, conversion tools, and template generation. Makes the agent Tailwind-literate. |
| **Design Token Bridge** | Local (`design-token-bridge-mcp`) | Translate design tokens between Tailwind, CSS, Figma Variables, W3C DTCG, Material 3, SwiftUI. Built-in WCAG contrast validation. |
| **WCAG** | Local (`wcag-server.js`) | WCAG digital librarian: all guidelines, criteria, and techniques available in-agent. |
| **Image Compare** | Local (`mcp-image-compare`) | Visual regression: pixel-perfect image comparison via Pixelmatch. Compare two images or screenshots of two URLs. Returns diff stats + color-coded diff image. 3 tools. |
| **Apify** | Remote (`https://mcp.apify.com`) | Screenshot → HTML/Tailwind/React code conversion. Also: web scraping, data extraction, search. |
| **Southleft Design** | Remote (`https://design-systems-mcp.southleft.com/mcp`) | Vector search across 200+ design system entries: W3C, WCAG 2.2, ARIA, Material Design 3, Fluent, Ant Design, Carbon, Polaris. |
| **Open Design** | Local | Agent-agnostic design system CLI. 150+ design system packages. Uses `DESIGN.md` as a brand contract for consistent output across agents. |

### Other Toggleable MCPs (preexisting, non-design)

14 additional MCP servers exist in the config but are irrelevant to design workflows: Blender, ElevenLabs, Railway, Chrome DevTools, yt-dlp, Audacity, nmap, Pentest AI, macOS Use, Screenpipe, macOS Automator, PyGhidra, Gemini API Docs, Vercel.

## Skills

10 skills auto-activate on keyword detection from `~/.opencode/skills/`. No manual enabling required — OpenCode loads the matching skill when relevant terms appear in a prompt.

| Skill | Size | Activates On | Description |
|-------|------|-------------|-------------|
| **ui-ux-pro-max** | 1.8 MB | Design, UI, UX, styling, colors, fonts, layout, product type | 84 UI styles, 192 color palettes, 74 font pairings, 192 product types, 98 UX guidelines, 16 GSAP motion presets. Built-in BM25 search. |
| **taste** | 88 KB | Landing page, portfolio, redesign, frontend, design | Anti-slop design enforcement. Sets DESIGN_VARIANCE, MOTION_INTENSITY, and VISUAL_DENSITY constraints to prevent generic AI aesthetics. |
| **design** | 316 KB | Logo, icon, CIP, brand identity, mockup | Logo design (55 styles via Gemini AI), icon design (15 styles), corporate identity program mockups (50 deliverables), brand identity generation. |
| **design-system** | 240 KB | Design tokens, design system, CSS variables, spacing scale, typography scale | Token architecture (primitive → semantic → component), CSS variables, spacing/typography scales, component specifications. |
| **ui-styling** | 204 KB | UI, styling, shadcn, Tailwind, theme, dark mode | shadcn/ui components (Radix UI + Tailwind), accessible theming, dark mode implementation, responsive layouts. |
| **brand** | 128 KB | Brand, brand voice, visual identity, messaging, marketing | Brand voice guidelines, visual identity frameworks, messaging frameworks, asset management, brand consistency enforcement. |
| **motion-design** | 80 KB | Animation, motion, transition, micro-interaction, loading | Disney animation principles adapted for UI: timing, easing, choreography, emotional targets, stagger patterns. Pairs with gsap skill. |
| **slides** | 32 KB | Slides, presentation, deck, pitch | Strategic HTML presentations with Chart.js, design tokens, responsive layouts, and copywriting formulas. |
| **gsap** | 16 KB | GSAP, tween, timeline, ScrollTrigger, animate | Official GSAP core API: `to()`, `from()`, `fromTo()`, easing, duration, stagger, `matchMedia()` (responsive), `ScrollTrigger`. |
| **banner-design** | 20 KB | Banner, social media, ad, hero, creative asset | Social media, ads, website hero banners — 22 art direction styles. Multi-platform (Facebook, Twitter/X, LinkedIn, YouTube, Instagram, Google Display). |

## Global CLI Tools

Tools available system-wide, not tied to OpenCode's agent context:

| Package Manager | Tools |
|----------------|-------|
| **npm** | `@21st-dev/cli`, `a11y-mcp`, `a11y-color-contrast-mcp`, `flowbite-mcp`, `@magicuidesign/mcp`, `tailwindcss-mcp-server`, `mcp-image-compare-server`, `stylelint`, `svgo`, `tonal` |
| **pip** | `manim` (0.20.1), `manim-mcp-server` |

## Quick Start

For step-by-step instructions on replicating this toolchain, see [`SETUP.md`](./SETUP.md).

## Prerequisites

- **OpenCode** — Desktop AI coding assistant
- **Node.js + npm** — For MCP servers and global CLI tools
- **Python 3.10+ with pip** — For Manim and OCR pipeline
- **macOS** — Some tools (macOS Use, macOS Automator, Screenpipe) are macOS-specific

## What We Skipped (and Why)

Tools researched but deliberately excluded from the installed toolchain:

| Tool | Reason |
|------|--------|
| **Framelink (Figma MCP)** | Removed. Figma free tier too restrictive for meaningful use; requires paid Figma seat. |
| **Higgsfield (video generation MCP)** | Upstream dependency conflict — fastmcp version deadlock with other servers. |
| **Storybook MCP** | Not using Storybook in current projects. Re-evaluate if Storybook is adopted. |
| **tints-cli** | Requires Rust toolchain (`cargo install`). ui-ux-pro-max skill covers palette generation without additional dependencies. |
| **fonttrio** | Project-level shadcn tool, not a global tool. Run per-project via `npx fonttrio` when needed. |
| **GSAP plugins/frameworks skills** | Core gsap skill is sufficient for the API surface. Additional variants (plugins, framework-specific wrappers) available in the taste-skill repo if needed. |
| **Swiss Design System skill** | Redundant — taste skill + ui-ux-pro-max cover the same design principles (grids, typography, systematic design). |
| **Aceternity UI / Eldora UI / Motion Primitives / Spell UI** | Project-level shadcn component libraries, not global tools. Install per-project via `npx shadcn@latest add` when needed. |
| **screenshot-to-code (OSS)** | 200 MB+ install footprint. Redundant with Apify MCP (screenshot→code) + 21st MCP (component generation). Both cover the same use case without local model overhead. |

## Maintenance Notes

- **Enable a disabled MCP:** Flip `"enabled": false` → `"enabled": true` for the server entry in `~/.config/opencode/opencode.json`, then restart OpenCode.
- **Add a new skill:** Place a valid `SKILL.md` in `~/.opencode/skills/<skill-name>/`. OpenCode auto-discovers it on next restart. Skills activate on keyword match — no manual wiring needed.
- **Reference docs** (`mcp-servers.md`, `ai-skills-tools.md`, `apis-platforms.md`, `gap-analysis.md`) track tools we've researched but haven't installed. Use these to evaluate new additions before committing.
- **MCP server types:** Local servers run as child processes spawned by OpenCode. Remote servers connect to hosted endpoints over HTTP. Remote servers have zero disk impact but require network access.

---

*Last updated: July 2026*
