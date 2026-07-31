# skill-family-hub

Verified skill-family governance and release plugins for Claude Code, CodeBuddy/WorkBuddy, OpenAI Codex, and Kimi Code.

**Marketplace version:** `20260731103831`

This repository contains only the marketplace manifests — plugin implementations live in their own repositories.

## Add this marketplace

| Platform | Command |
| --- | --- |
| Claude Code | `/plugin marketplace add ifoohoo/skill-family-hub` |
| CodeBuddy / WorkBuddy | `/plugin marketplace add ifoohoo/skill-family-hub` |
| OpenAI Codex | `codex plugin marketplace add ifoohoo/skill-family-hub` |
| Kimi Code | `/plugins marketplace https://raw.githubusercontent.com/ifoohoo/skill-family-hub/main/kimi-marketplace.json` |

## Using HTTPS instead of SSH

Claude Code resolves GitHub `owner/repo` shorthand (including plugin entries with `source: "github"` in this marketplace) over SSH by default. If you do not have a GitHub account, SSH key, or SSH agent configured, set the following environment variable **before** launching Claude Code to force HTTPS cloning:

- **macOS / Linux:** `export CLAUDE_CODE_PLUGIN_PREFER_HTTPS=1`
- **Windows PowerShell:** `$env:CLAUDE_CODE_PLUGIN_PREFER_HTTPS='1'`

You can also add this marketplace via an explicit HTTPS URL:

```
/plugin marketplace add https://github.com/ifoohoo/skill-family-hub.git
```

The environment variable above also causes `owner/repo` shorthand plugin installations to use HTTPS. Public repositories cloned over HTTPS do not require a GitHub account.

> **Tip:** If Git still rewrites HTTPS URLs to SSH, check your local Git `url.*.insteadOf` configuration.

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

## Plugins

| Plugin | Version | Source | Claude Code | CodeBuddy | Codex | Kimi Code |
| --- | --- | --- | --- | --- | --- | --- |
| release-skill | 0.3.0 | `ifoohoo/release-skill` | ✓ | ✓ | ✓ | ✓ |
| skill-family-audit | 0.1.7-candidate | `ifoohoo/skill-family-audit` | — | — | ✓ | — |

「✓」means the plugin is listed in that platform's manifest; 「—」means it is not. The `platforms` field in the source is the sole explicit distribution switch; CodeBuddy/WorkBuddy's official fallback to `.claude-plugin/plugin.json` does not change distribution status.

After adding the marketplace, install plugins with your platform's plugin manager (e.g. `/plugin install <name>@skill-family-hub` in Claude Code).

## English Summary

**skill-family-hub** is the public marketplace index of verified skill-family governance and release plugins, targeting Claude Code, CodeBuddy/WorkBuddy, OpenAI Codex, and Kimi Code.

- Add the marketplace with the commands above, then install individual plugins through each platform's plugin manager.
- Currently distributed: `release-skill`, `skill-family-audit`. See the table for per-platform availability.
- Each plugin's version authority lives in its own repository (self-contained manifests and git tags); this index only references them.
- Licensed under MIT — see [LICENSE](LICENSE).
