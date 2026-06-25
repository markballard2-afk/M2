# Make.com Blueprint Import Guide
*WNZN Power Mission Control — All 9 Automation Workflows*

---

## HOW TO IMPORT A BLUEPRINT INTO MAKE.COM

1. Log in to Make.com
2. Click **Create a new scenario**
3. Click the **three dots (...)** menu in the bottom toolbar
4. Select **Import Blueprint**
5. Upload the JSON file from this folder
6. The workflow appears fully built
7. Click each module and connect your accounts (HubSpot, Gmail, etc.)
8. Set it to **Active** when ready

**That's it.** Each file below is one complete workflow.

---

## THE 9 WORKFLOWS

| File | Workflow | Priority |
|---|---|---|
| `01-daily-briefing.json` | 6:30 AM & 9 PM briefing via Claude + ElevenLabs | High |
| `02-underwriting-renewal.json` | 90/60/30 day renewal alerts for Terrence | HIGH — Build First |
| `03-donor-followup.json` | Moriah's cultivation sequence automation | High |
| `04-gift-acknowledgment.json` | Same-day thank-you chain when gift received | HIGH — Build First |
| `05-new-listener-welcome.json` | Welcome email when someone signs up on WNZN.org | Medium |
| `06-event-ticket-flow.json` | Confirmation, reminder, post-event emails | Medium |
| `07-social-media-pipeline.json` | Content approval queue (Donte → Barbara/Nana) | Medium |
| `08-bishop-hank-monitoring.json` | Daily compliance and brand monitoring | Medium |
| `09-crm-hygiene.json` | Weekly HubSpot cleanup and stuck deal alerts | Low |

---

## CREDENTIALS YOU NEED CONNECTED IN MAKE.COM

Before importing, go to **Connections** in Make.com and connect:
- [ ] HubSpot (API Key from HubSpot Settings → Integrations)
- [ ] Gmail / Google Workspace (OAuth — sign in with Google)
- [ ] Google Calendar (OAuth — same Google account)
- [ ] Notion (Integration Token from notion.so/my-integrations)
- [ ] Slack (OAuth — authorize your workspace)
- [ ] Twilio (Account SID + Auth Token from console.twilio.com)
- [ ] Mailchimp (API Key from Mailchimp Account Settings)
- [ ] HTTP module (no pre-auth needed — API keys go inside each module)

---

## USING CLAUDE (CHROME EXTENSION / COMPUTER USE) TO BUILD THESE

If you want Claude to help you configure each workflow visually:

1. Open Make.com in your browser
2. Import a blueprint file (steps above)
3. Open Claude with computer use / screen sharing enabled
4. Say: "I just imported a Make.com blueprint. Help me configure each module — I'll tell you my credentials."
5. Claude will guide you through each connection step by step

This works especially well for the HTTP modules (Claude API and ElevenLabs) which require manual configuration of API keys and request bodies.

---

## VARIABLES TO REPLACE IN EVERY WORKFLOW

Search for these placeholders and replace with your real values:

| Placeholder | Replace With |
|---|---|
| `YOUR_HUBSPOT_PIPELINE_ID` | Found in HubSpot → Settings → Sales → Deals → Pipelines |
| `YOUR_HUBSPOT_STAGE_ID_ACTIVE` | The "Active Partner" stage ID in your underwriting pipeline |
| `YOUR_NOTION_DATABASE_ID` | Found in the Notion database URL |
| `YOUR_SLACK_CHANNEL_ID` | Right-click channel in Slack → Copy link → last part of URL |
| `YOUR_ELEVENLABS_VOICE_ID` | Found in ElevenLabs → Voices → your chosen voice |
| `YOUR_ANTHROPIC_API_KEY` | From console.anthropic.com |
| `YOUR_ELEVENLABS_API_KEY` | From elevenlabs.io/app/api-keys |
| `TERRENCE_EMAIL` | Terrence's actual email address |
| `MORIAH_EMAIL` | Moriah's actual email address |
| `DR_BALLARD_EMAIL` | Dr. Ballard's email for briefings |
| `DR_BALLARD_PHONE` | E.164 format: +12165550100 |
| `PAPA_EMAIL` | Clarence's email |

---

*All workflows built for Make.com. Compatible with free and paid plans.*
*Some workflows require Operations — monitor your monthly usage.*
