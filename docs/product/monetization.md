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
vendor earning = line total − commission − tax on commission
```

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

## Money flow

1. The customer pays the platform through Razorpay.
2. On delivery, the ledger credits the vendor with the order value less commission.
3. A scheduled payout sends the vendor's balance to their bank two days after delivery.
4. A refund or cancellation posts a reversing ledger entry; nothing is edited.

Diagram: [Money flow](../flows/system/money-flow.md). Storage rules: [Data model](../architecture/data-model.md#rules-that-protect-money-and-history).
