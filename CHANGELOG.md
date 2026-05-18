# Changelog

All notable changes to Kin2 Workforce are documented here.

---

## v3.9.8 — 8 April 2026

### DevOps and Security
- All 21 GitHub Actions workflows hardened with concurrency controls, explicit `timeout-minutes`, and `GITHUB_STEP_SUMMARY` output
- Secret Guard (`secret-guard.yml`) hardened with concurrency and timeout
- CodeQL code scanning enabled (GHAS) — runs weekly on Tuesdays 03:00 UTC and on every PR
- Release artifacts: SBOM (SPDX-JSON + CycloneDX) and SLSA Level 2 build provenance attached to every GitHub Release
- Dependency Review gate on all PRs: blocks HIGH/CRITICAL vulnerabilities and viral licences (GPL/AGPL/LGPL)
- App-to-GitHub integration: compliance schedulers open tracked GitHub Issues from the running app via `POST /api/github/dispatch`
- GitHub Environments: `production` and `staging` environments with protected secrets
- FUNDING.yml added; Projects v2 board published at [Kin2 Workforce Roadmap](https://github.com/users/Kenkin2/projects/2)

---

## v3.9.7 — 8 April 2026

### Compliance and Security
- Compliance check workflow (`compliance-check.yml`): NLW rate assertion gate, CRITICAL vulnerability gate, GPL licence gate — all block merge on failure
- Security audit workflow (`security-audit.yml`): weekly npm audit, opens a deduplicated GitHub Issue when HIGH/CRITICAL vulnerabilities are found
- `scripts/assert-nlw-rates.mjs`: validates all NLW/NMW constants match HMRC April 2026 statutory rates
- Compliance schedulers wired on server boot

---

## v3.9.6 — 8 April 2026

### Bug Fixes
- Auto-merge safety fix: Dependabot major-update PRs now blocked from auto-merge without human review (explicit guard condition added)
- Dependabot reviewer corrected to `Kenkin2` across all three dependency ecosystems (npm, docker, GitHub Actions)
- Deploy alert moved inline into `deploy.yml`, eliminating cross-workflow dependency; alert distinguishes token expiry vs. other failures

### Compliance
- NLW/NMW rates updated to April 2026 statutory rates: 21+ £13.03, 18–20 £10.66, 16–17 £7.79, Apprentice £7.79
- npm audit: reduced HIGH vulnerabilities from 10 to 1 via `npm audit fix`

---

## v3.9.5 — 8 April 2026

### New Features
- Annual NLW update workflow (`nlw-update.yml`): fires every 1 April and 1 November, opens a GitHub Issue with update checklist, auto-assigns Copilot, deduplicates

### Security
- npm audit: resolved 9 vulnerabilities, reducing HIGH count from 10 to 1

---

## v3.9.4 — 8 April 2026

### Bug Fixes
- Fixed `deploy-alert.yml` missing `actions: read` permission (previously caused all deploy alerts to fail silently)
- Deploy failure alerts moved from separate workflow into `deploy.yml` as inline step

---

## v3.9.3 — 7 April 2026

### Maintenance
- Merged Dependabot PRs: Vite (#215) and drizzle-orm (#216) — patch/minor security updates
- Secret Guard false positive fix: `.env` pattern updated to avoid flagging example files
- Copilot auto-merge actor corrected (`Copilot`, not `copilot[bot]`)
- Kin2 Monitor cron updated to every 30 minutes

---

## v3.8.0 — 2 April 2026

### New Features

**Enterprise SSO**
- SAML 2.0 SP-Initiated single sign-on for Growth and Scale plan organisations
- JIT (Just-in-Time) user provisioning on first login
- IdP metadata import and SP metadata export

**Shift-Fill Engine**
- Availability-aware worker matching for open shifts
- Twilio SMS and WhatsApp outreach with one-tap shift acceptance
- Fill audit trail with response tracking per worker

**Developer API**
- Public REST API with OAuth-compatible bearer token authentication
- API key management: create, rotate, and revoke keys from the admin portal
- Rate limiting: 100 requests per 15-minute window per key
- 54 documented endpoints with full OpenAPI 3.0 specification
- Interactive API reference at `/api/docs`

**HMRC RTI Direct Submission**
- Full Payment Submission (FPS) sent directly to HMRC on payroll finalisation
- Employer Payment Summary (EPS) for nil payment periods and reclaim declarations
- Submission status tracking and HMRC acknowledgement logging

**TUPE Transfer Management**
- End-to-end TUPE transfer workflow for business transfers and service provision changes
- Worker consent capture and timeline management
- Transfer pack generation with required statutory disclosures

**AWR Compliance Tracker**
- 12-week qualifying period monitoring for Agency Workers Regulations
- Automated alerts when workers approach or reach qualifying status
- Compliance dashboard for agency and hirers

**IR35 Status Checker**
- 15-question weighted assessment for contractor tax status determination
- Results: Inside IR35, Outside IR35, or Borderline with explanation
- Assessment records stored per engagement for audit purposes

**Observability**
- Chatwoot live support widget integrated for in-app customer support
- PostHog product analytics pipeline for feature usage tracking

### Bug Fixes

**Critical**
- Audit log multi-tenant isolation scoping: Resolved an issue where audit trail queries could expose records across organisation boundaries in shared-tenant deployments
- FCA/AML production gating: Regulated financial features (FCA-linked checks, AML transaction screening) now require explicit plan-level activation; features are fully gated in the UI and API until enabled by an authorised admin

**Platform**
- Predictive Intelligence SQL: Corrected FROM clause aliasing; all 5 prediction cards now return data correctly
- Schema initialisation: Idempotent boot-time table creation for all new compliance and API tables

### Security

- npm audit: 0 vulnerabilities across all production dependencies
- HMAC-SHA256 webhook signatures with timestamp and nonce to prevent replay attacks (applied to Developer API callbacks)
- API key hashing: Keys stored as bcrypt hashes; plaintext only shown once at creation

---

## v3.7.7 — 29 March 2026

### New Features
- IR35 Status Checker: 15-question weighted assessment for contractor tax status determination
- AWR Compliance Tracker: 12-week qualifying period monitoring for Agency Workers Regulations
- Database reconciliation: Fixed shift-fill table schema references and Neon serverless driver compatibility

---

## v3.7.3 — 28 March 2026

### New Features
- ROI Calculator: Industry-specific scenarios (Security/Care/Cleaning) with annual pricing accuracy corrected
- Pricing page: Outcome-led copy rewrite with objection-handling FAQ
- Trust signals: ICO registration (C1895789) and company details (Co. No. 14672114) added to landing page
- SEO: Consistent title, description, and canonical URL tags across all public pages

---

## v3.7.1 — 27 March 2026

### Bug Fixes
- Predictive Intelligence SQL: Corrected FROM clause aliasing; all 5 prediction cards now return data
- Job Board: `saved_jobs` table auto-created with supporting indexes
- Job Applications: `kfn_score` column added to prevent insertion errors

---

## v3.7.0 — 25 March 2026

### New Features
- Pricing page: Outcome-led taglines (replace spreadsheets, cut rostering time, manage multi-location)
- 5 new FAQ entries addressing common objections
- Trust strip updated with ICO registration reference

---

**Live at:** https://kin2serviceslimited.co.uk  
**Contact:** kin@kin2serviceslimited.com  
**Demo:** https://kin2serviceslimited.co.uk/book-demo
