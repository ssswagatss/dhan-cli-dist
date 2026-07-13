# dhan ip

Static IP whitelist — **required for live trading** on Dhan.

```bash
dhan ip get --json --no-color
dhan ip set --ip 203.0.113.10 --yes --json --no-color
dhan ip set --ip 203.0.113.10 --flag SECONDARY --yes --json --no-color
dhan ip modify --ip 203.0.113.20 --flag PRIMARY --yes --json --no-color
```

## Gotchas

1. After `ip set`, IP often **cannot change for 7 days** — plan carefully.
2. set/modify require `--yes` (live account mutation).
3. If order APIs return static-IP / authorization errors: **stop; do not retry-loop**.
