# dhan super

Super Orders. **Live** place/modify/cancel-leg need `--yes` (+ static IP for placement).

```bash
dhan super list --json --no-color
dhan super place --file super.json --dry-run --json --no-color
dhan super place --file super.json --yes --json --no-color
dhan super modify <order-id> --file super.json --yes --json --no-color
dhan super cancel-leg <order-id> ENTRY_LEG --yes --json --no-color
```

Legs: `ENTRY_LEG` | `TARGET_LEG` | `STOP_LOSS_LEG`.
