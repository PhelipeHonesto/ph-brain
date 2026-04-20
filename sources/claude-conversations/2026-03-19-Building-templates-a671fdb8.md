---
title: Building templates
created: 2026-03-19T17:31:07.538186Z
updated: 2026-03-19T21:19:18.317966Z
uuid: a671fdb8-7c32-42d3-8650-51b83bd85e76
source: claude-conversation
type: source
message_count: 28
---

# Building templates

## Phelipe

Hello.
ready to build templates?

---

## Claude

Phelipe, ready.

Before we start writing templates, let's get the order right. The daily note template is the one you will touch every single day, so it should be first. But it depends on a few decisions about how your days actually work.

Let me ask the key questions upfront so we can build it in one pass.
```
This block is not supported on your current device yet.
```

Once you answer these, I will build the full daily note template with the Templater syntax, explain each piece, and give you the exact steps to wire it up with Calendar + Periodic Notes so it auto-creates when you click a date.

---

## Phelipe

Q: What does your typical day start with when you open Obsidian?
A: No routine yet, that's what I need

Q: How do you want to handle flying days vs. OSA days?
A: Not sure yet, show me options

Q: Which sections feel essential in a daily note? (Select all that apply)
A: Schedule/time blocks, End-of-day reflection, Top 3 priorities, Inbox/quick capture area

---

## Claude

Good. You picked all four sections, which tells me you want the daily note to be your full cockpit for the day. That is the right call. We will keep it tight so it does not feel heavy.

Now let me show you the two real options for handling flying days vs. OSA days, because this shapes the template.

**Option A: One template, tag the day type.** You get one daily note template. At the top there is a `day-type` property you set to `flying`, `osa`, or `mixed`. The sections are always the same. On flying days, your Top 3 will just be simpler (maybe one OSA task you can do on a layover). This is lean, no friction, and you never have to think about which template to pick.

**Option B: Conditional sections with Templater.** One template, but Templater prompts you when the note is created: "What kind of day?" Based on your answer, it renders different sections. Flying days get a stripped-down version. OSA days get the full workspace. This is clever but adds complexity, and if your day type changes mid-day (you get released from a trip, or a trip gets added), the note is already rendered wrong.

My recommendation is Option A. One template. Tag the day type manually. The sections stay the same because even on flying days you still have priorities, you still capture thoughts, and you still reflect. The content changes, not the structure. Simpler to build, simpler to maintain, and the `day-type` property lets Dataview filter later if you ever want to see patterns like "what did I accomplish on flying days vs. OSA days."
```
This block is not supported on your current device yet.
```

Then I will build the full template file and walk you through wiring it up.

---

## Phelipe

Q: Which approach for flying vs. OSA days?
A: Option A: One template, tag the day type

---

## Claude

Good call. Let me build it.

Here is what the daily note template does and why each piece is there.

**YAML frontmatter** at the top gives you structured properties that Dataview can query later. `day-type` is the one you set manually each morning. `created` auto-fills with today's date via Templater.

**Day Theme** is a one-liner you write to set intention. Not a paragraph. Something like "Close the NetJets lead" or "Recover, light admin only." This is your forcing function against hyperfocus drift.

**Top 3** keeps you honest. Three things. Not five, not ten. If you finish all three, great, pull from your task list. But these three are the contract with yourself for the day.

**Schedule** is time blocks, not a full calendar mirror. Just enough to know where the hard edges are (sim time, a call, deadlines). On flying days this might just say your report time and legs.

**Quick Capture** is your inbox inside the daily note. Anything that pops into your head goes here so it does not derail you. You process these into `00-inbox` or directly into the right place during your end-of-day reflection or weekly review.

**End of Day** is three quick prompts. What got done, what did not, and one thing to carry forward. This feeds directly into your weekly review.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

That is the template file. Save it to your vault at `_templates/daily-note.md`.

Now the wiring. To make this auto-create when you click a date in the Calendar plugin:

1. Open Settings > Periodic Notes.
2. Under **Daily Notes**, turn it on.
3. Set **Format** to `YYYY-MM-DD` (this names your file like `2026-03-19`).
4. Set **Daily Note Folder** to `01-daily`.
5. Set **Template** to `_templates/daily-note.md`.

Then open Settings > Templater and make sure **Template Folder Location** is set to `_templates`. Also turn on **Trigger Templater on new file creation** so the `<% %>` codes actually execute when the note is created.

After that, click any date on the Calendar sidebar and your daily note will appear, pre-filled with today's date and the full structure. You fill in `day-type` (flying, osa, or mixed), write your day theme, set your Top 3, and you are running.

Want to test it now, or move on to the weekly review template next?

---

## Phelipe

this is just the daily notes right ? what re brewing for other tempaltes?

---

## Claude

Good question. Here is the full template set I have in mind, roughly in the order I would build them.

**Core rhythm templates** (these drive your daily and weekly system):
1. **Daily Note** -- done, you have it
2. **Weekly Review** -- structured reflection, inbox-to-zero processing, goal check against your 2026 targets
3. **Monthly Review** -- lighter than weekly, just a rollup of what moved and what stalled (could live inside the weekly review as a quarterly prompt instead, we will decide)

**OSA Connect templates** (these are your CRM and deal tracking):
4. **Customer** -- a person or company who needs a charter, with contact info, trip history, status, and notes
5. **Operator** -- a charter operator you broker through, with fleet info, pricing notes, reliability rating, relationship status
6. **Trip** -- a specific charter request or booking, linking a customer to an operator with dates, route, aircraft, price, and status

**OSA brand templates:**
7. **Loud Hawk Edition** -- a single newsletter issue, with topic, draft status, publish date, and links to related content
8. **Content Idea** -- quick capture for blog posts, social posts, newsletter topics, video ideas across any OSA brand
9. **Milestone** -- a business milestone worth recording (first booking, LLC formation, first revenue), feeds into your story over time

**People and reference:**
10. **Person** -- anyone in your network, with context on how you know them, last contact, and what matters to them
11. **Meeting Note** -- capture from any call or meeting, linked to the person or company

That is 11 templates total. Some might merge or get cut as we build. For example, if Meeting Note feels redundant with Quick Capture in the daily note, we drop it. The principle is start lean, add when triggered.
```
This block is not supported on your current device yet.
```

---

## Phelipe

Q: What do you want to build next?
A: Let me pick from the full list

---

## Claude

```
This block is not supported on your current device yet.
```

Pick everything you want now and I will build them in one run. Anything you skip we can always add later.

---

## Phelipe

[User denied question request]

---

## Claude

No problem. Just tell me which ones you want and I will build them.

---

## Phelipe

can we scalpe the web to see what people do. high productivity people

---

## Claude

```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Good research haul. Here is what the high-productivity Obsidian crowd is actually doing, distilled into what matters for your setup.

**Daily notes: the patterns that stick.** The best daily note systems evolve over months of small changes, not big redesigns. The people who keep the habit share a few traits: they use frontmatter properties for things they want to query later (energy level, day type, focus area), they keep the structure short enough to fill in under 2 minutes, and they treat the daily note as a launchpad rather than a journal. One popular approach tracks energy level (1-5) and focus area (Work, Wellness, Growth) as frontmatter properties, then uses Dataview in the weekly note to auto-build a table of the whole week. That is smart and we should steal it. I would add `energy` and `focus` to your daily note frontmatter so your weekly review can pull a table automatically.

**Weekly reviews: what works.** The most effective weekly reviews use Dataview to automatically pull data from the daily notes, showing a table of the week's energy, ratings, and summaries so the review starts pre-populated. This removes the friction of manually looking back. The people who stick with weekly reviews also keep a short free-write summary that feeds up into monthly reviews. The strongest systems cascade goals downward: yearly goals inform quarterly, quarterly informs monthly, monthly informs weekly, weekly informs daily. You already have this instinct with your 2026 Goals note. We just need to formalize the link.

**CRM in Obsidian: what solopreneurs do.** The best Obsidian CRM setups separate people, companies, and meetings into their own folders, then use Dataview queries to roll everything up on a customer page. One freelancer uses the Obsidian Projects plugin (or the new Bases core feature) to create a Kanban sales funnel view from the same frontmatter data, giving both a table view and a pipeline view. For OSA Connect, this maps perfectly: Customer, Operator, and Trip templates each get a `status` property in frontmatter, and Dataview (or Kanban) gives you a pipeline view.

**What I would add to your template set based on this research:**

Adding `energy` (1-5) and `focus` (osa/flying/personal) properties to the daily note frontmatter. This costs you 2 seconds each morning and gives your weekly review a Dataview table for free.

Adding a `week-summary` property to the weekly review so monthly/quarterly rollups can pull it automatically.

Using inline Dataview fields in the CRM templates (like `status::` and `next-action::`) so you can query your pipeline without leaving Obsidian.

None of this changes the template list. It just makes each template a little smarter. Want me to update the daily note with those two new properties and then start building the next templates? Or pick which ones you want first.

---

## Phelipe

lets put a pin on the CRM for now. lets focus on daily-notes and week-summary for now

---

## Claude

Good. Let me update the daily note with the two new frontmatter properties, then build the weekly review. Let me start by looking at what we already have.
```
This block is not supported on your current device yet.
```

Here is what changes on the daily note and why.

**`energy`** is a 1-5 number you set in the morning (or adjust at end of day). It takes one second. Over weeks, Dataview can show you patterns: are you always drained on flying days? Do your best OSA work days land when energy is 4+? You cannot see these patterns without the data.

**`focus`** replaces the more vague `day-type`. Same idea, but the values are clearer: `osa`, `flying`, `mixed`, or `personal`. This is what the weekly review will group by.

**`day-summary`** is a one-liner you write during End of Day. It feeds directly into the weekly review's auto-generated table. Without this, the weekly review has nothing to pull.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Now the weekly review. Here is the thinking behind it.

The weekly review does three jobs: look back (what happened), process (clear the decks), and look forward (set next week up). The Dataview table at the top auto-populates from your daily notes so you do not have to remember anything. You just read the table and reflect.

The `week-summary` property in frontmatter is a one-liner that cascades up. When you eventually do a monthly or quarterly check, Dataview can pull all your week summaries into a table and you get a birds-eye view of the whole month in seconds.

The inbox processing section is your forcing function for Design Principle 5: process inbox to zero weekly.

The "Carry Forward" section is where undone tasks and open loops from the daily notes land. This is where next week's Top 3s get seeded.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Both files are ready. Here is what to do with them.

**Daily note** (updated): Save to `_templates/daily-note.md`, replacing the old version. Your Periodic Notes config from before still works, no changes needed there.

**Weekly review** (new): Save to `_templates/weekly-review.md`. Then wire it up in Settings > Periodic Notes:
- Turn on **Weekly Notes**
- Set **Format** to `gggg-[W]ww` (this names files like `2026-W12`)
- Set **Weekly Note Folder** to `02-weekly`
- Set **Template** to `_templates/weekly-review.md`

After that, clicking a week number in the Calendar sidebar creates your weekly review, pre-populated with the Dataview table pulling from that week's daily notes.

**How the two connect:** Each morning you fill in `focus`, `energy`, and your Top 3. Each evening you write `day-summary` and fill in End of Day. On your review day (pick a consistent one, Friday or Sunday work best), you open the weekly note. The Dataview table is already there showing your whole week. You read it, reflect, process inbox, check goals, and set up next week. The whole review should take 15-20 minutes.

One note on the Dataview query: it matches daily notes to the weekly note by comparing the `created` date's week number to the weekly note's filename. For this to work, your daily note filenames need to follow the `YYYY-MM-DD` format, which you already have configured.

Want to do a dry run where you fill in a sample daily note and I walk you through how the weekly review looks when it pulls the data?

---

## Phelipe

downloaded how to set up ?

---

## Claude

Both files go into your `_templates` folder in the vault.

**Daily note** (updated version): drop `daily-note.md` into `_templates/`, replacing the one you saved earlier. Your Periodic Notes settings from before still apply, nothing to change.

**Weekly review** (new): drop `weekly-review.md` into `_templates/`. Then open Settings > Periodic Notes and configure weekly notes:

- Turn on **Weekly Notes**
- **Format:** `gggg-[W]ww`
- **Weekly Note Folder:** `02-weekly`
- **Template:** `_templates/weekly-review.md`

After that, click any week number on the left edge of the Calendar sidebar and your weekly review will auto-create with the Dataview table ready to pull from that week's daily notes.

Let me know once both are in place and we can do a test run.

---

## Phelipe

i havend done any periodic settings

---

## Claude

Got it. Let's do all of it now. Open Obsidian Settings (gear icon, bottom left).

**Step 1: Periodic Notes plugin**

Go to **Community Plugins** on the left sidebar. Find **Periodic Notes** in your installed list and make sure it is toggled on. Then click the gear icon next to it to open its settings.

**Step 2: Configure Daily Notes**

Inside Periodic Notes settings, under **Daily Notes**:
- Toggle it **on**
- **Format:** `YYYY-MM-DD`
- **Daily Note Folder:** `01-daily`
- **Template:** `_templates/daily-note.md`

**Step 3: Configure Weekly Notes**

Still inside Periodic Notes settings, under **Weekly Notes**:
- Toggle it **on**
- **Format:** `gggg-[W]ww`
- **Weekly Note Folder:** `02-weekly`
- **Template:** `_templates/weekly-review.md`

**Step 4: Templater settings**

Go back to the main Settings sidebar. Find **Templater** under Community Plugins and click its gear icon.
- Set **Template Folder Location** to `_templates`
- Turn on **Trigger Templater on new file creation**

This is what makes the `<% %>` codes in your templates actually execute when a note is created.

**Step 5: Disable core Daily Notes plugin**

Go to **Core Plugins** in Settings. Find **Daily notes** (the built-in one) and toggle it **off**. Periodic Notes replaces it. Having both on creates conflicts.

**Step 6: Test**

Click a date on the Calendar sidebar. Your daily note should appear in `01-daily/` with today's date, the frontmatter filled in, and the full template rendered. Then click a week number on the left edge of the Calendar. Your weekly review should appear in `02-weekly/`.

Walk through those steps and let me know what you see.

---

## Phelipe

is falling

---

## Claude

I can see the error in the top right: "Failed to load plugin 'periodic-notes'." This happens sometimes with Periodic Notes, especially on older versions. Yours is showing version 0.0.17 which is quite old.

Try this fix:

1. Close the Settings window
2. Quit Obsidian completely (Cmd+Q, not just close the window)
3. Reopen Obsidian
4. Go back to Settings > Community Plugins
5. Toggle **Periodic Notes** off, then back on

If it still fails after that, the plugin may need a reinstall:

1. Click the trash icon next to Periodic Notes to uninstall it
2. Click the folder icon (top right of the Installed Plugins section) to browse community plugins
3. Search for **Periodic Notes** and install it fresh
4. Toggle it on

Once it loads without that error, you should see it appear in the left sidebar under the plugin list with a gear icon you can click to configure. Let me know what happens.

---

## Phelipe

plugins desapiered?

---

## Claude

Looks like the uninstall of Periodic Notes may have cleared all your community plugins. It says "You currently have 0 plugins installed" and the Installed Plugins section is empty. No worries, we just need to reinstall them.

Click the **Browse** button and install these one at a time, toggling each one on after installing:

1. **Templater** (by SilentVoid)
2. **Dataview** (by Michael Brenan)
3. **Periodic Notes** (by Liam Cain)
4. **Calendar** (by Liam Cain)
5. **Tasks** (by Clare Macrae)
6. **Kanban** (by mgmeyers)
7. **Minimal Theme Settings** (by @kepano)

After all seven are installed and toggled on, take a screenshot and send it over so I can confirm everything is loaded before we configure.

---

## Claude

Good, all seven are installed. But I can see that only **Periodic Notes** and **Minimal Theme Settings** are toggled on (purple). The rest are off. Toggle these on:

- **Dataview**
- **Kanban**
- **Tasks**
- **Templater**
- **Calendar**

Just click each toggle so they all turn purple. No error on Periodic Notes this time, which is good. Once all seven are on, we will configure them.

---

## Phelipe

all on how to set

---

## Claude

Good. Now let's configure. Go through these in order.

**1. Templater**

Click the gear icon next to Templater in the plugin list.
- **Template Folder Location:** `_templates`
- **Trigger Templater on new file creation:** toggle **on**

**2. Periodic Notes**

Click the gear icon next to Periodic Notes.

Under **Daily Notes:**
- Toggle **on**
- **Format:** `YYYY-MM-DD`
- **Daily Note Folder:** `01-daily`
- **Template:** `_templates/daily-note.md`

Under **Weekly Notes:**
- Toggle **on**
- **Format:** `gggg-[W]ww`
- **Weekly Note Folder:** `02-weekly`
- **Template:** `_templates/weekly-review.md`

**3. Core Daily Notes plugin**

Go to **Core plugins** in the left sidebar. Find **Daily notes** and toggle it **off**. Periodic Notes replaces it. Having both on causes conflicts.

**4. Dataview, Calendar, Tasks, Kanban**

These work out of the box with default settings. No configuration needed right now.

Once you have done steps 1-3, click a date on the Calendar sidebar to test. You should see a new note appear in `01-daily/` with the full template rendered. Send a screenshot of what you get.

---
