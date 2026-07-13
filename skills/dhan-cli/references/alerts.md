# dhan alerts

Conditional triggers.

```bash
dhan alerts list --json --no-color
dhan alerts get <id> --json --no-color
dhan alerts place --file alert.json --dry-run --json --no-color
dhan alerts place --file alert.json --yes --json --no-color
dhan alerts modify <id> --file alert.json --yes --json --no-color
dhan alerts delete <id> --yes --json --no-color
```

Confirm leaf flags with `--help`. Treat place/modify/delete as live when `--yes` is required.
