# Changelog

All notable changes to Kin2 Workforce are documented here.

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
