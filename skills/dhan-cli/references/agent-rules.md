# Dhan CLI — agent operating rules

## Must

- Always `--json --no-color`.
- Confirm auth with `dhan auth status` before protected calls.
- For live actions: `--dry-run` when available → show operator → re-run with `--yes`.
- On static-IP / 403 authorization errors: stop immediately; instruct operator to fix whitelist.
- Use `dhan <path> --help` when flags are ambiguous.

## Must not

- Invent security IDs, quantities, prices, products, or sides.
- Retry live trading or auth failures in a loop.
- Put tokens, PIN, or TOTP codes into shared logs.
- Use `raw` to bypass safety on mutual-fund or undisclosed endpoints without explicit operator request.

## Transcript hygiene

Redact: `<client_id>`, `<access_token>`, `<app_secret>`, `<pin>`, `<totp>`, `<partner_secret>`.
Never paste `Authorization` headers.
