# Launch readiness

[Docs](../README.md) / Launch / Readiness

Everything that must be in place before the pilot city goes live, beyond the product
itself. Items marked **Blocker** stop the launch; start them first, because several take
weeks outside our control.

Legal and tax items are questions to confirm with a lawyer and a chartered accountant (CA).
This page lists what to ask; it is not legal or tax advice.

Status values: Not started, In progress, Done, Not needed.

## 1. Legal, tax and payments

| # | Item | Why | Owner | Lead time | Priority | Status |
|---|---|---|---|---|---|---|
| L1 | Company registration and bank account | Needed for every account below | Founder | 2–4 weeks | Blocker | Not started |
| L2 | Razorpay business KYC and Route activation | Payments and vendor settlement cannot go live without it | Founder | 2–4 weeks | Blocker | Not started |
| L3 | Confirm money handling with Razorpay and a lawyer | Holding customer money and paying vendors ourselves can require an RBI payment-aggregator licence. Plan: settle through Route linked accounts so funds never sit in our bank account. See [Money flow](../flows/system/money-flow.md) | Founder, lawyer | 1–2 weeks | Blocker | Not started |
| L4 | GST registration and tax model sign-off | Platform pays GST on restaurant orders under GST section 9(5); collects TCS under GST and deducts TDS under section 194-O on vendor payouts. See [Taxes](../product/monetization.md#taxes) | CA | 2–3 weeks | Blocker | Not started |
| L5 | SMS DLT registration (entity, sender ID, every template) | Unregistered SMS, including OTPs, is not delivered in India | Engineering, founder | 2–4 weeks | Blocker | Not started |
| L6 | FSSAI licences | Food vendors need valid licences; confirm whether the platform also needs one as an e-commerce food business | Lawyer, operations | 2–6 weeks | Blocker | Not started |
| L7 | Terms of service, privacy policy, refund and cancellation policy | Required by the Consumer Protection (E-Commerce) Rules and app stores | Lawyer | 2–3 weeks | Blocker | Not started |
| L8 | Vendor agreement | Commission, plans, payouts, deductions, liability, termination | Lawyer | 2–3 weeks | Blocker | Not started |
| L9 | Rider agreement and insurance | Riders are gig workers; accident cover and Social Security Code duties | Lawyer, operations | 3–4 weeks | Blocker (phase 2) | Not started |
| L10 | Grievance officer named and shown in the apps | Required by e-commerce and data protection rules | Founder | 1 week | Blocker | Not started |
| L11 | DPDP Act compliance | Consent, privacy notice, breach notification process, data grievance contact | Lawyer, engineering | 2–3 weeks | Blocker | Not started |
| L12 | Seller details shown to buyers | E-commerce rules require seller name, address and grievance contact on each listing | Engineering | 1 week | Blocker | Not started |
| L13 | Trademark search and filing for the final name | Avoid a forced rename after launch | Lawyer | Filing 1 week | High | Not started |
| L14 | Pharmacy vertical | Online pharmacy rules in India are unsettled; deferred until legal advice. See [decision 12](../decisions/README.md) | Lawyer | — | Deferred | Not started |

## 2. Product

| # | Item | Why | Owner | Priority | Status |
|---|---|---|---|---|---|
| P1 | Per-item GST rates and invoices | Correct tax on every order line; who issues which invoice | Engineering, CA | Blocker | Not started |
| P2 | Coupon funding (platform or vendor) | Decides whose earning a discount reduces. See [Discounts and fees](../product/monetization.md#discounts-and-fees) | Product | Blocker | Not started |
| P3 | Fees: packaging, delivery, small-order, rider tip | Price shown at checkout must match what is charged and settled | Product | Blocker | Not started |
| P4 | Store busy mode | Vendors pause or slow new orders at peak without closing | Product | High | Not started |
| P5 | Menu timings and scheduled orders | Breakfast-only items; order now for later | Product | Medium | Not started |
| P6 | Fraud controls | Cash-on-delivery abuse, coupon abuse, fake accounts, refund abuse, rider GPS spoofing | Product, engineering | High | Not started |
| P7 | Help centre and in-app support chat | Customers and vendors need a way to reach support | Product | Blocker | Not started |
| P8 | Hindi and regional languages | At least for vendor and rider apps | Product | High | Not started |
| P9 | Rider safety: SOS, insurance details, earnings statements | Needed before the rider app launches | Product | Blocker (phase 2) | Not started |
| P10 | Referral codes, deep links, SEO pages for cities and stores | Growth basics | Product | Medium | Not started |
| P11 | Product analytics (PostHog or Mixpanel) | Measure browse-to-checkout conversion from day one | Engineering | High | Not started |

## 3. Engineering and operations

| # | Item | Why | Owner | Priority | Status |
|---|---|---|---|---|---|
| E1 | Dev, staging and production environments | Test safely before release | Engineering | Blocker | Not started |
| E2 | Database migration and rollback process | Schema changes without downtime or data loss | Engineering | Blocker | Not started |
| E3 | Disaster recovery targets and tested restore | Decide how much data we can lose and how long we can be down; database across multiple availability zones | Engineering | Blocker | Not started |
| E4 | Monitoring, alerts and on-call rota | Know about failures before customers report them | Engineering | Blocker | Not started |
| E5 | Incident process and public status page | Clear steps and communication during outages | Engineering | High | Not started |
| E6 | Security testing (VAPT) and dependency scanning | Payment partners often require a VAPT report | Engineering | Blocker | Not started |
| E7 | Testing strategy: unit, integration, end-to-end | Catch regressions before release | Engineering | Blocker | Not started |
| E8 | Load test to 1 lakh concurrent users | Prove the [scaling targets](../architecture/scaling.md) | Engineering | High | Not started |
| E9 | Feature flags per city | Turn features on gradually; switch off fast | Engineering | High | Not started |
| E10 | Email domain setup (SPF, DKIM, DMARC) | Keep emails out of spam | Engineering | Blocker | Not started |
| E11 | App store accounts, push certificates, over-the-air updates | Needed to ship native apps | Engineering | Blocker (phase 2) | Not started |
| E12 | Monthly cost estimate | Cloud, Maps, SMS and payment fees at pilot scale and at 1 lakh users | Engineering, founder | High | Not started |
| E13 | Payment and payout reconciliation report | Match our ledger to Razorpay's settlement reports daily | Engineering | Blocker | Not started |

## 4. Launch operations

| # | Item | Why | Owner | Priority | Status |
|---|---|---|---|---|---|
| O1 | Pilot city and launch zones chosen | Everything else is sized from this | Founder | Blocker | Not started |
| O2 | First vendors signed and onboarded | Enough stores that customers find something to order | Operations | Blocker | Not started |
| O3 | Delivery supply | Vendors' own riders at launch; platform rider sourcing for phase 2 | Operations | Blocker | Not started |
| O4 | Support staffing and hours | Who answers tickets, and response-time targets | Operations | Blocker | Not started |
| O5 | Go/no-go checklist and rollback plan | Agreed criteria for launching, and how to pause safely | Founder, engineering | Blocker | Not started |

## Go/no-go criteria

Launch only when all of these are true:

- [ ] Every **Blocker** above is Done or Not needed.
- [ ] Ten end-to-end test orders, paid online and by cash on delivery, have settled correctly to vendor bank accounts through Route.
- [ ] A refund and a cancellation have been tested end to end, including tax and ledger reversals.
- [ ] The load test meets the targets in [Scaling and traffic](../architecture/scaling.md).
- [ ] A database restore has been tested.
- [ ] On-call, support and the grievance officer are reachable during launch hours.
