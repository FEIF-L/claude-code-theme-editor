# Claude Code Theme Editor

English | [简体中文](./README.zh-CN.md)

A single-file, offline visual editor for [Claude Code](https://claude.com/claude-code) custom themes. Pick colors with drag-and-drop color pickers, watch a live mock of the Claude Code TUI update in real time, then copy a ready-to-use `theme.json` to your clipboard.

No build step, no dependencies, no server. Just open the HTML file in a browser.

## Features

- **Live preview** — a mock Claude Code terminal on the left updates as you edit.
- **Drag-and-drop color pickers** — plus a hex input for every token, kept in sync both ways.
- **Two modes**
  - **Simple** — ~15 everyday tokens (brand, text, status, permission, plan mode, user message, diff).
  - **Full** — all **72 tokens** (including internal/reverse-engineered ones: subagent palette, rainbow, mascot, rate-limit bar, etc.).
- **Bilingual UI** — switch between English and 中文 on the fly. Token descriptions and the preview are both translated.
- **One-click export** — copy JSON to clipboard, or download a `.json` file.
- **Known-issue markers** — tokens with upstream bugs are flagged with ⚠ (see below).

## Usage

1. Open `cc-theme-editor.html` in any modern browser.
2. Edit colors on the right; watch the preview on the left.
3. Toggle **Simple / Full** and **中 / EN** as needed.
4. Click **Copy JSON to clipboard**.
5. Save it to your Claude Code themes directory:
   - macOS / Linux: `~/.claude/themes/my-theme.json`
   - Windows: `%USERPROFILE%\.claude\themes\my-theme.json`
6. In Claude Code, run `/theme` and pick your custom theme. Claude Code watches the directory and hot-reloads on save — no restart needed.

## Theme file format

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

- `name` — display name.
- `base` — `dark` or `light`; every token you don't override inherits from this preset.
- `overrides` — any subset of the 72 tokens. Keys Claude Code doesn't recognize are ignored, so exporting all 72 is safe.

## Token reference (72 total)

61 are officially documented; 11 are internal / reverse-engineered from the binary (Claude Code v2.1.x). Grouped as: Brand/Accent, Text, Status, Input Box/Mode, Diff, Fullscreen Backgrounds, Subagent Palette, Rate-Limit Bar, Brief Mode, Clawd Mascot, Rainbow.

Full enumerated list with descriptions lives in the editor's Full mode. Token list credit: [cameronsjo's gist](https://gist.github.com/cameronsjo/34a6fb8ade2b44c8380e1a2adebbac2b).

## Known issues (upstream, not this tool)

These are flagged with ⚠ in the editor:

- **Diff colors may not apply** — [`diffAdded`](https://github.com/anthropics/claude-code/issues/71543) and the other `diff*` keys are reported to be silently ignored on some versions; they resolve against the base theme instead of your overrides ([#71543](https://github.com/anthropics/claude-code/issues/71543), [#85821](https://github.com/anthropics/claude-code/issues/85821)).
- **User message text color is not separately themeable** — there is no dedicated key for user-message text; it uses the global `text` color. If you set a bright `userMessageBackground`, make sure `text` still contrasts against it.
- **`messageActionsBackground`** — removed since v2.1.140; the override is ignored.

## License

MIT
