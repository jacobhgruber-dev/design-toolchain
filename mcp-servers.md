# MCP Servers for UI/UX Design — Reference

A catalog of Model Context Protocol (MCP) servers relevant to UI/UX design workflows: design systems, component libraries, accessibility, visual regression, design-to-code, and more.

---

## Installation Status

Status of MCP servers from this catalog as of July 2026. Installation commands use `opencode mcp add` (or equivalent for your assistant).

| MCP Server | Status | Notes |
|---|---|---|
| 21st Magic MCP | ✅ Installed | Enabled — component search + generation. `npx @21st-dev/magic-mcp` |
| a11ymcp | ✅ Installed | Disabled — axe-core WCAG audits. `npx a11y-mcp-server` |
| a11y-color-contrast-mcp | ✅ Installed | Disabled — pairwise contrast checker (AA/AAA) |
| Apify MCP | ✅ Installed | Disabled — screenshot-to-code + web scraping. Remote: `mcp.apify.com` |
| Design Token Bridge MCP | ✅ Installed | Enabled — token translation (Tailwind, CSS, W3C DTCG, Material 3) |
| Flowbite MCP | ✅ Installed | Disabled — 60+ Tailwind components, Figma-to-code pipeline |
| image-compare MCP | ✅ Installed | Enabled — pixel-perfect comparison via Pixelmatch |
| Lighthouse MCP | ✅ Installed | Disabled — performance, a11y, SEO, Core Web Vitals. `npx @danielsogl/lighthouse-mcp` |
| Magic UI MCP | ✅ Installed | Disabled — animated React components, searchable + installable |
| manim MCP | ✅ Installed | Enabled — mathematical animation engine |
| Open Design MCP | ✅ Installed | Disabled — agent-agnostic design system, `DESIGN.md` contract |
| Playwright MCP | ✅ Installed | Enabled — browser automation, screenshots, a11y snapshots. `npx @playwright/mcp` |
| Southleft Design Systems MCP | ✅ Installed | Disabled — vector search across 200+ design entries |
| tailwindcss MCP | ✅ Installed | Disabled — Tailwind utilities, docs, templates |
| WCAG MCP | ✅ Installed | Enabled — WCAG 2.2 guideline and technique lookup |
| Framelink MCP for Figma | ❌ Removed | Installed then removed — Figma free tier too restrictive for API access (`figma-developer-mcp`) |
| Figma Official MCP | ⏭️ Skipped | Requires paid Figma seat |
| thirdstrandstudio/mcp-figma | ⏭️ Skipped | Requires Figma API token + org access |
| shadcn/ui MCP Server + shadcn CLI MCP | ⏭️ Skipped | Covered by 21st MCP (same component ecosystem) |
| Zeroheight, Supernova MCPs | ⏭️ Skipped | Enterprise, closed source |
| Carbon, SAP Fiori, Appian Aurora MCPs | ⏭️ Skipped | Platform-specific (IBM, SAP, Appian) |
| Chakra UI, MUI, Ant Design, Radix MCPs | ⏭️ Skipped | Framework-specific — use only if on that stack |
| Canva MCP | ⏭️ Skipped | Commercial, requires Canva account |
| Deque Axe, Evinced, BrowserStack MCPs | ⏭️ Skipped | Commercial accessibility — open-source a11ymcp + Lighthouse cover needs |
| Applitools, Happo, SmartUI, Wopee MCPs | ⏭️ Skipped | Commercial visual regression — Playwright + image-compare cover needs |
| Penpot MCP | ⏭️ Skipped | Requires self-hosted Penpot instance |
| Storybook MCP | ⏭️ Skipped | Project-level dependency (requires Storybook in project) |
| Frame0, MockFlow MCPs | ⏭️ Skipped | Nascent — low adoption, not production-ready |
| MCP-UI-Org/mcp-ui | ⏭️ Skipped | SDK/standard, not a design tool |
| Other cataloged MCPs | ⏭️ Skipped | Evaluated but not needed (overlapping with installed stack) |

**Totals:** 15 installed (6 enabled, 9 disabled), 1 removed, ~25 skipped. 30 MCPs evaluated total.

---

## Design System MCPs

### Figma MCP Servers

| Server | Stars | License | Description | npm / URL | Status |
|--------|-------|---------|-------------|-----------|--------|
| **Framelink MCP for Figma** ([GLips/Figma-Context-MCP](https://github.com/GLips/Figma-Context-MCP)) | 15.5k | MIT | Dominant community server. Provides Figma layout, spacing, color tokens, typography, and screenshots to AI agents. | `figma-developer-mcp` | Active (v0.13.0, June 2026) |
| **Figma Official MCP** | — | Closed | Figma's built-in MCP. Read design context **and** write back to the canvas (frames, components, variables). Integrates with VS Code, Cursor, Claude Code, Copilot. | `https://mcp.figma.com/mcp` | Active |
| **thirdstrandstudio/mcp-figma** ([thirdstrandstudio/mcp-figma](https://github.com/thirdstrandstudio/mcp-figma)) | 75 | — | Full Figma REST API wrapper — 31 MCP tools: users, files, comments, teams, components, styles, webhooks, analytics. | — | Active |

### Design Token & Design System Documentation MCPs

| Server | Stars | Description | Key Features | Status |
|--------|-------|-------------|--------------|--------|
| **Design Token Bridge MCP** ([kenneives/design-token-bridge-mcp](https://github.com/kenneives/design-token-bridge-mcp)) | 5 | Extracts tokens from Tailwind, CSS, Figma Variables, W3C DTCG. | Translates to Material 3, SwiftUI, Tailwind, CSS Variables. WCAG contrast validation. 91 unit tests. | Active |
| **Design System MCP** ([yajihum/design-system-mcp](https://github.com/yajihum/design-system-mcp)) | 25 | Exposes `getComponentProps` and `getTokens` from JSON token files. Integrates with Style Dictionary. Built with Deno. | Token + props retrieval, Style Dictionary integration | Active |
| **Southleft Design Systems MCP** | 193 | AI-powered vector search across 200+ entries. | W3C, WCAG 2.2, ARIA, Material Design 3, Fluent, Ant Design, Carbon, Polaris. Hosted at `https://design-systems-mcp.southleft.com/mcp`. | Active |
| **Zeroheight MCP** | — | Connects AI assistants to zeroheight-hosted design system documentation, components, tokens. Enterprise. Closed source. | `@zeroheight/mcp-server` | Active |
| **Supernova MCP** ([supernova.io](https://supernova.io)) | — | Secure access to design system data: tokens, components, docs, assets. Resolves token references. Closed source. | Token resolution, component + asset access | Active |

### Enterprise Design System MCPs

| Server | Stars | Description | Source |
|--------|-------|-------------|--------|
| **Carbon MCP (IBM)** ([carbon-design-system/carbon-mcp](https://github.com/carbon-design-system/carbon-mcp)) | 27 | Makes any AI agent an expert in IBM Carbon: React, Web Components, Icons, Charts, AI Chat. | Hosted by IBM |
| **SAP Fiori MCP** | — | Fiori-specific knowledge, best practices, project-aware context. Closed source. | [sap.com](https://sap.com) |
| **Appian Aurora MCP** ([appian-design/aurora-mcp](https://github.com/appian-design/aurora-mcp)) | — | Access to Aurora Design System docs. | Appian |

---

## Component Library MCPs

### Major Component Libraries

| Server | Stars | Description | Key Details | Status |
|--------|-------|-------------|-------------|--------|
| **shadcn/ui MCP Server** ([Jpisnice/shadcn-ui-mcp-server](https://github.com/Jpisnice/shadcn-ui-mcp-server)) | 2.9k | shadcn/ui v4 components, blocks, demos for React, Svelte 5, Vue, React Native. Also supports Base UI. | SSE transport + Docker | Active |
| **shadcn CLI MCP (Official)** ([shadcn-ui/ui](https://github.com/shadcn-ui/ui)) | 48k+ | Built into shadcn CLI — browse, search, install components from any shadcn registry. | Part of core CLI | Active |
| **Radix MCP Server** ([gianpieropuleo/radix-mcp-server](https://github.com/gianpieropuleo/radix-mcp-server)) | 8 | Covers Radix Themes, Primitives, and Colors. 12 tools. | Nascent | Early |
| **Chakra UI MCP** ([chakra-ui/chakra-ui](https://github.com/chakra-ui/chakra-ui)) | 40.5k | Official MCP for Chakra UI components, tokens, themes, v2→v3 migration. | `@chakra-ui/react-mcp` v2.1.1 | Active |
| **MUI MCP (Official)** ([mui/material-ui](https://github.com/mui/material-ui)) | — | Official MUI MCP: `useMuiDocs`, `fetchDocs`, `generateReactCode` (natural language → React+MUI, optionally from Figma frames). | `@mui/mcp` v0.1.3 | Very active |
| **Ant Design CLI MCP** ([ant-design/ant-design](https://github.com/ant-design/ant-design)) | 241 | 8 tools, 2 prompts (`antd-expert`, `antd-page-generator`). Fully offline, version-accurate (v3/v4/v5/v6), bilingual. 316 commits. Gold standard for component library MCPs. | CLI-based, offline-first | Active |

### Tailwind CSS & Component Generation

| Server | Stars | Description | Key Details |
|--------|-------|-------------|-------------|
| **21st Magic MCP** ([21st-dev/magic](https://github.com/21st-dev/magic)) | ~5.5k | Searches curated component library, returns multiple variants, installs with dependencies. | Already configured in your setup |
| **Magic UI MCP** ([magic-ui/magic-ui](https://github.com/magic-ui/magic-ui)) | 197 | Animated React components from Magic UI — searchable and installable from AI editors. | Animation-focused component library |
| **Flowbite MCP** ([themesberg/flowbite](https://github.com/themesberg/flowbite)) | 38 | 60+ Flowbite components with Tailwind. Includes Figma-to-code conversion. | Figma → Tailwind pipeline |
| **tailwindcss-mcp-server** ([CarbonoDev/tailwindcss-mcp-server](https://github.com/CarbonoDev/tailwindcss-mcp-server)) | 34 | Tailwind utilities, docs, conversion tools, template generation. | Utility + doc access |

### Other Notable

| Server | Stars | Description | Access |
|--------|-------|-------------|--------|
| **Canva MCP (Official)** | — | Remote MCP for Canva: generate/edit/search designs, manage assets/brands, export. Closed source. | `https://mcp.canva.com/mcp` |
| **MCP-UI-Org/mcp-ui** ([MCP-UI-Org/mcp-ui](https://github.com/MCP-UI-Org/mcp-ui)) | 5,048 | MCP Apps standard SDK. `@mcp-ui/server` (TypeScript) + `@mcp-ui/client`. SDKs for TS, Ruby, Python. | SDK / standard |

---

## Accessibility Testing MCPs

### Full Web Accessibility Audit (axe-core)

| Server | Stars | Description | Key Features | Status |
|--------|-------|-------------|--------------|--------|
| **a11ymcp** ([ronantakizawa/a11ymcp](https://github.com/ronantakizawa/a11ymcp)) | 89 | axe-core + Puppeteer. Tests URLs/HTML for WCAG 2.0/2.1/2.2. | Color contrast, ARIA validation, orientation lock. npm: `a11y-mcp-server`. 10k+ downloads. | Active |
| **accessibility-agents** ([Community-Access/accessibility-agents](https://github.com/Community-Access/accessibility-agents)) | 373 | 79 agents, 24 MCP tools, axe-core integration, VPAT generation, WCAG 2.2 AA. | Web, DOCX, XLSX, PPTX, PDF, GitHub workflows. v6.0.0. | Very active |
| **lighthouse-mcp-server** ([danielsogl/lighthouse-mcp-server](https://github.com/danielsogl/lighthouse-mcp-server)) | 66 | Google Lighthouse wrapper. | 13+ tools: performance, accessibility, SEO, Core Web Vitals. npm: `@danielsogl/lighthouse-mcp`. 230 commits. | Very active |

### Color Contrast

| Server | Stars | Description | Key Features |
|--------|-------|-------------|--------------|
| **a11y-color-contrast-mcp** ([ryelle/a11y-color-contrast-mcp](https://github.com/ryelle/a11y-color-contrast-mcp)) | 2 | `get-color-contrast`, `are-colors-accessible` (AA/AAA), `use-light-or-dark`. | Hex, RGB, HSL, named colors. npm published. |
| **contrast-checker-mcp** ([ogSINGH/contrast-checker-mcp](https://github.com/ogSINGH/contrast-checker-mcp)) | — | WCAG 2.1 contrast with alpha transparency. | Matches WebAIM checker output. |

### Commercial / Enterprise Accessibility MCPs

| Server | Description | Access |
|--------|-------------|--------|
| **Deque Axe MCP** | Official Axe DevTools MCP: enterprise accessibility testing, AI remediation, sprint planning. | Commercial |
| **Evinced MCP** | Enterprise web + mobile accessibility. Computer vision, structural semantic modeling. | Commercial |
| **BrowserStack MCP** | Spectra Rule Engine, AI-suggested fixes, natural language WCAG/ADA compliance testing. | Commercial |

---

## Visual Regression Testing MCPs

| Server | Stars | Description | Key Details | Status |
|--------|-------|-------------|-------------|--------|
| **mcp-image-compare-server** ([leky90/mcp-image-compare-server](https://github.com/leky90/mcp-image-compare-server)) | 3 | Pixel-perfect comparison via Pixelmatch. Compares two images or screenshots of two URLs. | Returns diff stats + color-coded diff image. | Active |
| **Applitools MCP** ([applitools/eyes-mcp](https://github.com/applitools/eyes-mcp)) | — | Official. Sets up Applitools Eyes in Playwright, adds visual checkpoints, configures Ultrafast Grid. | npm: `@applitools/mcp`. New and official. | Active |
| **Happo MCP** ([happo.io/docs/mcp](https://happo.io/docs/mcp)) | — | Official Happo MCP. Inspect/resolve visual diffs. | OAuth 2.1, Streamable HTTP. Beta. | Commercial |
| **SmartUI MCP (LambdaTest)** ([lambdatest.com](https://lambdatest.com)) | — | AI-native visual regression. Natural-language diff explanations. | Pixel, layout, DOM, perceptual changes. Figma ↔ live page comparison. | Commercial |
| **Wopee MCP** ([wopee-io/wopee-mcp](https://github.com/wopee-io/wopee-mcp)) | 5 | Autonomous testing platform MCP: manages suites, generates artifacts, dispatches agents for visual regression. | 165 commits. | Active |

---

## Browser Automation with Visual Capabilities

| Server | Stars | Description | Key Details |
|--------|-------|-------------|-------------|
| **Playwright MCP (Microsoft)** ([microsoft/playwright-mcp](https://github.com/microsoft/playwright-mcp)) | 35.7k | Full browser automation: screenshots, accessibility snapshots, PDF generation, vision-based interactions, tracing. Headless Docker. Chromium, Firefox, WebKit. | npm: `@playwright/mcp`. 565 commits. Already configured in your setup. |

---

## Design-to-Code & Prototyping MCPs

| Server | Stars | Description | Key Details | Status |
|--------|-------|-------------|-------------|--------|
| **Penpot MCP (Official)** ([penpot/penpot](https://github.com/penpot/penpot)) | 342 | Open-source design platform MCP. Access layers, components, design tokens (colors, typography, spacing). Design↔code↔design. WebSocket via MCP Plugin. | Design↔code roundtrip | Active |
| **Apify MCP Server** ([apify/apify-mcp-server](https://github.com/apify/apify-mcp-server)) | 2.4k | "Screenshot to HTML/Code" tool converts UI screenshots → HTML, Tailwind CSS, React. Also: web scraping, data extraction, search. | Hosted: `mcp.apify.com`. 1,031 commits. | Very active |
| **Storybook MCP (Official)** ([storybookjs/storybook-mcp](https://github.com/storybookjs/storybook-mcp)) | 264 | Component library as MCP tools: docs (metadata, stories, APIs), development (code generation reusing components), testing (component/accessibility tests, self-healing). | 1,346 commits. | Very active |
| **Anima MCP** | — | Converts Figma/Adobe XD/Sketch → HTML, React, Vue. Connects to AI assistants. | Commercial | Active |
| **Google Stitch MCP** | — | Open-source CLI to build production React components from Google Stitch designs. Integrates with Claude Code, Cursor. | CLI-based, open source | Active |
| **Frame0 MCP** ([niklauslee/frame0-mcp-server](https://github.com/niklauslee/frame0-mcp-server)) | — | Balsamiq alternative MCP. Create/modify wireframes via natural language. Requires Frame0 v1.7.0+. Open source. | Wireframing via NL | Active |
| **MockFlow WireframePro MCP** | — | Generates wireframes from prompts. Converts wireframes → React, Vue, HTML/CSS. MIT open source. | Prompt → wireframe → code | Active |

---

## Recommended Stack

| Layer | Recommended | Why |
|-------|-------------|-----|
| **Design → Code** | [21st MCP](https://github.com/21st-dev/magic) + [Apify MCP](https://github.com/apify/apify-mcp-server) | Framelink removed — Figma free tier too restrictive for API access. Use 21st for component generation + Apify for screenshot-to-code instead of Figma pipeline. |
| **Component Library** | [shadcn-ui MCP Server](https://github.com/Jpisnice/shadcn-ui-mcp-server) (2.9k stars) + [21st MCP](https://github.com/21st-dev/magic) (configured) | Best ecosystem + already in your toolchain |
| **Component Docs** | [Storybook MCP](https://github.com/storybookjs/storybook-mcp) (264 stars, official) | Deepest component library integration — docs, code gen, testing |
| **Accessibility Audit** | [a11ymcp](https://github.com/ronantakizawa/a11ymcp) (89 stars) or [accessibility-agents](https://github.com/Community-Access/accessibility-agents) (373 stars) | Best open-source WCAG coverage |
| **Visual Regression** | [Playwright MCP](https://github.com/microsoft/playwright-mcp) (configured) + [Happo](https://happo.io/docs/mcp) or [Applitools](https://github.com/applitools/eyes-mcp) | Screenshot capture (Playwright) + hosted diff review (Happo/Applitools) |
| **Design Tokens** | [Design Token Bridge MCP](https://github.com/kenneives/design-token-bridge-mcp) or [Southleft Design Systems MCP](https://design-systems-mcp.southleft.com/mcp) | Token translation (Bridge) vs. knowledge retrieval (Southleft) |
| **Prototyping** | [Penpot MCP](https://github.com/penpot/penpot) (342 stars) | Best open-source design-tool MCP — full design↔code roundtrip |
| **Screenshot → Code** | [Apify MCP](https://github.com/apify/apify-mcp-server) (2.4k stars) | Most mature dedicated screenshot-to-code tool |
