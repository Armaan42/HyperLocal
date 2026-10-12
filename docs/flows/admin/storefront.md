# Storefront

[Docs](../../README.md) / [Flows](../README.md) / [Admin](README.md) / Storefront

What customers see on the home page, and the platform-wide switches that change how
ordering works.

## Featured sections flow

```mermaid
flowchart TD
    page([Home layout page]) --> city[Choose city]
    city --> act{Admin taps}
    act -->|Add section| type{Section type}
    type -->|Banner carousel| banners[Upload banners and set links]
    type -->|Store row| stores["Pick stores, or rule: top rated, new, nearest"]
    type -->|Product row| products["Pick products, or rule: best sellers, on offer"]
    type -->|Category grid| cats[Pick categories]
    banners --> settings
    stores --> settings
    products --> settings
    cats --> settings["Title, schedule, zones"]
    settings --> preview[Preview as customer]
    preview --> publish[Publish]
    publish --> live[Section live on home page]
    act -->|Reorder| drag[Drag sections]
    act -->|Hide| hide[Section hidden, kept for later]
```

## Platform settings flow

```mermaid
flowchart TD
    settings([Platform settings]) --> pick{Setting}
    pick -->|Multi-store checkout| multi{Switch}
    multi -->|On| on["Carts may contain items from several stores"]
    multi -->|Off| off["Cart limited to one store; 'Replace cart?' dialog shown"]
    on --> scope[Optional: restrict to chosen categories]
    pick -->|Cash on delivery| cod[Enable and set maximum order value]
    pick -->|Order timers| timers[Vendor accept time, rider offer time]
    pick -->|Fees| fees[Platform fee, small-order fee]
    pick -->|Refund limits| limits[Support agent refund limit]
```

## Actions

| Screen | Element | Admin does | What happens | Leads to |
|---|---|---|---|---|
| Home layout | City selector | Picks | Shows that city's sections in order | Stays |
| Home layout | **Add section** | Picks a type | Section editor opens | Section editor |
| Section editor | Banner upload + link target | Uploads, picks a store, category, product or URL | Tapping the banner opens the target | Stays |
| Section editor | Manual pick or rule | Chooses | A rule (top rated, best sellers) refreshes itself; a manual list stays fixed | Stays |
| Section editor | Schedule | Sets start and end, or days and hours | Section appears only in that window (for example a breakfast row) | Stays |
| Section editor | Zones | Ticks | Limits the section to chosen zones | Stays |
| Section editor | **Preview** | Taps | Shows the home page as a customer in that city would see it | Preview |
| Section editor | **Publish** | Taps | Section goes live; home page cache is cleared | Home layout |
| Home layout | Drag handle | Drags | Order on the home page changes | Stays |
| Home layout | **Hide** toggle | Switches | Section is hidden without being deleted | Stays |
| Platform settings | **Multi-store checkout** switch | Switches | On: mixed carts allowed. Off: adding from a second store prompts to replace the cart | Stays |
| Platform settings | Multi-store categories | Ticks categories | Mixed carts allowed only among stores in those categories | Stays |
| Platform settings | COD maximum | Enters | COD is hidden above this order value | Stays |
| Platform settings | Timers and fees | Enters | Applied to new orders | Stays |

## Rules and edge cases

- **Sponsored placement:** stores using a plan's featured slots are inserted into store rows and labelled "Sponsored".
- **Empty section:** a section with nothing to show for a customer (no matching store in their zone) is skipped.
- **Turning multi-store checkout off** does not break existing mixed carts mid-payment; it applies to carts from the next change.
- **Settings changes** take effect on new orders only and are recorded in the audit log.

## Related

- [Customer: home and search](../customer/home-and-search.md)
- [System: multi-store checkout](../system/multi-store-checkout.md)
