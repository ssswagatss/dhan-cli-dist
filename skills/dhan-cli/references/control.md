# dhan control

Kill switch and P&L-based exit. **All mutating subcommands are LIVE** and need `--yes`.

```bash
dhan control killswitch-status --json --no-color
dhan control killswitch --status ACTIVATE --yes --json --no-color
dhan control killswitch --status DEACTIVATE --yes --json --no-color

dhan control pnl-exit --json --no-color
dhan control configure-pnl-exit --file pnl.json --dry-run --json --no-color
dhan control configure-pnl-exit --file pnl.json --yes --json --no-color
dhan control stop-pnl-exit --yes --json --no-color
```

Only run on explicit operator instruction. May require static-IP whitelist.
