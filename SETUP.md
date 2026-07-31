# Setup Guide: UI/UX Design Toolchain for OpenCode

Step-by-step to replicate this toolchain. Assumes macOS with Node.js, npm, Python 3.10+, OpenCode already installed.

## 1. Core CLIs

```bash
# 21st.dev component marketplace
npm install -g @21st-dev/cli
21st login   # Opens browser for OAuth

# UI UX Pro Max skill (auto-installs 7 sub-skills)
npm install -g ui-ux-pro-max-cli
uipro init --ai opencode --global
```

## 2. Design MCP Servers (npm)

```bash
npm install -g a11y-mcp
npm install -g a11y-color-contrast-mcp
npm install -g @danielsogl/lighthouse-mcp
npm install -g design-token-bridge-mcp
npm install -g flowbite-mcp
npm install -g @magicuidesign/mcp
npm install -g tailwindcss-mcp-server
npm install -g mcp-image-compare-server
```

## 3. Design CLI Tools

```bash
npm install -g svgo
npm install -g stylelint stylelint-config-standard
```

## 4. Python Tools

```bash
pip3 install --break-system-packages manim
pip3 install --break-system-packages iflow-mcp-abhiemj-manim-mcp-server
```

## 5. WCAG MCP (manual setup)

```bash
mkdir -p ~/Projects/Design/wcag-mcp
git clone --depth 1 https://github.com/tsmd/wcag-mcp.git /tmp/wcag-mcp
cp -r /tmp/wcag-mcp/wcag-server/* ~/Projects/Design/wcag-mcp/
cd ~/Projects/Design/wcag-mcp && npm install
```

## 6. Skills (manual copy)

These go in `~/.opencode/skills/` and auto-activate:

```bash
# Taste skill (anti-slop design enforcement)
git clone --depth 1 https://github.com/Leonxlnx/taste-skill.git /tmp/taste-skill
mkdir -p ~/.opencode/skills/taste
cp /tmp/taste-skill/skills/taste-skill/SKILL.md ~/.opencode/skills/taste/

# GSAP skill (animation core API)
git clone --depth 1 https://github.com/greensock/gsap-skills.git /tmp/gsap-skills
mkdir -p ~/.opencode/skills/gsap
cp /tmp/gsap-skills/skills/gsap-core/SKILL.md ~/.opencode/skills/gsap/

# Motion Design skill (Disney animation principles for UI)
git clone --depth 1 https://github.com/LottieFiles/motion-design-skill.git /tmp/lottie-skill
cp -r /tmp/lottie-skill/skills/motion-design ~/.opencode/skills/
```

## 7. OpenCode Config (~/.config/opencode/opencode.json)

Add these to the `"mcp"` object:

```json
"21st": {
  "type": "remote",
  "url": "https://21st.dev/api/mcp",
  "headers": { "x-api-key": "YOUR_21ST_API_KEY" },
  "enabled": true
},
"a11y-color-contrast": {
  "type": "local",
  "command": ["a11y-color-contrast-mcp"],
  "enabled": true
},
"lighthouse": {
  "type": "local",
  "command": ["lighthouse-mcp-server"],
  "enabled": true
},
"manim": {
  "type": "local",
  "command": ["manim-mcp-server"],
  "enabled": true
},
"a11y": {
  "type": "local",
  "command": ["a11y-mcp"],
  "enabled": false
},
"design-token-bridge": {
  "type": "local",
  "command": ["design-token-bridge-mcp"],
  "enabled": false
},
"flowbite": {
  "type": "local",
  "command": ["flowbite-mcp"],
  "enabled": false
},
"magic-ui": {
  "type": "local",
  "command": ["node", "/opt/homebrew/lib/node_modules/@magicuidesign/mcp/dist/server.js"],
  "enabled": false
},
"tailwindcss": {
  "type": "local",
  "command": ["tailwindcss-server"],
  "enabled": false
},
"image-compare": {
  "type": "local",
  "command": ["mcp-image-compare"],
  "enabled": false
},
"wcag": {
  "type": "local",
  "command": ["node", "/Users/jacobgruber/Projects/Design/wcag-mcp/wcag-server.js"],
  "enabled": false
},
"apify": {
  "type": "remote",
  "url": "https://mcp.apify.com",
  "enabled": false
},
"southleft-design": {
  "type": "remote",
  "url": "https://design-systems-mcp.southleft.com/mcp",
  "enabled": false
}
```

Add to both `"permission"` and `"agent"."supervisor"."permission"`:

```json
"21st_*": "allow",
"a11y_*": "allow",
"a11y-color-contrast_*": "allow",
"lighthouse_*": "allow",
"manim_*": "allow",
"design-token-bridge_*": "allow",
"flowbite_*": "allow",
"magic-ui_*": "allow",
"tailwindcss_*": "allow",
"image-compare_*": "allow",
"wcag_*": "allow",
"apify_*": "allow",
"southleft-design_*": "allow"
```

## 8. Verify

Test each MCP starts:

```bash
echo '{"jsonrpc":"2.0","id":1,"method":"initialize","params":{"protocolVersion":"2024-11-05","capabilities":{},"clientInfo":{"name":"test","version":"1.0"}}}' | a11y-mcp
echo '...' | a11y-color-contrast-mcp
echo '...' | lighthouse-mcp-server
echo '...' | manim-mcp-server
echo '...' | design-token-bridge-mcp
echo '...' | flowbite-mcp
echo '...' | tailwindcss-server
echo '...' | mcp-image-compare
```

Restart OpenCode. All 6 always-on MCPs should connect. Toggle others from the GUI as needed.

---

**Important:** Replace absolute paths (`/Users/jacobgruber/`, `/opt/homebrew/`) with your own. The 21st API key comes from `https://21st.dev/mcp` after logging in. The wcag-mcp path should point to wherever you cloned it.
