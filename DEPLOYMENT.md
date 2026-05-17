# Deployment Guide

_Platform: Fly.io · Region: London (LHR) · UK data residency_

Kin2 Workforce runs on Fly.io in the London (`lhr`) region. This satisfies UK GDPR data residency requirements.

---

## Environment

| Environment | Fly app name | URL | Deploy trigger |
|---|---|---|---|
| Production | `kin2workforce-yhedhw` | kin2serviceslimited.co.uk | Push to `main` (after CI gates pass) |

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
FROM node:22-alpine AS deps
WORKDIR /app
COPY package*.json ./
RUN npm ci

# ---- build ----
FROM node:22-alpine AS builder
WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY . .
RUN npm run build

# ---- production ----
FROM node:22-alpine AS runner
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

> **Note:** Node 22 is required (see `engines` field in `package.json`). Adjust `dist/index.js` to match the actual build output entry point.

---

## fly.toml

The production configuration is in `fly.toml` at the repository root. Key settings:

```toml
app = "kin2workforce-yhedhw"
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

[[vm]]
  memory = "2048"
  cpu_kind = "shared"
  cpus = 1
```

> `auto_stop_machines = false` and `min_machines_running = 1` are required — the 6 background AI agents are persistent processes and must not be stopped between requests.
> Memory is set to 2 GB to accommodate concurrent AI agent workloads.

---

## GitHub Actions integration

The deploy workflow (`.github/workflows/deploy.yml`) uses flyctl:

```yaml
- name: Set up flyctl
  uses: superfly/flyctl-actions/setup-flyctl@master

- name: Deploy to production
  run: flyctl deploy --remote-only --config fly.toml
  env:
    FLY_API_TOKEN: ${{ secrets.FLY_API_TOKEN }}

- name: Health check
  run: |
    sleep 15
    curl --fail https://kin2serviceslimited.co.uk/health || exit 1
```

---

## Secrets and environment variables

Set secrets via flyctl — never commit them to source:

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
  --app kin2workforce-yhedhw
```

**GitHub repository secrets required:**

| Secret | Purpose |
|---|---|
| `FLY_API_TOKEN` | Fly.io deploy authentication |

---

## Rollback

```bash
# List recent releases
flyctl releases --app kin2workforce-yhedhw

# Roll back to a specific version
flyctl deploy --image <image-ref> --app kin2workforce-yhedhw
```

Fly.io retains previous images. A rollback takes approximately 30 seconds.

---

## Monitoring

- **Fly dashboard:** https://fly.io/apps/kin2workforce-yhedhw
- **Logs:** `flyctl logs --app kin2workforce-yhedhw`
- **Status:** `flyctl status --app kin2workforce-yhedhw`
- **Health check:** https://kin2serviceslimited.co.uk/health
- **GitHub Actions health monitor:** runs every 30 minutes via `kin2-monitor.yml`

---

## Data residency

Production runs exclusively in Fly.io's `lhr` (London, UK) region. No data is processed or stored outside the United Kingdom. This satisfies UK GDPR Article 44 requirements for data transfers.

---

## Contact

Deployment issues: kin@kin2serviceslimited.com
