# ZAI Quota HUD

[中文](README.zh-CN.md)

A Claude Code plugin that displays your ZAI/GLM Coding Plan token quota usage in the statusline.

![ZAI ██░░░ 37%](https://img.shields.io/badge/statusline-quota-brightgreen) ![License](https://img.shields.io/github/license/n1majne3/zai-quota-hud) ![Stars](https://img.shields.io/github/stars/n1majne3/zai-quota-hud)

## Install

Inside a Claude Code instance, run the following commands:

**Step 1: Add the marketplace**

```
/plugin marketplace add n1majne3/zai-quota-hud
```

**Step 2: Install the plugin**

```
/plugin install zai-quota-hud
```

After that, reload plugins:

```
/reload-plugins
```

**Step 3: Configure the statusline**

```
/zai-quota-hud:setup
```

Done! Restart Claude Code to load the new statusLine config, then the HUD will appear.

### Manual Install

If you prefer not to use the marketplace:

```bash
git clone https://github.com/n1majne3/zai-quota-hud.git ~/.claude/plugins/zai-quota-hud
claude --plugin-dir ~/.claude/plugins/zai-quota-hud
```

Then run `/zai-quota-hud:setup` and restart Claude Code.

## What you see

Below the input bar:

```
ZAI ██░░░ 37%
```

Color changes automatically: green (< 50%), yellow (50-80%), red (> 80%).

At 100% usage, a countdown timer shows time until reset:

```
ZAI █████ 100% ⏳ 1h 23m
```

## Commands

| Command | Description |
|---------|-------------|
| `/zai-quota-hud:setup` | Configure the statusline in Claude Code settings |
| `/zai-quota-hud:quota` | Show detailed quota breakdown (per-model) |

## Requirements

- Claude Code v1.0.80+
- Node.js 18+
- `ANTHROPIC_BASE_URL` and `ANTHROPIC_AUTH_TOKEN` environment variables set (ZAI or Zhipu endpoint)

## License

MIT — see [LICENSE](LICENSE)

## 友情链接

- [Linux Do 社区](https://linux.do/)  
