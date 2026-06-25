# WNZN POWER DAILY BRIEFING SYSTEM
*6:30 AM Rise & Run | 9:00 PM Close of Day*
*Marleigh Ballard (audio production) + Jessie (automation) + ElevenLabs (voice)*

---

## HOW IT WORKS

Every morning at 6:30 AM and every evening at 9:00 PM, Dr. Ballard receives:
1. An **audio file** (1–3 minutes) in his own synthesized voice or a chosen voice via ElevenLabs
2. A **text summary** email with the same information
3. A **Slack message** in the private #briefings channel for quick reference

Jessie's N8n workflow pulls live data from every connected tool, sends it to Claude to generate the script, then sends the script to ElevenLabs to generate the audio. Dr. Ballard wakes up informed and ready.

---

## 6:30 AM — "RISE & RUN" BRIEFING

### CLAUDE PROMPT TEMPLATE
*N8n sends this prompt with live data filled in to generate the script.*

```
You are the WNZN Power Mission Control morning briefing system.
Generate a 90-second spoken briefing for Dr. Mark Ballard.

Voice: Warm, direct, plain-spoken. Like a trusted colleague giving a 
quick rundown over the phone. No corporate language. No filler. 
Faith-aware but not preachy.

Format: Conversational script, meant to be read aloud. Short sentences.
No bullet points in the spoken version.

DATA:
- Today's date: {date}
- Day's appointments: {calendar_events}
- Revenue pipeline: Open deals this week: {hubspot_open_deals}
  Underwriting revenue MTD: ${hubspot_underwriting_mtd}
  Donor pipeline active: {hubspot_donor_count} prospects
- Overdue tasks: {notion_overdue_tasks}
- Website traffic yesterday: {ga4_sessions} visitors
- Top source: {ga4_top_source}
- Any system alerts: {bishop_hank_alerts}
- Featured content going out today: {donte_content_today}

Generate the briefing in this structure:
1. Good morning greeting (1–2 sentences)
2. Today's schedule (what's on the calendar)
3. Revenue snapshot (what Terrence and Moriah are working)
4. One thing that needs Dr. Ballard's attention today
5. What's going out to the community today (Donte's content)
6. Close with one grounding sentence — nothing preachy, just real

Keep it under 250 words. Make it sound like a person, not a report.
```

### SAMPLE OUTPUT (what Dr. Ballard actually hears)

---

*"Good morning, Dr. Ballard. It's Tuesday, July 8th, and here's where things stand.*

*Your calendar today: You have a 10 AM call with Allen Smith at Boys & Girls Clubs, and Kalisha has the Spring Gospel Jam venue confirmation scheduled for 2 PM. That's it — a focused day.*

*On the revenue side, Terrence has three underwriting conversations this week. Northeast Ohio Health System is the one to watch — they're in the final stage. Moriah's in cultivation with eight prospects right now. Good momentum.*

*One thing that needs your attention: the Google Ad Grant application is ready for your sign-off. Jamie's been waiting two days. Takes about ten minutes — worth your time this morning.*

*Donte's got a Williams Singers spotlight going out on Facebook and Instagram at noon today. Clean post. Barbara approved it.*

*Everything's running. Go make it count."*

---

### DELIVERY
- **Audio file:** Attached to email and posted in Slack
- **Email subject:** "WNZN Power | Good Morning, Dr. Ballard — [Day, Date]"
- **Email body:** Text version of briefing + links to any items needing action
- **Slack channel:** #morning-briefing (private)

---

## 9:00 PM — "CLOSE OF DAY" BRIEFING

### CLAUDE PROMPT TEMPLATE

```
Generate a 60-second end-of-day briefing for Dr. Mark Ballard.

Voice: Slightly warmer than the morning. Wind-down energy — not slow, 
but settling. Report what happened, look ahead, close clean.

DATA:
- Revenue logged today: ${hubspot_revenue_today}
- MTD total: ${hubspot_revenue_mtd}  
- MTD goal: ${revenue_goal_mtd}
- Tasks completed today: {notion_completed_today}
- Tasks still open and overdue: {notion_overdue}
- Tomorrow's first three calendar items: {calendar_tomorrow}
- Any evening alerts from Bishop Hank: {bishop_hank_pm_alerts}
- One piece of content Donte has ready for tomorrow: {donte_tomorrow_content}

Structure:
1. Short close-of-day greeting
2. Revenue: what came in today, where MTD stands vs. goal
3. What got done / what didn't
4. Look ahead: first three things on tomorrow's calendar
5. One thing to release before sleeping — nothing to solve tonight

Keep it under 150 words. Grounded and human.
```

### SAMPLE OUTPUT

---

*"Good evening, Dr. Ballard. Here's how the day closed.*

*Revenue today: $2,400 from the Lorain Federal Credit Union underwriting renewal. Month-to-date is $18,700 against a $25,000 goal. You're on pace.*

*Terrence completed two follow-up calls. Moriah sent the impact document to the Johnson prospect. The Google Ad Grant sign-off is still open — first thing in the morning.*

*Tomorrow starts with your board prep at 8 AM, then the 10 AM Boys & Girls Clubs call. Kalisha confirmed the Spring Gospel Jam venue at Lorain County Community College — contract coming tomorrow.*

*You did good work today. Rest. The system is running."*

---

### DELIVERY
- **Audio file:** Same format as morning
- **Email subject:** "WNZN Power | Evening Report — [Date]"
- **Slack channel:** #evening-briefing (private)

---

## MARLEIGH'S VOICE SETUP
*ElevenLabs configuration for the briefing audio.*

### Recommended Voice Settings
- **Voice:** Choose from ElevenLabs library or clone a voice Dr. Ballard approves
  - Option A: A warm, authoritative male voice (like a trusted advisor)
  - Option B: Clone Dr. Ballard's own voice (ElevenLabs Professional Voice Clone — requires audio samples)
- **Stability:** 0.60 (some natural variation, not robotic)
- **Similarity Boost:** 0.80
- **Style:** 0.30 (conversational, not theatrical)
- **Speaking Rate:** Slightly slower than default (0.90)

### Audio File Format
- MP3, 128kbps
- Named: `briefing-YYYY-MM-DD-AM.mp3` or `briefing-YYYY-MM-DD-PM.mp3`
- Stored in Google Drive folder: "WNZN Power / Daily Briefings / [Year]"

---

## SETUP CHECKLIST
*Tom Jones (tech) + Jessie (workflow) + Marleigh (voice)*

- [ ] ElevenLabs account active with chosen voice configured
- [ ] Claude API key connected in N8n
- [ ] HubSpot API connected and revenue fields mapped
- [ ] Google Analytics 4 connected via service account
- [ ] Google Calendar connected via OAuth
- [ ] Notion integration token connected
- [ ] Slack webhook configured for #morning-briefing and #evening-briefing
- [ ] Gmail SMTP configured for briefing emails
- [ ] Google Drive folder created for audio file storage
- [ ] Test run completed: verify all data pulls work and audio generates correctly
- [ ] Dr. Ballard approves voice and format before going live

---

## WHAT TO DO WHEN THE BRIEFING IS WRONG
*Because it will happen sometimes.*

- **Data missing or wrong:** Jessie checks which API call failed. Tom Jones fixes the connection. Flag in Slack with @jessie.
- **Audio sounds off:** Marleigh adjusts ElevenLabs voice settings. Regenerate and resend.
- **Briefing is too long:** Edit the Claude prompt — reduce word count limit.
- **Dr. Ballard wants something added:** Update the Claude prompt template in N8n. Document the change in this file.

---

*Updated: June 2026 | Marleigh Ballard, AI Music Factory | Jessie, Automation Systems | Tom Jones, Infrastructure*
