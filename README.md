# Ayomide Adejola

Software engineer. TypeScript, NestJS, Flutter, Next.js. Been doing this since 2020 — mobile, web, and backend, mostly fintech, crypto, and whatever interesting problems show up in between.

I care about clean architecture, good test coverage, and systems that don't break at 3am. My work tends to live in the layer between the database and the API surface — queues, webhooks, real-time pipelines, payment flows — and lately in the apps people actually hold.

---

**TypeScript · NestJS · Node.js · Flutter · Dart · Next.js · React · PostgreSQL · Redis · BullMQ · RabbitMQ · WebSockets · gRPC · Prisma · Tailwind · Moralis · Turnkey**

---

## Things I've built

**[Raqet](https://getraqet.com)** — the operating platform for padel clubs, and the player app that fills their courts. Live on the App Store and Google Play. I built it end to end solo: a NestJS/PostgreSQL API, three web surfaces (public site, club staff console, super admin), and a Flutter player app generated from the API spec in a Turborepo. The payment layer is where the care went — a Redis lock across the payment window plus a database-level unique constraint so a court can never be double-booked, row-level locks so a wallet can't be double-spent under concurrency, idempotent webhook handlers, and split bookings that only commit once every player in the group has actually paid. Tournaments, coaching, facility orders, and IPR rating run on the same core.

**Vendoorly** *(live — [vendoorly.store](https://vendoorly.store))* — a restaurant operating system with an ordering marketplace attached. An Ibadan restaurant runs its whole day on it: tables and seats, waiter rounds, fire-to-kitchen, bill split, tender and change, shifts and cash-drawer reconciliation, recipe-level stock depletion, and a financial analytics cockpit that reconciles against the bank. The interesting constraints were physical, not technical — the trading day rolls at 5am because that's when a restaurant actually closes, and every report is cut on the same rule. NestJS + Next.js 15 on top of CloudCommerce (catalog, checkout, order lifecycle) and InboxPay (transfer confirmation), with WebSocket push on the operational hot paths, seven operator roles, and an immutable restatement pipeline so a correction changes the report without rewriting history.

**Cakeys With Love** *(live — [cakeyswithlove.com](https://www.cakeyswithlove.com))* — a branded ordering platform for an Ibadan artisan bakery. Storefront, cart and checkout, customer accounts, delivery zones, an owner console for the order queue and catalog, and branded email receipts. Next.js 15, NestJS 11, Prisma, Firebase Auth, Resend, running on CloudCommerce and InboxPay.

**[@ayorcodes/claudespace](https://www.npmjs.com/package/@ayorcodes/claudespace)** — a multi-agent software delivery pipeline that runs in one terminal window. Separate Claude Code processes, one per role — chief, researcher, analyst, planner, principal, implementer, reviewer, plus a conductor that turns one goal into a backlog and drives it unattended — each pinned to its own model and effort tier, and none able to read another's session. The handoff is files and hooks, not a chatroom: a role ends its turn by writing a marker (`<role>.done`, or `<role>.blocked` to bounce a question or a rejection back) whose contents are the path to the artifact it just produced, and a Claude Code Stop hook reads that marker, resolves the next role from the pipeline map, and delivers a prompt into its pane pointing at the artifact. A role that ends a turn with no marker gets its stop blocked and a reminder fed back into the same session, rather than the pipeline going quiet. Pipeline state lives outside your project, in `~/.claudespace/projects/<slug>/`. macOS on Apple Silicon. The GUI is next.

**[Faxo](https://github.com/ayorcodes/faxo)** — crypto payment gateway, Stripe-style. Every payment intent gets its own MPC wallet address via Turnkey. Moralis Streams watches the chain and drives the `pending → confirming → confirmed → finalized` lifecycle. EIP-3009 gasless sweeps move USDC from deposit wallets to treasury without the deposit address ever needing ETH. Webhook delivery with exponential backoff, HMAC signing, and full delivery logs. Runs across Ethereum, Base, and BNB Chain.

**Social Watch / Overwatch** *(Opsin — closed source)* — real-time social signal system built into Opsin's crypto trading platform. Users connect their Discord and Telegram accounts, select channels to watch, and the platform ingests every message looking for token calls — `$TICKER` mentions, `.c` contract references, raw address pastes. Each call gets matched to a caller, timestamped, and streamed to the frontend over WebSocket so traders see who called what and when, live.

**[SenDT](https://github.com/ayorcodes/sendt)** — deposit crypto, receive naira in your bank. Non-custodial MPC wallet per user (Turnkey), Moralis detects the on-chain transfer, NGN gets credited atomically at the live CoinGecko rate, and Paystack handles the bank transfer. The whole thing is event-driven — no polling anywhere in the stack. SSE keeps the frontend live.

**SpottR** *(closed source)* — hyperlocal crypto-enabled marketplace. Users list products with location data, buyers discover them by proximity, and transactions flow through a full order lifecycle — request, negotiation, confirmation, logistics, escrow release. The wallet supports both NGN (Paystack) and crypto (Cliq Token, BNB, ETH via Threshold Network), with atomic debit/credit on every transfer. Real-time chat runs over WebSockets with Redis pub/sub fan-out and FCM push for offline users. Location-aware search uses a bounding-box DB filter ranked by Google Maps distance, with Redis-cached results keyed to the user's last-known location. Corporate storefronts, QR-based check-in verification for in-person handoffs, and a Cliq Token referral reward system round it out. Flutter mobile app, NestJS backend.

**[Volta](https://github.com/ayorcodes/volta)** — smart power operations SaaS for facilities that run on backup generators. Multi-tenant, role-based (owner / facility manager / security). FIFO tank ledger tracks fuel across multiple purchase lots so session cost estimates are accurate even when fuel came from different batches at different prices. Generator scheduling materializes into concrete sessions with pre-run reminders via in-app, email, or WhatsApp (Twilio). Power switch events are logged with fuel snapshots; configurable thresholds control auto-switch-back. Event-driven notification pipeline, Socket.io real-time dashboard, audit trail on everything, Stripe + Paystack billing, and VoltaBot — a Claude-powered AI assistant for querying operations data conversationally.

**[SyBoard](https://github.com/ayorcodes/syboard)** — collaborative kanban with real multiplayer. Yjs CRDT handles conflict-free card editing so two people editing the same card simultaneously don't stomp on each other. Redis pub/sub fans out WebSocket events across instances, meaning horizontal scaling doesn't break presence or live updates.

**[EstateOS](https://github.com/ayorcodes/estateos)** — the backend OS for residential estates. Multi-tenant SaaS with unit/resident hierarchy, electricity metering, generator scheduling, dues, and Paystack billing. Built with NestJS and Next.js.

**[Billflow](https://github.com/ayorcodes/billflow)** — billing infrastructure as a service. Handles subscriptions, usage metering, automated dunning, and routes payments to Stripe or Paystack based on the customer's country.

---

## Experience

**CopyMe Crypto** `2026 – Present`
Crypto copy-trading platform. I work across all four surfaces — NestJS backend, Flutter mobile app, React admin dashboard, and the public site. Built and maintain the copy engine that mirrors lead traders' positions onto their followers' exchange accounts, including the fixes that keep every trade attributed and credited to the right trader. Added exchange-account connection checks that block copying when an account isn't set up correctly, plus cost and risk rules that bound what a follower can lose. Shipped account deletion end to end across all four, with the audit trail a launch reviewer expects. Redesigned the mobile app against a token-driven design system so every colour, spacing, and motion value comes from the theme, and set up CI checks and alerting so failures surface before customers find them.

**Raqet** `2026 – Present`
Padel club platform and player app, live on the App Store and Google Play. Solo build end to end — backend API, three web apps, a Flutter player app, and the infrastructure to run it. Designed the payment layer for correctness under concurrency: row-level locks against wallet double-spend, idempotent webhook handlers, and bookings that only commit once every player in a split has paid.

**Opsin** `2025 – 2026`
Crypto trading platform. Built the real-time social signal layer — Discord and Telegram ingestion, token-call parsing (`$TICKER`, `.c` commands), caller performance panels, and the overwatch feed that traders actually rely on. Also reworked discovery and watchlist data flows using ClickHouse, fixed some gnarly RabbitMQ connection handling that was causing silent ingestion drops, and added wallet import/export for multi-wallet traders.

**Moralis** `2021 – 2025`
Joined when the whole backend was Express and left it NestJS + gRPC microservices. Over ~3.5 years I shipped 30+ production features — dynamic pricing engines, NFT floor pricing, token metadata pipelines, blockchain node integrations, a tiered BullMQ queue for NFT jobs that meaningfully improved premium user latency. Also built internal tooling, Slack-based error alerting, and wrote most of the API documentation that new engineers used to get up to speed.

**SpottR** `2021 – 2022`
Crypto marketplace. Built the wallet system from scratch — fiat and crypto (Cliq Token, BNB, ETH), Threshold Network integration, Paystack, Redis caching, and the location-aware listing logic. Also did chat, notifications, and the queue-based transaction layer.

**Joovlin** `2020 – 2021`
Fintech. First real production backend I owned end-to-end. Designed the payment and wallet microservices, migrated a monolith to services, and built the transaction audit trail that compliance actually needed.

---

**[@ayorcodes/claudespace](https://www.npmjs.com/package/@ayorcodes/claudespace)** — multi-agent Claude Code pipeline, installable globally

**[@ayorcodes/remita-js](https://www.npmjs.com/package/@ayorcodes/remita-js)** — Node.js SDK for the Remita payment API

[linkedin.com/in/ayomide-adejola](https://linkedin.com/in/ayomide-adejola) · adeayo35@gmail.com
