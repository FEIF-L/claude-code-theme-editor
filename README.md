<div align="center">

# 🎨 Claude Code Theme Editor

**Visual editor for [Claude Code](https://claude.com/claude-code) custom themes — pick colors, watch a live preview, copy a ready-to-use `theme.json`.**

English | [简体中文](./README.zh-CN.md)

[![Live Demo](https://img.shields.io/badge/▶_Live_Demo-13F4FB?style=for-the-badge&logoColor=black)](https://feif-l.github.io/claude-code-theme-editor/)
&nbsp;
[![License: MIT](https://img.shields.io/badge/License-MIT-D568E3?style=for-the-badge)](./LICENSE)
&nbsp;
![No dependencies](https://img.shields.io/badge/deps-zero-39FF14?style=for-the-badge)

![Claude Code Theme Editor](./assets/hero.svg)

</div>

---

## ✨ What is this?

A **single HTML file** that lets you design a Claude Code color theme visually. Drag color pickers on the right, watch a mock Claude Code terminal update instantly on the left, then export a `theme.json` with one click.

No build step. No dependencies. No server. Open the file (or the [live demo](https://feif-l.github.io/claude-code-theme-editor/)) and start.

## 🚀 Quick start

**Option A — use it online**

👉 **[Open the live editor](https://feif-l.github.io/claude-code-theme-editor/)**

**Option B — run it locally**

```bash
git clone https://github.com/FEIF-L/claude-code-theme-editor.git
cd claude-code-theme-editor
# just open index.html in a browser — no install needed
```

Then:

1. Edit colors on the right, watch the preview on the left.
2. Toggle **Simple / Full** and **中 / EN** as you like.
3. Click **Copy JSON to clipboard**.
4. Save it as a theme file:
   - macOS / Linux → `~/.claude/themes/my-theme.json`
   - Windows → `%USERPROFILE%\.claude\themes\my-theme.json`
5. In Claude Code, run `/theme` and pick it. Themes hot-reload on save — no restart.

## 🎯 Features

| | |
|---|---|
| 🖼️ **Live preview** | A mock Claude Code terminal reflects every change in real time |
| 🎚️ **Drag-and-drop pickers** | Color picker + hex input for every token, synced both ways |
| 🔀 **Simple / Full modes** | ~15 everyday tokens, or all **72** including internal ones |
| 🌐 **Bilingual UI** | Switch English ↔ 中文 on the fly — labels, descriptions, preview |
| 📋 **One-click export** | Copy JSON to clipboard or download a `.json` |
| ⚠️ **Known-issue flags** | Tokens with upstream bugs are marked so you're not surprised |

## 🎨 Theme file format

```json
{
  "name": "My Theme",
  "base": "dark",
  "overrides": {
    "claude": "#13F4FB",
    "text": "#18ECA5",
    "userMessageBackground": "#D568E3"
  }
}
```

- **`name`** — display name.
- **`base`** — `dark` or `light`; any token you don't override inherits from this preset.
- **`overrides`** — any subset of the 72 tokens. Unknown keys are ignored, so exporting all 72 is safe.

## 📚 Token reference

**72 tokens total** — 61 officially documented, 11 internal / reverse-engineered (Claude Code v2.1.x). Grouped into: Brand · Text · Status · Input Box / Mode · Diff · Fullscreen Backgrounds · Subagent Palette · Rate-Limit Bar · Brief Mode · Clawd Mascot · Rainbow.

The full enumerated list with descriptions lives inside the editor's **Full** mode. Token list credit: [cameronsjo's gist](https://gist.github.com/cameronsjo/34a6fb8ade2b44c8380e1a2adebbac2b).

## ⚠️ Known issues (upstream, not this tool)

Flagged with ⚠ in the editor:

- **Diff colors may not apply** — `diffAdded` / `diffRemoved` and friends are silently ignored on some versions; they resolve against the base theme instead of your overrides. See [#71543](https://github.com/anthropics/claude-code/issues/71543), [#85821](https://github.com/anthropics/claude-code/issues/85821).
- **User-message text isn't separately themeable** — there's no dedicated key; it uses the global `text` color. If `userMessageBackground` is bright, make sure `text` still contrasts.
- **`messageActionsBackground`** — removed since v2.1.140; the override is ignored.

## 🗺️ Roadmap

- [ ] 🎲 **Random seed** — generate a tasteful, usable palette with one click (contrast-checked, never all-white)
- [ ] 🖥️ Light-theme preview parity
- [ ] 📦 A gallery of community-submitted themes
- [ ] ♿ Built-in WCAG contrast checker per token

## 🤝 Contributing

Issues and PRs welcome. This is one self-contained `index.html` — no toolchain to set up. Just edit and open in a browser.

## 📄 License

[MIT](./LICENSE)
