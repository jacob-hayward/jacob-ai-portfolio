**Date:** 15 March 2026
**Phase:** Phase 1 — Architecture Design Decisions (Pre-Build)

**What I did:**

Mapped out the full system architecture before touching n8n. Coming from an automation background I already knew this kind of build would have distinct sections doing different jobs — you don't build it all in one workflow and hope for the best. What this session did was help me articulate and document those sections properly.

The system breaks into three separate "parts":

**1 — The Data Pipeline** (cron triggered, runs silently every 5-7 days)
Scrapes official government visa pages → strips HTML to plain text → LLM extracts only the relevant visa information → chunks and embeds → upserts into vector store. Error branch sends an alert if anything fails. Silent failures are designed out from day one.

**2 — The Conversation Flow** (triggers on every user message)
Webhook receives message from Typebot → guardrail check (in-scope or not?) → fetch chat history from Redis → AI orchestrator with tools attached → response back to Typebot → log conversation to trigger Workflow 3.

**3 — The Logging & Evaluation**
Every conversation gets logged to Google Sheets — timestamp, session ID, user message, agent response, tools used, data freshness returned, token counts, cost per conversation. Evaluation framework mirrors what we use at work: scenarios tab, review tab, stats tab, regression tracker.

Also locked in the model split — Haiku 4.5 for the guardrail and scraping extraction nodes, Sonnet 4.6 for the main orchestrator and email composer. Cost per conversation estimated at less than a cent at current volume.

**What worked:**

The architectural thinking came naturally from experience — I already understood that different sections of an automation serve different purposes. This session was about getting it out of my head and into documentation before a single node gets placed.

The logging and eval framework felt immediately familiar. When you've been through a few different builds you start to understand why each phase exists, and you bring that instinct to your own builds. Being able to carry that across directly into this project is genuinely valuable.

**What failed:**

Nothing broke today. But I know finding the right specific pages for each country is going to take time — government websites aren't exactly built for easy navigation. That's a known challenge sitting in the backlog.

**What I learned:**

Token cost awareness isn't just a personal finance question — in a real organisation running thousands of conversations an hour it becomes a risk, governance, and finance conversation. Designing cost visibility in from day one, with token logging and a running monthly total. Great for forecasting and comparing for future projects.

Also — the moment an idea arrives, your mind immediately starts asking "how would that work?" That instinct gets sharper the more projects you've been through. Knowing which phases a project needs, and why, is something you earn from experience. It's starting to show up naturally in how I approach this build.

**Next session:**

Open n8n. Start with "part" 1 — the data pipeline. Find and confirm the specific government URLs for each country in scope before the first node gets placed.
