# dhan — full command index

Always append `--json --no-color`. Live leaves usually need `--yes`; prefer `--dry-run` first.  
Your installed `dhan --help` is authoritative if a path is missing.

| Path | Notes |
|------|-------|
| `dhan auth configure` | Store client-id + access-token |
| `dhan auth status` | Auth booleans |
| `dhan auth login` | Browser consent |
| `dhan auth consume` | tokenId exchange |
| `dhan auth totp` | PIN+TOTP |
| `dhan auth partner-login` / `partner-consume` | Partner flows |
| `dhan auth renew` | Renew token |
| `dhan auth logout` | Clear token / `--forget-client-id` |
| `dhan config get` / `set` | Non-secret prefs |
| `dhan account profile` / `funds` / `ledger` | Account reads |
| `dhan portfolio holdings` / `positions` | Reads |
| `dhan portfolio convert` | **LIVE** |
| `dhan portfolio exit-all` | **LIVE** |
| `dhan orders list` / `get` / `correlation` | Reads |
| `dhan orders place` / `modify` / `cancel` / `slice` | **LIVE** |
| `dhan trades list` / `order` / `history` | Trades |
| `dhan super list` / `place` / `modify` / `cancel-leg` | Super (**LIVE** mutators) |
| `dhan alerts …` | Conditional triggers |
| `dhan quote ltp` / `ohlc` / `full` | Data API |
| `dhan historical …` | Candles |
| `dhan option-chain …` | Data API |
| `dhan margins …` | Calculators |
| `dhan edis …` | eDIS |
| `dhan control killswitch*` / `pnl-exit*` | **LIVE** mutators |
| `dhan instruments download` / `search` | Master cache |
| `dhan ip get` / `set` / `modify` | Static IP (**LIVE** set/modify) |
| `dhan global orders*` / `trades*` / `holdings` / `funds` / … | US Global Stocks |
| `dhan raw get|post|put|delete` | Escape hatch |
| `dhan update` | Release URL |
