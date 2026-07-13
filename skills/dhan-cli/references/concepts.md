# Dhan CLI — concepts

## Output contract

```bash
dhan <command> --json --no-color
```

Do **not** parse human table output. `--verbose` is debug-only (stderr can include raw API bodies).

## Exit codes

| Code | Meaning |
|------|---------|
| `0` | Success |
| `2` | Usage (missing args / missing `--yes`) |
| `3` | Auth (401/403) |
| `4` | Other API error |
| `5` | File / I/O |
| `10` | Unexpected |

## Secrets

| Key | Purpose |
|-----|---------|
| `dhan-cli:client-id` | Client id |
| `dhan-cli:access-token` | Access token |

OS keyring preferred; file fallback on some headless Linux setups.

## Preferences

| OS | Path |
|----|------|
| Windows | `%AppData%\dhan-cli\config.json` |
| macOS/Linux | `~/.config/dhan-cli/config.json` |

Common keys: `baseUrl`, `redirectPort`.

## Live trading model

- Mutating commands require **`--yes`**.
- Prefer **`--dry-run`** first when available (validates/prints payload; no HTTP).
- Live order APIs need **static IP whitelist** (`dhan ip`).

## Instrument identity

- **securityId** (numeric string) + **exchangeSegment** / `--segment` (e.g. `NSE_EQ`).
- Not Kite-style `NSE:INFY` for Dhan market data endpoints.

## Hosts

- Auth/consent: `https://auth.dhan.co/`
- Trading API: `https://api.dhan.co/v2/`
