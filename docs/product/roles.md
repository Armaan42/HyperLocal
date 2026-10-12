# Roles

[Docs](../README.md) / Product / Roles

Five roles use four apps. The support agent has no app of their own; they log into the
admin panel with restricted permissions.

| Role | App | What they do | Flow |
|---|---|---|---|
| Customer | Customer web app (installable PWA); native app in phase 2 | Find nearby stores, order, pay, track, reorder, review | [Customer journey](../flows/customer/README.md) |
| Vendor | Vendor dashboard | Onboard, manage catalog and stock, accept orders, see earnings, manage their plan | [Onboarding](../flows/vendor/onboarding.md), [Order handling](../flows/vendor/orders.md) |
| Rider | Rider mobile app (phase 2) | Go online, accept jobs, navigate, confirm delivery, see payouts | [Rider delivery](../flows/rider/jobs-and-delivery.md) |
| Admin | Admin panel | Approve vendors, draw zones, set categories, commissions and plans, settle payouts, read reports | [Admin operations](../flows/admin/README.md) |
| Support agent | Admin panel, restricted role | Look up orders, issue refunds within a limit, handle disputes | [Support](../flows/support/refunds-and-disputes.md) |

## Permissions at a glance

| Capability | Customer | Vendor | Rider | Support agent | Admin |
|---|---|---|---|---|---|
| Place orders | Yes | | | | |
| Manage own store and products | | Yes | | | |
| Accept delivery jobs | | | Yes | | |
| View any order | | | | Yes | Yes |
| Issue refunds | | | | Within limit | Yes |
| Approve vendors and riders | | | | | Yes |
| Set commissions, plans, zones | | | | | Yes |
| Settle payouts | | | | | Yes |

Diagram: [Roles and apps](../flows/system/roles-and-apps.md).
