---
title: LoudHawk_Beehiiv_Launch_Playbook.md
project: Loud Hawk + OSA Connect Marketing
doc_uuid: 990c84bb-4cd9-4f23-b467-be4a1e077399
source: claude-project-doc
type: source
---

# LOUD HAWK — Beehiiv Launch Playbook

**Edition 1 Launch + First 30 Days Subscriber Acquisition**

---

## PART 1: BEEHIIV ACCOUNT SETUP

### Account & Publication Settings

1. **Sign up at beehiiv.com** — Start on the free Launch plan. You don't need Scale or Max yet. The free tier handles custom domains, basic analytics, and email sends. Upgrade only when the list earns it (your Execution Memo says the same thing).

2. **Publication name:** `Loud Hawk`

3. **Publication handle:** `loudhawk` (this sets your default beehiiv URL to loudhawk.beehiiv.com)

4. **Tagline / description:** *Private aviation intelligence for people who pay attention.*

5. **Custom domain:** Connect your Loud Hawk domain so emails come from something like `newsletter@loudhawk.com` or `signal@loudhawk.com` rather than a beehiiv subdomain. This matters for deliverability and credibility with your audience. Go to Settings → Domain to configure DNS records.

6. **Sender name:** `Loud Hawk` (not your personal name, not OSA — the editorial brand stands on its own)

7. **Reply-to address:** Use a monitored inbox. Replies from readers are gold — especially early. Something like `editor@loudhawk.com` or route replies to your main email.

8. **Publication category:** Business / Finance (closest fit for aviation advisory intelligence)

---

## PART 2: TEMPLATE DESIGN — BRAND IDENTITY

### Your Brand Color System

These are extracted directly from your logo assets:

| Element | Hex Code | Usage |
|---------|----------|-------|
| Loud Hawk Purple | `#521F84` | Hawk icon, accent, section dividers |
| Loud Hawk Orange | `#FF4900` | Wordmark, CTA links, highlights |
| Black | `#1A1A1A` | Body text (not pure black — easier on eyes) |
| White | `#FFFFFF` | Email background |
| Light Gray | `#F5F5F5` | Optional background tint for quick hits section |

### Beehiiv Style Panel Settings

Go to the Post Builder → Style tab → Basic:

**Colors:**
- Background: `#FFFFFF` (clean white — most emails have white backgrounds for a reason; readability wins)
- Text on Primary: `#1A1A1A`
- Secondary (borders, dividers): `#521F84` (purple — distinctive, not typical newsletter gray)
- Links: `#FF4900` (orange — your wordmark color, high visibility)

**Typography:**
- Heading font family: Use a clean sans-serif. **Inter**, **DM Sans**, or **Helvetica** if available. Nothing decorative.
- Heading font weight: Bold
- Paragraph font family: Same as headings for consistency. System sans-serif is fine.
- Paragraph font weight: Regular
- Keep body text at 16px minimum for readability.

**Spacing:**
- Generous padding. Don't crowd the content. Loud Hawk reads like intelligence, not a coupon mailer.
- Margin: medium to wide — give the content room to breathe.

### Newsletter Template Structure

Build this as a saved template in Beehiiv (Posts → Templates → Create New):

```
┌─────────────────────────────────────┐
│  [LOUD HAWK wordmark — orange]      │
│  Small text: "Private aviation      │
│  intelligence" in gray              │
│                                     │
│  ─── purple divider ───             │
│                                     │
│  THE SIGNAL                         │
│  [50-75 word opening. Sharp,        │
│   specific. No preamble.]           │
│                                     │
│  ─── thin divider ───               │
│                                     │
│  [MAIN PIECE HEADLINE]              │
│  [400-500 words. One topic,         │
│   real depth. Specifics.]           │
│                                     │
│  ─── thin divider ───               │
│                                     │
│  QUICK HITS                         │
│  ▸ [Item 1 — 50-80 words]          │
│  ▸ [Item 2 — 50-80 words]          │
│  ▸ [Item 3 — 50-80 words]          │
│                                     │
│  ─── purple divider ───             │
│                                     │
│  [THE CLOSE — 30-50 words.          │
│   Quiet CTA. Rotated each issue.]   │
│                                     │
│  ─── thin divider ───               │
│                                     │
│  Loud Hawk is published by          │
│  Orange Sunshine Aviation.           │
│  orangesunshineaviation.com         │
│                                     │
└─────────────────────────────────────┘
```

### Template Implementation in Beehiiv

1. **Header:** Upload the orange LOUD HAWK wordmark (`LH_NOME_0000_Layer2_1.png`) as a header image. Size it to roughly 200px wide — prominent but not overwhelming. Center-aligned.

2. **Below the logo:** Add a small line of text: *Private aviation intelligence for people who pay attention.* Set it in gray (`#999999`), small font, centered.

3. **Section headers** (THE SIGNAL, QUICK HITS): Use H3 or bold text in purple (`#521F84`). All caps. Keep them as text, not images — simpler to maintain.

4. **Dividers:** Use Beehiiv's built-in horizontal rule. Set the secondary color to purple so dividers carry brand color.

5. **Quick Hits items:** Use bold lead-in text (the topic) followed by the observation. No bullet points needed — use paragraph breaks or bold text to separate items.

6. **The Close:** Set in slightly lighter text or italics. This is the soft CTA zone. One sentence connecting back to OSA, rotated each issue.

7. **Footer:** Standard Beehiiv footer with unsubscribe link. Add one line above it: "Loud Hawk is published by Orange Sunshine Aviation." with a link to `orangesunshineaviation.com`.

8. **Save as template.** Name it "LH Standard Issue v1." Every edition starts from this template.

### Logo Files to Upload

Upload these to your Beehiiv media library:

- `LH_NOME_0000_Layer2_1.png` — Orange wordmark (for header on white background)
- `LH_NOME_0001_Layer3.png` — Black wordmark (backup)
- `PERFIL_1_1.jpg` — Purple background profile image (for Beehiiv publication avatar)
- `LOGOPRINCIPAL_0002_Layer1_1.png` — Full color logo with hawk (for welcome email or special editions)

### Beehiiv Website / Subscribe Page

Beehiiv gives you a built-in landing page. Customize it:

- **Background color:** `#521F84` (deep purple — the most distinctive option from your palette)
- **Text color:** White
- **Accent / button color:** `#FF4900` (orange)
- **Headline on subscribe page:** "Private aviation intelligence for people who pay attention."
- **Subhead:** "Market signals, operator reality, and what's actually happening in the business of flying private. Free. Every two weeks."
- **Upload the white Loud Hawk wordmark** as the page logo (use the white version on the purple background)
- Keep the page minimal. No paragraphs of copy. The tagline does the work.

---

## PART 3: WELCOME EMAIL

Set up an automated welcome email in Beehiiv (Automations → Welcome Email):

**Subject line:** `You're in. Here's what Loud Hawk is.`

**Body:**

> You just subscribed to Loud Hawk — private aviation intelligence for people who pay attention.
>
> Here's what to expect:
>
> Every two weeks, you'll get a short, specific read covering what's actually happening in the private aviation market. Charter pricing shifts. Operator moves. The gap between how the industry markets itself and how it actually performs. No lifestyle fluff. No sales pitches. Just signal.
>
> Loud Hawk is published by Orange Sunshine Aviation — advisory-first charter brokerage. We write what we observe because the market is more transparent when someone is paying attention.
>
> Edition 1 is [already in your inbox / coming soon]. Read it.
>
> — Loud Hawk

Keep the welcome email clean. Same template styling. No images beyond the header logo. The writing should demonstrate the voice immediately.

---

## PART 4: LAUNCH ANNOUNCEMENT — LINKEDIN

LinkedIn is your highest-leverage channel for launch. Your target readers (business owners, aviation professionals, wealth advisors, charter users) are there.

### Post 1 — Launch Day (Personal Profile)

Post from your personal LinkedIn profile, not a company page. Personal profiles get 5-10x the reach of company pages on LinkedIn.

**Format:** Text post. No image carousel. No link in the body (LinkedIn suppresses link posts). Put the subscribe link in the first comment.

---

**Draft:**

I started a newsletter about private aviation.

Not the lifestyle version. The version where I tell you what charter actually costs this month, why that operator just lost their certificate, and what the broker quoting you $38,000 isn't mentioning.

It's called Loud Hawk. It comes out every two weeks. It's short. It's free. And it says what most people in this industry won't.

If you charter aircraft, own aircraft, manage aircraft, or advise people who do — this is written for you.

First edition is live. Link in the comments.

---

**First comment (post immediately after publishing):**

Subscribe here → [Beehiiv subscribe URL]

---

### Post 2 — Day 3-4 (Follow-up, different angle)

**Draft:**

The private aviation market has an information problem.

Clients don't know what a fair charter price looks like. They don't know which operators are cutting corners. They don't understand why the quote they got on Monday is $12,000 more than the same trip last month.

Loud Hawk is a biweekly newsletter that fixes some of that. Market signals, operator reality, and the gap between how this industry markets itself and how it actually performs.

Edition 1 just dropped. It's free. Link below.

---

### Post 3 — Day 7-10 (Content-led post, not a promo)

Pull a sharp observation from Edition 1 and post it as native LinkedIn content. Don't link to the newsletter — just deliver the insight. Then add at the bottom:

"I write about this in Loud Hawk, a biweekly aviation intelligence newsletter. Link to subscribe in my profile."

This is the "prove it" post. You're demonstrating the voice and the value before asking anyone to subscribe.

---

## PART 5: LAUNCH ANNOUNCEMENT — INSTAGRAM

Instagram is secondary for subscriber acquisition but useful for brand presence and Loud Hawk awareness, especially if you plan to run Loud Hawk content there over time.

### Profile Setup

- **Profile picture:** Use `PERFIL_1_1.jpg` (purple background, LH monogram with hawk — the most visually distinctive version)
- **Bio:** `Private aviation intelligence. Newsletter every 2 weeks. Subscribe ↓`
- **Link in bio:** Beehiiv subscribe page URL

### Launch Post (Feed)

**Visual:** Create a simple graphic — solid purple (`#521F84`) background, orange LOUD HAWK wordmark centered, with the tagline below in white text: *Private aviation intelligence for people who pay attention.*

This is a brand announcement, not an article. Keep it clean.

**Caption:**

Loud Hawk is live.

A biweekly newsletter covering what's actually happening in private aviation — charter pricing, operator moves, market signals, and the gap between how the industry markets itself and how it performs.

No lifestyle content. No sales pitches. Just the information that makes you a better-informed participant in business aviation.

Edition 1 is out now. Link in bio to subscribe.

---

### Stories (Launch Day + Day 2)

**Story 1:** Screenshot of the Edition 1 email in your inbox. Add text overlay: "Edition 1 — live now" with a link sticker to subscribe.

**Story 2:** Text-on-background story (purple background, white text): "Most aviation newsletters tell you where to fly. This one tells you what's actually happening in the market." Swipe-up / link sticker.

---

## PART 6: 30-DAY SUBSCRIBER ACQUISITION STRATEGY

Your goal for the first 30 days is not 10,000 subscribers. It's 50-150 real, relevant subscribers who actually care about private aviation intelligence. Quality of list matters more than size, especially at launch. A small list of the right people is the foundation of everything.

### Week 1 (Days 1-7): Launch Push

**Actions:**
- Publish LinkedIn Post 1 (launch day) from personal profile
- Comment with subscribe link immediately
- Send the Beehiiv link directly via DM to 15-20 people you know personally who fit the reader profile — aviation colleagues, business contacts who fly private, industry connections. Personalize each message. "I started this, thought you'd find it useful."
- Post Instagram launch content (feed post + stories)
- Publish LinkedIn Post 2 (day 3-4)
- Add Loud Hawk subscribe link to your LinkedIn profile headline or featured section
- Add subscribe link to your email signature

**Target:** 30-50 subscribers by end of Week 1.

### Week 2 (Days 8-14): Content-Led Growth

**Actions:**
- Publish LinkedIn Post 3 — the "prove it" post. Native insight from Edition 1, no hard CTA.
- Identify 3-5 LinkedIn posts from others in the aviation space. Leave thoughtful comments that demonstrate your market knowledge. This builds visibility with their audience. Do not drop newsletter links in comments on other people's posts.
- Share one Loud Hawk observation as an Instagram post (text-based graphic, editorial voice).
- Personal outreach: DM 10 more people. By now you may have early readers who can tell you what resonated — use that signal.

**Target:** 50-80 cumulative subscribers.

### Week 3 (Days 15-21): Edition 2 Drop + Momentum

**Actions:**
- Publish Edition 2. This is critical — the second edition proves you're consistent, not a one-off.
- LinkedIn post teasing one insight from Edition 2 (native content, link in comments).
- Instagram story with a screenshot or key quote from Edition 2.
- Ask 2-3 early subscribers directly: "What did you think? Would you forward this to someone?" Word-of-mouth from real readers is the most credible growth channel at this stage.
- Enable Beehiiv's referral program if available on your plan. Even a simple "share with a friend" prompt at the bottom of each edition helps.

**Target:** 75-120 cumulative subscribers.

### Week 4 (Days 22-30): System & Habits

**Actions:**
- LinkedIn: One more content-led post. You should now have a rhythm — one post per edition cycle, plus engagement on others' posts.
- Review Beehiiv analytics: open rate, click rate, subscriber growth. Your open rate target for a niche newsletter at this stage should be 45%+ (niche B2B newsletters often hit 50-60% early). If you're below 40%, your subject lines or audience fit need attention.
- Start planning Edition 3 and 4 — get ahead of the biweekly cadence so you're never scrambling.
- Evaluate whether any early feedback suggests adjusting the editorial mix (more Market Signal? More How It Actually Works?).

**Target:** 100-150 cumulative subscribers.

---

## PART 7: WHAT NOT TO DO IN THE FIRST 30 DAYS

- **Don't buy subscribers or use list-building services.** They'll destroy your deliverability and open rates.
- **Don't run paid ads for subscribers yet.** You need to prove the content resonates organically before spending money to amplify it. The Execution Memo budgets $0-$180 for Loud Hawk operating costs in Year 1. Respect that.
- **Don't post on LinkedIn more than 2-3x per week.** Over-posting dilutes each post's reach and makes you look like you're selling, not sharing.
- **Don't cross-post the entire newsletter to LinkedIn or Instagram.** The newsletter is the product. Social content should create interest and drive subscriptions, not replace the email.
- **Don't obsess over subscriber count.** At this stage, 50 engaged readers who open every edition and occasionally respond are worth more than 500 who signed up and never opened.
- **Don't change the template or editorial structure after one edition.** The blueprint says revisit after 10 editions. Stick with it.

---

## PART 8: SUBJECT LINE APPROACH

Your subject lines should match the Loud Hawk voice — sharp, specific, no clickbait. The subject line is the first line of editorial trust.

**Good subject lines (examples):**
- "Light jet pricing is up 18% since January"
- "What your broker isn't telling you about repositioning fees"
- "Three things that changed in charter this month"
- "The operator that just lost its ARG/US rating"
- "Why that $28K quote doesn't mean what you think"

**Bad subject lines (avoid):**
- "Loud Hawk Edition #1" (says nothing)
- "This Week in Aviation" (generic)
- "🔥 You won't believe what's happening in charter" (clickbait)
- "The Ultimate Guide to Private Aviation" (content marketing cliché)

The subject line should make the reader want to know the answer. Be specific enough that it's clear this comes from someone with actual market visibility.

---

## PART 9: QUICK SETUP CHECKLIST

- [ ] Create Beehiiv account (free Launch plan)
- [ ] Set publication name, handle, tagline
- [ ] Connect custom domain
- [ ] Configure sender name and reply-to
- [ ] Upload logo files to media library
- [ ] Set brand colors and typography in Style panel
- [ ] Build and save "LH Standard Issue v1" template
- [ ] Customize subscribe landing page (purple bg, white text, orange button)
- [ ] Write and activate welcome email automation
- [ ] Load Edition 1 into the template
- [ ] Preview on desktop and mobile
- [ ] Add subscribe link to LinkedIn profile (headline or featured section)
- [ ] Add subscribe link to email signature
- [ ] Schedule or publish Edition 1
- [ ] Post LinkedIn announcement (personal profile)
- [ ] Drop subscribe link in first comment
- [ ] DM 15-20 personal contacts with subscribe link
- [ ] Post Instagram launch content
- [ ] Plan Edition 2 content

---

*This playbook is built for the current stage: solo founder, zero list, first edition ready to ship. Follow the checklist, execute the first 30 days, and revisit after Edition 5 with real data to decide what to expand.*
