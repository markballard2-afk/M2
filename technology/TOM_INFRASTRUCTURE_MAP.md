# TOM JONES — INFRASTRUCTURE & TECHNOLOGY MAP
*Infrastructure & Technology | P.A.C.E. Foundation / WNZN Power 89.1 FM*
*Formerly Architect. Tom keeps the foundation solid so everyone else can build.*

---

## MASTER TOOL STACK

### CORE OPERATIONS
| Tool | Purpose | Who Uses It | Plan/Cost |
|---|---|---|---|
| **Notion** | Operations hub, task management, docs | All agents | Team plan |
| **HubSpot** | CRM — donors, underwriters, pipeline | Terrence, Moriah, Louise, Seven | Free CRM + paid Sales Hub |
| **Gmail / Google Workspace** | Email, calendar, Drive | All agents | Google for Nonprofits (free) |
| **Slack** | Internal team communication | All agents | Free or Pro |
| **Google Calendar** | Scheduling | Kalisha, Dr. Ballard, all | Google Workspace |

### AUTOMATION
| Tool | Purpose | Who Uses It | Plan/Cost |
|---|---|---|---|
| **N8n** | Complex multi-step workflows | Jessie | Self-hosted (free) or Cloud |
| **Make.com** | Lightweight automations | Jessie | Free or Core plan |

### AI & CONTENT
| Tool | Purpose | Who Uses It | Plan/Cost |
|---|---|---|---|
| **Claude (Anthropic API)** | Strategy, content, briefing scripts | All agents | API — pay per use |
| **ElevenLabs** | Voice audio for daily briefings | Marleigh | Creator or Business plan |
| **Canva** | Visual content, graphics | Donte | Pro plan |
| **Mailchimp** | Email marketing | Donte, Moriah | Nonprofit discount available |

### RADIO & BROADCAST
| Tool | Purpose | Who Uses It | Plan/Cost |
|---|---|---|---|
| **Futuri** | Music scheduling, radio automation | Darnell | Existing contract |
| **WNZN.org** | Main website | Tom Jones, Donte | Hosting: [current provider] |

### MUSIC & DISTRIBUTION
| Tool | Purpose | Who Uses It | Plan/Cost |
|---|---|---|---|
| **The Orchard** | Music distribution (Marxan Records) | Darnell, Dr. Ballard | Revenue share |

### PAYMENTS & FINANCE
| Tool | Purpose | Who Uses It | Plan/Cost |
|---|---|---|---|
| **PayPal / Stripe** | Online donations | Tom Jones setup | Transaction fees |
| **QuickBooks** | Accounting | Dr. Ballard / accountant | Nonprofit pricing |

### STREAMING
| Tool | Purpose | Who Uses It | Plan/Cost |
|---|---|---|---|
| **PGN App** | Power Gospel Network streaming | Mark Anthony, Tom Jones | Existing platform |

### SCHEDULING & BOOKING
| Tool | Purpose | Who Uses It | Plan/Cost |
|---|---|---|---|
| **Calendly** | Appointment scheduling | Kalisha | Free or Standard |

### ANALYTICS
| Tool | Purpose | Who Uses It | Plan/Cost |
|---|---|---|---|
| **Google Analytics 4** | Website traffic | Seven, Jamie, Tom | Free |
| **Google Search Console** | SEO monitoring | Tom, Jamie | Free |
| **Google Ads** | Google Ad Grant management | Jamie | Free (Ad Grant) |

### COMMUNICATIONS
| Tool | Purpose | Who Uses It | Plan/Cost |
|---|---|---|---|
| **Twilio** | SMS alerts and follow-ups | Jessie (automation), Louise | Pay per message |
| **Zoom** | Video calls | Kalisha, all | Existing account |

---

## SYSTEM INTEGRATION MAP

```
                         WNZN.org
                         (Website)
                             |
                    Google Analytics 4
                    Google Search Console
                    Google Ad Grant ←── Jamie Ballard
                             |
                    ┌────────┴────────┐
                    |                 |
               New Email          Event Ticket
               Signups             Purchase
                    |                 |
                    └────────┬────────┘
                             |
                         Mailchimp
                        (Email Lists)
                             |
                    ┌────────┴────────┐
                    |                 |
              Listener List      Donor Segment
                    |                 |
                 Donte           Moriah/Dr. Ballard
                             
                         HubSpot CRM
                         (Central Hub)
                    ┌────────┴────────┐
              Underwriting         Donors
               Pipeline           Pipeline
                    |                 |
                Terrence           Moriah
                    |                 |
                 Louise ────────────┘
                 (Closing)
                    
                    N8n / Make.com
                   (Automation Hub)
                         |
           ┌─────────────┼─────────────┐
           |             |             |
       HubSpot      Google Cal     Notion
       triggers      triggers      tasks
           |             |             |
           └─────────────┼─────────────┘
                         |
                   Claude API
                  (AI processing)
                         |
                    ElevenLabs
                   (Audio output)
                         |
                  Daily Briefing
                  → Email + Slack
                  → Dr. Ballard
```

---

## WNZN.ORG WEBSITE REQUIREMENTS
*Tom Jones owns this. Current status: upgrade in progress.*

### Must Have (Phase 1 — Month 1)
- [ ] Site loads in < 3 seconds on mobile (Google Core Web Vitals)
- [ ] HTTPS active (SSL certificate)
- [ ] "Listen Live" button prominent on homepage
- [ ] Donation page with working PayPal/Stripe integration
- [ ] Contact form functional
- [ ] Privacy policy page
- [ ] About page with P.A.C.E. Foundation 501(c)(3) info and EIN
- [ ] Google Analytics 4 installed and verified
- [ ] Google Search Console verified
- [ ] No broken links
- [ ] Mobile responsive design

### Should Have (Phase 1 — Month 2)
- [ ] Events page with ticket purchasing
- [ ] Underwriter acknowledgment page (who supports WNZN Power)
- [ ] PGN app download page
- [ ] Email signup form on homepage
- [ ] Blog/news section for SEO and Google Ad Grant landing pages

### Nice to Have (Phase 2)
- [ ] Donor portal (log in, see giving history)
- [ ] Archived show content or podcast feed
- [ ] WNZN Power merchandise store

---

## SLA — SERVICE LEVEL AGREEMENTS
*Tom Jones's response commitments.*

| Issue Type | Response Time | Resolution Target |
|---|---|---|
| Website completely down | 15 minutes | 2 hours |
| Donation page broken | 30 minutes | 4 hours |
| Email/calendar down | 1 hour | Same business day |
| Automation failure | 2 hours | Same business day |
| Non-critical bug | Next business day | 3 business days |
| New feature request | Reviewed weekly | Scheduled sprint |

---

## SECURITY RULES
*Bishop Hank enforces. Tom Jones implements.*

1. **All API keys** stored in a secrets manager (never in Notion, never in code files, never in email)
2. **All financial data** stays in HubSpot and QuickBooks — not exported to spreadsheets unless actively needed and then deleted after
3. **Google Workspace accounts** require 2-factor authentication for all users
4. **WNZN.org admin access** limited to Tom Jones + Dr. Ballard only
5. **HubSpot admin access** limited to Tom Jones + Papa Ballard
6. **N8n / Make.com access** limited to Jessie + Tom Jones
7. **No agent shares login credentials** via email, Slack, or text
8. **Annual password rotation** for all shared accounts
9. **Google Drive permissions audited quarterly** — remove access for anyone no longer active
10. **Backup** of WNZN.org weekly, Notion export monthly

---

## WHAT TOM JONES NEVER DOES

- Grants system access to anyone without Dr. Ballard or Papa Ballard approval
- Pushes code changes to WNZN.org in production without testing on a staging environment first
- Makes changes to FCC-related broadcast systems without Terrence and Bishop Hank review
- Ignores a security alert, no matter how minor it looks

---

## ONBOARDING ANY NEW TOOL

Before adding any new tool to the stack, Tom Jones answers:
1. Does it integrate with N8n or Make.com?
2. Does it require access to financial or donor data? (Security review required)
3. Is there a nonprofit discount available?
4. Who owns the account and the data if we stop using it?
5. Has Dr. Ballard or Papa Ballard approved the cost?

---

*Updated: June 2026 | Tom Jones, Infrastructure & Technology | Bishop Hank Ballard, security review*
