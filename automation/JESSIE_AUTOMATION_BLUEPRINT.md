# JESSIE — AUTOMATION BLUEPRINT
*Automation Systems | N8n + Make.com | P.A.C.E. Foundation / WNZN Power*
*Formerly Simone. Jessie builds the workflows that make the whole operation run without Dr. Ballard having to touch it.*

---

## ARCHITECTURE OVERVIEW

```
                    DR. MARK BALLARD
                          |
              CLARENCE "PAPA" BALLARD
              (Daily Operations Review)
                          |
         ┌────────────────┼────────────────┐
         │                │                │
    N8N HUB          MAKE.COM          CLAUDE API
    (complex         (lightweight      (AI content
     workflows)       automations)      & analysis)
         │                │                │
         └────────────────┼────────────────┘
                          │
              ALL CONNECTED TOOLS:
    HubSpot | Notion | Gmail | Google Calendar
    Mailchimp | Slack | ElevenLabs | GA4
    Calendly | Twilio | Google Drive
```

**Rule:** N8n handles multi-step, conditional, data-heavy workflows. Make.com handles simple triggers and lightweight sequences. Claude API handles any step that requires writing, analysis, or decision-making.

---

## WORKFLOW 1: DAILY BRIEFING COMPILATION
*Triggers at 6:00 AM and 8:30 PM every day. Output delivered by 6:30 AM and 9:00 PM.*
*Full details in `automation/BRIEFING_SYSTEM.md`*

**N8n Workflow: "Morning Briefing Builder"**
```
Trigger: Schedule (6:00 AM daily)
→ Step 1: Pull HubSpot data (revenue pipeline, open deals, tasks due today)
→ Step 2: Pull Google Analytics (yesterday's website traffic, top pages)
→ Step 3: Pull Mailchimp (last email open rate, unsubscribes)
→ Step 4: Pull Google Calendar (today's appointments for Dr. Ballard)
→ Step 5: Pull Notion (open tasks marked urgent)
→ Step 6: Send all data to Claude API → generate briefing script
→ Step 7: Send script to ElevenLabs → generate audio file
→ Step 8: Email audio file + text summary to Dr. Ballard
→ Step 9: Post text summary to designated Slack channel (#morning-briefing)
```

---

## WORKFLOW 2: UNDERWRITING RENEWAL AUTOMATION
*Terrence's safety net. No underwriter falls off without a call.*

**Make.com Scenario: "Underwriting Renewal Alert"**
```
Trigger: HubSpot deal field "Contract End Date" = 90 days from today
→ Create task in HubSpot assigned to Terrence: "Renewal call needed"
→ Send Terrence email: "[Business Name] contract expires in 90 days. 
   Call this week."

At 60 days:
→ Send Terrence second reminder + upgrade talking points
→ Add "Renewal - 60 days" tag to HubSpot deal

At 30 days:
→ Louise triggered: send renewal proposal email to underwriter
→ Create task for Terrence: "Confirm renewal receipt"

At 7 days:
→ Escalate to Papa Ballard if still not renewed
→ Flag in morning briefing
```

**HubSpot Deal Stages for Underwriting:**
- Prospect → Contacted → Proposal Sent → Negotiating → Active Partner → Renewal Due → Renewed / Lapsed

---

## WORKFLOW 3: DONOR FOLLOW-UP SEQUENCE
*Moriah's automation. Louise handles the follow-up timing.*

**N8n Workflow: "Donor Cultivation Tracker"**
```
Trigger: HubSpot contact tag changes to "Touch 1 Complete"
→ Wait 7 days
→ Send Moriah task: "Schedule station tour or coffee for [Name]"
→ Wait for Moriah to mark "Touch 2 Complete"

On "Touch 2 Complete":
→ Send impact document email to prospect (pre-written template)
→ Create HubSpot task: "Touch 3 - Impact doc sent. Follow up in 5 days."
→ Wait 5 days → send Moriah reminder

On "Touch 4 Complete" (event attended):
→ Wait 3 days → trigger handwritten note reminder to Dr. Ballard via email
→ Create Notion task: "Send handwritten note to [Name]"

On "Touch 5 Complete" (note sent):
→ Wait 14 days → send Moriah "ASK READY" alert
→ Create HubSpot task for Dr. Ballard: "Ask conversation with [Name]"

On gift received (HubSpot deal marked "Won"):
→ Trigger acknowledgment letter workflow (see Workflow 4)
→ Tag contact as "Active Donor"
→ Add to Mailchimp "Donors" segment
→ Notify Seven Townsel with gift amount and donor name
```

---

## WORKFLOW 4: GIFT ACKNOWLEDGMENT & STEWARDSHIP
*Runs automatically the moment a gift is logged in HubSpot.*

**Make.com Scenario: "Donor Thank You Chain"**
```
Trigger: HubSpot deal stage changes to "Gift Received"
→ Immediately: Create task for Dr. Ballard in Notion: 
  "CALL [Name] TODAY - gift received: $[amount]"
→ Send Moriah email alert with donor name and amount
→ Wait 1 hour → send Dr. Ballard SMS via Twilio: 
  "Reminder: Call [Name] today. Gift received: $[amount]"

Within 48 hours:
→ Generate acknowledgment letter via Claude API (fill template with 
   donor name, amount, date, EIN)
→ Email to Moriah for printing and mailing
→ Log in HubSpot: "Ack letter sent [date]"

At 30 days:
→ Send Moriah task: "Send 30-day impact update to [Name]"

At 90 days:
→ Generate impact update email via Claude API
→ Send to Moriah for review → she approves → sends to donor

At 335 days (30 days before 1-year mark):
→ Send Moriah alert: "Renewal ask due in 30 days for [Name]"
→ Add to Dr. Ballard's call list
```

---

## WORKFLOW 5: NEW LISTENER WELCOME SEQUENCE
*Anyone who signs up on WNZN.org or the PGN app gets this.*

**Make.com Scenario: "New Listener Welcome"**
```
Trigger: New email signup on WNZN.org (form submission)
→ Immediately: Add to Mailchimp "Listeners" audience
→ Send Welcome Email (pre-built template):
  Subject: "Welcome to WNZN Power — Lorain, Ohio's gospel home"
  Body: Quick intro, listen live link, PGN app download, social links,
        soft donation ask ("If WNZN Power ever moves you, consider giving")

At Day 7:
→ Send "Did you know?" email: feature about PGN app, one artist spotlight

At Day 30:
→ Add to monthly newsletter segment
→ If no engagement (no opens): move to re-engagement sequence
```

**Make.com Scenario: "PGN App New User"**
```
Trigger: New PGN app registration
→ Send in-app welcome message
→ Add to Mailchimp "PGN Users" segment
→ After 7 days: send "upgrade to premium" soft pitch email
→ After 30 days: if still free tier, send Louise-triggered upgrade offer
```

---

## WORKFLOW 6: EVENT TICKET FLOW
*Spring Gospel Jam and all events.*

**Make.com Scenario: "Event Registration Flow"**
```
Trigger: Ticket purchase on WNZN.org/events
→ Send confirmation email with event details, directions, what to expect
→ Add to Mailchimp "Spring Gospel Jam" segment
→ Add to HubSpot contact with tag "Event Attendee [Year]"
→ At 7 days before event: send reminder email with parking, doors open time
→ At 1 day before: send "See you tomorrow" email
→ At 3 days after event: send thank-you email with photos (when available)
   + soft ask: "Want to support what made tonight possible?" + donate link
```

---

## WORKFLOW 7: SOCIAL MEDIA CONTENT PIPELINE
*Donte drafts. Barbara/Nana approves. Jessie schedules.*

**N8n Workflow: "Content Approval & Schedule"**
```
Trigger: Donte adds new post to Notion "Content Queue" database
→ Send notification to Barbara/Nana: "New post needs voice review"
→ Barbara/Nana marks "Approved" or "Needs Edit" in Notion
→ If Approved: post added to social scheduler queue
→ If Needs Edit: send back to Donte with notes
→ After post publishes: log in Notion "Content Published" database
→ At end of week: compile engagement stats from social platforms
   → send to Seven Townsel for monthly report
```

---

## WORKFLOW 8: BISHOP HANK MONITORING
*Automated security and compliance alerts.*

**Make.com Scenario: "Daily Compliance Check"**
```
Trigger: Daily at 6:15 AM (runs before morning briefing)
→ Check WNZN.org uptime status (via monitoring service)
→ Check Google Ad Grant CTR (if below 5%, create urgent alert)
→ Check for mentions of "WNZN Power" or "Dr. Mark Ballard" online
   (via Google Alerts webhook)
→ Compile into Bishop Hank's briefing section:
  - System status: [UP/DOWN/WARNING]
  - Brand mentions: [count and sentiment]
  - Compliance flags: [any issues]
→ Feed into 6:30 AM morning briefing
```

**Make.com Scenario: "Revenue Anomaly Alert"**
```
Trigger: Daily HubSpot revenue pull
→ Compare to same day previous month
→ If more than 20% below last month's pace → alert Papa Ballard immediately
→ Add red flag to morning briefing
→ Create task: "Revenue review needed"
```

---

## WORKFLOW 9: HUBSPOT CRM HYGIENE
*Jessie keeps the data clean so Seven can trust the numbers.*

**Make.com Scenario: "Weekly CRM Cleanup"**
```
Trigger: Every Monday at 7:00 AM
→ Find HubSpot contacts with no activity in 90 days → tag "Needs Review"
→ Find deals stuck in same stage for 30+ days → create Terrence/Moriah task
→ Find tasks past due → escalate to assigned agent via email
→ Send weekly pipeline summary to Papa Ballard
```

---

## SETUP PRIORITY ORDER
*Tom Jones handles technical setup. Jessie configures the workflows.*

| Priority | Workflow | Est. Build Time | Impact |
|---|---|---|---|
| 1 | Underwriting Renewal (Workflow 2) | 2 hours | Immediate — stops revenue leakage |
| 2 | Gift Acknowledgment (Workflow 4) | 2 hours | Immediate — required for donor relations |
| 3 | Daily Briefing (Workflow 1) | 4 hours | High — Dr. Ballard's daily command center |
| 4 | Donor Follow-up (Workflow 3) | 3 hours | High — Moriah's backbone |
| 5 | New Listener Welcome (Workflow 5) | 1 hour | Medium — growth engine |
| 6 | Event Ticket Flow (Workflow 6) | 2 hours | Medium — needed before next event |
| 7 | Bishop Hank Monitoring (Workflow 8) | 3 hours | Medium — risk management |
| 8 | Content Pipeline (Workflow 7) | 2 hours | Medium — Donte's structure |
| 9 | CRM Hygiene (Workflow 9) | 1 hour | Low — maintenance |

---

## API KEYS & CONNECTIONS NEEDED
*Tom Jones secures these. Jessie connects them.*

| Tool | Connection Type | Who Manages |
|---|---|---|
| HubSpot | API Key | Tom Jones |
| Mailchimp | API Key | Tom Jones |
| Google Analytics 4 | Service Account | Tom Jones |
| Google Calendar | OAuth | Tom Jones |
| Gmail | OAuth | Tom Jones |
| ElevenLabs | API Key | Tom Jones |
| Claude API (Anthropic) | API Key | Tom Jones |
| Twilio (SMS) | API Key + Phone # | Tom Jones |
| Notion | Integration Token | Tom Jones |
| Slack | Webhook URL | Tom Jones |
| Calendly | API Key | Tom Jones |

*All API keys stored securely — never in code files, never in Notion. Tom Jones manages the secrets vault.*

---

*Updated: June 2026 | Jessie, Automation Systems | Tom Jones, Infrastructure review*
