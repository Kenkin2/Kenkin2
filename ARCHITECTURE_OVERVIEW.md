# Architecture Overview

_Version: v3.9.8 · Last updated: May 2026_

## System design

Kin2 Workforce is a multi-tenant SaaS platform. Each organisation operates in complete isolation — separate data, permissions, and billing — on shared infrastructure.

## Tech stack

| Layer | Technology | Notes |
|---|---|---|
| **Frontend** | React 18 + TypeScript + Vite | shadcn/ui, TailwindCSS v3, TanStack Query v5, Wouter |
| **Backend** | Node.js + Express + TypeScript | 274 API namespaces, REST architecture |
| **Database** | Neon PostgreSQL | Drizzle ORM, connection pooling, serverless-compatible |
| **Auth** | Custom session auth | express-session, connect.sid, multi-tenant isolation |
| **Payments** | Stripe | Subscription billing, webhooks, plan enforcement |
| **Email** | SendGrid | Transactional and notification email |
| **SMS / WhatsApp** | Twilio | Shift-fill automation, alerts |
| **AI / LLMs** | OpenAI GPT-4o · Anthropic Claude · Google Gemini · Perplexity | Multi-model routing via AI orchestrator |
| **Identity** | SAML 2.0 | Enterprise SSO, JIT user provisioning |
| **HMRC** | RTI Direct Submission | Full Payment Submission (FPS), Employer Payment Summary (EPS) |
| **Deployment** | Fly.io (London — LHR) | kin2serviceslimited.co.uk — production and staging environments, UK data residency |
| **CI/CD** | GitHub Actions | 21 workflows: secret guard, deploy, monitor, CodeQL, SBOM, SLSA, compliance gate, auto-merge |

## Key architectural decisions

### Multi-tenant isolation
Every database query is scoped to `organization_id`. Cross-tenant data access is architecturally impossible — there is no admin bypass or shared data store.

### AI agent architecture
14 autonomous agents run as background services. Each agent has a defined scope, input/output schema, and human-in-the-loop checkpoints (GDPR Article 22 compliant). Agents cover:
- Demand forecasting
- Timesheet fraud detection
- Right-to-Work document intelligence
- NLW/NMW compliance monitoring
- Shift anomaly detection
- Predictive scheduling

### Compliance engine
UK employment law compliance is enforced at the data layer, not the UI layer:
- NLW/NMW rates validated on every wage write (April 2026: £13.03/hr 21+)
- AWR 12-week tracking runs as a background job
- IR35 assessments stored with full audit trail
- GDPR consent records immutable once written

### CI/CD pipeline
Every push to `main` runs through:
1. Secret Guard (hard gate — blocks deploy if live keys found in source)
2. Dependency Review (blocks HIGH/CRITICAL CVEs and GPL/AGPL/LGPL licences)
3. Compliance gate — NLW rate assertion, CRITICAL vulnerability gate
4. Deploy to production and staging environments
5. Health check (kin2serviceslimited.co.uk)
6. Inline deploy alert (opens GitHub Issue + assigns Copilot on failure)

Every release:
- SBOM generated in SPDX-JSON and CycloneDX formats, attached to GitHub Release
- SLSA Level 2 build provenance attestation attached to every release artifact

Scheduled:
- Health monitor every 30 minutes
- NLW rate review reminder every 1 April and 1 November
- Security audit (npm audit) weekly — opens deduplicated GitHub Issue on HIGH/CRITICAL
- CodeQL static analysis weekly (Tuesdays 03:00 UTC) and on every PR
- Stale issue/PR cleanup daily

## Repository structure

```
client/         React frontend (TypeScript + Vite)
  src/
    components/ UI components (shadcn/ui + custom)
    pages/      Route-level page components
    hooks/      Custom React hooks
    locales/    i18n strings (14 languages)
server/         Express backend (TypeScript)
  routes/       API route handlers (thin — delegate to storage)
  services/     Business logic and compliance engines
  middleware/   Auth, error handling, rate limiting
shared/
  schema.ts     Drizzle ORM schema + Zod types (single source of truth)
.github/
  workflows/    21 CI/CD pipelines
  copilot-instructions.md
  claude-instructions.md
```

## Deployment

See [DEPLOYMENT.md](DEPLOYMENT.md) for the full deployment guide — Dockerfile, Fly.io configuration, GitHub Actions integration, environment variables, and rollback procedure.

## Compliance certifications

- ICO Registration: C1895789
- Company: Kin2 Services Limited · No. 14672114
- GDPR / UK GDPR: Article 22 human-in-the-loop for all AI decisions
- HMRC: RTI-authorised payroll software
