# Monetization

[Docs](../README.md) / Product / Monetization

Revenue comes from two streams: a commission on each order line, and a monthly plan fee
from each vendor.

## Category-wise commission

The rate for an order line is the first one that exists, in this order:

1. A store-specific rate for that category
2. The category's rate
3. The platform default

The vendor's plan can then lower it.

```text
commission     = line total × (category rate − plan discount)
vendor earning = line total − commission − GST on commission − TCS − TDS
```

GST, TCS and TDS are explained under [Taxes](#taxes).

The rate is copied onto the order line at purchase, so a later rate change never rewrites
past orders.

## Vendor subscription plans

Plans are configured by the admin. These three are examples and the prices are placeholders.

| | Free | Growth | Pro |
|---|---|---|---|
| Price per month (INR) | 0 | 999 | 2,999 |
| Products allowed | 50 | 500 | Unlimited |
| Commission discount (points) | 0 | 1 | 3 |
| Featured slots | 0 | 1 | 5 |
| Analytics | Basic | Advanced | Advanced with export |

Razorpay webhooks drive renewals and a nightly job reconciles them. One entitlement check
enforces plan limits for every module. States: [Subscription lifecycle](../flows/system/subscription-lifecycle.md).

## Discounts and fees

Every discount and fee records who funds it or who receives it, so each party's earning is
correct.

| Item | Paid by | Goes to | Notes |
|---|---|---|---|
| Platform coupon | Platform | Customer (discount) | Vendor earning is unchanged; the platform's share is reduced |
| Store coupon | Vendor | Customer (discount) | Reduces the vendor's earning; commission is calculated on the discounted price |
| Co-funded coupon | Split by agreed % | Customer (discount) | The split is set on the coupon when it is created |
| Delivery fee | Customer | Platform, or vendor when the vendor delivers | Set per zone or per store |
| Packaging charge | Customer | Vendor | Set per product or per store |
| Small-order fee | Customer | Platform | Below a minimum order value |
| Rider tip | Customer | Rider, in full | Not subject to commission |

## Taxes

These are the rules to confirm with a chartered accountant before launch. Rates change, so
they are stored as configuration, not code.

| Tax | What it is | Effect on the platform |
|---|---|---|
| GST on goods and services | Each product has a GST rate by category | Shown per line; prices are stored either tax-inclusive or tax-exclusive per store |
| GST on restaurant orders (GST section 9(5)) | For food ordered from restaurants, the platform, not the restaurant, collects and pays this GST | The platform issues the invoice for restaurant orders; the vendor's earning excludes this GST |
| GST on commission and fees | The platform's own services to vendors | Charged to the vendor and shown on the commission invoice |
| TCS under GST | Tax the platform must collect on vendors' taxable sales | Deducted from vendor earnings and filed by the platform |
| TDS under section 194-O | Income tax the platform must deduct on payments to vendors | Deducted from vendor earnings; vendors receive a TDS certificate |

## Money flow

The platform never holds vendor money in its own bank account. Payments are split and
settled through **Razorpay Route**: each vendor has a linked account, and their share of
each payment is transferred to it and held until it is safe to release.

1. The customer pays through Razorpay.
2. On payment, the vendor's share is transferred to the vendor's Route linked account, on hold. The platform's share (commission, fees, platform-collected taxes) stays with the platform.
3. Two days after delivery, if no refund is pending, the hold is released and Razorpay settles the vendor's share to their bank.
4. A refund or cancellation reverses the vendor's transfer, if needed, and refunds the customer. The ledger posts reversing entries; nothing is edited.
5. Our ledger mirrors every transfer and is reconciled daily against Razorpay's settlement report.

How the hold, release and reversal work in Route must be confirmed with Razorpay during
onboarding. See [Launch readiness](../launch/readiness.md).

Diagram: [Money flow](../flows/system/money-flow.md). Storage rules: [Data model](../architecture/data-model.md#rules-that-protect-money-and-history).
