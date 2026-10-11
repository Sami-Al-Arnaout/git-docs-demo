# Troubleshooting

## Common problems

### The deploy is stuck

The canary step waits for error rates to settle. If it has been more than 20
minutes, check the dashboard and roll back:

```bash
./scripts/rollout.sh --status
./scripts/rollout.sh --rollback --to previous
```

### Local tests fail with `ECONNREFUSED`

The database container is not running. Start it with `docker compose up -d database`
— see [getting started](../getting-started.md#run-it).

<details>
<summary>Still failing? Collect diagnostics</summary>

Run the diagnostics script and attach the output to your support request:

```bash
./scripts/diagnose.sh > diagnostics.txt
```

It collects versions and container status. It never collects secrets.

</details>

## Getting help

Post in `#platform` with what you ran, what you expected and what happened.
