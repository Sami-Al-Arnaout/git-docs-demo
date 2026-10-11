# Deploying

Production deploys run from the `main` branch through GitHub Actions.

## Before you deploy

- [x] The pull request is approved by a code owner
- [x] CI is green, including the end-to-end suite
- [ ] The change is behind a feature flag if it touches billing

## Deploy

Merge the pull request. The pipeline builds, runs migrations and rolls out:

```yaml
# .github/workflows/deploy.yml (excerpt)
jobs:
  deploy:
    environment: production
    steps:
      - uses: actions/checkout@v4
      - run: npm ci && npm run build
      - run: ./scripts/migrate.sh
      - run: ./scripts/rollout.sh --strategy canary --steps 10,50,100
```

> [!CAUTION]
> A deploy that runs a migration cannot be rolled back by the pipeline. Read
> [rolling back](#rolling-back) before merging one on a Friday.

## Rolling back

```bash
./scripts/rollout.sh --rollback --to previous
```

If the rollback fails, follow [troubleshooting](troubleshooting.md#the-deploy-is-stuck).
