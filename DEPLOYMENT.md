# Deployment Guide

_Platform: Fly.io · Region: London (LHR) · UK data residency_

Kin2 Workforce runs on Fly.io in the London (`lhr`) region. This satisfies UK GDPR data residency requirements. Two environments are maintained: `production` and `staging`, each as a separate Fly app.

---

## Environments

| Environment | Fly app name | URL | Deploy trigger |
|---|---|---|---|
| Production | `kin2workforce` | kin2serviceslimited.co.uk | Push to `main` (after CI gates pass) |
| Staging | `kin2workforce-staging` | staging.kin2serviceslimited.co.uk | Push to `main` (deploys before production) |

---

## Prerequisites

1. [Install flyctl](https://fly.io/docs/hands-on/install-flyctl/)
2. Authenticate: `flyctl auth login`
3. Generate a deploy token: `flyctl tokens create deploy -x 999999h`
4. Add the token as `FLY_API_TOKEN` in GitHub repository secrets

---

## Dockerfile

Place this in the root of the `Kin2Workforce` repository. It uses a multi-stage build: dependencies → build → production image.

```dockerfile
# ---- deps ----
FROM node:20-alpine AS deps
WORKDIR /app
COPY package*.json ./
RUN npm ci

# ---- build ----
FROM node:20-alpine AS builder
WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY . .
RUN npm run build

# ---- production ----
FROM node:20-alpine AS runner
WORKDIR /app
ENV NODE_ENV=production

COPY package*.json ./
RUN npm ci --omit=dev && npm cache clean --force

COPY --from=builder /app/dist ./dist

# Run as non-root
USER node

EXPOSE 8080
CMD ["node", "dist/index.js"]
```

> **Note:** Adjust `dist/index.js` to match your actual build output entry point. If the Vite client build outputs to `dist/public`, ensure the Express server serves static files from that path in production.

---

## fly.toml (production)

```toml
app = "kin2workforce"
primary_region = "lhr"

[build]
  dockerfile = "Dockerfile"

[env]
  PORT = "8080"
  NODE_ENV = "production"

[http_service]
  internal_port = 8080
  force_https = true
  auto_stop_machines = false
  auto_start_machines = true
  min_machines_running = 1

  [http_service.concurrency]
    type = "connections"
    hard_limit = 100
    soft_limit = 80

  [[http_service.checks]]
    grace_period = "10s"
    interval = "30s"
    method = "GET"
    path = "/health"
    timeout = "5s"

[[vm]]
  memory = "1gb"
  cpu_kind = "shared"
  cpus = 1
```

> `auto_stop_machines = false` and `min_machines_running = 1` are required — the 14 background AI agents are persistent processes and must not be stopped between requests.  
> Memory is set to 1 GB to accommodate concurrent AI agent workloads. Increase to 2 GB if agents show memory pressure under load.

---

## fly.staging.toml (staging)

```toml
app = "kin2workforce-staging"
primary_region = "lhr"

[build]
  dockerfile = "Dockerfile"

[env]
  PORT = "8080"
  NODE_ENV = "staging"

[http_service]
  internal_port = 8080
  force_https = true
  auto_stop_machines = true
  auto_start_machines = true
  min_machines_running = 0

  [[http_service.checks]]
    grace_period = "10s"
    interval = "60s"
    method = "GET"
    path = "/health"
    timeout = "5s"

[[vm]]
  memory = "512mb"
  cpu_kind = "shared"
  cpus = 1
```

> Staging uses `auto_stop_machines = true` and `min_machines_running = 0` to keep costs low when idle.

---

## GitHub Actions integration

Replace the Replit deploy step in `.github/workflows/deploy.yml` with the following. Staging deploys first; production only deploys if staging succeeds.

```yaml
- name: Set up flyctl
  uses: superfly/flyctl-actions/setup-flyctl@master

- name: Deploy to staging
  run: flyctl deploy --remote-only --config fly.staging.toml
  env:
    FLY_API_TOKEN: ${{ secrets.FLY_API_TOKEN }}

- name: Deploy to production
  run: flyctl deploy --remote-only --config fly.toml
  env:
    FLY_API_TOKEN: ${{ secrets.FLY_API_TOKEN }}
```

Remove any references to `kin2workforce.replit.app` from the health check step and replace with:

```yaml
- name: Health check
  run: |
    sleep 15
    curl --fail https://kin2serviceslimited.co.uk/health || exit 1
```

---

## Secrets and environment variables

Set secrets via flyctl — never commit them to source. Apply to both apps:

```bash
flyctl secrets set \
  DATABASE_URL="..." \
  SESSION_SECRET="..." \
  STRIPE_SECRET_KEY="..." \
  STRIPE_WEBHOOK_SECRET="..." \
  SENDGRID_API_KEY="..." \
  TWILIO_ACCOUNT_SID="..." \
  TWILIO_AUTH_TOKEN="..." \
  TWILIO_PHONE_NUMBER="..." \
  OPENAI_API_KEY="..." \
  ANTHROPIC_API_KEY="..." \
  HMRC_CLIENT_ID="..." \
  HMRC_CLIENT_SECRET="..." \
  SAML_CERT="..." \
  --app kin2workforce
```

Repeat with `--app kin2workforce-staging` for staging, using staging-specific values where applicable (e.g. Stripe test keys, HMRC sandbox credentials).

**GitHub repository secrets required:**

| Secret | Purpose |
|---|---|
| `FLY_API_TOKEN` | Fly.io deploy authentication |

**GitHub environment secrets (set on the `production` environment):**

| Secret | Purpose |
|---|---|
| Fly app secrets above | Managed via flyctl, not GitHub |

---

## Initial setup (first deploy)

```bash
# Create production app in London
flyctl apps create kin2workforce --org personal
flyctl regions set lhr --app kin2workforce

# Create staging app in London
flyctl apps create kin2workforce-staging --org personal
flyctl regions set lhr --app kin2workforce-staging

# Set secrets on both apps (see above)

# First deploy
flyctl deploy --remote-only --config fly.toml
flyctl deploy --remote-only --config fly.staging.toml

# Point custom domain
flyctl certs create kin2serviceslimited.co.uk --app kin2workforce
flyctl certs create staging.kin2serviceslimited.co.uk --app kin2workforce-staging
```

Update your DNS provider to point `kin2serviceslimited.co.uk` to the Fly.io IP returned by `flyctl ips list --app kin2workforce`.

---

## Rollback

```bash
# List recent releases
flyctl releases --app kin2workforce

# Roll back to a specific version
flyctl deploy --image <image-ref> --app kin2workforce
```

Fly.io retains previous images. A rollback takes ~30 seconds.

---

## Monitoring

- **Fly dashboard:** https://fly.io/apps/kin2workforce
- **Logs:** `flyctl logs --app kin2workforce`
- **Status:** `flyctl status --app kin2workforce`
- **Health check:** https://kin2serviceslimited.co.uk/health
- **GitHub Actions health monitor:** runs every 30 minutes via `kin2-monitor.yml`

---

## Data residency

Both production and staging run exclusively in Fly.io's `lhr` (London, UK) region. No data is processed or stored outside the United Kingdom. Fly.io's infrastructure in this region is operated within the UK, satisfying UK GDPR Article 44 requirements for data transfers.

---

## Contact

Deployment issues: kin@kin2serviceslimited.com
