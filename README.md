# ZAI Quota HUD

A Claude Code plugin that displays your ZAI/GLM Coding Plan token quota usage in the statusline.

![ZAI ██░░░ 37%](https://img.shields.io/badge/statusline-quota-brightgreen)

## Install

### Local

```bash
claude --plugin-dir /path/to/zai-usage-claude-code-plugin
```

Then run `/zai-quota-hud:setup` to configure the statusline. Restart Claude Code.

### Marketplace

```
/plugin install zai-quota-hud
```

Then `/zai-quota-hud:setup` and restart.

## What you see

Below the input bar:

```
ZAI ██░░░ 37%
```

Color changes automatically: green (< 50%), yellow (50-80%), red (> 80%).

## Commands

| Command | Description |
|---------|-------------|
| `/zai-quota-hud:setup` | Configure the statusline in Claude Code settings |
| `/zai-quota-hud:quota` | Show detailed quota breakdown (per-model) |

## Requirements

- Claude Code v1.0.80+
- Node.js 18+
- `ANTHROPIC_BASE_URL` and `ANTHROPIC_AUTH_TOKEN` environment variables set (ZAI or Zhipu endpoint)
