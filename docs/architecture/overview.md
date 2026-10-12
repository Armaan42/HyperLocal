# System overview

[Docs](../README.md) / Architecture / System overview

Every app reaches one API through Cloudflare. Slow work is handed to background workers,
and third-party services are called only from the backend.

```mermaid
flowchart TD
    subgraph clients [Apps]
        web["Customer web app<br/>Next.js PWA"]
        vendor["Vendor dashboard<br/>Next.js"]
        admin["Admin panel<br/>Next.js"]
        mobile["Mobile apps<br/>React Native, Expo"]
    end

    edge["Cloudflare<br/>CDN, firewall, DDoS and bot protection"]
    api["NestJS API<br/>stateless replicas behind a load balancer"]
    workers["Background workers<br/>payouts, invoices, renewals,<br/>notifications, search indexing"]

    subgraph data [Data stores]
        pg[("PostgreSQL + PostGIS<br/>orders, money, geo queries")]
        redis[("Redis<br/>cache, job queues, pub/sub")]
        search[("Typesense<br/>store and product search")]
        files[("R2 storage<br/>images, KYC documents")]
    end

    third["Third parties<br/>Razorpay, Google Maps, push, SMS, email"]

    web --> edge
    vendor --> edge
    admin --> edge
    mobile --> edge
    edge --> api
    api --> workers
    api --> pg
    api --> redis
    api --> search
    api --> files
    workers --> pg
    workers --> search
    api -.-> third
    workers -.-> third
```

## Backend modules

The API is a modular monolith: one deployable, split into modules with enforced boundaries.

`auth` · `users` · `vendors` · `catalog` · `inventory` · `geo` · `storefront` · `cart` ·
`checkout` · `orders` · `payments` · `commissions` · `subscriptions` · `ledger` · `payouts` ·
`dispatch` · `notifications` · `reviews` · `promotions` · `search-indexer` · `admin` · `analytics`

A module reaches another module's data only through that module's exported service or a
domain event, never by reading its tables. This is what keeps a later split into services cheap.

## Related

- [Tech stack](tech-stack.md)
- [Scaling and traffic](scaling.md)
- [Data model](data-model.md)
- [Security and compliance](security.md)
