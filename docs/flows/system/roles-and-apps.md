# Roles and apps

[Docs](../../README.md) / [Flows](../README.md) / [System](README.md) / Roles and apps

Five roles use four apps; the support agent works inside the admin panel with restricted permissions.

```mermaid
flowchart LR
    customer([Customer])
    vendor([Vendor])
    rider([Rider])
    admin([Admin])
    support([Support agent])

    web["Customer web app<br/>browse, order, pay, track"]
    vdash["Vendor dashboard<br/>catalog, orders, earnings, plan"]
    rapp["Rider app<br/>jobs, pickup, delivery"]
    apanel["Admin panel<br/>vendors, zones, commissions, plans, payouts"]

    api[["Hyperlocal API"]]

    customer --> web
    vendor --> vdash
    rider --> rapp
    admin --> apanel
    support -->|restricted role| apanel

    web --> api
    vdash --> api
    rapp --> api
    apanel --> api
```

