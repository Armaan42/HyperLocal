# Money flow

[Docs](../../README.md) / [Flows](../README.md) / [System](README.md) / Money flow

The platform never holds vendor money in its own bank account. Each vendor has a Razorpay
Route linked account; their share of each payment is transferred there on hold and released
two days after delivery. Details: [Monetization](../../product/monetization.md#money-flow).

```mermaid
sequenceDiagram
    autonumber
    actor Customer
    participant Platform as Hyperlocal
    participant Gateway as Razorpay
    participant Linked as Vendor linked account
    participant Ledger
    actor Vendor

    Customer->>Platform: Place order
    Platform->>Gateway: Create payment
    Customer->>Gateway: Pay
    Gateway-->>Platform: Payment captured (webhook)
    Platform->>Gateway: Transfer vendor share, on hold
    Gateway->>Linked: Vendor share held
    Platform->>Ledger: Record vendor share, commission, fees, taxes
    Note over Platform,Vendor: Order is prepared and delivered
    Note over Platform,Linked: 2 days after delivery, no refund pending
    Platform->>Gateway: Release hold
    Gateway-->>Vendor: Settled to vendor's bank
    Platform->>Ledger: Mark vendor share as settled
    opt Refund approved
        Platform->>Gateway: Reverse vendor transfer and refund customer
        Platform->>Ledger: Post reversing entries
    end
```

The vendor's share is the order value minus commission, GST on commission, TCS and TDS.
The platform keeps commission, platform fees and any taxes it must file.
