# dhan instruments

```bash
dhan instruments download --segment NSE_EQ --json --no-color
dhan instruments search INFY --segment NSE_EQ --json --no-color
```

Cache under app data (`%AppData%\dhan-cli\instruments\` on Windows). Search is capped (docs: ≤25 matches). Use returned **securityId** for quotes/historical/orders.
