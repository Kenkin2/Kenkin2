# Roadmap

_Last updated: May 2026 · Current version: v3.21.0_

For what is live today, see [STATUS.md](STATUS.md). For version history, see [RELEASES.md](RELEASES.md).

---

## In active development

### Webhooks and automation
Rule-based event triggers and outbound delivery infrastructure. Allows organisations to connect Kin2 Workforce events (shift published, timesheet approved, compliance alert, clock-in) to external systems without polling the API.

### Advanced reporting
Organisation-level analytics and compliance dashboards. Covers workforce cost breakdowns, shift coverage rates, NLW exposure reports, and AWR qualifying period summaries across all locations.

---

## Next up

### Mobile app (iOS and Android)
Native mobile application for field workers. Priority features: GPS clock-in / clock-out, shift viewing, timesheet submission, and shift-fill one-tap acceptance. Required to replace browser-based clock-in for care and security staff with limited connectivity.

### Offline mode
Clock-in and shift data sync on reconnect. Targets care and security workers in low-signal environments where a browser-based GPS session is not reliable.

### Marketplace integrations
Third-party connector framework for accounting (Xero, QuickBooks), HR (BambooHR), and payroll (Sage, IRIS). Builds on the existing public API foundation.

### API expansion
Additional endpoints beyond the current 54, covering webhooks management, bulk operations, and compliance report exports. Full OpenAPI 3.0 spec maintained.

---

## Future

### Biometric and NFC clock-in
Alternative to GPS-only verification for high-security sites or environments where GPS spoofing risk is elevated. Complements the existing fraud detection layer.

### Customer webhook portal
Self-service UI for configuring and monitoring webhook endpoints, delivery logs, and retry history. Builds on the Webhooks and automation work above.

---

## Completed

| Feature | Version | Notes |
|---|---|---|
| Payroll Summary to core nav; pilot pack, ops checklist, governance docs | v3.21.0 | Starter users can access payroll export; pilot + ops documentation complete |
| SaaS plans (Starter/Growth/Scale), SAIS AI add-ons billing, employee limit enforcement | v3.21.0 | Stripe integration; 9 AI add-ons (£19–£99/mo); plan-gated worker cap |
| Personal Data Vault — GDPR Art.20 export + Art.17 erasure | v3.21.0 | Full audit trail, rate-limited |
| Production lock-file repair, HIGH vulnerability eliminated | v3.21.0 | 0 HIGH/CRITICAL (was 1 HIGH via Replit packages) |
| Soft-open runtime proxy on Fly.io | v3.21.0 | Health-check gated startup |
| Enterprise-grade platform — security, API, pricing, compliance docs | v3.21.0 | |
| 50+ client/server API contract fixes | v3.20.0 | |
| Bulk expense actions, payslip PDF download, payroll CSV export | v3.19.0 | |
| GitHub Actions hardening — 21 workflows, SBOM, SLSA Level 2, CodeQL | v3.9.8 | |
| Compliance enforcement automation — NLW gate, vulnerability gate, GPL licence gate | v3.9.7 | |
| Auto-merge safety fix, NLW/NMW April 2026 rates, deploy alert system | v3.9.6 | |
| Annual NLW update workflow, security vulnerability reduction | v3.9.5 | |
| CI pipeline stability, Dependabot updates, Secret Guard fixes | v3.9.3 | |
| Enterprise SSO — SAML 2.0 SP-initiated, JIT user provisioning | v3.8.0 | Growth and Scale plans |
| Shift-Fill Engine — Twilio SMS/WhatsApp, one-tap acceptance | v3.8.0 | |
| Developer API — 54 endpoints, key management, rate limiting, OpenAPI spec | v3.8.0 | |
| HMRC RTI Direct Submission — FPS and EPS | v3.8.0 | |
| TUPE Transfer Management — end-to-end workflow, worker consent tracking | v3.8.0 | |
| AI workforce agents — 14 autonomous agents (demand forecasting, fraud detection, document intelligence, compliance monitoring) | v3.8.0 | |
| Multi-location dashboard — cross-site analytics and reporting | v3.8.0 | |
| AWR Compliance Tracker — 12-week qualifying period monitoring | v3.7.7 | |
| IR35 Status Checker — 15-question weighted assessment | v3.7.7 | |
| RTW Document AI — automated right-to-work data extraction | v3.7.7 | |
| Timesheet Fraud Detection — GPS spoofing and pattern anomaly detection | v3.7.7 | |
| Demand Forecasting — AI-powered shift demand predictions | v3.7.7 | |
