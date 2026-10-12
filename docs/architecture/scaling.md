# Scaling and traffic

[Docs](../README.md) / Architecture / Scaling and traffic

Delivery traffic spikes at lunch and dinner and concentrates by city, so the plan keeps
most requests away from the database. The measures run cheapest first.

## Measures

1. **Cache at the edge.** Images, scripts and store and category pages are served by the
   CDN; most browsing never reaches the API.
2. **Stateless API replicas.** Any replica can serve any request, so the load balancer adds
   replicas as CPU or request rate rises.
3. **Redis for hot reads.** Store lists per area, category trees and product pages are
   cached with short lifetimes and cleared when the data changes.
4. **Search runs on Typesense.** Discovery queries with geo filters never touch PostgreSQL.
5. **Database hygiene.** Geo and foreign-key indexes, PgBouncer connection pooling, read
   replicas for dashboards and reports, partitioned ledger and event tables.
6. **Queues for slow work.** Checkout returns as soon as the order and payment are recorded;
   notifications, invoices, indexing and payouts run in workers.
7. **Protection.** Rate limits per user and IP, bot filtering, timeouts and circuit breakers
   on third parties, idempotency keys on order and payment calls.
8. **Graceful degradation.** If maps fail, the ETA is hidden and ordering still works.
9. **Realtime at scale.** WebSocket gateways scale sideways through Redis pub/sub; rider
   location pings are throttled and batched.
10. **Scale by city.** Every city-scoped table carries a `city_id` from day one, so a region
    can move to its own database when it outgrows a shared one.

## Targets

To hold before launch, proven with k6 load tests on the browse, cart and checkout path:

| Target | Value |
|---|---|
| Read requests | 95% under 300 ms |
| Checkout availability | 99.9% |

Related: [System overview](overview.md), [Tech stack](tech-stack.md).
