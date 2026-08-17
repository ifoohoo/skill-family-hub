# skill-family-hub

[English](README.md)

这是一个面向 Claude Code、CodeBuddy/WorkBuddy、OpenAI Codex 和 Kimi Code 的技能族全生命周期插件市场。进入市场的插件都带有经过核验的发布坐标。

**市场版本：** `20260817185130`

这个仓库只存放市场清单。每个插件的实现、版本和发布记录都在各自的仓库中维护。

## 添加市场

| 平台 | 命令 |
| --- | --- |
| Claude Code | `/plugin marketplace add ifoohoo/skill-family-hub` |
| CodeBuddy / WorkBuddy | `/plugin marketplace add ifoohoo/skill-family-hub` |
| OpenAI Codex | `codex plugin marketplace add ifoohoo/skill-family-hub` |
| Kimi Code | `/plugins marketplace https://raw.githubusercontent.com/ifoohoo/skill-family-hub/main/kimi-marketplace.json` |

## 使用 HTTPS，不走 SSH

Claude Code 默认会通过 SSH 解析 GitHub 的 `owner/repo` 简写，本市场中使用 `source: "github"` 的插件也一样。如果本机没有配置 GitHub 账号、SSH 密钥或 SSH Agent，请在启动 Claude Code **之前**设置下面的环境变量，强制使用 HTTPS：

- **macOS / Linux：** `export CLAUDE_CODE_PLUGIN_PREFER_HTTPS=1`
- **Windows PowerShell：** `$env:CLAUDE_CODE_PLUGIN_PREFER_HTTPS='1'`

也可以直接使用完整 HTTPS 地址添加市场：

```
/plugin marketplace add https://github.com/ifoohoo/skill-family-hub.git
```

设置该环境变量后，通过 `owner/repo` 简写安装插件时也会改用 HTTPS。公开仓库通过 HTTPS 拉取，不需要登录 GitHub。

> 如果 Git 仍然把 HTTPS 改写成 SSH，请检查本机的 `url.*.insteadOf` 配置。

## 国内用户下载加速方式

没有科学上网的手段，又需要拉取本站技能时，可参考下面的配置，让 Git 通过第三方下载代理访问本站在 GitHub 上公开发布的仓库。下面以 `ghfast.top` 为例：

```bash
git config --global \
  url."https://ghfast.top/https://github.com/ifoohoo/".insteadOf \
  "https://github.com/ifoohoo/"
```

配置以后照常使用上面的安装命令即可。Git 只会在本机改写实际下载地址，市场清单和插件清单里记录的 GitHub 仓库地址不会改变。

> **请注意：** 本站技能最终以 GitHub 上由 `ifoohoo` 维护的仓库为准。`ghfast.top` 是第三方下载代理，不是本站维护的镜像，也不参与版本发布。这种方式只适合公开仓库的只读拉取；不要通过代理访问私有仓库，也不要向代理发送 GitHub Token、密码等凭证。第三方代理可能中断服务或出现缓存延迟；市场仍以插件的 Git Tag 和完整 Commit SHA 核对版本，取不到对应提交时应停止安装。

查看当前 URL 改写配置：

```bash
git config --global --get-regexp '^url\..*\.insteadof$'
```

不再需要代理时，可以删除这项配置：

```bash
git config --global --unset-all \
  url."https://ghfast.top/https://github.com/ifoohoo/".insteadOf
```

## 已收录插件

| 插件 | 版本 | 源仓库 | Claude Code | CodeBuddy | Codex | Kimi Code |
| --- | --- | --- | --- | --- | --- | --- |
| loop-agent | 0.3.0 | `mzdbxqh/loop-agent` | ✓ | — | ✓ | — |
| release-skill | 0.5.0 | `ifoohoo/release-skill` | ✓ | ✓ | ✓ | ✓ |
| skill-failure-auditor | 1.0.0 | `ifoohoo/skill-failure-auditor` | ✓ | ✓ | ✓ | ✓ |
| skill-family-audit | 1.0.0 | `ifoohoo/skill-family-audit` | — | — | ✓ | — |
| skill-family-docs | 0.1.1 | `ifoohoo/skill-family-docs` | — | ✓ | — | ✓ |

“✓”表示该插件已进入对应平台的市场清单，“—”表示没有进入。是否分发只看真源中的 `platforms` 开关；CodeBuddy/WorkBuddy 即使可以回退读取 `.claude-plugin/plugin.json`，也不会因此自动开启分发。

添加市场后，请使用对应平台的插件管理器安装具体插件。例如在 Claude Code 中执行 `/plugin install <name>@skill-family-hub`。

## 关于这个市场

- 当前收录：`loop-agent`、`release-skill`、`skill-failure-auditor`、`skill-family-audit`、`skill-family-docs`。各平台是否可用，以表格为准。
- 每个插件的版本以自身仓库中的清单和 Git Tag 为准，本市场只引用已经核验的发布坐标。
- 采用 MIT 许可证，详见 [LICENSE](LICENSE)。
