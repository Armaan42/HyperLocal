# Decision log

[Docs](../README.md) / Decisions

Choices made so far. Each one is a default that can still change before the build starts;
the last column says what a different choice would cost.

| # | Question | Decision | Status | What changes if reversed |
|---|---|---|---|---|
| 1 | Country and currency | India, INR | Default, unconfirmed | Stripe Connect replaces Razorpay; tax and SMS providers change |
| 2 | Who delivers | Vendors' own riders at launch; platform riders in phase 2 | Default, unconfirmed | A fleet at launch pulls the rider app and dispatch into phase 1 |
| 3 | First verticals | Food and grocery | Default, unconfirmed | Pharmacy adds prescription upload and compliance checks |
| 4 | Mobile | Installable web app first, native apps in phase 2 | Default, unconfirmed | Native from day one adds app-store work to phase 1 |
| 5 | Auth | Built into the API | Default, unconfirmed | A bought service (Clerk, Supabase Auth) saves build time for a monthly fee |
| 6 | Hosting | AWS, Mumbai region | Default, unconfirmed | A simpler platform (Render, Fly.io) is cheaper at pilot scale |
| 7 | Backend shape | NestJS modular monolith, not microservices | Decided | Microservices add deployment and operations work before there is load to justify it |
| 8 | Rider assignment | Riders accept open jobs themselves | Decided | Auto-assignment needs a dispatch algorithm and rider acceptance rules |
| 9 | Product limits | Capped by the vendor's plan; no platform-wide limit | Default, unconfirmed | Uncapped products on every plan removes one reason to upgrade |
| 10 | Order cancellation | Allowed until the vendor marks the order ready | Default, unconfirmed | A later cutoff means refunds for prepared orders |
| 11 | Holding vendor money | Never in the platform's bank account; vendor shares settle through Razorpay Route linked accounts, on hold until 2 days after delivery | Decided, confirm with lawyer and Razorpay | Holding funds ourselves can require an RBI payment-aggregator licence |
| 12 | Pharmacy vertical | Deferred until legal advice on online pharmacy rules | Decided | Launching pharmacy adds licensing, prescription checks and legal risk |
| 13 | Coupon funding | Every coupon is marked platform-funded, vendor-funded or co-funded | Decided | Without it, vendor earnings and platform margin cannot be calculated correctly |

## Adding a decision

Add a row with the next number. When a decision needs more than one line of reasoning,
create `decisions/NNNN-short-title.md` (context, options considered, decision, consequences)
and link it from the Decision cell.
