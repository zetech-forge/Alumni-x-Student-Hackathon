---
title: Challenges
parent: Software Development
nav_order: 4
---

# Software Development: Challenges

Pick **one** of the three challenges below and build it for the full two days. Unlike a CTF, there's no separate points-per-challenge system -- whichever you pick is judged against the shared rubric in Track Rules.

Every team must connect their solution to a specific UN Sustainable Development Goal. Each challenge below has a suggested SDG to start from, but you can pick your own specific angle as long as you can explain the link.

---

## Challenge A -- Backend Data Reconciliation & Fuzzy Search
*Recommended starting point if your team is newer to shipping end-to-end projects.*

**Suggested SDG:** SDG 1 (No Poverty) or SDG 16 (Peace, Justice & Strong Institutions) -- e.g. deduplicating and cleaning beneficiary records for a cash-transfer, food-aid, or registration program, so aid reaches the right person once, and nobody eligible is missed due to inconsistent spelling or formatting across source systems.

**The problem:** Build an ingestion engine that matches, cleans, and deduplicates messy, user-submitted records arriving in different formats (CSV, JSON, XML) into one unified schema.

**What "done" looks like:**
- Accepts input in at least 2 of the 3 formats (CSV/JSON/XML)
- Groups near-duplicate entries using fuzzy matching (not exact string match) -- e.g. Levenshtein distance, Jaccard similarity, or a library like RapidFuzz
- Processes the provided seed dataset within a stated time budget
- Flags ambiguous matches for human review rather than silently merging them

**Provided:**
- Seed data files with intentionally corrupted records and typos
- A small automated test harness so teams can self-check match accuracy
- A short reference sheet on matching metrics (Levenshtein distance, Jaccard similarity)

**Judging note:** correctly deduping 90% of records and clearly flagging the rest for review beats silently "resolving" everything with no visibility into confidence.

---

## Challenge B -- Offline-First Resource Tracker

**Suggested SDG:** SDG 3 (Good Health & Well-Being) -- tracking medical supplies, patient visits, or vaccine stock at a rural clinic with intermittent connectivity. You can swap the domain (e.g. SDG 2/food-aid logistics, SDG 6/water-point monitoring) as long as the offline-first, sync-later problem stays the same.

**The problem:** Build a lightweight web or mobile dashboard for low-connectivity environments that stores state locally and syncs once a connection returns.

**What "done" looks like:**
- Create, read, update, and delete records all work correctly with no internet connection
- No data is lost when connectivity returns and a sync runs
- Simultaneous edits from two offline devices are resolved with a stated, consistent strategy (e.g. last-write-wins with a visible conflict log, or a manual merge prompt) -- you need to be able to explain your strategy, not just avoid conflicts by luck
- Demonstrated live: judges should watch you go offline, make changes, reconnect, and see the sync happen correctly

**Provided:**
- Boilerplate using IndexedDB or PouchDB
- A simple UI component library (e.g. Tailwind CSS)
- No special tooling needed to simulate offline -- your browser's dev tools network throttling/offline mode is enough

**Judging note:** "flawless" and "zero data loss" aren't pass/fail bars -- show 2-3 concrete scenarios (create offline + sync, edit the same record on two devices + sync) and you'll be scored on what's actually demonstrated.

---

## Challenge C -- Purposeful Agentic AI / RAG Workflow
*Highest ceiling, highest risk -- recommended if your team already has some ML/LLM experience.*

**Suggested SDG:** SDG 16 (Peace, Justice & Strong Institutions) -- turning messy local regulations, bylaws, or public-service documents into something a citizen can query in plain language. Or SDG 11 (Sustainable Cities & Communities) -- processing multi-lingual citizen feedback (roads, water, waste collection) into structured, assignable action items for a local authority.

**The problem:** Build a retrieval system that doesn't just answer generic questions, but automates a specific multi-step workflow -- e.g. parsing messy local PDF regulations into a queryable citizen-facing assistant, or turning multi-lingual community feedback into structured, categorized action items.

**What "done" looks like:**
- Handles noisy/unstructured source documents (messy plain text is fine to simulate scanned/poorly formatted PDFs)
- Every answer cites which specific source document/section it came from -- no un-sourced claims
- Runs a **fixed, bounded pipeline** (retrieve → synthesize → cite → done) rather than an open-ended autonomous agent. This is a hard scope constraint, not a suggestion -- open-ended agent loops are unreliable in a live demo, so keep the number of chained steps small and deterministic
- Comes with a short recorded backup demo (even a 60-second screen recording) in case the live demo hits a flaky API or model response during judging

**Provided:**
- Starter template using LangChain or LlamaIndex
- A curated sample dataset of unstructured text/PDFs
- Shared API keys or a local model endpoint (e.g. via Ollama) -- confirm with organizers which one is available at the venue; relying on live external API calls for ~150 participants on shared wifi is risky

**Judging note:** reliability matters more than flashiness. A team with a narrow pipeline that works every time should score higher on "functionality" than a team with a broader but flaky agent.
