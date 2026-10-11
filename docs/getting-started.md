---
title: Getting started
weight: 1
---

# Getting started

This guide takes you from a fresh laptop to a running platform in about fifteen
minutes.

## Prerequisites

- [x] Node.js 22 or later
- [x] Docker Desktop
- [ ] Access to the `acme` GitHub organisation (request it in `#it-help`)

> [!NOTE]
> On Apple silicon, enable *Use Rosetta for x86/amd64 emulation* in Docker Desktop
> before the first build.

## Clone and install

```bash
git clone https://github.com/acme/platform.git
cd platform
npm ci
```

## Configure

Copy the example environment file and fill in the two required values:

```bash
cp .env.example .env
```

| Variable | Required | Example |
|---|---|---|
| `DATABASE_URL` | yes | `postgres://localhost:5432/acme` |
| `API_PORT` | no | `8080` |
| `FEATURE_FLAGS` | no | `search,exports` |

## Run it

```bash
docker compose up -d database
npm run dev
```

Open <http://localhost:8080/health>. You should see:

```json
{ "status": "ok", "version": "local" }
```

Next: read how the pieces fit together in the [architecture overview](architecture/README.md),
or jump to [deploying](guides/deploying.md#before-you-deploy).
