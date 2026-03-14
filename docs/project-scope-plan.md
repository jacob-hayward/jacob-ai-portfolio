# Visa Information Agent
## Project Scope & Plan

| Field | Detail |
|---|---|
| Version | 1.0 — Initial Release |
| Author | Jacob Hayward |
| Status | Phase 1 Complete — Entering Build |
| Last Updated | March 2026 |
| Repository | github.com/jacob-hayward/jacob-ai-portfolio |

---

## 1. Objective

Build a publicly accessible AI-powered Visa Information Agent as the centrepiece of a personal portfolio website. The agent helps people navigate visa and immigration requirements across EU and Oceania countries, drawing from official government sources on a scheduled pipeline.

This project exists to demonstrate real AI system design capability — not just the ability to wire up nodes, but the ability to architect, build, test, document, and reflect on a complete production-grade system.

### Vision

An always-available visa information assistant that is honest about what it knows, transparent about when its data was last updated, and designed to gracefully handle the edges of its own knowledge — pointing users to authoritative sources rather than guessing.

### Why This Project

- Personally relevant — Jacob is a New Zealander considering international career ambitions. He is the target user.
- Technically demonstrable — RAG pipeline, scheduled scraping, multi-agent orchestration, failure handling, and graceful degradation are all production-relevant patterns.
- Narrative clarity — the problem being solved is immediately legible to any hiring manager in five seconds.
- Extendable — the architecture supports future capability additions without a rebuild.

---

## 2. Problem Statement

Navigating visa and immigration requirements across multiple countries is genuinely difficult. Information is scattered across government websites, changes without notice, and varies significantly by nationality, job type, and destination. Most people waste significant time cross-referencing multiple sources to get a coherent picture.

### What Happens Without This

- Users manually cross-reference multiple official government websites — time consuming and error-prone
- Information found via search engines is frequently outdated or from unreliable secondary sources
- No single tool provides a conversational, honest interface that acknowledges data freshness limitations
- People make visa planning decisions based on stale or inaccurate information

### The Opportunity

A conversational agent that retrieves current visa information from official sources, communicates data freshness transparently, and directs users to authoritative links when uncertainty exists — delivers genuine value while demonstrating sophisticated system design thinking.

---

## 3. Stakeholders

### Primary Users

| Stakeholder | Description |
|---|---|
| Job Seekers & Migrants | People researching visa requirements for work or relocation to EU or Oceania countries |
| NZ/AU Residents | People considering international relocation — a use case Jacob understands first-hand |
| EU Residents | People considering relocation to Oceania (NZ, Australia) |

### Portfolio Stakeholders

| Stakeholder | Interest |
|---|---|
| Technical Hiring Managers | Evaluating AI system design capability, architectural thinking, and production awareness |
| Non-Technical Stakeholders | Understanding the problem solved, the outcome achieved, and the business relevance |
| Jacob Hayward | Portfolio centrepiece demonstrating end-to-end AI build capability for international job market |

---

## 4. MVP Scope

### What the Agent Will Do — MVP Day 1

- Answer conversational questions about visa requirements for EU and Oceania countries
- Retrieve information from a RAG pipeline populated by scheduled scraping of official government sources
- Transparently communicate data freshness — the agent will always indicate when its information was last updated
- Provide direct links to official government sources for verification
- Gracefully degrade when data is stale or a scrape has failed — never answer confidently with potentially outdated information
- Send an email alert to Jacob when a scrape fails — silent failures are explicitly designed out
- Accept a user's nationality and destination country to personalise responses
- Offer to email the user a summary of the relevant visa pathway

### What the Agent Will Not Do — Explicit Exclusions

- Provide legal advice or immigration consultancy — always directs to official sources
- Cover countries outside EU and Oceania regions — deliberate scope discipline for MVP
- Handle visa applications or form filling
- Provide real-time processing times or queue data — too volatile for a scrape-based pipeline
- Support languages other than English in MVP

### Geographic Scope

| Region | Countries Covered |
|---|---|
| European Union | Finland, Estonia, Netherlands, Germany (priority EU markets for the initial release) |
| Oceania | New Zealand, Australia |

### Benefits of a Restricted MVP

- Low risk validation — test the full pipeline end-to-end before expanding scope
- Rapid feedback loops — identify and fix architectural issues before adding complexity
- Scope discipline — a fully-built focused system is more impressive than a half-built ambitious one
- Extendable — additional countries and capabilities can be layered in post-MVP

---

## 5. System Architecture

### Overview

The Visa Information Agent uses a hybrid architecture combining a scheduled data pipeline, a RAG retrieval system, and a conversational agent layer — all orchestrated through n8n and surfaced via a Typebot UI on the portfolio website.

### Core Components

| Component | Description |
|---|---|
| Conversational UI | Typebot — embedded chat widget on the portfolio website |
| Agent Orchestration | n8n — self-hosted on Hetzner VPS |
| RAG Pipeline | Scheduled scraping → chunking → embedding → vector store |
| Vector Store | Stores processed visa information for retrieval at query time |
| LLM | Claude or OpenAI — processes retrieved context and generates responses |
| Hosting | Hetzner VPS — Finnish or German data centre, GDPR jurisdiction |
| Version Control | GitHub — full build journal and project documentation |

### Data Pipeline Flow

1. Cron trigger fires in n8n
2. HTTP request nodes scrape target government URLs
3. Content is chunked and embedded
4. Vector store is upserted with fresh data and timestamp
5. If any scrape fails — error branch triggers email alert to Jacob

### Three-Tier Fallback Chain

| Tier | Source |
|---|---|
| Primary | Official government immigration website (e.g. migri.fi for Finland) |
| Secondary | Reputable immigration aggregator (e.g. Visaguide.world) — more stable HTML structure |
| Tertiary | Graceful degradation message — latest info as of [date], with link to official source |

### Tech Stack

| Tool | Role |
|---|---|
| n8n (self-hosted) | Workflow automation, agent orchestration, cron scheduling |
| Typebot | Conversational UI layer embedded on website |
| Hetzner VPS | Production hosting — Finnish or German data centre |
| Docker | Container runtime for n8n on both local and Hetzner environments |
| Vector Store | RAG retrieval for visa information |
| GitHub | Build journal, documentation, version control |

---

## 6. Success Criteria

### Technical Success

- Scraping pipeline runs reliably on schedule with documented success/failure rates
- RAG retrieval returns relevant, accurate visa information for test queries
- Graceful degradation functions correctly when data is stale or scrape has failed
- Error alert system fires correctly on scrape failure
- Agent correctly declines out-of-scope queries and directs to official sources
- System is deployed and publicly accessible on Hetzner

### Portfolio Success

- A technical hiring manager can understand the full architecture within five minutes of landing on GitHub
- Build journal documents the complete journey including failures, diagnoses, and fixes
- README serves both a technical and non-technical reader simultaneously
- The live demo on the portfolio website is functional and impressive on first interaction

### Personal Success

- Jacob can confidently explain every architectural decision in an interview
- The project demonstrates production-awareness, not just build capability
- The failure log and retrospective sections demonstrate senior-level thinking

---

## 7. Risks & Mitigations

| Risk | Mitigation |
|---|---|
| Government website HTML structure changes, breaking scraper silently | Error branch on all scrape nodes sends immediate email alert. Three-tier fallback ensures graceful degradation rather than silent failure. |
| JavaScript-rendered government pages that basic HTTP scraping cannot access | Test each target URL before building pipeline. If JS-rendered, evaluate Playwright/Puppeteer node or pivot to secondary aggregator source. |
| Scope creep — adding countries or capabilities before MVP is stable | Strict scope discipline: EU priority markets and Oceania only. Additional countries documented as post-MVP fast follows. |
| Stale data misleads users | Agent always communicates data freshness date. Tertiary fallback directs to official source. Scrape schedule keeps data within 5-7 day freshness window. |
| Build complexity exceeds available time | Phase discipline: each phase has defined entry and exit criteria. MVP is deliberately minimal. V2 adds capability only after V1 is stable and documented. |

---

## 8. Build Phases

| Phase | Description |
|---|---|
| Phase 1 — Design & Ideation ✅ | Problem definition, architecture design, scope decisions, stakeholder identification. COMPLETE. |
| Phase 2 — Build v1 (MVP) | Build the simplest working version. Document decisions as they are made. Keep a build log. |
| Phase 3 — Stress Test & Failure Log | Systematic adversarial testing. Every failure documented precisely. |
| Phase 4 — Diagnose & Fix | Root cause analysis for each failure. Architecture diagram updated to reflect reality vs plan. |
| Phase 5 — Build v2 | One meaningful capability added. Clearly versioned. |
| Phase 6 — What I'd Do Differently | Candid retrospective. Most important section for senior technical interviewers. |

### Local vs Production

Workflows are designed and tested locally using Docker Desktop and n8n running at localhost. Once stable, they are deployed to the Hetzner VPS instance. Local environment is the staging environment — Hetzner is production.

---

## 9. Post-MVP Follows

- Extended country coverage beyond initial four EU markets
- Eligibility assessment — user inputs nationality and job type, agent assesses visa pathway fit
- Email summary action — agent composes and sends a personalised visa pathway summary to the user
- Multi-language support — German or Finnish language responses for broader accessibility
- The Berlin Bound concept — a full relocation orchestrator using the Visa Agent as its core module. Deliberately scoped out to reduce risk but documented as the logical next evolution.

---

## 10. In Conclusion

This project is not just a technical build — it is a documented demonstration of how Jacob thinks through problems, makes architectural decisions, handles failure, and improves iteratively. The build journal is as important as the system itself.

The Visa Information Agent is scoped deliberately to be completable, testable, and deployable as a public-facing system — while being architecturally sophisticated enough to demonstrate production-grade thinking to technical hiring managers in any market Jacob targets.

Every decision documented here will be visible in the GitHub build journal, live in the deployed system, and articulable in an interview.

---

*Document prepared by Jacob Hayward*
*github.com/jacob-hayward/jacob-ai-portfolio*
