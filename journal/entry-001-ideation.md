**Date:** 9–12 March 2026
**Phase:** Phase 1 — Design / Ideation

**What I did:**

Spent a few days bouncing ideas around across four different LLMs trying to figure out what to actually build for my portfolio site. The concept I kept coming back to was a website that works as a living resume — something a hiring manager could actually play with, not just read.

What eventually came together is a three-part site:

- A **resume agent** — ask it anything about me (professionally with limited personal info)
- A **showcase agent** — something technically interesting that any visitor can actually use
- An **architecture agent** — explains how the whole thing was built, for the technical people who want to go deeper

*"The showcase agent took the longest to figure out. I went through maybe 30+ ideas across several sessions — everything from a tea guide to a full relocation concierge for people moving to Melbourne or Berlin. What I landed on is a **Visa Information Agent** covering EU and Oceania. It won out for a few reasons: it's personally relevant to me if I decide to look internationally (and having lived internationally in Europe in the past), it solves a real problem people actually have, the data complexity gives it enough technical meat to be interesting, and it tells a coherent story to anyone reading the portfolio. 

It'll use RAG, pulling from official government visa sources on a scheduled scrape so the data stays reasonably fresh. If something goes stale or a scrape fails, the agent tells you that honestly and points you to the official source — rather than just confidently making something up.

The relocation agent idea was genuinely tempting but I made a deliberate call to park it. Too much scope for a solo build. The plan is to mention it in interviews as the natural next phase.

**What worked:**

Using multiple LLMs to stress-test the ideas was actually really useful — each conversation pulled the thinking in a slightly different direction. The shift that helped most was stopping thinking about *what the agent is about* and starting thinking about *what the agent can actually do*. That reframe opened up a lot better ideas.

The three-part structure also just makes sense. Each part of the site does a different job depending on who's looking at it.

**What failed:**

Nothing dramatically broke but the ideation sprawled across four days and four different tools with no real home base for decisions. By the end I had good thinking scattered everywhere. Should have been logging it from day one — which, well, here we are.

**What I learned:**

Scope discipline is just as important as ambition. The flashier concept loses if it never gets finished. A clean, well-documented focused build beats an impressive half-built one every time.

Also — designing for failure is actually a sign of mature thinking. Building in honest fallbacks isn't admitting weakness, it's showing you've thought about what happens in the real world.

**Next session:**

Lock down the tech stack — n8n, Typebot, Hetzner, vector store. Might also run the concept past my mentor at work before committing fully to Phase 2. Fresh eyes never hurt.
