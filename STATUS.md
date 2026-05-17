# Platform Status

_Last updated: 17 May 2026 · Current version: v3.21.0_

## Live now

### Core workforce operations
- Shift scheduling — drag-and-drop rota builder with conflict detection
- GPS clock-in / clock-out — location-verified attendance, geofence alerts
- Timesheet management — digital approval chains, overtime tracking
- Staff records — employment history, documents, emergency contacts
- Communications — team messaging, announcements, shift notifications

### Payroll and compliance
- Payroll calculation support workflows
- HMRC RTI Direct Submission — Full Payment Submission (FPS) and Employer Payment Summary (EPS)
- NLW/NMW enforcement — **April 2026 rates** (£13.03/hr NLW, £10.66 18-20, £7.79 16-17)
- AWR Compliance Tracker — 12-week qualifying period monitoring for agency workers
- IR35 Status Checker — 15-question weighted contractor tax status assessment
- TUPE Transfer Management — end-to-end transfer workflows with worker consent tracking
- GDPR / UK GDPR workflows — data export, right to erasure, consent records
- Right-to-Work document verification and expiry tracking
- WTR monitoring — 48-hour opt-out, rest breaks, holiday accrual

### AI Agent Suite (v3.21.0 — 13 agents)

| Agent | Schedule | Purpose |
|---|---|---|
| Compliance Agent | Every 4 hours | RTW, WTR, NLW, certifications |
| Payroll Agent | Daily 06:00 UTC | Timesheet errors, NLW underpayment |
| Scheduling Agent | Every 2 hours | Unfilled shifts, availability match |
| Founder Oversight Agent | Every 30 minutes | Platform health, critical errors |
| Tender Agent | Daily 07:00 UTC | Public-sector tender opportunities |
| Grant Agent | Daily 07:30 UTC | Grant and funding opportunities |
| Absence Risk Agent | Weekly Monday 08:00 | Bradford Factor scoring |
| Cost Optimisation Agent | Weekly Monday 09:00 | Overtime patterns, rate benchmarking |
| Onboarding Validation Agent | Daily 08:30 UTC | New worker document gaps (14-day window) |
| Document Intelligence Agent | Daily 09:00 UTC | RTW expiry, stale DBS, missing docs |
| Workforce Forecasting Agent | Weekly Monday 06:00 | Coverage gaps, demand patterns |
| Legal Monitor Agent | Weekly Monday 07:00 | AWR threshold, young workers, zero-hours |
| Report Generation Agent | Weekly Monday 07:30 | Health summaries, payroll readiness |

All agents are advisory only. No autonomous decisions on pay, dismissal, or Right to Work (GDPR Article 22). Human approval required for flagged actions.

### Platform features
- Billing and subscriptions — Starter · Growth · Scale plans via Stripe
- Enterprise SSO — SAML 2.0 SP-initiated with JIT user provisioning (Growth / Scale)
- Shift-fill automation — Twilio SMS/WhatsApp cover requests, one-tap acceptance
- Developer API — REST API with key management and rate limiting
- Multi-location dashboard — cross-site analytics and reporting
- BYOK AI — bring your own OpenAI/Anthropic/Gemini key (Growth/Scale/Enterprise)
- Founder cost dashboard — per-org AI running cost vs plan revenue monitoring
- Mobile app (React Native 0.75) — iOS and Android, GPS clock-in, offline queue, push notifications

### Security and compliance
- Multi-tenant isolation — every database query filtered by `organization_id`
- 446 compliance tests passing (NLW, WTR, IR35, AWR, Bradford Factor, AI Article 22, multi-tenant)
- AES-256-GCM encryption for BYOK keys (AWS KMS with local fallback)
- Route security audit — 215 organisation-scoped, 203 authenticated, 50 public/system
- OWASP route scoping audit script — CI-enforceable

### GitHub and DevOps (v3.21.0)
- 21 GitHub Actions workflows — full CI/CD pipeline
- NLW gate — CI fails if any code path would pay below HMRC statutory minimums
- Dependency review — PRs blocked on HIGH/CRITICAL vulnerabilities or viral licences
- SBOM generation — SPDX-JSON and CycloneDX on every GitHub Release
- SLSA Level 2 build provenance attestation
- Docker build passing (golang:1.23-alpine — fixed from 1.26)
- Kubernetes manifests — deployment, HPA, PDB, ingress, namespace, secrets (v3.21.0)

### In active development
- Webhooks delivery infrastructure — retry, HMAC-SHA256 signing, auto-disable (existing)
- Advanced reporting — compliance dashboards, payroll summaries
- OpenAPI 3.1 specification
- Developer portal at `/developers`

### Certification roadmap
1. Internal security checks — in progress
2. Cyber Essentials via IASME — requires founder action
3. Cyber Essentials Plus — follows above
4. CREST-accredited penetration test — requires engagement
5. SOC 2 readiness gap analysis — planned

### What requires founder/company action
- Cyber Essentials application (IASME)
- CREST-accredited penetration test
- HMRC production RTI setup (live PAYE reference)
- Apple/Google developer accounts (App Store / Play Store)
- Pilot customer acquisition
- Render/cloud account access and staging environment
- Business banking / Stripe verification

---

## Contact

- Website: [kin2serviceslimited.co.uk](https://kin2serviceslimited.co.uk)
- Demo: [Book a demo](https://kin2serviceslimited.co.uk/book-demo)
- Email: [kin@kin2serviceslimited.com](mailto:kin@kin2serviceslimited.com)
- Security: security@kin2serviceslimited.co.uk

_Kin2 Workforce is a serious UK workforce SaaS platform for small and medium businesses. It is in active development. Claims on this page reflect code and tests, not third-party certification unless stated._
