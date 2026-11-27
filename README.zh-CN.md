# skill-family-hub

[English](README.md)

面向 Claude Code、CodeBuddy/WorkBuddy、OpenAI Codex、Kimi Code 与 Qoder 的技能族全生命周期插件市场。收录进本市场的每个插件都绑定了经核验的 Git 标签与完整提交哈希。

**市场版本：** `20261127225800`

本仓库只发布多平台市场索引清单；各插件的业务代码、版本标签与发布记录均在其各自源仓库内独立维护。

## 添加市场

在所用宿主环境中执行对应命令，即可接入本市场：

| 平台 | 命令 |
| --- | --- |
| Claude Code | `/plugin marketplace add ifoohoo/skill-family-hub` |
| CodeBuddy / WorkBuddy | `/plugin marketplace add ifoohoo/skill-family-hub` |
| OpenAI Codex | `codex plugin marketplace add ifoohoo/skill-family-hub` |
| Kimi Code | `/plugins marketplace https://raw.githubusercontent.com/ifoohoo/skill-family-hub/main/kimi-marketplace.json` |
| Qoder | `qoder plugins marketplace add https://github.com/ifoohoo/skill-family-hub --scope user` |

## 使用 HTTPS 拉取（免配 SSH）

Claude Code 默认通过 SSH 解析 GitHub 的 `owner/repo` 简写（含本市场中 `source: "github"` 的插件条目）。如果本机未配置 GitHub 账号、SSH 密钥或 SSH Agent，请在启动 Claude Code **之前**设置以下环境变量，强制改走 HTTPS 克隆：

- **macOS / Linux：** `export CLAUDE_CODE_PLUGIN_PREFER_HTTPS=1`
- **Windows PowerShell：** `$env:CLAUDE_CODE_PLUGIN_PREFER_HTTPS='1'`

也可以直接用完整 HTTPS 地址添加市场：

```
/plugin marketplace add https://github.com/ifoohoo/skill-family-hub.git
```

设置上述环境变量后，后续通过 `owner/repo` 简写安装具体插件时也会走 HTTPS；公开仓库走 HTTPS 拉取无需登录 GitHub。

> 若设置后 Git 仍把 HTTPS 地址改写成 SSH，请检查本机 Git 配置中是否存在 `url.*.insteadOf` 规则。

## 国内用户下载加速方式

如果网络环境无法直连 GitHub，可在本地配置 Git URL 改写规则，通过第三方下载代理拉取本站在 GitHub 上公开发布的仓库。下面以 `ghfast.top` 为例：

```bash
git config --global \
  url."https://ghfast.top/https://github.com/ifoohoo/".insteadOf \
  "https://github.com/ifoohoo/"
```

配置完成后，照常执行上方的添加市场与安装插件命令即可。这项改写只作用于本机 Git 下载地址，市场清单和插件清单记录的权威 GitHub 仓库坐标不会改变。

> **安全与版本核验边界：** 本站技能最终以 GitHub 上由 `ifoohoo` 维护的仓库为准。`ghfast.top` 属于第三方下载代理，并非本站官方镜像，也不参与版本发布。该方式仅限公开仓库的只读拉取；不要通过代理访问私有仓库，也绝不要向代理发送 GitHub Token、密码等敏感凭证。若代理中断或缓存滞后导致取不到插件锁定的 Git Tag 与完整 Commit SHA，请立即停止安装。

查看本机当前生效的 URL 改写规则：

```bash
git config --global --get-regexp '^url\..*\.insteadof$'
```

网络恢复直连或不再需要代理时，执行以下命令移除改写：

```bash
git config --global --unset-all \
  url."https://ghfast.top/https://github.com/ifoohoo/".insteadOf
```

## 已收录插件

| 插件 | 版本 | 源仓库 | Claude Code | CodeBuddy | Codex | Kimi Code | Qoder |
| --- | --- | --- | --- | --- | --- | --- | --- |
| foundation-adoption-review | 0.39.2 | `ifoohoo/foundation-adoption-review` · [在线文档](https://ifoohoo.github.io/skill-family-foundation-site/) | ✓ | ✓ | ✓ | ✓ | ✓ |
| release-skill | 0.10.5 | `ifoohoo/release-skill` | ✓ | ✓ | ✓ | ✓ | ✓ |
| skill-failure-auditor | 1.1.19 | `ifoohoo/skill-failure-auditor` | ✓ | ✓ | ✓ | ✓ | — |
| skill-family-audit | 1.1.67 | `ifoohoo/skill-family-audit` | ✓ | ✓ | ✓ | — | — |
| skill-family-docs | 0.7.0 | `ifoohoo/skill-family-docs` · [在线文档](https://ifoohoo.github.io/skill-family-doc-render-site/) | ✓ | ✓ | ✓ | ✓ | — |
| skill-family-test | 0.2.4 | `ifoohoo/skill-family-test` | ✓ | ✓ | ✓ | ✓ | ✓ |

表中“✓”表示该插件已写入对应宿主的市场清单，“—”表示未向该宿主分发。各平台是否分发完全取决于事实源中的 `platforms` 显式开关；即使 CodeBuddy/WorkBuddy 支持回退读取 `.claude-plugin/plugin.json`，也不会在开关关闭时自动混入分发清单。

添加市场后，即可通过所用宿主的插件管理器按需安装，例如在 Claude Code 中执行 `/plugin install <name>@skill-family-hub`。

使用 `skill-family-test` 插件执行测试计划校验、运行收据核收或增量失效计算时，请同步在目标项目或运行环境中安装配套公开 npm 包 `skill-family-test`（提供 `sft` 命令行工具）：`pnpm add -D skill-family-test` 或 `npm install -D skill-family-test`。

## Google Antigravity 直装指引

Google Antigravity 通过官方中心目录管理插件，第三方技能族插件可直接将对应发布标签克隆至 `~/.gemini/config/plugins/<插件名>` 由宿主自动识别加载：

- `foundation-adoption-review`（`0.39.2`）：`git clone --branch foundation-adoption-review-v0.39.2 https://github.com/ifoohoo/foundation-adoption-review.git ~/.gemini/config/plugins/foundation-adoption-review`
- `release-skill`（`0.10.5`）：`git clone --branch release-skill-v0.10.5 https://github.com/ifoohoo/release-skill.git ~/.gemini/config/plugins/release-skill`
- `skill-failure-auditor`（`1.1.19`）：`git clone --branch skill-failure-auditor-v1.1.19 https://github.com/ifoohoo/skill-failure-auditor.git ~/.gemini/config/plugins/skill-failure-auditor`
- `skill-family-audit`（`1.1.67`）：`git clone --branch skill-family-audit-v1.1.67 https://github.com/ifoohoo/skill-family-audit.git ~/.gemini/config/plugins/skill-family-audit`
- `skill-family-docs`（`0.7.0`）：`git clone --branch skill-family-docs-v0.7.0 https://github.com/ifoohoo/skill-family-docs.git ~/.gemini/config/plugins/skill-family-docs`
- `skill-family-test`（`0.2.4`）：`git clone --branch skill-family-test-v0.2.4 https://github.com/ifoohoo/skill-family-test.git ~/.gemini/config/plugins/skill-family-test`

## 已退役归档与迁移指引

以下插件已从新用户默认推荐安装清单中移除，仅保留归档说明供存量用户查阅与平滑迁移：

- **`loop-agent`（归档版本 `0.5.1`）：** 证据封存与评测判据契约已分别归并入 skill-family-contracts 与 skill-family-eval，本独立插件已转为退役归档状态。 该插件已由 `skill-family-eval` 接替，请通过公开 npm 包 `npm install -g skill-family-eval` 安装迁移。

## 关于这个市场

- 当前收录：`foundation-adoption-review`、`release-skill`、`skill-failure-auditor`、`skill-family-audit`、`skill-family-docs`、`skill-family-test`。各宿主平台的具体开放情况以上表为准。
- 插件版本权威归属各插件自身仓库的清单与不可变 Git Tag，本市场仅引用已完成核验的发布坐标。
- 采用 MIT 许可证发布，详见 [LICENSE](LICENSE)。
