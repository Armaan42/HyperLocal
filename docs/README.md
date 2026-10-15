# Hyperlocal Documentation

This page is the index for all project documentation. Every document is linked from here.

## Product

What we are building and for whom.

| Document | Summary |
|---|---|
| [Overview](product/overview.md) | What the platform is and how it earns |
| [Roles](product/roles.md) | The five roles and the four apps they use |
| [Features](product/features.md) | Feature list with status and phase |
| [Monetization](product/monetization.md) | Commission rules, subscription plans, money flow |
| [Roadmap](product/roadmap.md) | Three build phases and the gates between them |

## Architecture

How it is built.

| Document | Summary |
|---|---|
| [System overview](architecture/overview.md) | Components and how they connect |
| [Tech stack](architecture/tech-stack.md) | The choice for each layer and why |
| [Technology integration](architecture/integrations.md) | Diagram of how every technology connects |
| [Scaling and traffic](architecture/scaling.md) | How the system handles load |
| [Data model](architecture/data-model.md) | Table groups and the rules that protect money |
| [Security and compliance](architecture/security.md) | Controls that ship with the first release |

## Flows

What happens on every screen: each action, what the system does, and where it leads.
Organised by role. Full index: [flows/README.md](flows/README.md).

| Folder | Covers | Detailed flows |
|---|---|---|
| [Customer](flows/customer/README.md) | Login, address, browsing, cart, checkout, tracking, reviews, account | 8 |
| [Vendor](flows/vendor/README.md) | Onboarding, store setup, products, orders, earnings, subscription | 6 |
| [Rider](flows/rider/README.md) | Onboarding, jobs and delivery, earnings | 3 |
| [Admin](flows/admin/README.md) | Zones, commissions, plans, storefront, approvals, orders, payouts, reports | 8 |
| [Support](flows/support/README.md) | Refunds and disputes | 1 |
| [System](flows/system/README.md) | Order lifecycle, multi-store checkout, money flow, subscription lifecycle | 5 |

## Decisions

| Document | Summary |
|---|---|
| [Decision log](decisions/README.md) | Choices made so far and what changes if they are reversed |

## Folder structure

```text
docs/
├── README.md          # this index
├── product/           # what and why
├── architecture/      # how it is built
├── flows/             # screen-by-screen flows
│   ├── customer/      # one folder per role, each with its own README
│   ├── vendor/
│   ├── rider/
│   ├── admin/
│   ├── support/
│   ├── system/        # cross-role processes
│   └── svg/           # SVG exports for Figma, same folders
└── decisions/         # decision log
```

## Adding or changing a document

1. Put the file in the folder that matches its subject. Create a new folder only when a
   subject has three or more documents of its own (for example `api/` or `runbooks/`).
2. Name files in lowercase with hyphens: `delivery-zones.md`.
3. One subject per file. If a file needs more than about five top-level sections, split it.
4. Start the file with an `# H1` title, then a breadcrumb line linking back to this index.
5. Add a row for it in the matching table on this page. A document that is not linked from
   here does not exist for readers.
6. For a new flow, also follow [flows/README.md](flows/README.md#adding-a-flow).
