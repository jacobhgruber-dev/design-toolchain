# Design APIs & Platforms — Reference

Catalog of APIs, platforms, and services for UI/UX design that integrate with AI coding workflows.

---

## Design APIs (Color, Fonts, Logo)

| Service | URL | Category | Description | Pricing |
|---------|-----|----------|-------------|---------|
| **Google Cloud Vision** | [cloud.google.com/vision](https://cloud.google.com/vision) | Color + Logo | Dominant colors, logo detection, OCR in one API | Freemium: 1K/mo free, $1.50/1K |
| **Context.dev** | [context.dev](https://context.dev) | Color + Fonts | Extracts brand colors + fonts from any domain. Crawls homepage CSS, manifests, rendered DOM | Freemium: 500 credits free; $25/mo |
| **Color Thief** | [github.com/lokesh/color-thief](https://github.com/lokesh/color-thief) | Color | JS library for dominant color & palette extraction. v3 supports OKLCH, WCAG contrast, Display P3 | Free (MIT) |
| **Mixfont** | [mixfont.com](https://mixfont.com) | Font | AI font recognition from screenshots. Isolates text and returns ranked open-source font matches | Freemium: 50 free credits; $20/mo |
| **Google Fonts API** | [developers.google.com/fonts](https://developers.google.com/fonts) | Font | Metadata for all Google Fonts families. No key required | Free, unlimited |
| **Clarifai** | [clarifai.com](https://clarifai.com) | Logo | Pre-trained logo detection (6,500+ logos) + custom model training | Freemium: 1K ops/mo free; $30/mo |
| **Brandfetch** | [brandfetch.com](https://brandfetch.com) | Logo lookup | Logo CDN by domain — returns logos in multiple formats/themes | Freemium: 500K req/mo free |
| **Logo.dev** | [logo.dev](https://logo.dev) | Logo lookup | Logo images for 50M+ companies by domain/name/ticker | Freemium: 500K req/mo free |
| **Amazon Rekognition** | [aws.amazon.com/rekognition](https://aws.amazon.com/rekognition) | Logo | Deep learning logo detection via DetectLabels | Freemium: 1K images/mo free |

---

## Screenshot-to-Code APIs

| Service | URL | Description | Pricing |
|---------|-----|-------------|---------|
| **screenshot-to-code (OSS)** | [github.com/abi/screenshot-to-code](https://github.com/abi/screenshot-to-code) | Converts screenshots/Figma/mockups → HTML, React, Vue. Uses GPT-4o, Claude, Gemini | Free (self-host); Hosted: $29–$99/mo |
| **Vercel v0 Platform API** | [v0.dev](https://v0.dev) | AI code gen from prompts + images → React + Tailwind + Shadcn. Public beta API | Freemium; Premium/Team for API |
| **Builder.io Visual Copilot** | [builder.io](https://builder.io) | Figma → React, Vue, Angular with component mapping. MCP server for AI agents | Freemium |
| **Anima** | [animaapp.com](https://animaapp.com) | Design-to-code from Figma, screenshots, prompts. SDK GA Q2 2025 | Freemium: 5 gens/day; $20–$500+/mo |
| **Codia AI** | [codia.ai](https://codia.ai) | Screenshots/Figma/PDF → design tokens + code (React, Vue, Flutter, iOS, Android) | $49/mo+ |
| **Google Stitch** | [ai.google.dev/stitch](https://ai.google.dev/stitch) | Text + sketches → HTML, React, Vue, Flutter, SwiftUI | Free (beta) |
| **Tempo Labs** | [tempo.new](https://tempo.new) | AI visual IDE for React. REST API with OAuth 2.0 | Freemium |

---

## Accessibility Audit APIs

| Service | URL | Description | Pricing |
|---------|-----|-------------|---------|
| **Deque axe-core** | [deque.com/axe](https://deque.com/axe) | Industry-standard engine. Open-source core; DevTools adds CI/CD, dashboards, MCP | Free (OSS) / $500–1K/seat/yr (Pro) |
| **WAVE API (WebAIM)** | [wave.webaim.org/api](https://wave.webaim.org/api) | Automated accessibility analysis after JS rendering. JSON/XML output | Freemium: 100 free; $0.04/credit |
| **Evinced** | [evinced.com](https://evinced.com) | AI-powered using computer vision. MCP tools for agentic coding | Enterprise (~$500–2K/mo) |
| **PageBolt /audit** | [pagebolt.com](https://pagebolt.com) | axe-core-powered /audit endpoint. WCAG 2.0/2.1/2.2 + Section 508 | Freemium: 100 req/mo free; $9–$199/mo |
| **AccessibilityChecker.org** | [accessibilitychecker.org](https://accessibilitychecker.org) | WCAG 2.1 checks + AI remediation (SmartFix). PDF reports, CI/CD integration | $69–$249/domain/mo |

---

## Visual Comparison / Visual Regression APIs

| Service | URL | Description | Pricing |
|---------|-----|-------------|---------|
| **Percy (BrowserStack)** | [percy.io](https://percy.io) | AI-powered visual testing. Cross-browser screenshots, visual diffs, AI review agent | Freemium: 5K screenshots/mo free; $199/mo |
| **Chromatic** | [chromatic.com](https://chromatic.com) | Built for Storybook/Playwright/Cypress. GraphQL API. Accessibility testing included | Freemium: 5K snapshots/mo free; $179–$399/mo |
| **Applitools Eyes** | [applitools.com](https://applitools.com) | Computer vision AI detects meaningful regressions. Self-healing | Freemium: 100 checkpoints/mo free; $99–$199/mo |
| **RegressionBot** | [regressionbot.com](https://regressionbot.com) | API-first (OpenAPI spec + TypeScript SDK). AI summaries explain what changed | Paid: from $9/mo |
| **Happo** | [happo.io](https://happo.io) | Cross-browser (Chrome, Firefox, Safari, Edge, iOS). No per-seat pricing | Freemium: 5K snapshots/mo free; $125–$399/mo |
| **Argos** | [argos-ci.com](https://argos-ci.com) | Open-source with managed SaaS. Playwright/Cypress/Storybook integration | Freemium: 5K screenshots/mo free; $100–$1K/mo |

---

## Design Token APIs

| Service | URL | Description | Pricing |
|---------|-----|-------------|---------|
| **Style Dictionary** | [amzn.github.io/style-dictionary](https://amzn.github.io/style-dictionary) | Canonical open-source token build system. v5 supports W3C DTCG spec. Transforms to CSS, Sass, JS, iOS, Android | Free (MIT/Apache) |
| **Tokens Studio** | [tokens.studio](https://tokens.studio) | Figma plugin + standalone. W3C DTCG compliant. Bidirectional sync with Git, Supernova, JSONBin | Freemium: €17–€499/mo |
| **Supernova** | [supernova.io](https://supernova.io) | Full design system platform. SDK, CLI, REST API, MCP server (Supernova Relay) | Freemium: $20–$35/seat/mo |
| **Zeplin** | [zeplin.io](https://zeplin.io) | Design handoff platform with auto-generated tokens. MCP server (2025) | Freemium; Team/Enterprise paid |
| **Zeroheight** | [zeroheight.com](https://zeroheight.com) | Design system docs + token manager. Uses Style Dictionary v5 + W3C DTCG | Freemium: free 1 editor; $49/editor/mo |

---

## Icon APIs

| Service | URL | Description | Pricing |
|---------|-----|-------------|---------|
| **Iconify** | [iconify.design](https://iconify.design) | Unified framework for 200K+ icons from 100+ sets. On-demand SVG via REST. No auth | Free (MIT) |
| **Font Awesome** | [fontawesome.com](https://fontawesome.com) | 30K+ icons. GraphQL API for search and metadata. Private npm registry for Pro | Free tier; Pro from $99/yr |
| **Lucide Icons** | [lucide.dev](https://lucide.dev) | 1.5K+ tree-shakable SVG icons. Fork of Feather | Free (ISC) |
| **Simple Icons** | [simpleicons.org](https://simpleicons.org) | 3.4K+ brand SVG icons. Programmatic API. CC0 license | Free (CC0) |
| **Phosphor Icons** | [phosphoricons.com](https://phosphoricons.com) | 9K+ icons in 6 weights (Thin, Light, Regular, Bold, Fill, Duotone) | Free (MIT) |
| **Tabler Icons** | [tabler-icons.io](https://tabler-icons.io) | 6.1K+ MIT-licensed outline icons. SVG sprite for `<use>` tag integration | Free (MIT) |

---

## Illustration/Asset Generation APIs

| Service | URL | Description | Pricing |
|---------|-----|-------------|---------|
| **OpenAI (GPT-Image / DALL-E)** | [platform.openai.com](https://platform.openai.com) | GPT-Image 1.5: state-of-the-art text-to-image with exceptional text rendering | $0.005–$0.17/image |
| **Google Gemini / Imagen** | [ai.google.dev](https://ai.google.dev) | Gemini 3.1 Flash Image + Imagen 4. Free tier: 500–1K images/day via AI Studio | $0.02–$0.151/image |
| **Replicate** | [replicate.com](https://replicate.com) | Unified API for thousands of models: FLUX, Stable Diffusion, Ideogram, Recraft | $0.003–$0.09/image |
| **Stability AI** | [stability.ai](https://stability.ai) | Stable Diffusion 3.5 + editing APIs (inpaint, outpaint, upscale, background removal) | $0.002–$0.08/image |
| **Ideogram** | [ideogram.ai](https://ideogram.ai) | Specializes in accurate text rendering in images. Key differentiator for UI mockups | $0.03–$0.10/image |

---

## Design Handoff & Collaboration APIs

| Service | URL | Description | Pricing |
|---------|-----|-------------|---------|
| **Figma REST API + MCP** | [figma.com/developers/api](https://figma.com/developers/api) | Read file contents (JSON node tree), styles, components, variables. MCP server for AI agents | Free (Figma seat required for MCP) |
| **Zeplin API + MCP** | [zeplin.io](https://zeplin.io) | Design specs, assets, tokens from Figma/Sketch/XD. MCP server | Freemium |
| **Anima SDK** | [animaapp.com](https://animaapp.com) | Programmatic design-to-code. Accepts Figma links → React, HTML, Vue with Tailwind, MUI, Radix | Freemium: 5 gens/mo; $20–$500+/mo |
| **Builder.io Fusion** | [builder.io](https://builder.io) | Figma → framework code mapping to real project components. MCP server | Freemium; Fusion Pro: $24/user/mo |
| **Liveblocks** | [liveblocks.io](https://liveblocks.io) | Complete collaboration: presence, cursors, CRDT storage, comments, AI Copilots (v3.0) | Freemium: Pro $25/mo; Team $500+/mo |
| **Yjs** | [docs.yjs.dev](https://docs.yjs.dev) | Dominant open-source CRDT for real-time collaboration. Shared data types, offline support | Free (MIT) |

---

## Recommended Stack

| Layer | Best Service | Runner-up | Rationale |
|-------|-------------|-----------|-----------|
| Design data extraction | Figma MCP + Context.dev | Google Cloud Vision | Free first-party + URL-based brand extraction |
| Screenshot → Code | screenshot-to-code (OSS) | Vercel v0 API | Full control, self-hostable, multi-model |
| Accessibility | axe-core + PageBolt | Evinced (enterprise) | Free engine, lightweight REST |
| Visual regression | Percy | RegressionBot | Scale, ecosystem, AI features |
| Design tokens | Style Dictionary v5 + Tokens Studio | Supernova (with MCP) | Free transform engine + Figma sync |
| Icons | Iconify | Font Awesome | Only free REST API; 200K+ icons, no auth |
| Illustration/Assets | Replicate + OpenAI | Google Gemini | One API for all models + best text-in-image |
| Component discovery | shadcn/ui registry + Storybook MCP | Bit.dev | Only programmatic options available |
| Design handoff | Figma MCP + Anima SDK | Zeplin MCP | First-party data + mature code-gen |
| Collaboration | Liveblocks | Yjs + PartyKit | Turnkey multiplayer + AI Copilot |
