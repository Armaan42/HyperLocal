# Security and compliance

[Docs](../README.md) / Architecture / Security and compliance

These controls ship with the first release, not after it.

| Area | Control |
|---|---|
| Access | Role-based permissions with least privilege; every admin action lands in an audit log that cannot be edited |
| Tenant isolation | Every vendor-scoped query is filtered by `vendor_id` in the service layer, with tests that try to read another vendor's data |
| Payments | Card data never touches our servers (Razorpay-hosted checkout); every webhook signature is verified |
| Documents and personal data | KYC files sit in a private bucket behind expiring signed links; personal data is encrypted at rest |
| Input and transport | Schema validation on every request, parameterized queries only, HTTPS everywhere, secure cookies, a content security policy |
| Secrets | Held in AWS Secrets Manager and rotated; none in the repository |
| Recovery | Daily backups with point-in-time recovery, and a restore tested before launch |
| Privacy | Consent capture plus export and delete flows under India's DPDP Act |
| Tax | GST invoices for orders and commission, and the tax a marketplace must collect or deduct on vendor payouts |

## Open item

An accountant must confirm the GST and payout tax rules before launch.

Related: [Roles and permissions](../product/roles.md#permissions-at-a-glance).
