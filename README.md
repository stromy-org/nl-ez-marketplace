# Dutch Data Marketplace

Public marketplace for Dutch Data Claude Code plugins.

## Prerequisites

| Requirement | Version | Why |
|-------------|---------|-----|
| Claude Code | v2.1.49+ | Plugin runtime (CLI or Desktop Code tab) |

## Installation

### Option A: From the Cowork Desktop UI

1. Open **Customize** → **Browse plugins** → **Personal** tab
2. Click the `+` to add a marketplace → enter `stromy-org/dutch-data-marketplace`
3. Click **Dutch Data** → Install

### Option B: From the CLI

```bash
# Add marketplace (one-time)
claude plugin marketplace add stromy-org/dutch-data-marketplace

# Install plugin
claude plugin install dutch-data-plugin@dutch-data-marketplace
```

### Post-install: dependencies (one-time)

```bash
cd ~/.claude/plugins/cache/dutch-data-marketplace/dutch-data-plugin/0.1.0
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
| _example_ | `/dutch-data-plugin:example` |

## Updating

```bash
claude plugin update dutch-data-plugin@dutch-data-marketplace
```

## Troubleshooting

| Problem | Fix |
|---------|-----|
| "Failed to install plugin" | Ensure you have internet access; try CLI install (Option B) |
| Skills don't appear | Start a new session; ensure you're in the **Code** tab |
| Dependency errors on first use | Run `npm install && uv sync` in the plugin cache dir |
| "Plugin not found in marketplace" | Run `claude plugin marketplace add stromy-org/dutch-data-marketplace` first |

## Architecture

- **Marketplace** (this repo): public — hosts `marketplace.json` only
- **Plugin** (`dutch-data-plugin`): public — contains skills, brand data, company info
- **Source format**: `marketplace.json` uses `"source": "url"` with a full `.git` URL
