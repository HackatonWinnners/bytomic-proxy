# Bytomic Proxy — 3-min demo script (verified live)

~2:55 total. Format: **[TIME] SHOW (screen) / SAY (voiceover).**

Live URLs: landing `https://proxy.bytomic.tech/` · dashboard `/dashboard` · deck `/deck`.

---

## [0:00–0:20] Hook — landing
**SHOW:** `proxy.bytomic.tech` — hero wire animation (packet → 402 → USDC coin → tx).
**SAY:**
> "AI agents can't browse at scale. The moment one scrapes from its datacenter IP it hits 429s, geo-blocks, bans. The usual fix — a proxy — wants an account, KYC, a monthly contract. A bot can't sign that. So we built Bytomic Proxy: web egress an agent just *pays for*, per request, in USDC. No account. No key. The wallet is the access."

## [0:20–0:42] What it is — landing "How it works"
**SHOW:** scroll to the 4-step section (Discover → Pay → Relay → Receipt).
**SAY:**
> "It runs on x402 — the HTTP 402 'Payment Required' protocol. The agent reads our price on a free catalog endpoint, calls the proxy, gets a 402, signs a tenth-of-a-cent USDC payment from its Circle Agent Wallet, and retries. Circle Gateway settles it — gaslessly, we never hold a key — and we fetch the target through our IP and hand back the data with a receipt."

## [0:42–1:40] LIVE proof — the core
**SHOW:** terminal.
```bash
# 1. unpaid → 402
curl -i "https://proxy.bytomic.tech/proxy?url=https://api.ipify.org?format=json"
```
**SAY:** "Unpaid request — the server answers 402, with the x402 challenge: the price, the USDC asset, our wallet, on Base and Polygon."

**SHOW:**
```bash
# 2. the PAID call — real USDC over Circle Gateway
CIRCLE_ACCEPT_TERMS=1 circle services pay \
  "https://proxy.bytomic.tech/proxy?url=https://api.ipify.org?format=json" \
  --address 0x822083271add89584e0cba18279a8e861f7faf2e \
  --chain MATIC-AMOY --method GET --max-amount 0.001 --output json
```
**SAY (while it runs):** "Now the agent pays — a Circle agent wallet, a tenth of a cent, budget-capped with max-amount. Circle Gateway settles it…"

**SHOW:** JSON result → `"response": { "ip": "92.5.84.57" }`.
**SAY (emphasize):** "…and look at the response: the IP is 92.5.84.57 — *our server's* IP, not the agent's. The request actually relayed through our proxy. One paid call, the whole product proven."

## [1:40–2:15] The ledger — both sides
**SHOW:** open `proxy.bytomic.tech/dashboard`. New row: payer `0x54b9…1976`, 0.001 USDC, target ipify, status 200, settlement id.
**SAY:**
> "Every paid call lands in a live spend ledger. Each row carries the Circle Gateway settlement receipt — payer, amount, network, the target it fetched, and the egress it left through. The agent gets its data, the operator gets paid, and it's all auditable. A repeatable workflow where the wallet *is* the agent's job: discover, pay, fetch, receipt — under a hard budget cap."

## [2:15–2:42] Stack / why it wins
**SHOW:** landing "Standing on the Circle agent stack" (5 cards) — or jump to `/deck`.
**SAY:**
> "We didn't reinvent payments. Circle Agent Wallet is the agent's identity and budget. x402 is the per-call payment. Circle Gateway settles it gaslessly. The buyer is an autonomous agent. Base carries it. Bytomic Proxy is the new piece — metered egress as a primitive every agent needs."

## [2:42–2:55] Close
**SHOW:** `/deck` final slide ("Give your agent an exit") or landing footer.
**SAY:**
> "Bytomic Proxy. Give your agent an exit. Live right now at proxy.bytomic.tech. Thanks."

---

## Recording notes
- The dashboard already has a **real settled row** — safe to show immediately.
- The pay command is **verified working**. Buyer `0x822083271add89584e0cba18279a8e861f7faf2e`
  holds ~1.997 USDC in Gateway (Polygon Amoy) — enough for several on-camera calls.
- **Don't promise a clickable on-chain 0x explorer link.** The batched Gateway scheme
  settles via a Circle settlement id (UUID), shown on the dashboard. Say "Gateway
  settlement receipt," not "Etherscan link." (A clickable basescan tx needs the
  direct/vanilla scheme + Base Sepolia ETH for gas — not wired.)
- Pre-open tabs: terminal · `/` · `/dashboard` · `/deck`.
- If a call 503s on camera (container hiccup right after a redeploy), just re-run —
  the second call succeeds; the already-settled row is still your proof.

## Key facts (for Q&A)
- Seller wallet (receives USDC): `0x2d84CFadFE7f73B1C026661b919E5450A32eae78`.
- Price: $0.001 / request. Networks in the 402: Base Sepolia (eip155:84532),
  Arc testnet (5042002), Polygon Amoy (80002).
- Stack: Circle Agent Wallet · x402 (`@circle-fin/x402-batching`) · Circle Gateway
  (gasless batched settlement) · Express seller on Coolify · egress IP 92.5.84.57.
- Repo: github.com/HackatonWinnners/bytomic-proxy.
