# Claude-design prompt — Landing page

Paste everything below the line into Claude as an artifact request.

---

Build a single-page marketing landing site as one self-contained HTML file (inline
CSS + JS, no external build). Dark, premium, developer-grade — think Linear ×
Stripe × Vercel. Smooth, tasteful, GPU-friendly animations everywhere, but never
janky. Mobile responsive.

## Product

**Relay402** — *Bandwidth agents can buy.*
A pay-per-request proxy/VPN egress for AI agents. An agent pays USDC **per HTTP
request** over the **x402** protocol, routes its fetch through Relay's network,
and gets the data back plus an on-chain receipt — all from its **Circle Agent
Wallet**, under a hard budget. "Stripe for agent egress."

The problem: AI agents get rate-limited, geo-blocked, and IP-banned the second
they scrape at scale. The fix: metered, pay-as-you-go egress with no API keys, no
subscriptions — the agent just pays cents per call and the wallet IS the access.

## Brand / visual system

- Background `#0b0f14`; surfaces `#111823`; hairline borders `#1c2530`.
- Text `#d7e0ea`; muted `#6b7888`.
- Accent mint `#6ee7b7` (primary), electric blue `#60a5fa` (secondary).
- Monospace for data/code (`ui-monospace, Menlo`); clean sans (Inter) for prose.
- Subtle animated gradient-mesh / aurora glow behind the hero (mint→blue, very
  low opacity, slow drift). Faint dotted-grid texture on section backgrounds.

## Signature animation — the hero "wire"

A horizontal pipeline diagram, center of hero, that animates on a loop:

`[ 🤖 Agent ]  ───────  [ ⚡ Relay402 ]  ───────  [ 🌐 Web ]`

1. A glowing **packet dot** travels Agent → Relay along the wire.
2. At Relay a red **`402`** stamp flashes ("Payment Required").
3. A **USDC coin** spins from Agent → Relay; the wire turns mint (paid).
4. Packet continues Relay → Web; a response packet returns Web → Agent → and a
   **tx hash** `0x7a3f…e91c` materializes/typewriters under Relay, then a row
   drops into a small "ledger" card.
5. Loop. Each loop a "$0.001" floats up and a counter (`Earned $0.014…`) ticks.

Do it with CSS keyframes / SVG `offset-path` / requestAnimationFrame. Keep it
buttery (transform/opacity only).

## Sections (in order)

1. **Nav** (sticky, blur backdrop): `Relay402` wordmark (mint dot), links: How it
   works · Live ledger · Docs · `Launch demo` (mint button, magnetic hover).

2. **Hero**: headline **"Bandwidth agents can buy."** Sub: "Pay-per-request proxy
   egress for AI agents. USDC per call over x402, settled on-chain through Circle
   Gateway. No keys. No plans. The wallet is the access." Two CTAs: `Watch 60s
   demo` (primary), `View on GitHub` (ghost). Below: the animated wire diagram.
   Trust strip: "Built on Circle Agent Wallet · x402 · USDC · Base".

3. **The problem** (3 cards, fade+rise on scroll): *Rate-limited* — "429 the moment
   you scale." *Geo-blocked* — "Half the web is region-walled." *Key sprawl* —
   "Per-site auth, plans, and invoices don't fit autonomous agents." Each card a
   small looping micro-animation (a counter hitting 429, a globe with a lock, a
   tangle of keys).

4. **How it works** (4 numbered steps, connected by an animated vertical line that
   "fills" as you scroll):
   1. **Discover** — agent GETs free `/catalog`, reads the $0.001 price + egress IP.
   2. **Pay** — unpaid request returns `402`; agent signs a USDC payment from its
      Circle wallet and retries.
   3. **Relay** — Circle Gateway settles on-chain; Relay forwards the fetch through
      its egress IP and streams the response back.
   4. **Receipt** — every call lands in a spend ledger with the tx hash; the agent
      stops at its budget cap.
   Show a tiny faux terminal/code block per step with the real shape, e.g.
   `GET /proxy?url=…  →  402  →  pay $0.001  →  200 + x-payment-tx: 0x…`.

5. **Live ledger** (the money shot): a mock of the real dashboard — a dark card
   titled "Relay402 · spend ledger" with: big mint stat `Earned $0.0190`, `19 paid
   calls`, `3 agents`; a table of receipts (Time · Payer `0x9f…a4` · USDC `0.001`
   · Target `api.github.com/zen` · Status `200` green pill · Tx `0x7a3f…e91c` blue
   link). Rows **slide in** one by one on a loop, the counter ticking. Caption:
   "Both sides of every trade — the agent gets data, the operator gets paid,
   on-chain."

6. **Why it wins / stack** (logo-ish row + short lines): *Circle Agent Wallet* —
   the agent's payment identity & budget. *x402* — HTTP-native 402 payments.
   *Circle Gateway* — gasless USDC settlement, we never touch a key. *Claude Agent
   SDK* — the autonomous buyer. *Base* — on-chain receipts.

7. **Use cases** (4 chips that expand on hover): research agents reaching paywalled
   /geo data · price/market scrapers dodging rate limits · QA agents geo-testing
   from many exits · any agent that needs an IP that isn't its own.

8. **CTA footer**: "Give your agent an exit." Buttons: `Launch demo`, `GitHub`.
   Small print: built at [hackathon] for the Circle Agentic Commerce track.

## Animation rules

- Scroll-reveal (fade + 16px rise, staggered) via IntersectionObserver.
- Number count-ups when stats enter view.
- Magnetic / glow hover on buttons; cards lift + border brightens on hover.
- Respect `prefers-reduced-motion` (disable loops, keep static).
- 60fps: animate only `transform` and `opacity`. No layout thrash.

Ship one polished HTML file. Make it feel alive.
