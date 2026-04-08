# Public Release Notes

_Full changelog: [CHANGELOG.md](CHANGELOG.md)_

---

## v3.9.6 — 8 April 2026

**Summary**
CI/CD automation hardening + auto-merge safety fix

**Highlights**
- Auto-merge safety fix: Dependabot major-update PRs previously received both `copilot-review` and `major-update` labels — the Copilot auto-merge job would have merged them without human review. Fixed with an explicit guard condition.
- Dependabot reviewer: Replaced non-existent `kin2-team` reviewer with `Kenkin2` (the actual owner) across all three dependency ecosystems (npm, docker, GitHub Actions).
- Deploy alert system: Moved alerting inline into `deploy.yml` (eliminating cross-workflow dependency), added `issues: write` permission, inline alert distinguishes token expiry vs. other failures.
- NLW/NMW compliance: Updated UK statutory rates to **April 2026** across the compliance engine, API responses, and frontend. Rates: 21+ £13.03, 18–20 £10.66, 16–17 £7.79, Apprentice £7.79. Reduced npm HIGH vulnerabilities from 10 to 1 via `npm audit fix`.

---

## v3.9.5 — 8 April 2026

**Summary**
Annual NLW rate update workflow + security vulnerability reduction

**Highlights**
- Annual NLW update workflow: New `.github/workflows/nlw-update.yml` fires every 1 April (HMRC statutory rates) and 1 November (Living Wage Foundation rates), opens a GitHub Issue with a full update checklist, auto-assigns Copilot, and deduplicates.
- NLW/NMW rates updated to April 2026 statutory rates throughout the compliance engine.
- npm audit: Resolved 9 vulnerabilities (`npm audit fix`), reducing HIGH count from 10 to 1.

---

## v3.9.4 — 8 April 2026

**Summary**
Deploy alert permissions fix + inline alerting

**Highlights**
- Fixed `deploy-alert.yml` missing `actions: read` permission (caused all deploy alerts to fail silently).
- Moved deploy failure alerts from a separate workflow into `deploy.yml` as an inline step — fires immediately on failure, eliminates cross-workflow event dependency.
- Deploy to Production workflow confirmed green on all recent commits.

---

## v3.9.3 — 7 April 2026

**Summary**
Dependabot dependency updates + CI pipeline stability

**Highlights**
- Merged Dependabot PRs #215 (Vite) and #216 (drizzle-orm) — patch/minor security updates.
- Secret Guard false positive fix: `.env` pattern updated to avoid flagging example files.
- Copilot auto-merge actor corrected (`Copilot`, not `copilot[bot]`).
- Full automation loop: `auto-assign.yml`, `ci-fix.yml`, `stale.yml`, `deploy-alert.yml` — all configured.
- Kin2 Monitor cron updated to every 30 minutes.

---

## v3.8.0 — 2 April 2026

**Summary**
Enterprise SSO · Shift-Fill SMS · Developer API · HMRC RTI · TUPE · AWR · IR35

**Highlights**
- **Enterprise SSO**: SAML 2.0 SP-initiated flow with JIT user provisioning on Growth and Scale plans
- **Shift-Fill Engine**: Availability-aware worker cover with Twilio SMS/WhatsApp messaging and one-tap shift acceptance
- **Developer API**: Public REST API — 54 documented endpoints, OAuth-compatible bearer tokens, key management, rate limiting (100 req/15min), OpenAPI spec
- **HMRC RTI Direct Submission**: Full Payment Submission (FPS) and Employer Payment Summary (EPS) sent directly to HMRC
- **TUPE Transfer Management**: End-to-end transfer workflow with worker consent tracking and timeline management
- **AWR Compliance Tracker**: 12-week qualifying period monitoring for Agency Workers Regulations
- **IR35 Status Checker**: 15-question weighted assessment engine — Inside / Outside / Borderline determination
- Multi-location Dashboard: Cross-site analytics and reporting now operational
- AI Document Intelligence: RTW document data extraction automated
- Timesheet Fraud Detection: GPS spoofing and pattern-based anomaly detection live
- Demand Forecasting: AI-powered shift demand predictions from historical patterns

**Critical fixes**
- Audit log multi-tenant isolation: Fixed cross-organisation data leakage in audit trail queries
- FCA/AML production gating: Regulated financial features now require explicit plan-level activation

---

## v3.7.7 — 29 March 2026

**Summary**
IR35 Status Checker + AWR Compliance Tracker

**Highlights**
- IR35 Status Checker: 15-question weighted assessment for contractor tax status (Inside/Outside/Borderline)
- AWR Compliance: 12-week qualifying period tracker for Agency Workers Regulations
- Database: Fixed shift-fill table schema references and Neon serverless driver compatibility

---

## v3.7.3 — 28 March 2026

**Summary**
Trust and conversion — commercial polish

**Highlights**
- ROI Calculator: Industry-specific scenarios (Security/Care/Cleaning) with corrected annual pricing
- Pricing page: Outcome-led copy rewrite with objection-handling FAQ
- Trust signals: ICO registration (C1895789) and company details (Co. No. 14672114) added to landing page
- SEO: Consistent title, description, and canonical URL tags across all public pages

---

_For older releases, see [CHANGELOG.md](CHANGELOG.md)._
