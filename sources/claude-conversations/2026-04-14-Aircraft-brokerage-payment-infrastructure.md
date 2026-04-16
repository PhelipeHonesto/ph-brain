---
title: Aircraft brokerage payment infrastructure
created: 2026-04-14T05:15:37.734039Z
updated: 2026-04-14T05:16:32.134798Z
uuid: f4eb9783-91e6-40b8-b463-24c19294709c
source: claude-conversation
type: source
message_count: 4
---

# Aircraft brokerage payment infrastructure

*Summary: **Conversation Overview**

The person asked two focused questions about payment infrastructure in the aircraft brokerage industry, specifically in the context of what appears to be their company, OSA (referenced as OSA Pay and OSA Aircraft). The conversation was entirely informational and industry-focused, with the person seeking to understand the current state of payment rails in both charter brokerage and aircraft sales (buy/sell transactions).

Claude provided a detailed breakdown of the charter brokerage payment model, describing how wire transfer dominates, how broker commissions are embedded and opaque, and how Tuvoli (owned by Directional Aviation) serves as the primary payment infrastructure on the operator side but is structurally conflicted. Claude positioned OSA Pay's model — including yield-bearing client accounts, real-time operator settlement tied to ADS-B departure data, credit lines, and 2% payment processing — as a differentiated client-side financial layer that no incumbent currently offers.

For the aircraft sales follow-up, Claude detailed the aviation escrow company ecosystem (IATS, Aerospace Escrow, First American, AOPA Finance, etc.), the manual FAA registry closing process centered in Oklahoma City, and the absence of any technology coordination layer. Claude identified a potential product opportunity for OSA Aircraft in building a closing coordination dashboard — covering document tracking, lien search status, wire confirmation, and FAA filing status — as a tool acquisition advisory clients would value. Industry-specific terminology used throughout includes ADS-B, FAA registry, AC Form 8050-2, Bill of Sale, title chain, and escrow officer.*

## Phelipe

What is the payment infrastructure today for aircraft brokerage?

---

## Claude

Phelipe is asking about the current payment infrastructure in aircraft brokerage. This is a knowledge question I can answer from my training data plus what I know about OSA's competitive landscape from his memories. Let me think about this carefully.

This is about the broader industry - how payments work in private aviation charter brokerage and aircraft sales brokerage today. I can answer this well from knowledge without searching.## Payment Infrastructure in Aircraft Brokerage Today

**Charter brokerage (your direct market):**

The dominant model is wire transfer. Client wires funds to broker's operating account, broker holds float, pays operator net of commission after the trip (sometimes days later). No escrow, no real-time settlement, no yield on idle deposits. Commission is opaque — typically 10–15% baked into the quote, not disclosed. Stripe and ACH exist at the margins for smaller operators but wire is still king for anything above ~$10K.

Tuvoli is the closest thing to actual payment infrastructure — $900M+ annually processed, focused on operator-to-operator and broker-to-operator settlements. But Tuvoli is owned by Directional Aviation (which owns operators), so it's structurally conflicted. It serves the supply side, not the client side.

**Aircraft sales brokerage (buy/sell):**

Even more primitive. Escrow attorneys or title companies hold funds during the transaction. No tech layer — just wires into a trust account, title search, FAA registry transfer, release. The whole process takes days to weeks. Major title companies: AOPA, VREF, Insured Aircraft Title Service. Aviation-specific escrow is a cottage industry with zero modernization.

**What doesn't exist anywhere:**

- Yield-bearing client accounts (your OSA Pay APY model)
- Real-time operator settlement tied to ADS-B departure confirmation
- Credit lines underwritten by deposit + transaction history
- 2% payment processing with embedded fintech rails
- Any equivalent of Brex/Column N.A. applied to aviation

**The incumbent payment "stack" in one sentence:** wire in, hold float, wire out — with an attorney if the asset is large enough.

OSA Pay's moat is real. Nobody is building the client-side financial layer. Tuvoli owns the operator side and can't cross over without eating its own base.

---

## Phelipe

What they use for aircraft sales?

---

## Claude

The user is asking specifically about payment infrastructure for aircraft sales (buy/sell transactions), building on my previous answer.**Aircraft Sales Payment Stack (Buy/Sell)**

The entire industry runs on aviation escrow companies. The main players:

- **AOPA Aviation Finance** (for smaller GA)
- **Insured Aircraft Title Service (IATS)**
- **Aviation Title Inc.**
- **First American Title** (aviation division)
- **Aerospace Escrow**

**How it works:**

1. Buyer wires purchase funds into escrow account
2. Title company does FAA registry lien search, title chain review
3. Both parties sign closing docs (Bill of Sale, AC Form 8050-2)
4. Escrow releases funds to seller simultaneously with FAA registry transfer filing
5. FAA processes the transfer — takes 1–3 weeks for official registration

**The tech layer:** there isn't one. It's PDFs, DocuSign at best, and phone calls. The "simultaneous close" is coordinated manually between the escrow officer, buyer's counsel, seller's counsel, and the FAA registry in Oklahoma City.

**Financing side:** AOPA Finance, Global Jet Capital, TVPX, and a handful of aviation-specific lenders hold the paper. They wire directly into escrow at close. Standard stuff — no embedded fintech, no API.

**The gap OSA Aircraft could exploit long-term:** nobody owns the financial coordination layer for the transaction. You could theoretically build a closing coordination tool that sits on top of escrow — document tracking, lien search status, wire confirmation, FAA filing status — all in one dashboard. Acquisition advisory clients would pay for that alone.

---
