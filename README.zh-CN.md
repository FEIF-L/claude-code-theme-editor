# Claude Code 主题编辑器

[English](./README.md) | 简体中文

一个单文件、离线的 [Claude Code](https://claude.com/claude-code) 自定义主题可视化编辑器。用拖拽调色盘选颜色,左侧实时预览 Claude Code 界面,选好后一键把 `theme.json` 复制到剪贴板。

无需构建、无依赖、无服务器。浏览器打开 HTML 即可用。

## 功能

- **实时预览** —— 左侧模拟 Claude Code 终端,边改边看。
- **拖拽调色盘** —— 每个 token 都有调色盘 + hex 输入框,双向同步。
- **两种模式**
  - **简单** —— 约 15 个常用 token(品牌、文字、状态、权限、Plan 模式、用户消息、diff)。
  - **完整** —— 全部 **72 个 token**(含逆向出来的内部键:子代理调色板、彩虹、吉祥物、速率条等)。
- **中英双语界面** —— 随时切换,token 说明和预览都会翻译。
- **一键导出** —— 复制 JSON 到剪贴板,或下载 `.json` 文件。
- **问题标记** —— 有上游 bug 的 token 标了 ⚠(见下)。

## 使用

1. 浏览器打开 `cc-theme-editor.html`。
2. 右侧改颜色,左侧看预览。
3. 按需切换 **简单 / 完整** 和 **中 / EN**。
4. 点 **复制 JSON 到剪贴板**。
5. 存到 Claude Code 主题目录:
   - macOS / Linux:`~/.claude/themes/my-theme.json`
   - Windows:`%USERPROFILE%\.claude\themes\my-theme.json`
6. 在 Claude Code 里运行 `/theme` 选你的自定义主题。Claude Code 会监听该目录、保存即热重载,无需重启。

## 主题文件格式

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

- `name` —— 显示名。
- `base` —— `dark` 或 `light`;没覆盖的 token 都从这个预设继承。
- `overrides` —— 72 个 token 的任意子集。Claude Code 不认识的键会被忽略,所以全导出 72 个也安全。

## Token 参考(共 72 个)

61 个官方文档化,11 个是从二进制逆向出来的内部键(Claude Code v2.1.x)。分组:品牌/强调色、文字、状态、输入框/模式、Diff、全屏背景、子代理调色板、速率条、Brief 模式、Clawd 吉祥物、彩虹。

完整键名 + 说明在编辑器「完整」模式里。Token 列表来源:[cameronsjo 的 gist](https://gist.github.com/cameronsjo/34a6fb8ade2b44c8380e1a2adebbac2b)。

## 已知问题(上游 bug,非本工具)

编辑器里用 ⚠ 标记:

- **Diff 颜色可能不生效** —— [`diffAdded`](https://github.com/anthropics/claude-code/issues/71543) 等 `diff*` 键在部分版本被静默忽略,会去读 base 主题而不是你的 override([#71543](https://github.com/anthropics/claude-code/issues/71543)、[#85821](https://github.com/anthropics/claude-code/issues/85821))。
- **用户消息文字色无法单独设置** —— 没有专属键控制用户消息文字,它用全局 `text` 色。如果 `userMessageBackground` 设得很亮,注意 `text` 要跟它有足够对比。
- **`messageActionsBackground`** —— v2.1.140 起已移除,override 被忽略。

## 许可

MIT
