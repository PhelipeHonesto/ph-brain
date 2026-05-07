---
title: Recovering Twilio account after phone number change
created: 2026-05-04T22:51:16.408944Z
updated: 2026-05-05T02:01:08.678081Z
uuid: 8a5b0ae2-3562-4658-b034-d1c7a00eedf0
source: claude-conversation
type: source
message_count: 16
---

# Recovering Twilio account after phone number change

## Phelipe

i changed my phone number. and i can find my recory code from twilio. what to do

---

## Claude

That's a frustrating spot to be in. Let me make sure I understand what's going on before suggesting next steps.

When you say "recovery code from Twilio" — do you mean:

1. You're locked out of your **Twilio account** itself (can't log in because 2FA goes to your old number, and you can't find the recovery codes Twilio gave you when you set up 2FA)?

2. Or you're locked out of **another service** (Google, GitHub, a bank, etc.) that uses Twilio/Authy as its 2FA app, and you can't find recovery codes for that?

Also — when you say you "can find" the recovery code, did you mean **can't** find it? Just want to confirm before pointing you in the wrong direction.

Quick answer either way: most services (including Twilio itself) have an account recovery process for exactly this situation — usually involving identity verification via email + government ID. It's slow (often 24-72 hours) but it works. The path differs depending on which account you're locked out of, so let me know which one and I'll walk you through it.

---

## Phelipe

Verify Your Identity
Enter the recovery code you were provided during your initial enrollment.
Enter your recovery code *
Continue
__Try another method__

i dont have this research how to recovery

---

## Claude

Got it — you're stuck on Twilio's 2FA recovery code screen during login, you don't have the code, and your old phone number is gone so SMS/voice won't work either. Let me search for the current recovery process.
```
This block is not supported on your current device yet.
```

Here's what you need to do. Twilio has a manual identity-verification path for exactly this situation — old phone gone, no recovery code.

**The path:**

1. Go to Twilio's Support Help Center: submit a help request directly to Support without needing to login. The direct URL is **support.twilio.com** → "Submit a request."

2. If that route doesn't surface a "can't log in" form, email **support@twilio.com** directly. If you are unable to login to your account, and have lost your recovery code, they have a manual identification process to help regain access to your account.

**What to include in the ticket** (this speeds it up massively — Twilio's Trust Hub team is strict):

- Account email address
- Account SID (starts with `AC...`) if you have it from any old email/invoice
- The old phone number that was on the account
- Your new phone number
- Last 4 digits of the credit card on file, plus the billing name and address
- A government-issued photo ID (driver's license or passport)
- A recent Twilio invoice or any account-identifying email if you have one
- Brief explanation: phone number changed, no longer have access to old number, recovery code unavailable

**Important context for you specifically:** Since OSA likely has Twilio wired into something live (you mentioned WhatsApp/messaging-native charter inquiry agent on Twilio scoped at ~$0.40/conversation), check whether you have any **API keys** still working on the account. If you have valid API keys and can currently send email through your account — that's a useful signal you can include in the ticket as further proof of ownership. Same logic applies to SMS/Voice API keys.

**Realistic timeline:** 24–72 hours for a response, sometimes longer. They'll usually email back asking for the ID + billing verification, then unlock once it checks out.

**One thing to know going forward:** Twilio does not allow using a non-Twilio phone number for 2FA — wait, that's actually backwards in the doc; they require a real verifiable number, not a Twilio-purchased one. Either way, once you're back in: regenerate the recovery code immediately and store it in 1Password (or wherever your other credentials live). The new code invalidates the old one, so this is a clean reset.

Want me to draft the support ticket message for you?

---

## Phelipe

phone number i can call?

---

## Claude

Let me check whether Twilio offers phone support for account recovery.
```
This block is not supported on your current device yet.
```

Short answer: **no public phone number for account recovery**. Twilio is ticket-and-email only for this.

Here's what's actually available:

- All customers can submit a request via the ticket form, and Support staff will respond — usually within 24 hours. Customers with upgraded Support plans have access to faster guaranteed response times, live chat requests, and phone support for some users.
- Phone support is **gated behind paid Support plans** (Developer/Production/Business tiers) and even then, it's for technical issues — not lockouts. Account recovery specifically goes through the ticket form regardless.
- You'll see a number floating around the internet — **1-844-814-4627** — but that's a third-party-listed number, not Twilio's official recovery line. I'd skip it.

**The real path is still:**

1. Go to **help.twilio.com** → "Submit a request" (works without login)
2. Or email **support@twilio.com** directly with the identity-verification info I listed before

If you want speed, the ticket form is actually faster than waiting for a callback would be — Twilio's account recovery team is email-based by design (they need you to send ID anyway, which can't happen on a phone call).

Want me to draft the ticket message now? Tell me:
- The email on the Twilio account
- The old phone number (last 4 is fine if you don't want to type the whole thing)
- Whether you have any old Twilio invoices or the Account SID handy

---

## Phelipe

[phelipe.hon@gmail.com](mailto:phelipe.hon@gmail.com)
8634581728

We were unable to process your automatic balance recharge payment for $11.38 on Fofocando com P.H. with SID: AC8cbf41280cab2e13074df19edb7e2b10 and owner email [phelipe.hon@gmail.com](mailto:phelipe.hon@gmail.com)
Your current account balance is $8.62. To avoid a potential service interruption, please log into your account and update your payment information.
We also allow you to set a backup payment method, which can be charged automatically in the event that there are issues with the primary account payment method. You can find instructions for doing so here.
Visit Twilio's Billing dashboard page to retry your transaction or add a new Credit Card/Paypal first.
If you'd like to see the latest usage on the account - please visit your Usage page.
In case you are not using your Twilio account - please visit the Stop Recurring Charges page or our How-to-close a Twilio account guide.

---

## Claude

Perfect, you've got everything needed. The Account SID alone is gold — that's the strongest ownership signal you can give them. Here's the ticket draft:

---

**Subject:** Account Recovery — Lost 2FA Access, Phone Number Changed, Recovery Code Unavailable

**Body:**

Hello Twilio Support,

I am locked out of my Twilio account and need help recovering access. I changed my phone number, no longer have access to the old one, and I do not have my 2FA recovery code.

**Account details for verification:**

- Account email: phelipe.hon@gmail.com
- Account SID: AC8cbf41280cab2e13074df19edb7e2b10
- Account name (project): Fofocando com P.H.
- Old 2FA phone number: 863-458-1728
- Recent account balance: $8.62 (after a failed $11.38 auto-recharge)
- I am the account owner

**What I need:**

1. Reset 2FA on the account so I can log back in
2. Update the 2FA phone number to my new number (I will provide it once we are in contact through a verified channel)

I am happy to provide:

- Government-issued photo ID
- Last 4 digits of the credit card on file
- Billing name and address on the account
- Any additional verification you require

Please let me know the next steps. This is time-sensitive as I have an active integration on the account.

Thank you,
Phelipe

---

**Where to send it:**

- Primary: **help.twilio.com** → "Submit a request" (you don't need to log in)
- Backup: email **support@twilio.com** with the same content

**A few tips that will save you days:**

1. **Don't include your new phone number, ID, or credit card info in the first message.** Wait until they reply from a verified Twilio support address. Sending sensitive docs into a generic inbox before they've engaged the ticket is risky and they'll usually ask for them through a secure channel anyway.

2. **Reply fast when they come back.** These tickets often go cold because the customer takes 12+ hours to send the ID, then it cycles to a different agent. Watch your inbox.

3. **Mention the active integration.** Twilio prioritizes tickets where service interruption is a real concern — your failed auto-recharge actually helps here, it shows the account is live and in use.

4. **Don't open multiple tickets.** It splits the queue and slows you down. One ticket, then reply on that thread.

Want me to also draft a short follow-up reply for when they come back asking for ID + billing verification? That way you can just paste and send when it lands.

---

## Phelipe

sid does not work ?

---

## Claude

Which part isn't working — the support form is rejecting the SID, or you tried logging in with it? Tell me what you're seeing (error message or the screen you're stuck on) and I'll help debug.

A couple of possibilities depending on what you mean:

**If the support ticket form is asking for an SID and rejecting it:** the form may be looking for the *current logged-in* account SID, which you can't provide because you're locked out. In that case, just put the SID in the message body (not the form field), pick a category like "Login / Account Access" or "Other," and submit without it. The agent will use the SID from your message.

**If you're trying to log in with the SID:** that's not how Twilio login works — login is just email + password + 2FA. The SID is an account identifier, not a credential. You'd only use the SID for API calls or to identify the account to support.

**If the SID format looks wrong to them:** double-check there are no missing/extra characters. A valid Account SID is exactly **34 characters**, starts with `AC`, and is followed by 32 hexadecimal characters. The one you gave me — `AC8cbf41280cab2e13074df19edb7e2b10` — counts to 34 and is all valid hex, so that looks correct.

Tell me what screen you're on or paste the error and I'll get you unstuck.

---

## Phelipe

Verify Your Identity
Enter the recovery code you were provided during your initial enrollment.
Enter your recovery code *
Continue
__Try another method__

i cant find this

---

## Claude

Right, so you're stuck on that login screen. The "recovery code" page is a dead end for you — you don't have it, and there's no way to bypass it from that screen.

**Stop trying to log in.** You can't get past 2FA without either the old phone or the recovery code. The only path forward is the support ticket.

Here's exactly what to do right now:

**1. Open a new browser tab and go to:** https://help.twilio.com

**2. Click "Submit a request"** (top right, or scroll to bottom). You do NOT need to log in.

**3. In the form:**
- **Subject:** Locked out of account — lost 2FA access, no recovery code
- **Category/Topic:** Pick "Account" or "Login Issues" if available, otherwise "Other"
- **Description:** Paste the message I drafted in my previous reply

**4. Submit.**

**5. Wait for their email reply** (usually 24–72 hours) at phelipe.hon@gmail.com. They will email you asking for ID and billing verification. Reply fast when they do.

That's it. There is no other path. The recovery code screen is not solvable on your end — only Twilio's support team can reset it.

Do you want me to give you the ticket message again so you can copy-paste it directly?

---

## Phelipe

Seth (Authy Support) <support@authy.zendesk.com>
8:00 PM (6 minutes ago)
to me
## In replies all text above this line is added to the ticket ##
(Reply to this email to follow up on this issue)
Note: If you're cc'd on the ticket, please reply all to ensure comments are added to the ticket.
	
Seth (Authy)
May 4, 2026, 6:00 PM PDT
Hi Phelipe,
 
Thank you for reaching out to Authy Support at Twilio. My name is Seth, and I understand you're encountering some challenges. Rest assured, I'm here to provide assistance and guide you towards a resolution.
 
I’ve located an Authy account for you linked to the email you’re using to contact us and phone (+1) XXX-XXX-XX28.
 
To assist you with recovering your Authy account, please provide the following information:
The phone number registered with Authy
Any details about recent account activity or services you were trying to access
 
Once we have this information, we can guide you through the next steps for account recovery. If you have access to any backup devices or previously used Authy apps, please let us know as that may help speed up the process.
 
If you have any other questions or concerns, please let us know. We're committed to helping you regain access as quickly as possible.
 
Best,
Seth
Twilio Support
Did this solve your issue? You can set this ticket to solved by clicking the link below:
This ticket is solved
This is in reference to ticket # 26733976

---

## Claude

Good — Seth confirmed they found your account. Now you reply with the verification info. Here's the response:

---

**Reply (hit "Reply" on Seth's email, don't start a new thread):**

Hi Seth,

Thanks for the quick response. Here are the details:

**Phone number registered with Authy:** +1 863-458-1728

**Recent account activity / services:** This Authy account is the 2FA method for my Twilio account (SID: AC8cbf41280cab2e13074df19edb7e2b10, project name "Fofocando com P.H.", owner email phelipe.hon@gmail.com). I use it to log into the Twilio Console. The account is active — I received a failed auto-recharge notification today for $11.38, and my current balance is $8.62.

**Reason for recovery:** I changed my phone number and no longer have access to +1 863-458-1728. I do not have my Authy backup/recovery code. I need to update the 2FA method to my new phone number so I can log back into Twilio.

**Backup devices:** I do not have any other devices with Authy installed or any previously used Authy apps available.

I am happy to provide any additional verification you need — government-issued photo ID, last 4 of the credit card on file, billing address, etc. Please let me know what's required and I'll send it through whatever secure channel you prefer.

Thanks,
Phelipe

---

**A few things to keep in mind:**

1. **Reply on the same thread** — don't start a new ticket. Ticket #26733976 is your reference.

2. **This is Authy Support, not Twilio Console Support** — they're related teams under the same company, but the agent's job here is specifically to recover/reset the Authy 2FA. Once Seth resets it, you'll be able to log into Twilio with your password and either no 2FA or a fresh setup.

3. **Don't send your ID or new phone number yet.** Wait for Seth to ask. He may have a secure upload link or specific format. Sending sensitive docs into a Zendesk reply unprompted is bad practice.

4. **Watch your inbox tonight and tomorrow morning.** Authy support tends to move in business hours (PDT). If Seth replies and you take 12 hours to respond, the ticket may bounce to a different agent and you'll repeat steps.

You're on the right track — this is the normal flow.

---

## Phelipe

Seth (Authy Support) <support@authy.zendesk.com>
8:31 PM (29 minutes ago)
to me
## In replies all text above this line is added to the ticket ##
(Reply to this email to follow up on this issue)
Note: If you're cc'd on the ticket, please reply all to ensure comments are added to the ticket.
	
Seth (Authy)
May 4, 2026, 6:31 PM PDT
Hello Phelipe,
 
Thanks for your detailed response.
 
I'll be engaging your ticket now to the appropriate team best equipped to help you resolve the issue.
 
They will be in touch with you shortly.
 
Warm regards,
Seth
Twilio Support
Did this solve your issue? You can set this ticket to solved by clicking the link below:
This ticket is solved
This is in reference to ticket # 26733976

---

## Claude

Good — that's normal. Seth is just a tier-1 triage agent; the actual recovery requires the identity-verification team. Your ticket is now in the right queue.

**What happens next:**

The escalation team will email you back (same ticket #26733976) and almost certainly ask for:
- Government-issued photo ID (driver's license or passport)
- Possibly billing verification (last 4 of card on file, billing address)
- Possibly a selfie holding the ID

**Realistic timeline:** Anywhere from a few hours to 2-3 business days. Authy/Twilio's identity team isn't 24/7. Since Seth replied at 6:30 PM PDT on a Monday, you might hear back tonight or more likely tomorrow during PDT business hours.

**What to do now:**

1. **Have your ID ready.** Scan or take a clear photo of your driver's license or passport. Good lighting, all four corners visible, no glare. Save it somewhere you can attach quickly.

2. **Don't send the ID yet.** Wait for them to ask and follow their specific instructions (they may have a secure upload portal vs. email attachment).

3. **Keep an eye on your inbox** — including spam. Zendesk emails sometimes get filtered.

4. **Don't reply to the ticket again unless they ask you something.** Bumping the ticket can actually push it down the queue.

5. **Don't open a second ticket.** That will fragment the case and slow things down.

Nothing more to do tonight. You handled this correctly — clear info, fast responses, all the right identifiers. When the next email lands, send it to me and I'll help you reply.

---
