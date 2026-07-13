# dhan orders

Today's orders. **Live** place/modify/cancel/slice need static IP + `--yes`.

## Commands

| Command | Live | Flags |
|---------|------|-------|
| `dhan orders list` | no | — |
| `dhan orders get <order-id>` | no | — |
| `dhan orders correlation <correlation-id>` | no | — |
| `dhan orders place --file <json>` | **yes** | `--yes`, `--dry-run` |
| `dhan orders modify <order-id> --file <json>` | **yes** | `--yes`, `--dry-run` |
| `dhan orders cancel <order-id>` | **yes** | `--yes` |
| `dhan orders slice --file <json>` | **yes** | `--yes`, `--dry-run` |

## Payload example

CLI may auto-inject `dhanClientId` if missing:

```json
{
  "correlationId": "agent-run-001",
  "transactionType": "BUY",
  "exchangeSegment": "NSE_EQ",
  "productType": "CNC",
  "orderType": "LIMIT",
  "validity": "DAY",
  "securityId": "1333",
  "quantity": 1,
  "price": 1500,
  "afterMarketOrder": false
}
```

## Discipline

```bash
dhan orders place --file order.json --dry-run --json --no-color
dhan orders place --file order.json --yes --json --no-color
```

Without `--yes`, live commands fail with exit `2`.  
On static-IP errors: **do not retry**.
