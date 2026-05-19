# Platform Status

_Last updated: 19 May 2026_

## Current stage

**Production stabilisation · Controlled pilot preparation**

Kin2 Workforce is running on Fly.io (London, `lhr` region) and is being validated through a Golden Path QA process before wider customer rollout. Core workforce operations are functional. Some advanced modules are implemented and in internal testing — they are not yet pilot-proven.

---

## Confirmed functional

### Core workforce operations
- Shift scheduling — rota builder with conflict detection and mobile publishing
- Timesheet management — digital approval chains, overtime tracking
- Worker records — employment history, documents, emergency contacts, absence tracking
- Right-to-Work — document upload, verification status, expiry alerts
- Leave management — request and approval workflow
- Expense claims — submission and approval workflow
- HR management dashboard — workforce overview, status breakdown

### Payroll and compliance
- Payroll preparation — HMRC RTI-format output (FPS & EPS) for payroll providers
- NLW/NMW enforcement — **April 2026 rates** (£13.03/hr NLW, £10.66 18–20, £7.79 16–17)
- AWR Compliance Tracker — 12-week qualifying period monitoring for agency workers
- IR35 Status Checker — 15-question weighted contractor tax status assessment
- GDPR-aware workflows — data export, right to erasure, consent records (not a certified compliance tool)
- WTR monitoring — 48-hour opt-out, rest breaks, holiday accrual
- Compliance Action Inbox — prioritised alerts for expiring documents, RTW issues, NLW breaches

### Platform features
- Billing and subscriptions — Starter (£39/mo) · Growth (£79/mo) · Enterprise (£199/mo) via Stripe
- Multi-tenant — full organisation isolation, role-based access (admin / client / worker)
- AI advisory agents — agents for compliance monitoring, demand signals, document intelligence, absence risk — all advisory; human approval required
- Worker portal — workers can view own profile, shifts, timesheets, documents
- Developer API — REST API with documented endpoints and key management

### CI/CD and security (private repo)
- 21 GitHub Actions workflows with CI gate on every PR
- NLW gate — CI fails if any code path would pay below statutory minimums
- Dependency review — PRs blocked on HIGH/CRITICAL vulnerabilities
- Secret scanning with Gitleaks on every push
- SBOM generation — SPDX-JSON and CycloneDX attached to releases
- CodeQL code scanning

---

## In internal testing / not yet pilot-proven

The following modules are implemented and passing CI tests but have not yet been validated through a live customer pilot:

- HMRC RTI direct submission — format is ready; direct PAYE submission with HMRC not yet in pilot
- GPS clock-in / clock-out with geofence alerts
- Twilio SMS/WhatsApp shift-fill automation
- SAML 2.0 SSO
- Advanced analytics and demand forecasting
- Automated AI task scheduling

---

## In active development

- Golden Path QA — screenshot evidence for every core user journey
- Google OAuth production verification
- Performance review and offboarding modules
- Webhooks / automation rule triggers

---

## Contact

- Website: [kin2serviceslimited.co.uk](https://kin2serviceslimited.co.uk)
- Demo: [Book a demo](https://kin2serviceslimited.co.uk/book-demo)
- Email: [kin@kin2serviceslimited.com](mailto:kin@kin2serviceslimited.com)
