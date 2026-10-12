# Flows

[Docs](../README.md) / Flows

Flows are organised by role. Each role folder has a `README.md` with the overall journey
and one detailed file per screen area. System flows describe what happens behind the screens.

## Index

| Folder | Role | Detailed flows |
|---|---|---|
| [customer/](customer/README.md) | Customer | [Login](customer/login.md) · [Address](customer/address-and-location.md) · [Home and search](customer/home-and-search.md) · [Product and cart](customer/product-and-cart.md) · [Checkout](customer/checkout-and-payment.md) · [Tracking](customer/order-tracking.md) · [Reviews and refunds](customer/reviews-and-refunds.md) · [Account](customer/account.md) |
| [vendor/](vendor/README.md) | Vendor | [Onboarding](vendor/onboarding.md) · [Store setup](vendor/store-setup.md) · [Products](vendor/products.md) · [Orders](vendor/orders.md) · [Earnings and payouts](vendor/earnings-and-payouts.md) · [Subscription](vendor/subscription.md) |
| [rider/](rider/README.md) | Rider | [Onboarding](rider/onboarding.md) · [Jobs and delivery](rider/jobs-and-delivery.md) · [Earnings](rider/earnings.md) |
| [admin/](admin/README.md) | Admin | [Zones](admin/zones.md) · [Categories and commissions](admin/categories-and-commissions.md) · [Plans](admin/plans.md) · [Storefront](admin/storefront.md) · [Vendor approval](admin/vendor-approval.md) · [Orders and refunds](admin/orders-and-refunds.md) · [Payouts](admin/payouts.md) · [Riders, users and reports](admin/riders-users-reports.md) |
| [support/](support/README.md) | Support agent | [Refunds and disputes](support/refunds-and-disputes.md) |
| [system/](system/README.md) | Cross-role | [Roles and apps](system/roles-and-apps.md) · [Order lifecycle](system/order-lifecycle.md) · [Multi-store checkout](system/multi-store-checkout.md) · [Money flow](system/money-flow.md) · [Subscription lifecycle](system/subscription-lifecycle.md) |

## How a detailed flow file is laid out

Every detailed file has the same four parts:

1. **Flow:** a Mermaid diagram of the process, including decisions and failure paths.
2. **Actions:** a table with one row per button, field or gesture: the screen, the element,
   what the user does, what the system does, and where it leads.
3. **Rules and edge cases:** limits, timers and what happens when things go wrong.
4. **Related:** links to the flows on the other side of the same process.

Timers and limits in these files (OTP expiry, accept timer, refund window and so on) are
proposed defaults. Most are admin-configurable; change them here when they are decided.

## SVG exports for Figma

Every diagram is exported to [svg/](svg/), in a folder per role, named after its file
(`svg/customer/login.svg`; a file with two diagrams gives `-1` and `-2`). Drag a file into
Figma to get editable shapes and text.

## Adding a flow

1. Create `flows/<role>/<name>.md` following the layout above. Copy an existing file as a
   starting point.
2. Add it to the table in that role's `README.md` and to the index on this page.
3. Export its SVG:

   ```bash
   echo '{"htmlLabels":false,"flowchart":{"htmlLabels":false},"theme":"neutral"}' > mermaid.json
   bunx @mermaid-js/mermaid-cli -i docs/flows/<role>/<name>.md -o docs/flows/svg/<role>/<name>.svg -c mermaid.json -b white
   ```

   The tool appends `-1`, `-2` to the output name; for a single diagram rename it to
   `<name>.svg`. `htmlLabels: false` keeps labels as editable text in Figma.
