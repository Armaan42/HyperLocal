# Technology integration

[Docs](../README.md) / Architecture / Technology integration

How every technology in the [tech stack](tech-stack.md) connects. Solid arrows are requests
and data; dotted arrows are background, webhook, deployment or telemetry traffic.

```mermaid
flowchart TD
    subgraph clients ["Apps"]
        web["Customer web app<br/>Next.js PWA"]
        vendorApp["Vendor dashboard<br/>Next.js"]
        adminApp["Admin panel<br/>Next.js"]
        mobile["Customer and rider apps<br/>React Native, Expo"]
    end

    cloudflare["Cloudflare<br/>CDN, WAF, DDoS, bot protection"]

    subgraph aws ["AWS, Mumbai region, ECS Fargate"]
        lb["Load balancer"]
        api["NestJS API<br/>REST + OpenAPI"]
        ws["WebSocket gateway<br/>order status, rider location"]
        workers["BullMQ workers<br/>payouts, invoices, renewals,<br/>notifications, search indexing"]
        secrets["AWS Secrets Manager"]
    end

    subgraph data ["Data"]
        pgbouncer["PgBouncer<br/>connection pool"]
        pg[("PostgreSQL + PostGIS")]
        replica[("Read replica<br/>reports")]
        redis[("Redis<br/>cache, queues, pub/sub")]
        typesense[("Typesense<br/>search")]
        r2[("Cloudflare R2<br/>images, KYC documents")]
    end

    subgraph external ["Third-party services"]
        razorpay["Razorpay + Route<br/>payments, payouts, plan billing"]
        maps["Google Maps Platform<br/>geocoding, routes, ETA"]
        notify["Notifications<br/>FCM push, SMS, Resend email"]
    end

    subgraph ops ["Operations"]
        observe["Observability<br/>OpenTelemetry, Grafana, Sentry"]
        deploy["Delivery<br/>GitHub Actions, Terraform"]
    end

    web & vendorApp & adminApp & mobile --> cloudflare
    cloudflare --> lb
    lb --> api
    lb --> ws

    api --> pgbouncer --> pg
    pg -.->|"replication"| replica
    api --> redis
    ws <-->|"pub/sub"| redis
    api -->|"search"| typesense
    api -->|"signed upload links"| r2
    api --> secrets

    redis -.->|"queued jobs"| workers
    workers --> pgbouncer
    workers -->|"index updates"| typesense

    api -->|"create payments"| razorpay
    razorpay -.->|"webhooks"| api
    api -->|"zone checks, ETA"| maps
    workers -->|"payouts, refunds"| razorpay
    workers --> notify

    api & ws & workers -.-> observe
    deploy -.->|"build, deploy, provision"| api
```

The apps also load two third-party SDKs directly in the browser or phone: the Razorpay
checkout sheet for payment, and Google Maps for address search and the live tracking map.
Product images in R2 are served to the apps through Cloudflare's CDN.

Related: [System overview](overview.md), [Scaling and traffic](scaling.md), [Security](security.md).
