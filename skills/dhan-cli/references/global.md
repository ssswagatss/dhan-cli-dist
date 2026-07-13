# dhan global

US Global Stocks. Live order actions need static IP + `--yes`.

```bash
dhan global orders list --json --no-color
dhan global orders get <order-id> --json --no-color
dhan global orders place --file us-order.json --dry-run --json --no-color
dhan global orders place --file us-order.json --yes --json --no-color
dhan global orders modify <order-id> --file us-order.json --yes --json --no-color
dhan global orders cancel <order-id> --yes --json --no-color

dhan global trades list --json --no-color
dhan global trades by-security <security-id> --json --no-color

dhan global holdings --json --no-color
dhan global funds --json --no-color
dhan global market-status --json --no-color
dhan global estimate --file us-order.json --json --no-color
dhan global margin --file us-order.json --json --no-color
```

If a subcommand is missing on older binaries, run `dhan global --help`.
