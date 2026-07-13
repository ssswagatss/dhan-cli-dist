---
name: dhan-cli
description: >
  Drive the Dhan CLI (`dhan`) for DhanHQ API v2: auth, account, portfolio, orders,
  super orders, trades, alerts, quotes, historical, option-chain, margins, eDIS,
  control (kill switch / PnL exit), instruments, IP whitelist, global US stocks, raw,
  and config. Use when the user mentions dhan CLI, DhanHQ terminal, dhan orders/auth,
  static IP trading, or runs /dhan-cli.
---

# Dhan CLI skill

Binary: **`dhan`**. Docs: https://cli.jorli.in/dhan/overview/  
Install binary: `curl -fsSL https://cli.jorli.in/install/dhan.sh | sh` (or Windows `irm …/dhan.ps1 | iex`)  
Install this skill (from this repo, or the public dist mirror):

```bash
npx skills add ssswagatss/dhan-cli --skill dhan-cli
# public mirror (same package, no private-repo access required):
npx skills add ssswagatss/dhan-cli-dist --skill dhan-cli
```

## Hard rules (never break)

1. **Always** pass `--json --no-color` on agent-driven commands. Never parse table output.
2. **Never invent trades.** Live place/modify/cancel/slice/super/control/global/ip only from explicit operator intent. Do not silently change securityId, qty, price, product, or side.
3. **Every live mutation requires `--yes`.** Without it the CLI exits `2`. Prefer **`--dry-run` first** where supported (prints payload, no HTTP).
4. **Static IP whitelist** is required for live order APIs. On authorization / static-IP errors: **stop — do not retry** (Dhan may rate-limit retries).
5. **Secrets stay secret.** Never write client-id, access-token, app-secret, pin, totp, or partner secrets to files/logs. Redact placeholders.
6. **Avoid `--verbose` in shared transcripts.**
7. **No retry loops** on auth (exit `3`) or API (exit `4`) failures.
8. When flags are unclear, run `dhan <path> --help` — installed binary wins over this skill if they disagree.

## Global flags

| Flag | Purpose |
|------|---------|
| `--json` | Structured JSON stdout |
| `--no-color` | No ANSI colour |
| `--verbose` | Detailed errors — debug only |
| `-h` / `--help` | Help at every level |

## Exit codes

| Code | Meaning |
|------|---------|
| `0` | Success |
| `2` | Usage error (missing option, missing `--yes`, etc.) |
| `3` | Auth failure (HTTP 401/403) |
| `4` | Other API failure |
| `5` | I/O / file error |
| `10` | Unexpected runtime error |

## Operating workflow

```text
1. dhan --version / --help
2. dhan auth status --json --no-color     → authenticated?
3. Read-only: profile, funds, holdings, positions, orders list
4. Live orders: dry-run → operator confirm → --yes
5. If static-IP error: stop; operator fixes whitelist (dhan ip / dashboard)
```

### Auth (simplest: bring your own token)

```bash
dhan auth configure --client-id <client_id> --access-token <access_token> --json --no-color
dhan auth status --json --no-color
dhan auth renew --json --no-color
dhan auth logout --json --no-color
dhan auth logout --forget-client-id --json --no-color
```

Other flows (when present on binary — verify with `dhan auth --help`):

```bash
dhan auth login --client-id C --app-id A --app-secret S --json --no-color
dhan auth totp --client-id C --pin <pin> --totp <code> --json --no-color
dhan auth consume --token-id <id> --app-id A --app-secret S --json --no-color
dhan auth partner-login --partner-id P --partner-secret S --json --no-color
```

Redirect URL default: `http://127.0.0.1:17890/`

### Read-only sanity

```bash
dhan account profile --json --no-color
dhan account funds --json --no-color
dhan portfolio holdings --json --no-color
dhan portfolio positions --json --no-color
dhan orders list --json --no-color
dhan trades list --json --no-color
```

### Resolve instruments

Dhan uses **numeric security IDs** + **segment** (e.g. `NSE_EQ`), not `NSE:INFY`.

```bash
dhan instruments download --segment NSE_EQ --json --no-color
dhan instruments search INFY --segment NSE_EQ --json --no-color
```

Quotes / option-chain may require **Dhan Data API** subscription.

### Live orders — dry-run then yes

```bash
dhan orders place --file ./order.json --dry-run --json --no-color
dhan orders place --file ./order.json --yes --json --no-color
```

## Command map → references

| Group | Live notes | Reference |
|-------|------------|-----------|
| auth | token lifecycle | [references/auth.md](references/auth.md) |
| config | prefs | [references/config.md](references/config.md) |
| account | read | [references/account.md](references/account.md) |
| portfolio | convert, exit-all | [references/portfolio.md](references/portfolio.md) |
| orders | place/modify/cancel/slice | [references/orders.md](references/orders.md) |
| trades | read | [references/trades.md](references/trades.md) |
| super | super orders | [references/super.md](references/super.md) |
| alerts | triggers | [references/alerts.md](references/alerts.md) |
| quote | Data API | [references/quote.md](references/quote.md) |
| historical | candles | [references/historical.md](references/historical.md) |
| option-chain | Data API | [references/option-chain.md](references/option-chain.md) |
| margins | calculator | [references/margins.md](references/margins.md) |
| edis | T-PIN flows | [references/edis.md](references/edis.md) |
| control | kill switch / PnL exit | [references/control.md](references/control.md) |
| instruments | master cache | [references/instruments.md](references/instruments.md) |
| ip | static IP whitelist | [references/ip.md](references/ip.md) |
| global | US Global Stocks | [references/global.md](references/global.md) |
| raw | escape hatch | [references/raw.md](references/raw.md) |
| update | release URL | [references/update.md](references/update.md) |

Also: [references/concepts.md](references/concepts.md), [references/agent-rules.md](references/agent-rules.md), [references/command-index.md](references/command-index.md).

## Recovery quick table

| Symptom | Action |
|---------|--------|
| exit `3` not authenticated | `auth status`; configure or login |
| static-IP / authorization on live cmd | **Stop.** Fix whitelist; never retry-loop |
| instrument cache missing | `instruments download --segment …` |
| exit `2` missing `--yes` | Re-run only after operator confirms, with `--yes` |
| exit `4` API error | Stop; report; do not invent fixes |

## Docs

- Concepts: https://cli.jorli.in/concepts/
- Agent guide: https://cli.jorli.in/agent-guide/
- Security: https://cli.jorli.in/security/
