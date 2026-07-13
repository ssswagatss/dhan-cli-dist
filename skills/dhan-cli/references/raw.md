# dhan raw

Escape hatch for endpoints not wrapped by first-class commands.

```bash
dhan raw get <path> --json --no-color
dhan raw post <path> --file body.json --json --no-color
dhan raw put <path> --file body.json --json --no-color
dhan raw delete <path> --json --no-color
```

## Rules

- Only when the operator explicitly needs an unwrapped path.
- Do **not** use raw to place mutual-fund or arbitrary undisclosed trades without intent.
- Prefer first-class commands when they exist.
- Live POSTs that change account state still need operator approval; add `--yes` if the binary requires it (check `--help`).
