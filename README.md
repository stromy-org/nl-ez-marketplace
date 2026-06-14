# NL Gov Data Marketplace

Public marketplace for NL Gov Data Claude Code plugins.

## Prerequisites

| Requirement | Version | Why |
|-------------|---------|-----|
| Claude Code | v2.1.49+ | Plugin runtime (CLI or Desktop Code tab) |

## Installation

### Option A: From the Cowork Desktop UI

1. Open **Customize** → **Browse plugins** → **Personal** tab
2. Click the `+` to add a marketplace → enter `stromy-org/nl-gov-data-marketplace`
3. Click **NL Gov Data** → Install

### Option B: From the CLI

```bash
# Add marketplace (one-time)
claude plugin marketplace add stromy-org/nl-gov-data-marketplace

# Install plugin
claude plugin install nl-gov-data-plugin@nl-gov-data-marketplace
```

### Post-install: dependencies (one-time)

```bash
cd ~/.claude/plugins/cache/nl-gov-data-marketplace/nl-gov-data-plugin/0.1.0
npm install   # if the plugin has Node dependencies
uv sync       # if the plugin has Python dependencies
```

## Where skills work

| Interface | Skills available? | Notes |
|-----------|:-:|-------|
| **Claude Code CLI** | Yes | Terminal — full plugin support |
| **Desktop app — Code tab** | Yes | Same runtime as CLI |
| **Desktop app — Cowork tab** | Pending | Cowork plugin loading for marketplace plugins is a known limitation |

## Available skills

<!-- Update this table after adding skills to the plugin -->
| Skill | Command |
|-------|---------|
| _example_ | `/nl-gov-data-plugin:example` |

## Updating

```bash
claude plugin update nl-gov-data-plugin@nl-gov-data-marketplace
```

## Troubleshooting

| Problem | Fix |
|---------|-----|
| "Failed to install plugin" with `Permission denied (publickey)` | Refresh the marketplace and confirm the plugin source is the explicit HTTPS `.git` URL |
| Other installation errors | Check `~/Library/Logs/Claude/main.log`; then try CLI install (Option B) |
| Skills don't appear | Start a new session; ensure you're in the **Code** tab |
| Dependency errors on first use | Run `npm install && uv sync` in the plugin cache dir |
| "Plugin not found in marketplace" | Run `claude plugin marketplace add stromy-org/nl-gov-data-marketplace` first |

## Architecture

- **Marketplace** (this repo): public — hosts `marketplace.json` only
- **Plugin** (`nl-gov-data-plugin`): public — contains skills, brand data, company info
- **Source format**: `marketplace.json` uses `"source": "url"` with an explicit HTTPS clone URL ending in `.git`; the `github` shorthand is avoided because Claude Code can resolve it to SSH
