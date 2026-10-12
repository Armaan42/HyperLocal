# Tech stack

[Docs](../README.md) / Architecture / Tech stack

The rule is one language end to end and one deployable backend, split into services only
when a measured bottleneck demands it.

## Frontend

| Layer | Choice | Why |
|---|---|---|
| Customer, vendor and admin web | Next.js (App Router), TypeScript, Tailwind CSS, shadcn/ui | Server rendering makes store and product pages fast and indexable; one UI kit across three apps |
| Mobile | React Native with Expo | Shares types and validation with the web apps |

## Backend

| Layer | Choice | Why |
|---|---|---|
| API | NestJS modular monolith, REST with OpenAPI | Enforced module boundaries, so a module can become a service later without a rewrite |
| Auth | Phone OTP, email and Google sign-in; short-lived JWT with rotating refresh tokens; role-based access | |
| Background jobs | BullMQ on Redis | Payouts, invoices, notifications, plan renewals, retries |
| Realtime | WebSockets through Redis pub/sub | Order status and rider location |

## Data

| Layer | Choice | Why |
|---|---|---|
| Database | PostgreSQL with PostGIS | Transactions for orders and money; radius and delivery-zone queries |
| Data access | Drizzle ORM | Typed queries that stay close to SQL, which PostGIS needs |
| Cache, rate limits, locks | Redis | Hot reads, idempotency keys, session and geo caches |
| Search | Typesense | Typo-tolerant product and store search with geo filters, off the main database |
| Files | S3-compatible storage (Cloudflare R2) behind a CDN | Product images public; KYC documents private with signed links |

## Third-party services

| Need | Choice | Why |
|---|---|---|
| Payments | Razorpay with Route | Split settlement to vendors, UPI and cards, recurring plan billing |
| Maps | Google Maps Platform | Address autocomplete, geocoding, routes and ETAs |
| Push | Firebase Cloud Messaging | |
| SMS | An SMS provider for OTP (to be chosen) | |
| Email | Resend | |

## Infrastructure

| Layer | Choice | Why |
|---|---|---|
| Edge | Cloudflare | CDN, firewall, DDoS and bot protection |
| Hosting | Docker containers on AWS ECS Fargate, managed Postgres and Redis, Terraform | Autoscaling without running Kubernetes |
| Observability | OpenTelemetry, Sentry, Grafana | Traces, errors and dashboards from day one |
| Repo and CI | Turborepo with Bun, GitHub Actions | Shared packages for UI, types and config |

Choices that are still reversible are tracked in the [decision log](../decisions/README.md).
