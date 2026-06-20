# Claude-design prompt — Pitch deck (3-min live pitch)

Paste everything below the line into Claude as an artifact request.

---

Build a presentation deck as one self-contained HTML file: full-screen slides,
arrow-key / swipe navigation, slide counter, progress bar. Same dark premium
visual system as our landing (bg `#0b0f14`, surfaces `#111823`, borders
`#1c2530`, text `#d7e0ea`, mint `#6ee7b7`, blue `#60a5fa`, mono for data). Each
slide animates its elements in on entry (staggered fade+rise, count-ups, the wire
animation where noted). Built for a 3-minute live pitch — big type, one idea per
slide, minimal text, high contrast. 9 slides.

Product: **Relay402 — bandwidth agents can buy.** Pay-per-request proxy/VPN
egress for AI agents; USDC per request over x402, settled on-chain via Circle
Gateway, paid from the agent's Circle Agent Wallet, under a budget, with a
receipted spend ledger.

## Slides

1. **Title.** Huge `Relay402`. Tagline "Bandwidth agents can buy." Sub: "Pay-per-
   request proxy egress for AI agents." Footer: team name · Circle Agentic
   Commerce track. Background: slow aurora mesh; a single packet drifts across.

2. **The problem.** "Agents can't browse at scale." Three punchy stats/icons
   animating in: `429 Rate-limited`, `🌍 Geo-blocked`, `🔑 No keys, no plans fit
   autonomous agents`. One line: "The web wasn't built for agents that pay their
   own way."

3. **The insight.** Big line: "What if an agent could just **pay per request** for
   an IP that isn't its own?" Sub: "No API key. No subscription. The wallet is the
   access." Mint highlight on "pay per request".

4. **What it is.** The animated **wire**: `🤖 Agent → ⚡ Relay402 → 🌐 Web`, packet
   travels, `402` flashes, USDC coin flies, wire turns mint, `0x…` tx materializes,
   ledger row drops, `$0.001` floats up. This is the centerpiece — let it run while
   you talk. Caption: "Agent pays $0.001 USDC, routes its fetch through Relay,
   gets data + an on-chain receipt."

5. **How it works** (4 steps, reveal one-by-one): **Discover** free `/catalog` →
   **Pay** unpaid `402`, agent signs USDC from its Circle wallet → **Relay** Circle
   Gateway settles, fetch egresses through Relay's IP → **Receipt** logged to spend
   ledger, agent stops at budget cap. A faux terminal strip:
   `GET /proxy?url=…  →  402  →  pay $0.001  →  200 + x-payment-tx: 0x7a3f…e91c`.

6. **Proof / live demo.** The dashboard mock: `Earned $0.019`, `19 paid calls`,
   receipts table with tx links, rows sliding in, counter ticking. Callout bubble:
   "httpbin.org/ip returns `89.246.128.71` — Relay's egress, not the agent's. It
   actually relays." Label: "← switch to live demo here."

7. **Built on Circle.** Map our pieces to the Agent Stack (each row animates in):
   Circle **Agent Wallet** = agent payment identity + budget · **x402** = per-call
   payments · Circle **Gateway** = gasless USDC settlement (we never hold a key) ·
   Circle **Claude Agent SDK kit** = the autonomous buyer. Line: "Exactly the
   brief: a repeatable workflow where the wallet is part of the agent's job —
   buying data, returning receipts."

8. **Why it wins.** Four chips: *Real workflow* (N budgeted fetches, not one
   transfer) · *Both sides shipped* (paid seller + autonomous buyer + live ledger)
   · *On-chain receipts* (clickable tx per call) · *New market* (metered egress is
   a primitive every agent needs). Small: "+ Tavily picks targets, Nebius runs
   inference."

9. **Close.** "Give your agent an exit." `Relay402`. URLs: live demo · GitHub.
   Big mint CTA. Final packet completes the wire and the counter settles.

## Rules

- One concept per slide, ≤ ~20 words of body text each. Speaker carries detail.
- Entrance animations on every slide; the wire (slide 4) and dashboard (slide 6)
  loop. Animate transform/opacity only; respect `prefers-reduced-motion`.
- Keyboard: ←/→ and Space to advance; show `4 / 9` + thin top progress bar.
- Make slide 4 and 6 genuinely impressive — those win the room.

Ship one polished HTML file.
