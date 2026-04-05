# ZAI 配额 HUD

一个 Claude Code 插件，在状态栏中显示你的 ZAI/GLM Coding Plan 令牌配额使用情况。

![ZAI ██░░░ 37%](https://img.shields.io/badge/statusline-quota-brightgreen) ![License](https://img.shields.io/github/license/n1majne3/zai-quota-hud) ![Stars](https://img.shields.io/github/stars/n1majne3/zai-quota-hud)

[English](README.md)

## 安装

在 Claude Code 实例中，运行以下命令：

**第一步：添加市场**

```
/plugin marketplace add n1majne3/zai-quota-hud
```

**第二步：安装插件**

```
/plugin install zai-quota-hud
```

之后，重新加载插件：

```
/reload-plugins
```

**第三步：配置状态栏**

```
/zai-quota-hud:setup
```

完成！重启 Claude Code 以加载新的 statusLine 配置，HUD 即会出现。

### 手动安装

如果你不想使用市场：

```bash
git clone https://github.com/n1majne3/zai-quota-hud.git ~/.claude/plugins/zai-quota-hud
claude --plugin-dir ~/.claude/plugins/zai-quota-hud
```

然后运行 `/zai-quota-hud:setup` 并重启 Claude Code。

## 显示效果

在输入栏下方：

```
ZAI ██░░░ 37%
```

颜色自动变化：绿色（< 50%）、黄色（50-80%）、红色（> 80%）。

使用量达到 100% 时，会显示重置倒计时：

```
ZAI █████ 100% ⏳ 1h 23m
```

## 命令

| 命令 | 说明 |
|------|------|
| `/zai-quota-hud:setup` | 在 Claude Code 设置中配置状态栏 |
| `/zai-quota-hud:quota` | 显示详细的配额明细（按模型） |

## 要求

- Claude Code v1.0.80+
- Node.js 18+
- 已设置 `ANTHROPIC_BASE_URL` 和 `ANTHROPIC_AUTH_TOKEN` 环境变量（ZAI 或智谱端点）

## 许可证

MIT — 详见 [LICENSE](LICENSE)
