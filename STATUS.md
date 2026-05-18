# Kin2 Workforce — Current Status

> Last updated: 2026-05-18
> This is an honest, public-facing summary. It does not exaggerate or claim completion without evidence.

---

## What Kin2 Workforce is

Kin2 Workforce is a workforce management platform for UK small businesses. It helps organisations manage workers, shifts, timesheets, documents, payroll preparation, compliance organisation, and reports in one place.

**Company:** Kin2 Services Limited
**Founder:** Kennedy Kintu Gayita
**Stage:** Customer-acquisition validation — building toward first pilot customer

---

## Current build status

| Area | Status |
|------|--------|
| Core workforce features | Built — requires QA evidence |
| Shift and calendar management | Built — requires QA evidence |
| Timesheet approval flow | Built — requires QA evidence |
| Payroll export preparation | Built — requires QA evidence |
| Document storage | Built — requires QA evidence |
| Compliance dashboard | Built — requires QA evidence |
| Reports | Built — requires QA evidence |
| AI assistant (advisory only) | Built — limited to Starter tier |
| BYOK AI | Built — Growth/Scale/Enterprise |
| Mobile app (React Native) | Built — requires App Store setup |
| Password login | Built — being verified |
| Google OAuth | On hold — requires production verification |
| Render production deployment | Active — health checks passing |
| Fly.io | Legacy — archived |

---

## What still needs to happen before launch

- Golden Path QA with full evidence (screenshots, pass/fail logs)
- One real pilot customer onboarded
- Password login end-to-end verification
- Google OAuth production verification or friendly disable
- Usage/cost tracking per customer
- Cyber Essentials application
- Business banking / Stripe verification
- Apple and Google developer accounts (mobile)
- HMRC RTI production setup

---

## What the product does NOT do yet

- Kin2 is not yet certified under Cyber Essentials or SOC 2
- The mobile app is not yet on the App Store or Google Play
- No external penetration test has been completed
- AI features are advisory only — they do not make legal or HR decisions

---

## Deployment

**Production:** Render (cloud)
**Health checks:** `/health`, `/health/live`, `/health/ready`
**Version:** v3.21.0

---

## Contact and demo

If you are a small UK business interested in a founding pilot:
- Contact us for a setup walkthrough
- Founding offer: £99 setup + £39/month for 6 months
- In exchange for honest feedback used anonymously as a case study

---

## Links

- Full product: [Kin2Workforce private repo](https://github.com/Kenkin2/Kin2Workforce) (private)
- Security contact: See SECURITY_CONTACT.md
- Privacy and legal: Available on request
