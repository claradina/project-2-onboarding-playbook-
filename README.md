# 🌿 Onboarding Playbook Generator + Health Check

> An AI-powered tool that generates personalized 90-day customer onboarding plans **and monitors their execution in real time** — identifying risks before they become churn.

**Live demo:** open `onboarding_playbook_v2.html` in any browser · **API:** Gemini 2.5 Flash (free tier) · **No backend required**

---

## What it does

### Tab 1 — Playbook generator
Fill in a client profile and get a complete 90-day onboarding plan in seconds:
- 4 structured phases (Days 1–7, 8–30, 31–60, 61–90)
- Milestones per phase with ownership (CS / Client / Tech)
- 4 success KPIs tailored to the client's goal
- 3 follow-up email drafts at key onboarding moments
- SQL schema for storing milestones in a real CRM

### Tab 2 — Health check *(the step beyond)*
After 30, 60 or 90 days, come back and mark what actually happened:
- Check each milestone as Done, Delayed, Not done, or Pending
- Add CS notes per milestone
- Click "Run AI diagnosis" — Gemini analyzes the gaps and generates:
  - A **health score** from 0–100
  - A risk level: Healthy / At risk / Critical
  - **Flagged issues** in red (urgent), amber (attention), and green (on track)
  - A **recommended action** for each problem

---

## Why this matters in CS

Generating a plan is easy. The hard part is knowing *when a client is quietly going off track* — before they cancel, before they complain, before the relationship breaks.

This tool turns a static onboarding plan into a living document. Each flagged milestone becomes an opportunity for a proactive call, a personalized email, or an internal escalation. The health score gives you a number you can defend in a team meeting or a QBR.

> A CS team that waits for the client to reach out is reactive.  
> A CS team that detects risk before the client notices is strategic.

This is the difference this tool is built to demonstrate.

---

## This is a starting point — not a finished product

The tool is intentionally generic so anyone can run it. But its real value comes from **customization to a specific company and client context.**

Here is what would change for a real deployment:

### The prompt (the AI's "brain")
The current prompt uses generic solar onboarding logic. In a real company, you would replace it with:
- The company's actual process steps, in order, with real timelines
- The internal names for each role (e.g. "Installation Coordinator" instead of "Tech")
- Country-specific regulatory steps (e.g. Netzbetreiber pre-registration for Germany, DNO applications for the UK)
- The most common failure points that the company has seen before — so the AI knows what to watch for

**Example — Enpal Germany:**
```
Process: Contract signed → Technical survey (5 business days) → 
Netzbetreiber pre-registration (4–8 weeks) → Installation → 
Grid registration confirmation → First billing on the 15th of the following month.

Common failure points: Netzbetreiber confirmation delayed beyond day 25, 
CS first contact not made within 8 days of installation.
```

**Example — SaaS company:**
```
Process: Account created → Kickoff call (day 3) → 
Feature activation checklist (days 5–14) → 
First value moment logged (day 21) → QBR scheduled (day 60).

Common failure points: No login after day 7, key feature not adopted by day 30.
```

### The form fields
The current form has generic options (installation types, countries, company sizes). A real company would replace these with their actual product lines, markets, and customer segments — making the playbook feel internal, not templated.

### The SQL schema
The `onboarding_milestones` table is a foundation. Real deployments would add:
- `contract_type` — to distinguish rental, purchase, or lease
- `region` — for companies operating across multiple states or countries
- `grid_status` — for energy companies tracking Netzbetreiber or DNO status
- `feature_adopted` — for SaaS companies tracking product activation
- `churn_risk_flag` — a boolean updated by the AI diagnosis, queryable in dashboards

### The health score thresholds
The current score (0–100) uses generic thresholds. A company with historical data would calibrate these: if clients with a score below 60 at day 30 churn at 3x the rate, that threshold becomes a trigger for automatic escalation — not just a colored badge.

---

## How to run it

1. Download `onboarding_playbook_v2.html`
2. Open in any browser (Chrome, Firefox, Safari — no installation needed)
3. Get a free Gemini API key at [aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey) — takes 2 minutes, no credit card
4. Paste the key in the field at the top
5. Generate a playbook → then switch to Health Check after 30 days

Your API key is sent only to Google's Gemini API. Nothing is stored anywhere.

---

## Tech stack

| Layer | Choice |
|---|---|
| Frontend | Vanilla HTML + CSS + JS — single file, no build step |
| AI | Gemini 2.5 Flash (free: 10 req/min, 500 req/day) |
| Backend | None — fully client-side |

---

## Let's talk

This tool is a prototype built to show how AI can turn mechanical CS tasks — writing playbooks, tracking milestones, identifying risk — into moments of strategic action.

Every indicator in the health check is an opportunity: a reason to call, a signal to escalate, a data point to bring to leadership. The goal was never to replace the CSM's judgment — it was to give them more time to use it.

If you are building a CS team and want to explore how AI can make your processes faster, your data more actionable, and your team's time better spent — **I would love to talk.**

You can reach me at [claras.azambuja@gmail.com](mailto:claras.azambuja@gmail.com) or connect on [LinkedIn](https://www.linkedin.com/in/clarasilva).

---

## Project structure

```
projeto-2-onboarding-playbook/
├── README.md
├── onboarding_playbook_gemini.html   ← v1: playbook generator only
└── onboarding_playbook_v2.html       ← v2: playbook + health check
```

*Built with curiosity, structured thinking, and a genuine belief that good CS is about connection — not just completion.*
