# dhan auth

Configure and manage the Dhan API session. Verify subcommands with `dhan auth --help` (binaries vary by version).

## Commands (documented product surface)

| Command | Purpose |
|---------|---------|
| `dhan auth configure --client-id <id> --access-token <token>` | Store credentials (simplest) |
| `dhan auth status` | Booleans for stored client-id / token / authenticated |
| `dhan auth login --client-id --app-id --app-secret [--port] [--timeout-seconds] [--no-open]` | Browser consent |
| `dhan auth consume --token-id --app-id --app-secret` | Manual tokenId exchange |
| `dhan auth totp --client-id --pin --totp` | PIN+TOTP, no browser |
| `dhan auth partner-login --partner-id --partner-secret […]` | Partner browser flow |
| `dhan auth partner-consume --token-id --partner-id --partner-secret` | Partner token exchange |
| `dhan auth renew` | Renew active access token |
| `dhan auth logout [--forget-client-id]` | Drop token; optional full wipe |

## Examples

```bash
dhan auth configure --client-id <client_id> --access-token <access_token> --json --no-color
dhan auth status --json --no-color
dhan auth login --client-id C --app-id A --app-secret S --json --no-color
dhan auth totp --client-id C --pin <pin> --totp <code> --json --no-color
dhan auth renew --json --no-color
dhan auth logout --forget-client-id --json --no-color
```

Redirect URL: `http://127.0.0.1:17890/` (override with `--port` / config `redirectPort`).

Never echo real secrets into the agent transcript.
