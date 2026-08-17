# skill-family-hub

[简体中文](README.zh-CN.md)

Verified skill-family lifecycle plugins for Claude Code, CodeBuddy/WorkBuddy, OpenAI Codex, and Kimi Code.

**Marketplace version:** `20260818004656`

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

## Download acceleration for users in mainland China

If direct GitHub access is unavailable, you may configure Git to use a third-party download proxy for this organization's public repositories. The following example uses `ghfast.top`:

```bash
git config --global \
  url."https://ghfast.top/https://github.com/ifoohoo/".insteadOf \
  "https://github.com/ifoohoo/"
```

The rewrite is local to your Git configuration. Marketplace and plugin manifests continue to reference the canonical GitHub repositories.

> **Source and security:** Repositories maintained by `ifoohoo` on GitHub are the source of truth. `ghfast.top` is a third-party proxy, not an official mirror. Use it only for read-only access to public repositories. Never send GitHub tokens, passwords, or private-repository traffic through the proxy. Stop the installation if the pinned Git tag and full commit SHA cannot be retrieved.

Inspect active URL rewrites:

```bash
git config --global --get-regexp '^url\..*\.insteadof$'
```

Remove the rewrite when it is no longer needed:

```bash
git config --global --unset-all \
  url."https://ghfast.top/https://github.com/ifoohoo/".insteadOf
```

## Plugins

| Plugin | Version | Source | Claude Code | CodeBuddy | Codex | Kimi Code |
| --- | --- | --- | --- | --- | --- | --- |
| loop-agent | 0.3.0 | `mzdbxqh/loop-agent` | ✓ | — | ✓ | — |
| release-skill | 0.5.1 | `ifoohoo/release-skill` | ✓ | ✓ | ✓ | ✓ |
| skill-failure-auditor | 1.0.0 | `ifoohoo/skill-failure-auditor` | ✓ | ✓ | ✓ | ✓ |
| skill-family-audit | 1.1.0 | `ifoohoo/skill-family-audit` | ✓ | — | ✓ | — |
| skill-family-docs | 0.1.1 | `ifoohoo/skill-family-docs` | — | ✓ | — | ✓ |

"✓" means the plugin is listed in that platform's manifest; "—" means it is not. The `platforms` field in the source is the sole explicit distribution switch; CodeBuddy/WorkBuddy's official fallback to `.claude-plugin/plugin.json` does not change distribution status.

After adding the marketplace, install plugins with your platform's plugin manager (e.g. `/plugin install <name>@skill-family-hub` in Claude Code).

## About this marketplace

**skill-family-hub** is the public marketplace index of verified skill-family lifecycle plugins, targeting Claude Code, CodeBuddy/WorkBuddy, OpenAI Codex, and Kimi Code.

- Add the marketplace with the commands above, then install individual plugins through each platform's plugin manager.
- Currently distributed: `loop-agent`, `release-skill`, `skill-failure-auditor`, `skill-family-audit`, `skill-family-docs`. See the table for per-platform availability.
- Each plugin's version authority lives in its own repository (self-contained manifests and git tags); this index only references them.
- Licensed under MIT — see [LICENSE](LICENSE).
