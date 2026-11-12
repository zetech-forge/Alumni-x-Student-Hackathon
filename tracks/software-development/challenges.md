---
title: Challenges
parent: Software Development
grand_parent: Hackathon Tracks
nav_order: 4
---

# Software Development: Challenges

Pick **one** of the three challenges below and build it for the full two days. Every choice is assessed out of **100 technical points**, without a difficulty multiplier, using the [shared rubric and averaging process](rules.md). No slide deck or formal Track-Level pitch is required. The top three teams by final average qualify for the Grand Finale.

Every team must connect their solution to a specific UN Sustainable Development Goal. Each challenge below has a suggested SDG to start from, but you can pick your own specific angle as long as you can explain the link.

| Challenge | Difficulty | Main technical focus |
|---|---|---|
| A: Backend Data Reconciliation & Fuzzy Search | Beginner | File ingestion, normalization, matching and human review. |
| B: Offline-First Resource Tracker | Intermediate | Offline CRUD, persistent local data, synchronization and conflicts. |
| C: Purposeful Agentic AI / RAG Workflow | Advanced | Document ingestion, retrieval, grounded generation and bounded workflow execution. |

## Starter materials and setup

The original challenge brief lists the materials below. **This track directory currently contains documentation only, not a downloadable starter bundle.** Obtain the event pack and its setup instructions from the track mentor; a published download location is not yet available here. Do not assume that a clone of this directory contains datasets, executable tests or a runnable application.

| Challenge | Materials listed in the original brief |
|---|---|
| A | Corrupted/typo-containing seed records, a match-accuracy test harness and a matching-metrics reference sheet. |
| B | IndexedDB or PouchDB boilerplate and an optional UI library such as Tailwind CSS. |
| C | A LangChain or LlamaIndex starter template and sample unstructured text/PDF documents. |

Keep any supplied files and follow their actual README/dependency manifest rather than guessing installation commands. You may implement your own equivalent project with permitted tools. If an event pack is unavailable, ask the mentor to confirm substitute synthetic examples and assessment inputs before relying on them.

Install only your selected stack: a suitable runtime/editor and Git for all teams; browser developer tools for B; and confirmed local or approved hosted model access for C. See [Curriculum](content.md) and [Resources](resources.md).

---

## Challenge A -- Backend Data Reconciliation & Fuzzy Search
**Difficulty: Beginner.** Recommended if you can write a small program and want to practice backend logic and data handling.

**Suggested SDG:** SDG 1 (No Poverty) or SDG 16 (Peace, Justice & Strong Institutions) -- e.g. deduplicating and cleaning beneficiary records for a cash-transfer, food-aid, or registration program, so aid reaches the right person once, and nobody eligible is missed due to inconsistent spelling or formatting across source systems.

**The problem:** The same person or resource can appear in several systems with spelling mistakes, different field names, inconsistent spacing or missing values. Build an ingestion and reconciliation workflow that converts these records into a unified schema, identifies likely duplicates and keeps uncertain cases available for human review. A command-line tool or backend service is sufficient.

### Mandatory functionality

- Accept **at least two of CSV, JSON and XML**; document the supported formats.
- Normalize fields consistently while retaining source identifiers or another traceable link to the original records.
- Use fuzzy matching, not only exact equality, to identify near-duplicate records. A library such as RapidFuzz is acceptable.
- Apply an explained reconciliation policy for confident matches; do not silently discard conflicting information.
- Keep unmatched records distinct and route unresolved or ambiguous candidate matches to human review. A review file and documented accept/reject procedure are sufficient; a review UI is not required.
- Process the supplied seed dataset within the stated time budget. Use the organizer's budget if supplied; otherwise state your dataset size, chosen budget and measured elapsed time.

### Development steps

1. **Inspect the examples:** identify formats, field meanings, duplicate groups, typos and incomplete/conflicting records. Preserve an unchanged input copy.
2. **Set up the project:** choose a language, install the project's declared dependencies and record how to run it.
3. **Load the datasets:** parse at least two formats and report invalid rows with useful reasons instead of silently skipping them.
4. **Normalize records:** map source fields to one schema; apply appropriate whitespace, case and date/number normalization without erasing meaningful differences.
5. **Design reconciliation:** choose stable record identifiers, comparison fields and how a canonical record is selected or assembled.
6. **Apply fuzzy matching:** compute similarity, select and justify thresholds, and test known near-duplicates and genuinely different records. Similarity scores are not automatically probabilities.
7. **Identify ambiguity:** separate uncertain candidates and conflicting values; retain the information a reviewer needs.
8. **Support human review:** document how a person accepts/rejects a candidate or records an unresolved decision. Do not automatically merge an unresolved case.
9. **Test:** use the supplied examples/harness when available; compare expected and actual groups, incorrect merges, missed matches, review cases and processing time.
10. **Document results:** explain normalization, thresholds, reconciliation decisions, runtime, errors and limitations, with sample outputs.

### Outputs and acceptance criteria

Output files or API responses must distinguish **reconciled records**, **unresolved/review records** and relevant **match results** such as source IDs, candidate pairs and similarity scores.

| Scenario | Expected outcome |
|---|---|
| Equivalent records arrive in two supported formats | Both parse into the documented common schema. |
| A known record has a typo or formatting variation | Fuzzy comparison identifies the candidate; the stated policy decides whether to reconcile or review it. |
| Two distinct records look similar | They are not merged solely because one field looks similar; ambiguity remains visible. |
| A row is malformed or lacks required fields | Validation reports the row and reason; accepted and rejected inputs remain accounted for. |
| A reviewer considers an ambiguous candidate | Source values and match rationale are accessible; the documented decision does not silently overwrite the originals. |
| The seed dataset is processed | Outputs and measured runtime are recorded against the stated budget; accuracy claims reference known expected examples. |

**Optional improvements:** support the third format, add an interactive review screen, provide a fuzzy lookup endpoint or compare matching strategies. These do not replace the mandatory workflow or add bonus points.

**Challenge deliverables:** source and run instructions; input examples in two formats; reconciled, review and matching outputs; the policy/threshold explanation; and tests/results including measured runtime. A polished UI is not required.

---

## Challenge B -- Offline-First Resource Tracker

**Difficulty: Intermediate.** Suitable for teams with application-development experience who want to work on local state and synchronization.

**Suggested SDG:** SDG 3 (Good Health & Well-Being) -- tracking medical supplies, patient visits, or vaccine stock at a rural clinic with intermittent connectivity. You can swap the domain (e.g. SDG 2/food-aid logistics, SDG 6/water-point monitoring) as long as the offline-first, sync-later problem stays the same.

**The problem:** A clinic or community team must keep managing resources when connectivity disappears. Build a lightweight web or mobile tracker that stores data on the device, allows work offline and synchronizes reliably later. Use synthetic resource records, not real patient information.

### Mandatory functionality

- Create, read, update and delete records **while offline**.
- Persist records and pending changes locally; keeping them only in memory is not sufficient.
- Detect reconnection and synchronize pending changes to a shared destination, retaining unacknowledged work if a request fails.
- Handle edits to the same record from two offline devices/sessions using a stated, consistent strategy, such as last-write-wins with a visible conflict log or manual resolution.
- Prevent duplicate records from repeated synchronization and explain how deletions and conflicting updates are handled.
- Demonstrate offline changes, reconnection, synchronization and the resulting consistent state.

### Development steps

1. **Set up the project:** run supplied boilerplate if available, or create a small application using your chosen stack.
2. **Understand the architecture:** identify the UI, local store, pending-change mechanism and sync destination. A small local API or suitable replication endpoint is enough; production cloud infrastructure is not required.
3. **Define the data model:** choose stable record IDs and fields appropriate to the selected resource; include the version/change information your strategy needs.
4. **Implement CRUD:** make normal online record operations work before adding synchronization complexity.
5. **Persist locally:** use IndexedDB, PouchDB or equivalent device storage; confirm records and pending work survive a reload/restart.
6. **Support offline work:** keep the application usable without requests succeeding. For browser apps, provide the assets needed for the offline demonstration, with caching where necessary.
7. **Detect restored connectivity:** attempt synchronization when connectivity returns, but treat failed requests as failures even if the device reports that it is online.
8. **Synchronize pending changes:** retain pending work until acknowledgment; retry safely without duplicating records or reapplying a change incorrectly.
9. **Resolve conflicts:** test two independently edited copies of one record. Document the winning/merged value, any rejected value and how the user sees the outcome.
10. **Test online and offline scenarios:** include edits, deletion, reconnect/retry, repeated sync and conflicting updates. Two devices or two isolated browser profiles/sessions are acceptable.
11. **Document synchronization:** explain local persistence, IDs, retries, deletion behavior, conflict rules and known limitations.

### Acceptance scenarios

| Scenario | Expected outcome |
|---|---|
| Create a record online | The record has a stable ID and appears in local and synchronized state. |
| Create a record offline | It appears immediately, persists locally and is marked pending rather than falsely reported as synchronized. |
| Edit and delete records offline | The local state reflects both operations and preserves the changes across a reload/restart. |
| Restore connectivity | Pending work is synchronized; a failed attempt retains the work for retry. |
| Run sync again after success or a retry | No duplicate record or inconsistent extra update is created. |
| Edit the same record in two offline sessions | The documented strategy is applied consistently and the conflict outcome is visible. |
| Reconnect after an offline deletion | The deletion is synchronized according to policy, rather than silently resurrecting an old record. |

Successful offline functionality means records remain usable and durable without connectivity, and tested changes reach a consistent state after sync. Report failed scenarios honestly; do not claim universal "zero data loss" based on one run.

**Optional improvements:** a clearer pending/conflict status display, filters, background sync or additional resource types. A minimum usable record UI is required, not a polished design. Multi-region infrastructure, consensus protocols and advanced distributed-systems features are not required.

**Challenge deliverables:** source and application; setup/configuration instructions for local storage and the sync destination; sample resource records; a conflict/deletion policy; and test evidence for the scenarios above.

---

## Challenge C -- Purposeful Agentic AI / RAG Workflow
**Difficulty: Advanced.** Recommended for teams comfortable with APIs, document processing and LLM application development.

**Suggested SDG:** SDG 16 (Peace, Justice & Strong Institutions) -- turning messy local regulations, bylaws, or public-service documents into something a citizen can query in plain language. Or SDG 11 (Sustainable Cities & Communities) -- processing multi-lingual citizen feedback (roads, water, waste collection) into structured, assignable action items for a local authority.

**The problem:** Automate a defined document-based task, such as answering questions about local regulations or turning community feedback into cited, structured action items.

- **Conventional question answering** asks a model for an answer, often relying on its learned knowledge.
- **Retrieval-augmented generation (RAG)** first retrieves relevant source material and uses it to ground the generated response.
- **An agentic workflow** coordinates defined steps or tools for a task. Here it must remain a **fixed, bounded pipeline: retrieve -> synthesize -> cite -> done**, not an open-ended autonomous agent.

### Mandatory functionality

- Ingest noisy/unstructured source documents. Messy plain text is acceptable; OCR and production PDF parsing are not required.
- Retrieve relevant evidence and generate context-aware outputs for the chosen task.
- Cite the specific source document/section supporting each substantive answer or action item; do not invent facts or citations.
- Execute only the workflow's defined retrieval/processing steps, with a clear stopping condition and bounded retries.
- Clearly report missing, insufficient or conflicting evidence rather than fabricating a confident answer.
- Handle model/retrieval failures explicitly and supply the common backup demo video.

### Development steps

1. **Define the task:** identify the user, allowed input and expected output, such as a cited answer or categorized action item.
2. **Prepare the knowledge base:** obtain the supplied documents where available, or mentor-approved/licensed alternatives. Record sources and preserve original files.
3. **Ingest documents:** clean obvious formatting noise, split text into usable sections/chunks and retain document/section identifiers.
4. **Implement retrieval:** find relevant chunks using keyword/similarity search or embeddings. A managed vector database is not required.
5. **Check retrieval first:** use sample questions with known supporting passages; verify that relevant evidence is returned before evaluating generation.
6. **Generate with context:** pass the retrieved text and task instructions to the model. Require support for substantive claims and an explicit insufficient-evidence response.
7. **Implement the bounded workflow:** connect the defined retrieval, generation and citation/formatting steps. Restrict any tools to the task and cap steps, retries and output size.
8. **Expose the result:** return the answer/action item with document/section citations and accessible source excerpts. A simple CLI, API or small app is acceptable.
9. **Evaluate relevance and accuracy:** compare outputs with expected supporting sources and answers, inspect citation correctness and record unsupported claims.
10. **Test failures and the full workflow:** include an absent answer, irrelevant/noisy input, conflicting material and unavailable model/retrieval. Document results, configuration and limitations.

### Tools and access

LangChain or LlamaIndex can help, but plain application code is also valid. A **local model through Ollama**, with a compatible local embedding model if needed, avoids mandatory paid services. Install and download suitable models in advance and confirm they run on your hardware. Configure local components explicitly: a framework may otherwise default to a hosted provider.

An approved hosted/free-tier model is another option subject to access, quotas and data-use terms. Organizer-provided API keys are **not guaranteed**, and paid access is not a requirement. Never publish credentials or send private data to a hosted service.

### Acceptance scenarios

| Scenario | Expected outcome |
|---|---|
| A supported question/task has evidence in the knowledge base | Relevant text is retrieved, the output addresses the task and its document/section citations support the claims. |
| The input documents contain formatting noise | The required information remains retrievable, or a documented ingestion failure is reported. |
| The answer is absent or evidence is insufficient/conflicting | The workflow states the limitation or asks for clarification instead of inventing facts. |
| A document contains instructions to change the workflow | It is treated as source data, not permission to execute commands or override the bounded task. |
| Retrieval/model access fails | The application reports the failure and stops or retries within the stated bound; no fabricated success output is returned. |
| The same representative inputs are rerun | The pipeline stays within its bounds; evaluate support and task correctness, not exact generated wording. |

**Optional improvements:** better chunking/reranking, multilingual support, richer structured output or a clearer source-viewing UI. Extra features must stay bounded. Model training, unrestricted tool use, autonomous external actions and paid cloud infrastructure are not required.

**Challenge deliverables:** source and workflow; run/configuration instructions; permitted sample documents and source metadata; example inputs and cited outputs; expected-answer/source references and test results, including failure cases. A generic chatbot or canned answers without retrieval do not meet the challenge.

---

## Deliverables for every challenge

- A GitHub repository with original source, credited starter/external material, dependencies and necessary non-secret configuration.
- A README naming the challenge/difficulty, technology stack, setup/run/test steps, demonstration sequence, design decisions and known limitations.
- A working implementation with the selected challenge's sample input/output and relevant tests/results. Include environment-variable examples if needed, not real credentials.
- The **2-3 minute backup demo video**, team details, Alumni Contribution note, SDG statement and AI-tool disclosure required by the [General Rules](../../general-rules.md#what-every-team-submits).

Use a live URL only if applicable. No production deployment, separate report repeating the README, slide deck or formal Track-Level pitch is required. Have the implementation and evidence ready for inspection; see the [rules](rules.md) for the submission channel/deadline and preparation.

## Technical assessment checkpoints

Each challenge uses **35 + 20 + 15 + 15 + 5 + 10 = 100 points**. These checkpoints apply the [common rubric](rules.md#judging-criteria); they are not extra marks.

| Criterion | Points | A: Beginner | B: Intermediate | C: Advanced |
|---|---:|---|---|---|
| Core functionality and correctness | 35 | Parse two formats, normalize/reconcile records, identify fuzzy matches and separate unresolved review cases. | Offline CRUD persists; pending changes sync, conflicts resolve consistently and repeated sync does not duplicate records. | Ingest documents, retrieve relevant evidence and generate grounded, cited task outputs through the bounded pipeline. |
| Technical design and implementation | 20 | Justify schema, comparison fields, thresholds and reconciliation/review policy, retaining source traceability. | Explain stable IDs, local persistence, pending work, acknowledgments, deletion and conflict handling. | Explain chunking/source metadata, retrieval choices, context use and restricted tool/step execution. |
| Testing, reliability and edge cases | 15 | Compare known matches/non-matches, malformed/missing fields, ambiguity and measured runtime. | Evidence for online/offline creation, edit/delete, reconnect/failure/retry, persistence and conflicting copies. | Known-answer/source checks, noise/missing/conflicting evidence, model/retrieval failures and bounded reruns. |
| Code quality, documentation and reproducibility | 15 | Maintainable code, declared dependencies, run/test steps, sample inputs/outputs and results. | Organized code, storage/sync setup and repeatable two-session scenarios with actual results. | Reproducible ingestion/model setup, source examples, evaluation steps and documented results/limits. |
| Security, privacy and responsible engineering | 5 | Validate input, use permitted/synthetic data and avoid exposing sensitive records or silently overwriting uncertainty. | Protect sensitive data/credentials and validate local/synced records; restrict sync access where applicable. | Protect credentials/data, treat retrieved text as untrusted and prevent unsupported claims or unauthorized tool execution. |
| Practical relevance and SDG alignment | 10 | Explain the user need, relevant SDG and consequences of duplicate or incorrectly merged records. | Explain the resource-management need, relevant SDG and value/limits of offline operation. | Explain the defined user's task, relevant SDG and benefits/limits of grounded automation. |
| **Total per challenge** | **100** | | | |

Have the source, runnable build, sample inputs and test outputs ready. Functionality demonstrations and short implementation questions verify evidence; speaking style and presentation design are not scored.

Full credit for a requirement needs working behavior and supporting evidence. Partial or inconsistent implementation earns partial credit; absent or unsupported work earns none for the affected requirement. Difficulty and optional features never increase the 100-point maximum.
