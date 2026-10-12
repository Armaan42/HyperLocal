# Customer flows

[Docs](../../README.md) / [Flows](../README.md) / Customer

The customer uses the customer web app. This page shows the whole journey; each step links
to a detailed file that lists every action and what happens.

## Journey

```mermaid
flowchart TD
    start([Open app]) --> loggedIn{Logged in?}
    loggedIn -->|No| login["Log in: phone OTP, email or Google"]
    loggedIn -->|Yes| location
    login --> location["Set delivery address"]
    location --> inZone{Address inside a delivery zone?}
    inZone -->|No| noService[Show 'not serviceable yet']
    inZone -->|Yes| home["Home: featured sections, categories, nearby stores"]
    home --> find["Search or browse a store"]
    find --> product[View product]
    product --> choice{Add to cart or Buy now?}
    choice -->|Buy now| oneClick[One-click checkout]
    choice -->|Add to cart| cart[Cart]
    cart --> checkout[Checkout]
    oneClick --> pay
    checkout --> pay{Payment}
    pay -->|Fails| checkout
    pay -->|Paid or cash on delivery| placed[Order placed]
    placed --> track[Track order]
    track --> delivered[Delivered]
    delivered --> review[Rate rider, store and items]
    delivered --> problem{Problem?}
    problem -->|Yes| refundReq[Request refund]
```

## Detailed flows

| # | Flow | Screens covered |
|---|---|---|
| 1 | [Login and signup](login.md) | Login, OTP, profile setup |
| 2 | [Address and location](address-and-location.md) | Location prompt, address picker, add address |
| 3 | [Home and search](home-and-search.md) | Home, category, search, store page |
| 4 | [Product and cart](product-and-cart.md) | Product page, cart |
| 5 | [Checkout and payment](checkout-and-payment.md) | Checkout, payment, order confirmation, Buy now |
| 6 | [Order tracking](order-tracking.md) | Order list, order detail, live tracking, cancel |
| 7 | [Reviews and refunds](reviews-and-refunds.md) | Rating screen, refund request |
| 8 | [Account](account.md) | Profile, addresses, notifications, logout |
