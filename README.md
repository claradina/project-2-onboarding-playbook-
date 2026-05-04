# 🌿 Onboarding Playbook Generator

> An AI-powered tool that generates personalized 90-day customer onboarding plans for solar energy companies — built to demonstrate prompt engineering applied to Customer Success workflows.

**Live demo:** open `onboarding_playbook_gemini.html` in any browser · **API:** Gemini 1.5 Flash (free tier) · **No backend required**

---

## What it does

Fill in a client profile — installation type, country, company size, and main goal — and the tool calls the Gemini API to generate a complete, tailored onboarding playbook in seconds:

- **4 onboarding phases** covering Days 1–7, 8–30, 31–60, and 61–90
- **Milestones per phase** with ownership assigned (CS / Client / Tech)
- **4 success KPIs** relevant to solar onboarding
- **3 follow-up email drafts** at key moments in the journey
- **SQL schema** — a documented `onboarding_milestones` table showing how this data would live in a real CRM

Supports English, German, and Portuguese output. References country-specific details like Netzbetreiber registration for Germany.

---

## Why this project exists

Onboarding planning is one of the most time-consuming and repetitive tasks in Customer Success. A CSM managing multiple installations across different customer profiles has to manually recreate similar plans again and again.

This tool automates the starting point — giving the CS team a structured, personalized playbook in under 10 seconds, which they can then refine and own.

It was built as part of a CS portfolio to demonstrate:
- Practical application of AI to real CS workflows
- Prompt engineering for structured JSON output
- Understanding of what good onboarding looks like in the solar/energy sector
- SQL thinking applied to CS data structures

---

## Tech stack

| Layer | Choice | Why |
|---|---|---|
| Frontend | Vanilla HTML + CSS + JS | No build step — works as a single file, easy to share |
| AI | Gemini 1.5 Flash API | Free tier (1,500 req/day), no credit card required |
| Fonts | Syne + DM Sans (Google Fonts) | Clean, professional feel |
| Backend | None | All logic runs client-side |

---

## How to run it

**Option 1 — Open locally (easiest)**

1. Download `onboarding_playbook_gemini.html`
2. Open it in any browser (Chrome, Firefox, Safari)
3. Get a free Gemini API key at [aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey)
4. Paste the key in the field at the top and generate

**Option 2 — GitHub Pages**

1. Fork this repo
2. Go to Settings → Pages → Source: `main` branch
3. Access at `https://yourusername.github.io/repo-name/onboarding_playbook_gemini.html`

> Your API key is never stored or sent anywhere except directly to Google's Gemini API.

---

## SQL schema highlight

The SQL tab inside the tool shows a production-ready schema for storing onboarding milestones in a CRM database:

```sql
CREATE TABLE onboarding_milestones (
  id              UUID          PRIMARY KEY DEFAULT gen_random_uuid(),
  customer_id     UUID          NOT NULL REFERENCES customers(id),
  phase           INT           NOT NULL CHECK (phase BETWEEN 1 AND 4),
  milestone_text  TEXT          NOT NULL,
  owner           VARCHAR(50),  -- 'CS', 'Client', 'Tech'
  status          VARCHAR(20)   DEFAULT 'pending',
  due_day         INT,
  completed_at    TIMESTAMPTZ,
  ...
);
```

It also includes a `v_onboarding_health` view that calculates a completion percentage per customer — the kind of metric a CS team would track in a dashboard to identify at-risk accounts.

---

## Project context

This is **Project 2** of a CS + AI portfolio built by [Clara Silva](https://www.linkedin.com/in/clarasilva), a Customer Success professional with experience in solar energy operations at Enpal (Germany).

The portfolio demonstrates how AI tools can accelerate CS workflows — from onboarding documentation to customer communication — without replacing the human judgment that makes CS effective.

→ [View Project 1 — Customer Health Score Dashboard](#) *(link coming soon)*

---

## Prompt engineering note

The core of this tool is a structured prompt that constrains Gemini to return a valid JSON object with a specific schema. This avoids the common problem of LLMs returning markdown prose when you need machine-readable data.

Key techniques used:
- Explicit schema definition in the prompt
- Hard constraints on output format ("Return ONLY the JSON object")
- Country and context injection for personalization
- Graceful JSON parsing with regex fallback for edge cases

---

*Built with curiosity, structured thinking, and a lot of solar energy knowledge.*
