# NL Gov Data Marketplace

Public marketplace for NL Gov Data Claude Code plugins.

## Prerequisites

| Requirement | Version | Why |
|-------------|---------|-----|
| Claude Code | v2.1.49+ | Plugin runtime (CLI or Desktop Code tab) |

## Installation

### Option A: In Claude (desktop or web — Cowork, Claude for Work / Team)

1. Open **Settings → Plugins** (or **Connectors & plugins**)
2. **Add marketplace** → enter `stromy-org/nl-gov-data-marketplace`
3. Click **NL Gov Data** → **Install**
4. In **Settings → Connectors**, switch on the connectors the plugin declares in its `.mcp.json`

### Option B: From the CLI

```bash
# Add marketplace (one-time)
claude plugin marketplace add stromy-org/nl-gov-data-marketplace

# Install plugin
claude plugin install nl-gov-data-plugin@nl-gov-data-marketplace
```

### Post-install: dependencies (one-time)

```bash
cd ~/.claude/plugins/cache/nl-gov-data-marketplace/nl-gov-data-plugin/<version>
npm install   # if the plugin has Node dependencies
uv sync       # if the plugin has Python dependencies
```

## Where skills work

| Interface | Skills available? | Notes |
|-----------|:-:|-------|
| **Claude desktop / web — Cowork, Claude for Work** | Yes | Install via **Settings → Plugins**; connectors via **Settings → Connectors** |
| **Claude Code CLI** | Yes | Terminal — full plugin support |
| **Desktop app — Code tab** | Yes | Same runtime as CLI |

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
| "Failed to install plugin" with `Permission denied (publickey)` | Confirm the plugin entry uses an explicit `https://...git` URL, not the `github` shorthand |
| Other "Failed to install plugin" errors | Check `~/Library/Logs/Claude/main.log`; then try CLI install (Option B) |
| Skills don't appear | Start a new session; ensure you're in the **Code** tab |
| Dependency errors on first use | Run `npm install && uv sync` in the plugin cache dir |
| "Plugin not found in marketplace" | Run `claude plugin marketplace add stromy-org/nl-gov-data-marketplace` first |

## Architecture

- **Marketplace** (this repo): public — hosts `marketplace.json` only
- **Plugin** (`nl-gov-data-plugin`): public — contains skills, brand data, company info
- **Source format**: use `"source": "url"` with an explicit HTTPS clone URL ending in `.git`, for example `https://github.com/stromy-org/nl-gov-data-plugin.git`
- **Why not `github` shorthand?** Anthropic supports it, but Claude Code can resolve it to SSH (`git@github.com:...`) and fail on machines without a configured GitHub SSH key. Explicit HTTPS is the org portability standard.
