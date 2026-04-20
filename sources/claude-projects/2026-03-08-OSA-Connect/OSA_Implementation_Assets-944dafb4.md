---
title: OSA_Implementation_Assets.md
project: OSA Connect
doc_uuid: 944dafb4-cca3-4809-8bc2-54816925bf68
source: claude-project-doc
type: source
---

# OSA Connect — Implementation Assets v1
*Derived from Charter Brokerage Operating System v1.0 — No new strategy added*

---

# ASSET 1: NOTION OS — PAGE TREE, DATABASES, PROPERTIES, AND TEMPLATES

---

## 1.1 PAGE TREE

```
OSA Connect HQ
├── 📋 Operations
│   ├── 🗂 Trips Database
│   ├── 👤 Clients Database
│   ├── 💬 Quotes Database
│   ├── ✈️ Operators Database
│   └── ✅ Tasks Database
├── 📁 SOPs & Reference
│   ├── Master Trip Checklist
│   ├── Disruption Playbook
│   ├── Quote Workflow
│   └── Scripts Library
├── 📊 Dashboard
│   ├── Daily Ops View
│   └── Weekly Metrics View
└── 📦 Trip Packets (client-facing, linked from Trips DB)
```

---

## 1.2 DATABASE: TRIPS

**Icon:** ✈️ | **Title property:** Trip ID (auto or manual: CHI-MIA-2025-001)

### Properties

| Property Name | Type | Options / Notes |
|---|---|---|
| Trip ID | Title | Format: [ORG]-[DEST]-[YYYY]-[###] |
| Client | Relation → Clients DB | Required |
| Route | Text | "ORD → MIA" |
| Departure Date | Date | Include time |
| Return Date | Date | Leave blank if one-way |
| Trip Type | Select | One-Way / Round-Trip / Multi-Leg |
| Passengers | Number | Integer |
| Aircraft Category | Select | Light / Midsize / Super-Mid / Heavy |
| Aircraft Tail # | Text | Confirmed at booking |
| Operator | Relation → Operators DB | |
| Quote Selected | Relation → Quotes DB | |
| All-in Price (Client) | Number | Format: Currency USD |
| Operator Cost | Number | Format: Currency USD (internal) |
| Margin $ | Formula | `prop("All-in Price (Client)") - prop("Operator Cost")` |
| Margin % | Formula | `round(prop("Margin $") / prop("All-in Price (Client)") * 100)` |
| Pipeline Stage | Select | See stage list below |
| Lead Source | Select | Referral / Cold-Outreach / Inbound-Web / Partner |
| Charter Agreement Signed | Checkbox | |
| Payment Received | Checkbox | |
| T-48 Sent | Checkbox | |
| T-24 Confirmed | Checkbox | |
| Wheels-Up Logged | Checkbox | |
| Post-Flight Sent | Checkbox | |
| Follow-Up Scheduled | Date | 30 days post-flight |
| Notes | Text | CRM notes field |
| Related Tasks | Relation → Tasks DB | |

### Pipeline Stage Options (Select)
- 🟡 INQUIRY
- 🟠 QUOTING
- 🔵 OPTIONS SENT
- 🟣 NEGOTIATING
- 🟢 CONFIRMED
- ✅ BOOKED
- 🏁 COMPLETED
- ❌ LOST

### Views to Create
1. **Active Trips** — Filter: Stage ≠ COMPLETED, ≠ LOST | Sort: Departure Date ASC
2. **Pipeline Kanban** — Group by: Pipeline Stage
3. **This Week** — Filter: Departure Date = this week
4. **Needs Attention** — Filter: T-48 Sent = unchecked AND Departure Date ≤ today + 3 days
5. **All Trips** — No filter, Sort: Created DESC

### Trip Template

```
✈️ [TRIP ID]

---
## 📋 INTAKE
- Route: 
- Departure: 
- Return: 
- Passengers: 
- Aircraft Requested: 
- Special Requirements: 
- Budget Range: 
- How Referred: 

---
## 💬 QUOTING
Operators Contacted:
- [ ] Operator 1 — contacted [time] — response: 
- [ ] Operator 2 — contacted [time] — response: 
- [ ] Operator 3 — contacted [time] — response: 

Quote sent to client: [date/time]
Quote expiry: 24h from above

---
## 📄 BOOKING
- [ ] Client confirmed option in writing — [date]
- [ ] Charter agreement sent — [date]
- [ ] Charter agreement countersigned — [date]
- [ ] Payment received — [date] — Wire ref: 
- [ ] Operator booking confirmed in writing — [date]
- [ ] Tail # confirmed: 
- [ ] Crew confirmed: 
- [ ] Catering ordered: Y / N

---
## 🛫 PRE-FLIGHT
- [ ] T-48 client message sent — [date]
- [ ] T-24 weather checked — METAR/TAF: OK / Issues: 
- [ ] T-24 aircraft position confirmed with operator
- [ ] T-24 FBO handling confirmed — FBO Name: 
- [ ] T-24 passenger manifest finalized
- [ ] All confirmations logged

---
## 🛬 DAY-OF
- [ ] Departure reminder sent to client
- [ ] Phone available until wheels-up
- [ ] Wheels-up time: 

---
## 📬 POST-FLIGHT
- [ ] Post-flight message sent — [date]
- [ ] Client feedback: 
- [ ] Operator payment confirmed — [date]
- [ ] Operator reliability updated in Operators DB
- [ ] 30-day follow-up scheduled: 

---
## 🗒 NOTES
[Running notes log with timestamps]
```

---

## 1.3 DATABASE: CLIENTS

**Icon:** 👤 | **Title property:** Full Name

### Properties

| Property Name | Type | Options / Notes |
|---|---|---|
| Full Name | Title | |
| Company | Text | |
| Email | Email | |
| Phone / WhatsApp | Phone | |
| Location / City | Text | |
| Client Type | Select | UHNW / Corporate / Family-Office / Concierge / Other |
| Travel Frequency | Select | First-Time / Occasional / Frequent / VIP |
| Preferred Aircraft | Select | Light / Midsize / Super-Mid / Heavy |
| Preferred Airports | Text | FBOs / airports they use |
| Catering Preferences | Text | |
| Typical Passenger Count | Number | |
| Special Notes | Text | Pets, security, accessibility |
| Lead Source | Select | Referral / Cold-Outreach / Inbound-Web / Partner |
| Referred By | Text | Person or company |
| Trips | Relation → Trips DB | |
| Total Trips Completed | Rollup | Count of Trips where Stage = COMPLETED |
| Total Volume | Rollup | Sum of All-in Price from Trips |
| Last Trip Date | Rollup | Latest Departure Date from Trips |
| Last Contact Date | Date | |
| Next Follow-Up | Date | |
| VIP Flag | Checkbox | Priority sourcing and response |
| Status | Select | Active / Inactive / Prospect |

### Views to Create
1. **Active Clients** — Filter: Status = Active
2. **VIP** — Filter: VIP Flag = checked
3. **Follow-Up Due** — Filter: Next Follow-Up ≤ today | Sort: Next Follow-Up ASC
4. **By Type** — Group by: Client Type
5. **All** — No filter

### Client Template

```
👤 [CLIENT NAME]

---
## Contact
- Email: 
- WhatsApp: 
- Company: 
- Location: 

---
## Travel Profile
- Type: 
- Frequency: 
- Preferred Aircraft: 
- Preferred Airports/FBOs: 
- Typical Pax Count: 
- Catering Preferences: 
- Special Notes: 

---
## Relationship Log
[Date] — [Touchpoint summary]
[Date] — [Touchpoint summary]

---
## Trips
[Linked from Trips DB]
```

---

## 1.4 DATABASE: QUOTES

**Icon:** 💬 | **Title property:** Quote ID (format: Q-[TripID]-[##])

### Properties

| Property Name | Type | Options / Notes |
|---|---|---|
| Quote ID | Title | |
| Trip | Relation → Trips DB | |
| Operator | Relation → Operators DB | |
| Aircraft Type | Text | e.g. Citation CJ3+, Challenger 350 |
| Aircraft Year | Number | |
| Tail Number | Text | |
| Seats Available | Number | |
| Operator Quote ($) | Number | What operator charges us |
| Client Price ($) | Number | With margin applied |
| Margin $ | Formula | `prop("Client Price ($)") - prop("Operator Quote ($)")` |
| Margin % | Formula | `round(prop("Margin $") / prop("Client Price ($)") * 100)` |
| Safety Rating | Select | ARGUS Gold / ARGUS Platinum / Wyvern Wingman / Wyvern Registered / None |
| Part 135 Verified | Checkbox | |
| Quote Status | Select | Pending / Sent / Selected / Rejected / Expired |
| Quote Sent Date | Date | |
| Quote Expiry | Date | +24h from sent |
| Notes | Text | Aircraft amenities, caveats |

---

## 1.5 DATABASE: OPERATORS

**Icon:** ✈️ | **Title property:** Operator Name

### Properties

| Property Name | Type | Options / Notes |
|---|---|---|
| Operator Name | Title | |
| HQ City / State | Text | |
| Region Coverage | Multi-select | Midwest / East / West / Southeast / International |
| Fleet Size | Number | |
| Aircraft Types | Text | CJ3, Challenger 350, G550, etc. |
| Primary Category | Select | Light / Midsize / Super-Mid / Heavy / Mixed |
| Safety Rating | Select | ARGUS Gold / ARGUS Platinum / Wyvern Wingman / Wyvern Registered / Unrated |
| Part 135 Certificate | Checkbox | |
| Charter Desk Email | Email | |
| Charter Desk Phone | Phone | |
| Contact Name | Text | Main quoting contact |
| Preferred Comms | Select | Email / WhatsApp / Phone |
| WhatsApp Number | Phone | |
| Pricing Tier | Select | Budget / Mid / Premium |
| Response Speed | Select | Fast (<2h) / Medium (2–6h) / Slow (>6h) |
| Reliability Score | Select | Excellent / Good / Fair / Poor |
| Empty Leg Updates | Checkbox | |
| Last Contact Date | Date | |
| Broker Relationship | Select | New / Active / Strong |
| Quotes | Relation → Quotes DB | |
| Trips Completed | Rollup | Count of Trips from Quotes where Stage = COMPLETED |
| Notes | Text | Relationship notes, preferences |

### Views to Create
1. **Active Partners** — Filter: Broker Relationship = Active or Strong
2. **By Region** — Group by: Region Coverage
3. **By Category** — Group by: Primary Category
4. **Fast Responders** — Filter: Response Speed = Fast
5. **All Operators** — No filter

---

## 1.6 DATABASE: TASKS

**Icon:** ✅ | **Title property:** Task Name

### Properties

| Property Name | Type | Options / Notes |
|---|---|---|
| Task Name | Title | |
| Trip | Relation → Trips DB | |
| Client | Relation → Clients DB | |
| Operator | Relation → Operators DB | |
| Task Type | Select | Intake / Quote / Booking / Pre-Flight / Day-Of / Post-Flight / Follow-Up / Admin |
| Priority | Select | Urgent / High / Normal / Low |
| Status | Select | To Do / In Progress / Done / Blocked |
| Due Date | Date | Include time for SLA tasks |
| Assigned To | Person | |
| Notes | Text | |

### Views to Create
1. **Today** — Filter: Due Date = today | Sort: Priority DESC
2. **Overdue** — Filter: Due Date < today AND Status ≠ Done
3. **By Trip** — Group by: Trip
4. **Urgent** — Filter: Priority = Urgent AND Status ≠ Done

---
---

# ASSET 2: CRM PIPELINE — STAGES, EXIT CRITERIA, FIELDS, TAGS, SLAs, AUTOMATIONS

---

## 2.1 PIPELINE STAGES WITH EXIT CRITERIA

### 🟡 INQUIRY
**Definition:** Client has made contact. No intake info collected yet.
**Entry trigger:** Any inbound message, referral intro, cold-outreach response.
**Required fields to exit:** Name, contact info, any travel intent noted in CRM.
**SLA:** Respond within **15 minutes** during business hours.
**Exit criteria → QUOTING:** All 15 intake fields collected.

---

### 🟠 QUOTING
**Definition:** Full intake complete. Actively sourcing aircraft options.
**Required fields to exit:** ≥3 operators contacted (logged), quotes received, client quote document prepared.
**SLA:** Options delivered to client within **4 hours** of intake completion.
**Exit criteria → OPTIONS SENT:** Quote document sent to client via email.

---

### 🔵 OPTIONS SENT
**Definition:** Quote document delivered. Awaiting client response.
**SLA:** Follow up with client if no response within **4 hours**.
**Exit criteria → NEGOTIATING:** Client responds with feedback or counter.
**Exit criteria → CONFIRMED:** Client accepts an option in writing.
**Exit criteria → LOST:** Client explicitly declines or goes silent 48h+ after follow-up.

---

### 🟣 NEGOTIATING
**Definition:** Client has feedback. Adjusting pricing, aircraft, or timing.
**SLA:** Respond to client input within **2 hours**.
**Exit criteria → CONFIRMED:** Client accepts revised option in writing.
**Exit criteria → LOST:** No resolution after 72 hours of engagement.

---

### 🟢 CONFIRMED
**Definition:** Client accepted option in writing. Agreement + payment pending.
**Required actions before exit:** Charter agreement sent.
**SLA:** Agreement sent within **2 hours** of verbal confirmation.
**Exit criteria → BOOKED:** Agreement countersigned AND payment wire confirmed.

---

### ✅ BOOKED
**Definition:** Agreement signed. Payment received. Operator booking confirmed in writing.
**Required fields:** Tail number, crew confirmed, catering status, FBO confirmed.
**SLA:** Operator booking confirmed within **4 hours** of payment received.
**Exit criteria → COMPLETED:** Flight has departed. Post-flight message sent.

---

### 🏁 COMPLETED
**Definition:** Flight complete. Post-flight done. Operator paid.
**Required actions:** Post-flight message sent, client feedback logged, 30-day follow-up scheduled, operator reliability updated.
**No further exit.**

---

### ❌ LOST
**Definition:** Client declined, went elsewhere, or went cold.
**Required action:** Log reason (price / speed / competitor / timing / unresponsive).
**Do not delete.** Schedule 90-day re-engagement check.

---

## 2.2 REQUIRED FIELDS BY STAGE

| Field | Required At |
|---|---|
| Client name + contact | INQUIRY → QUOTING |
| Route + date + pax count | INQUIRY → QUOTING |
| Aircraft category requested | INQUIRY → QUOTING |
| Lead source logged | INQUIRY → QUOTING |
| Operators contacted (min 3) | QUOTING → OPTIONS SENT |
| Quote expiry date | OPTIONS SENT |
| Client written confirmation | CONFIRMED |
| Charter agreement countersigned | CONFIRMED → BOOKED |
| Payment wire confirmed | CONFIRMED → BOOKED |
| Operator booking confirmed | BOOKED |
| Tail # and crew | BOOKED |
| Post-flight message sent | COMPLETED |
| Lost reason logged | LOST |

---

## 2.3 TAGS

**Client Type**
- `UHNW`
- `Corporate`
- `Family-Office`
- `Concierge-Partner`
- `First-Time`

**Lead Source**
- `Referral`
- `Cold-Outreach`
- `Inbound-Web`
- `Partner-Intro`

**Travel Frequency**
- `Occasional` (1–2x/year)
- `Frequent` (3–6x/year)
- `VIP` (7+/year or high-value relationship)

**Aircraft Preference**
- `Light`
- `Midsize`
- `Super-Mid`
- `Heavy`

**Trip Flags**
- `Last-Minute` (booking < 48h before departure)
- `Multi-Leg`
- `International`
- `Disruption-Occurred`
- `Catering-Required`
- `Pet-On-Board`

---

## 2.4 SLA SUMMARY TABLE

| Trigger | SLA Target | Action if Missed |
|---|---|---|
| Inbound inquiry received | Respond in 15 min | Flag in Daily Ops view immediately |
| Intake complete | Deliver options in 4h | Prioritize above all other tasks |
| Options sent, no client reply | Follow up at 4h mark | One call + one message |
| Client negotiation input | Reply within 2h | Do not let go cold |
| Client confirms option | Send agreement in 2h | Agreement must precede operator lock |
| Payment received | Confirm operator booking in 4h | Operator hold lapses without confirmation |
| T-48 hours before departure | Send client reminder | Triggers pre-flight SOP |
| Flight completes | Post-flight message in 24h | Relationship maintenance |

---

## 2.5 AUTOMATIONS (HubSpot or Notion automations)

### Automation 1 — New Inquiry Alert
- **Trigger:** New deal created with Stage = INQUIRY
- **Action:** Create task "Respond to inquiry — 15 min SLA" due NOW, Priority = Urgent

### Automation 2 — Quote Deadline
- **Trigger:** Deal moves to QUOTING
- **Action:** Create task "Deliver options to client" due +4h, Priority = High

### Automation 3 — Options Follow-Up
- **Trigger:** Deal remains in OPTIONS SENT for 4h with no stage change
- **Action:** Create task "Follow up with client — no response" due NOW, Priority = High

### Automation 4 — Agreement Reminder
- **Trigger:** Deal moves to CONFIRMED
- **Action:** Create task "Send charter agreement — 2h SLA" due +2h, Priority = Urgent

### Automation 5 — T-48 Pre-Flight
- **Trigger:** Trip Departure Date = today + 2 days
- **Action:** Create task "Send T-48 client reminder" due today, Priority = High

### Automation 6 — T-24 Pre-Flight
- **Trigger:** Trip Departure Date = today + 1 day
- **Action:** Create tasks: "Check weather (METAR/TAF)", "Confirm aircraft position", "Confirm FBO handling", "Finalize passenger manifest" — all due today, Priority = High

### Automation 7 — Post-Flight
- **Trigger:** Deal moves to COMPLETED
- **Action 1:** Create task "Send post-flight message — 24h" due +24h
- **Action 2:** Create task "Confirm operator payment" due +5 days
- **Action 3:** Set Client "Next Follow-Up" date to +30 days

### Automation 8 — Lost Deal Re-Engagement
- **Trigger:** Deal moves to LOST
- **Action:** Create task "Re-engage check" due +90 days, Priority = Low

---
---

# ASSET 3: CLIENT INTAKE FORM — GOOGLE FORM

---

## Form Title: OSA Connect — Flight Request

**Description:** *Please complete all required fields. We'll confirm receipt and have options to you within 4 hours.*

---

### SECTION 1: YOUR INFORMATION

**Q1 — Full Name**
Type: Short answer
Required: Yes
Validation: None

**Q2 — Company or Organization** *(if applicable)*
Type: Short answer
Required: No
Validation: None

**Q3 — Email Address**
Type: Short answer
Required: Yes
Validation: Must be valid email format

**Q4 — Best Phone Number (WhatsApp preferred)**
Type: Short answer
Required: Yes
Validation: None (handle manually — international formats vary)

**Q5 — How did you hear about OSA Connect?**
Type: Dropdown
Required: Yes
Options:
- Referred by a person (fill in below)
- Referred by a company or agency
- LinkedIn
- Instagram
- Internet search
- Existing client / past flight
- Other

**Q6 — Referred by (name or company)** *(if applicable)*
Type: Short answer
Required: No
Validation: None
Show if: Q5 = "Referred by a person" OR "Referred by a company or agency"

---

### SECTION 2: FLIGHT DETAILS

**Q7 — Departure City or Airport**
Type: Short answer
Required: Yes
Helper text: *City name or airport code (e.g. Chicago / ORD / Midway)*

**Q8 — Destination City or Airport**
Type: Short answer
Required: Yes

**Q9 — Preferred Departure Date**
Type: Date
Required: Yes

**Q10 — Preferred Departure Time**
Type: Short answer
Required: Yes
Helper text: *Approximate is fine (e.g. "8am" or "as early as possible")*

**Q11 — Is this a round trip?**
Type: Multiple choice
Required: Yes
Options:
- Yes — I need a return flight
- No — one-way only
- Open return (I'll confirm the return date later)

**Q12 — Return Date** *(if round trip)*
Type: Date
Required: No
Show if: Q11 = "Yes — I need a return flight"

**Q13 — Return Time** *(if round trip)*
Type: Short answer
Required: No
Show if: Q11 = "Yes — I need a return flight"

**Q14 — Number of Passengers (adults)**
Type: Short answer
Required: Yes
Validation: Number only

**Q15 — Number of Passengers (minors under 18)**
Type: Short answer
Required: Yes
Helper text: *Enter 0 if none*
Validation: Number only

---

### SECTION 3: AIRCRAFT PREFERENCE

**Q16 — Aircraft size preference**
Type: Multiple choice
Required: Yes
Options:
- Light Jet (up to 7 passengers, shorter range)
- Midsize Jet (up to 9 passengers, cross-country capable)
- Super-Midsize Jet (up to 10 passengers, transcontinental)
- Heavy Jet (up to 16 passengers, long range)
- Not sure — please recommend based on my route

**Q17 — Any specific aircraft requirements?**
Type: Paragraph
Required: No
Helper text: *E.g. stand-up cabin, specific seating layout, Wi-Fi, etc.*

---

### SECTION 4: SPECIAL REQUIREMENTS

**Q18 — Catering requested?**
Type: Multiple choice
Required: Yes
Options:
- Yes — please arrange
- No
- Not sure yet

**Q19 — Will any pets be traveling?**
Type: Multiple choice
Required: Yes
Options:
- Yes
- No

**Q20 — Any accessibility or special assistance needs?**
Type: Paragraph
Required: No

**Q21 — Approximate budget range** *(optional — helps us prioritize options)*
Type: Multiple choice
Required: No
Options:
- Under $10,000
- $10,000 – $25,000
- $25,000 – $50,000
- $50,000 – $100,000
- $100,000+
- No preference / flexible

---

### SECTION 5: TIMING

**Q22 — How soon do you need options?**
Type: Multiple choice
Required: Yes
Options:
- Within 1 hour (urgent)
- Within 4 hours (standard)
- By end of today
- No rush — tomorrow is fine

**Q23 — Anything else we should know about this trip?**
Type: Paragraph
Required: No

---

### Form Settings

- **Confirmation message:** *"Thank you. We've received your request and will be in touch within 4 hours — sooner if you marked urgent. For immediate needs, call or WhatsApp us at [PHONE]."*
- **Collect email addresses:** Yes (automatically)
- **Response receipt to respondent:** Yes — send copy
- **Restrict to one response:** No
- **Edit after submit:** No

### Post-Submission Action
- Connect via Zapier or Make to HubSpot: create new Contact + Deal (Stage = INQUIRY) from form response
- Trigger internal notification to broker: email or Slack message with form summary

---
---

# ASSET 4: TRIP PACKET — CLIENT-FACING TEMPLATE

---

## Document Title: Your Flight Details — OSA Connect

*This is the client-facing document sent at booking confirmation. Deliver as PDF (from Google Doc or Notion) or formatted email body.*

---

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
OSA CONNECT
YOUR FLIGHT DETAILS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Prepared for: [CLIENT FULL NAME]
Trip Reference: [TRIP ID]
Prepared by: [BROKER NAME]
Date Issued: [DATE]
Direct Contact: [PHONE / WHATSAPP]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SECTION 1 — FLIGHT SUMMARY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

ROUTE:         [DEPARTURE CITY / AIRPORT] → [DESTINATION CITY / AIRPORT]
DEPARTURE:     [DAY, DATE] at [TIME] local
RETURN:        [DAY, DATE] at [TIME] local   [OR: One-Way]
PASSENGERS:    [#]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SECTION 2 — YOUR AIRCRAFT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Aircraft:      [TYPE — e.g. Bombardier Challenger 350]
Year:          [YEAR]
Registration:  [N-NUMBER]
Seats:         [#] passengers
Cabin:         [Brief description — e.g. Stand-up cabin, club seating]
Range:         [X] nautical miles
WiFi:          [Yes / No]
Lavatory:      [Yes / No]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SECTION 3 — DEPARTURE INSTRUCTIONS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

FBO NAME:      [FBO NAME]
ADDRESS:       [FULL STREET ADDRESS]
AIRPORT:       [AIRPORT NAME & CODE]

▸ Plan to arrive 15 minutes before your scheduled departure time.
▸ Proceed directly to the FBO terminal — no commercial check-in required.
▸ Government-issued photo ID required for all passengers.
▸ [IF INTERNATIONAL: Valid passports required for all passengers.]

Parking:       [FBO parking details or "complimentary ramp parking available"]
FBO Contact:   [FBO PHONE NUMBER]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SECTION 4 — ARRIVAL DETAILS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

DESTINATION FBO:  [FBO NAME]
ADDRESS:          [FULL ADDRESS]
AIRPORT:          [AIRPORT NAME & CODE]
FBO CONTACT:      [PHONE]

[IF GROUND TRANSPORT ARRANGED:]
Ground Transport: [Details or "arranged — contact will greet you at FBO"]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SECTION 5 — PASSENGER MANIFEST
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

The following passengers are confirmed on this flight:

1. [FULL LEGAL NAME]
2. [FULL LEGAL NAME]
3. [FULL LEGAL NAME]
[Continue as needed]

▸ Please notify us immediately of any changes to the passenger list.
▸ All passengers must present valid government-issued photo ID at the FBO.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SECTION 6 — CATERING & PREFERENCES
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[IF CATERING ARRANGED:]
Catering has been arranged per your preferences:
▸ [Item / description]
▸ [Item / description]
▸ Beverages: [Details]

[IF NO CATERING:]
Catering was not requested for this flight.
If you'd like to add catering, please contact us by [DEADLINE DATE/TIME].

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SECTION 7 — PRICING SUMMARY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Charter Price (all-in):    $[AMOUNT]
Catering:                  $[AMOUNT]   [OR: Included / N/A]
                           ──────────
TOTAL:                     $[TOTAL]

Payment Status:            ✅ Paid in Full   [OR: ⏳ Balance of $X due by DATE]

Payment was received via bank wire. This document serves as your booking confirmation.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SECTION 8 — CANCELLATION POLICY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Cancellations are subject to the terms in your signed charter agreement.

Summary:
▸ More than 7 days before departure: [per agreement]
▸ 3–7 days before departure: [per agreement]
▸ Less than 72 hours: [per agreement]
▸ Same-day / no-show: 100% of charter price retained

For questions about your agreement, contact [BROKER NAME] directly.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SECTION 9 — YOUR DIRECT CONTACT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[BROKER NAME]
OSA Connect | Orange Sunshine Aviation

Phone / WhatsApp:  [NUMBER]
Email:             [EMAIL]

Available from wheels-up to landing on your trip day.
For any changes, delays, or questions — contact me directly, not the FBO.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
OSA CONNECT — CONFIDENTIAL
This document is prepared exclusively for [CLIENT NAME].
Trip Reference: [TRIP ID]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---
---

# DECISIONS NEEDED

The following items were not specified in the BOS v1 and require a decision before implementation is complete:

1. **Broker margin policy** — BOS states "typical broker margin: 10–20%." Decide on your standard margin floor and whether it varies by aircraft category or charter size. Needed for Quote DB formula accuracy.

2. **Payment split policy** — BOS gives a range (50–100% deposit). Decide: Is your default 50/50 (deposit + balance 5–7 days out), or 100% upfront? A single policy makes the booking workflow and charter agreement consistent.

3. **Charter agreement terms** — Cancellation percentages in Trip Packet Section 8 are shown as placeholders "[per agreement]" because the BOS does not specify exact percentages. These must come from your aviation lawyer's template.

4. **Google Form to CRM connection** — Decide which tool handles the form → CRM automation: Zapier, Make (formerly Integromat), or HubSpot native forms. This affects how you set up Section 3 of the intake form.

5. **Notion vs HubSpot as primary CRM** — BOS recommends HubSpot. The Notion OS built here can serve as the ops layer. Decide whether HubSpot is the deal pipeline (with Notion as ops reference) or whether Notion handles everything. This affects which automation tool you configure.

6. **Operator identity disclosure policy** — BOS says "do not expose operator identity to client." Decide whether the Trip Packet includes the operator company name or only the tail number. Currently the template uses tail # only.

7. **Trip Packet delivery format** — Decide: PDF attached to email, or formatted email body, or Notion page shared via link. This determines which tool you use to generate it (Google Docs → PDF, Notion template, or email template in HubSpot).

8. **Catering sourcing process** — BOS references "catering ordered if applicable" but does not specify who arranges it (you, the operator, or the FBO). Decide ownership before the pre-flight SOP becomes executable.
```
