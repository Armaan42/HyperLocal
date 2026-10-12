# Features

[Docs](../README.md) / Product / Features

The feature list, how each is built, and the phase it ships in. Phases are defined in the
[roadmap](roadmap.md).

## Stores and catalog

| Feature | How it is built | Phase |
|---|---|---|
| Connect local stores easily | Self-serve vendor signup, then admin approval | 1 |
| Seller verification system | KYC document upload, admin review, a verified badge on the store | 1 |
| Unlimited categories and products | Category tree of any depth; no platform limit on products, only the vendor's plan limit | 1 |
| Customizable featured sections | Admin builds home-page sections (banners, store rows, product rows) per city, with ordering and schedules | 1 |

## Location and delivery

| Feature | How it is built | Phase |
|---|---|---|
| Location-based store system | PostGIS query returns only stores whose zone contains the customer's address | 1 |
| Manage multiple delivery zones | Each city holds many zones; a store serves one or more | 1 |
| Geo-fencing delivery map | Admin draws zone polygons on a map editor; stored as PostGIS polygons | 1 |
| Instant delivery within zones | Orders are accepted only inside a store's zone; delivery fee and ETA are set per zone | 1 |
| Rider self-order acceptance | Nearby riders see open jobs and the first to accept takes it | 2 |
| Live order tracking | Status updates in phase 1; rider on a live map in phase 2 | 1 and 2 |

## Ordering and payment

| Feature | How it is built | Phase |
|---|---|---|
| Seamless multi-store checkout | One checkout and one payment, split into one order per store. See [flow](../flows/system/multi-store-checkout.md) | 1 |
| Control multi-store checkout access | Admin switch, platform-wide or per category, that allows or blocks carts spanning stores | 1 |
| One-click checkout / Buy now | Skips the cart using the default address and last payment method | 1 |
| Secure payment gateways | Razorpay-hosted checkout with UPI, cards, net banking and wallets, plus cash on delivery | 1 |
| Smart search with suggestions | Typesense autocomplete with typo tolerance, recent and popular searches | 1 |

## Accounts and engagement

| Feature | How it is built | Phase |
|---|---|---|
| Multiple login methods | Phone OTP, email and password, Google sign-in | 1 |
| Manage multiple addresses | Saved addresses with labels and a default; each is checked against delivery zones | 1 |
| Real-time notifications | Push, SMS and in-app alerts on every order status change | 1 |
| Delivery, seller and item feedback | Three separate ratings after delivery: rider, store and each item | 2 |

## Monetization

| Feature | How it is built | Phase |
|---|---|---|
| Earn commission category wise | Rate per category, optional store override, copied onto each order line | 1 |
| Vendor subscription plans | Monthly plans with product limits, commission discounts and featured slots | 1 |

Details: [Monetization](monetization.md).
