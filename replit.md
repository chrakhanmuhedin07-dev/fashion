# KURA Men's Clothing Store

A premium men's fashion e-commerce store for the Iraqi market — browse, shop, and checkout with FIB (First Iraqi Bank) or FastPay Iraq payments.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 8080)
- `pnpm --filter @workspace/shop run dev` — run the frontend (port 24349)
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `DATABASE_URL` — Postgres connection string

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- Frontend: React + Vite, Tailwind CSS, shadcn/ui, wouter, TanStack Query
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `lib/api-spec/openapi.yaml` — OpenAPI spec (source of truth for API contracts)
- `lib/db/src/schema/` — Drizzle schema files (products, categories, cart, orders)
- `artifacts/api-server/src/routes/` — Express route handlers
- `artifacts/shop/src/` — React frontend

## Architecture decisions

- Contract-first API: OpenAPI spec drives codegen for React hooks and Zod validators
- Session-based cart: cart tied to a UUID stored in localStorage (no auth required)
- Iraqi payment methods: FIB and FastPay Iraq with phone number 07733129689
- Prices displayed in IQD (Iraqi Dinar)

## Product

- Homepage with hero banner, featured products, and category grid
- Shop page with filter sidebar (category, price range) and sort options
- Product detail page with size/color picker and add-to-cart
- Cart with quantity management and order summary
- Checkout with FIB, FastPay Iraq, or Cash on Delivery payment
- Order confirmation and order history pages

## User preferences

- Payment methods: FIB and FastPay Iraq, phone 07733129689
- Prices in IQD (Iraqi Dinar)
- No emojis in UI
- Premium masculine aesthetic — deep navy / charcoal palette

## Gotchas

- Cart uses sessionId from localStorage — always pass it as a query param to GET /api/cart
- Google Fonts @import must be FIRST in index.css (before tailwindcss imports)
- After OpenAPI spec changes, always re-run codegen before modifying routes or frontend

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
