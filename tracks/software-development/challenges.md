---
title: Challenges
parent: Software Development
grandparent: Hackathon Tracks
nav_order: 4
---

# Software Development: Challenges

Pick **one** of the three challenges below and build it for the full two days. Every choice is assessed out of **100 technical points**, without a difficulty multiplier, using the [shared rubric and averaging process](rules.md). No slide deck or formal Track-Level pitch is required. The top three teams by final average qualify for the Grand Finale.

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

**Assessment note:** Demonstrate match accuracy and ambiguous cases honestly. Correctly deduplicating 90% of records and flagging the rest for review is stronger evidence than silently "resolving" everything without confidence information.

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

**Assessment note:** Show 2-3 concrete scenarios, including offline creation followed by sync and edits to the same record on two offline devices. Credit reflects demonstrated correctness and retained data, not an unsupported claim of "zero data loss."

---

## Challenge C -- Purposeful Agentic AI / RAG Workflow
*Highest ceiling, highest risk -- recommended if your team already has some ML/LLM experience.*

**Suggested SDG:** SDG 16 (Peace, Justice & Strong Institutions) -- turning messy local regulations, bylaws, or public-service documents into something a citizen can query in plain language. Or SDG 11 (Sustainable Cities & Communities) -- processing multi-lingual citizen feedback (roads, water, waste collection) into structured, assignable action items for a local authority.

**The problem:** Build a retrieval system that doesn't just answer generic questions, but automates a specific multi-step workflow -- e.g. parsing messy local PDF regulations into a queryable citizen-facing assistant, or turning multi-lingual community feedback into structured, categorized action items.

**What "done" looks like:**
- Handles noisy/unstructured source documents (messy plain text is fine to simulate scanned/poorly formatted PDFs)
- Every answer cites which specific source document/section it came from -- no un-sourced claims
- Runs a **fixed, bounded pipeline** (retrieve → synthesize → cite → done) rather than an open-ended autonomous agent. This is a hard scope constraint, not a suggestion -- open-ended agent loops are unreliable in a live demo, so keep the number of chained steps small and deterministic
- Comes with the required 2-3 minute recorded backup demo in case the live demo hits a flaky API or model response during assessment

**Provided:**
- Starter template using LangChain or LlamaIndex
- A curated sample dataset of unstructured text/PDFs
- Confirm any organizer-approved model endpoint before relying on it; shared API credentials are not guaranteed. A local model through Ollama is an alternative. Do not commit credentials, and plan for unreliable shared wifi.

**Assessment note:** Reliability matters more than flashiness. A narrow, repeatable pipeline provides stronger functionality evidence than a broader but unreliable agent.

---

## Technical assessment checkpoints

The same five allocations apply to each challenge: **30 + 25 + 15 + 15 + 15 = 100 points**. These checkpoints explain the evidence expected under the [rubric](rules.md#judging-criteria), not additional marks.

| Criterion | Points | A: Data reconciliation | B: Offline-first tracker | C: Bounded AI/RAG workflow |
|---|---:|---|---|---|
| Functionality and correctness | 30 | Ingest at least two supported formats, normalize records, group fuzzy matches and flag ambiguous cases. | Offline CRUD, persistent local state, reconnection sync and the stated simultaneous-edit resolution work. | Noisy documents flow through a bounded retrieve/synthesize/cite pipeline, with document/section citations supporting answers. |
| Testing, reliability and responsible handling | 25 | Show accuracy and runtime on the supplied data; test ambiguous/incorrect matches and malformed inputs without silently merging them. | Show offline create/sync and conflicting edits on two devices or equivalent sessions; verify retained records, conflict handling and repeat sync. | Repeat grounded and missing-evidence queries; show bounded execution, safe unsupported-answer handling and model/API failure behavior. |
| Code quality and documentation | 15 | Explain parsing, schema and matching choices; provide commands, sample inputs/outputs and results. | Document local storage, sync and conflict rules with setup and test steps. | Document ingestion, retrieval, model configuration and run steps; keep credentials outside source control. |
| Creativity and approach | 15 | Justify matching/confidence decisions for the chosen data problem. | Justify storage and conflict decisions for realistic connectivity constraints. | Justify retrieval and workflow choices for a specific useful task, rather than a generic chatbot. |
| SDG and social-impact alignment | 15 | Explain the user need and consequences of duplicate or wrongly merged records. | Explain the user need, relevant SDG and value of reliable offline use. | Explain who uses the workflow, its SDG connection and the limits of automated outputs. |
| **Total per challenge** | **100** | | | |

Have the source, runnable build, sample inputs and test outputs ready. Functionality demonstrations and short implementation questions verify evidence; speaking style and presentation design are not scored.
