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

### Platform features
- Billing and subscriptions — Starter · Growth · Scale plans via Stripe
- Enterprise SSO — SAML 2.0 SP-initiated with JIT user provisioning (Growth / Scale)
- Shift-fill automation — Twilio SMS/WhatsApp cover requests, one-tap acceptance
- Developer API — public REST API with documented endpoints, key management, rate limiting
- Multi-location dashboard — cross-site analytics and reporting
- AI workforce agents — 6 active agents (compliance, payroll, scheduling, tender, grant, founder oversight); all advisory with GDPR Article 22 human-in-the-loop gates
- Demand forecasting — AI-powered shift demand predictions from historical patterns
- RTW Document AI — automated Right-to-Work document data extraction
- Timesheet fraud detection — GPS spoofing and pattern-based anomaly detection
- BYOK AI — customer-provided API keys with AES-256-GCM encryption and AWS KMS fallback

### v3.21.0 additions
- Operational knowledge graph — event stream projection service for shift and compliance events
- Skill ecosystem — agent skill registry and orchestrator with capability routing
- H3 spatial indexing — geofence optimisation for high-density GPS clock-in
- Columnar analytics store — OLTP→OLAP bridge for timesheet and payroll reporting at scale
- Internal event bus — decoupled domain event emission from timesheets, shifts, and payroll
- Read replica routing — consistency-level routing to separate analytical from transactional queries
- RAG architecture — chunked document retrieval and vector search preview endpoints
- Ops Agent subsystem — AI infrastructure agent with DB schema, API routes, and health monitoring
- Cursor-based pagination — stable ordering on notifications and activity feeds

### GitHub and DevOps (v3.21.0)
- 21 GitHub Actions workflows — full CI/CD pipeline with concurrency controls, timeouts, and job summaries
- NLW gate — CI fails if any code path would pay below HMRC statutory minimums
- Dependency review — PRs blocked on HIGH/CRITICAL vulnerabilities or viral (GPL) licences
- SBOM generation — SPDX-JSON and CycloneDX attached to every GitHub Release
- SLSA Level 2 build provenance attestation on every release artifact
- App-to-GitHub integration — compliance schedulers open tracked Issues directly from the running app
- production + staging deployment environments with protected secrets
- Projects v2 board: [Kin2 Workforce Roadmap](https://github.com/users/Kenkin2/projects/2)
- i18n hardcode audit — CI guard preventing locale-key logic from being driven by hardcoded strings
- Feature-specific rate limiters — per-endpoint limits for AI, payroll, and developer API routes

### In active development
- Mobile app (React Native) — offline queue, GPS geofencing, push notifications; backend integration in progress
- Additional AI agents — tender discovery integration with live public-sector tender sources
- Enterprise SCIM directory sync — beyond SAML SSO
- Cyber Essentials certification — pre-Enterprise sales milestone
- Formal penetration test — planned at Scale milestone

---

## Contact

- Website: [kin2serviceslimited.co.uk](https://kin2serviceslimited.co.uk)
- Demo: [Book a demo](https://kin2serviceslimited.co.uk/book-demo)
- Email: [kin@kin2serviceslimited.com](mailto:kin@kin2serviceslimited.com)
