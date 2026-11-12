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

**Every team must complete three mandatory parts:** the original core challenge,
its integrated **Data Structures and Algorithms (DSA) task**, and a **working
PrimeCloud deployment**. Optional features cannot replace any of them. These
requirements use the existing 100-point rubric; they do not create extra marks
or a separate Track-Level presentation.

Use the [PrimeCloud Deployment Guide](deployment.md) for the complete initial
deployment procedure, configuration, verification and submission checklist.
Build a small end-to-end version and deploy early; full production architecture
is not required.

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

**The problem:** The same person or resource can appear in several systems with spelling mistakes, different field names, inconsistent spacing or missing values. Build an ingestion and reconciliation workflow that converts these records into a unified schema, identifies likely duplicates and keeps uncertain cases available for human review.

The original reconciliation engine may remain a CLI or library, but the
additional deployment requirement means exposing it through a lightweight
HTTP API or equivalent cloud-accessible application interface. A polished
frontend is not required.

### Original core functionality (mandatory)

- Accept **at least two of CSV, JSON and XML**; document the supported formats.
- Normalize fields consistently while retaining source identifiers or another traceable link to the original records.
- Use fuzzy matching, not only exact equality, to identify near-duplicate records. A library such as RapidFuzz is acceptable.
- Apply an explained reconciliation policy for confident matches; do not silently discard conflicting information.
- Keep unmatched records distinct and route unresolved or ambiguous candidate matches to human review. A review file and documented accept/reject procedure are sufficient; a review UI is not required.
- Process the supplied seed dataset within the stated time budget. Use the organizer's budget if supplied; otherwise state your dataset size, chosen budget and measured elapsed time.

### Mandatory DSA: Efficient Record Indexing and Ambiguous Match Queue

**Hash-map index:** implement a lookup structure such as
`Map<NormalizedKey, List<RecordReference>>`. Use normalized identifiers or
suitable composite keys present in your actual inputs: email, phone, reference
number or an appropriate field combination. Do not assume every dataset has
every identifier.

- Preserve every record reference associated with a key; append to its list
  rather than overwriting an earlier record.
- Keep distinct keys distinct even when their hashes collide; a standard
  language-provided map handles its internal hash collisions.
- Retain source IDs and the original values. Missing/unusable identifiers
  must not cause unrelated records to be merged under one empty key.
- Use the index for candidate lookup, not as proof that records represent the
  same entity. Keep fuzzy matching and review available when exact lookup
  finds no match or returns conflicting candidates.

**FIFO review queue:** enqueue ambiguous candidates with the original record
reference, potential matching record reference, similarity score, ambiguity
reason and relevant conflicting values. Process items in insertion order,
record accept/reject/unresolved decisions and retain source traceability.
An unresolved item must not silently become an automatic merge.

Standard hash maps and queues are allowed; do not build a hash table from
scratch. Use a deque, ring buffer or equivalent queue implementation with
constant-time or amortized constant-time enqueue/dequeue, not repeated
linear-time removal from the front of an array.

**Complexity:** average map insertion/lookup is O(1); indexing n records is
average O(n), excluding normalization/key construction. Returning m references
for one key costs O(m), and fuzzy comparisons have their own cost. Queue
enqueue/dequeue is O(1), or amortized O(1) where appropriate. Describe these
assumptions rather than claiming the entire reconciliation workflow is O(1).

### Development steps

1. **Inspect the examples:** identify formats, field meanings, duplicate groups, typos and incomplete/conflicting records. Preserve an unchanged input copy.
2. **Set up the project:** choose a language, install the project's declared dependencies and record how to run it.
3. **Load the datasets:** parse at least two formats and report invalid rows with useful reasons instead of silently skipping them.
4. **Normalize records:** map source fields to one schema; apply appropriate whitespace, case and date/number normalization without erasing meaningful differences.
5. **Build the index:** select usable normalized keys and store all associated source-record references.
6. **Design fuzzy matching:** select comparison fields and justify thresholds; test near-duplicates and distinct records. Similarity scores are not automatically probabilities.
7. **Reconcile confident matches:** explain how a canonical record is selected or assembled, preserving conflicting/source values according to policy.
8. **Queue ambiguous candidates:** retain candidate references, scores, reasons and conflicting values in the FIFO review queue.
9. **Process human review:** document accept/reject/unresolved decisions in queue order without losing the originals.
10. **Test the workflow and structures:** use the supplied harness where available; check expected groups, incorrect merges, missed matches, malformed inputs, index buckets and queue order.
11. **Compare lookup approaches:** use the same normalized keys and records for linear-search and indexed retrieval; verify identical results and measure lookup time separately from index construction.
12. **Document results:** explain normalization, thresholds, reconciliation/review decisions, complexity, dataset size, measured runtime, errors and limitations.
13. **Expose the engine:** provide `GET /healthz` and a reconciliation endpoint such as `POST /api/reconcile`. Document how callers submit your supported input formats and receive results.
14. **Deploy to PrimeCloud:** follow the [deployment guide](deployment.md), using non-sensitive sample data and supported configuration.
15. **Verify the hosted workflow:** submit sample inputs through the assigned HTTPS URL and inspect actual reconciled, ambiguous/review and matching results.

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

### DSA acceptance checks

Demonstrate index construction, normalized-key retrieval, multiple references
under one key and no silent overwriting. Enqueue at least three distinguishable
review items and show FIFO processing with recorded decisions. Compare indexed
and linear lookup on the same probes, including a missing key, and explain the
measured results and complexity. Show that fuzzy matching still handles an
exact-key miss.

### PrimeCloud acceptance checks

The assigned HTTPS URL must serve `GET /healthz` and execute the real
reconciliation engine through the documented interface. Submit examples in
at least two supported formats; retrieve reconciled records, ambiguous review
records and matching results with source references. Show invalid-input
handling and the review workflow/decisions. A static page, canned response
or health check alone does not satisfy deployment.

**Optional improvements:** support the third format, add an interactive review screen, provide a fuzzy lookup endpoint or compare matching strategies. These do not replace the mandatory workflow or add bonus points.

**Challenge deliverables:** source and run instructions; input examples in two formats; reconciled, review and matching outputs; policy/threshold explanation; index and queue implementation with complexity notes; linear/indexed comparison and FIFO evidence; tests/results including measured runtime; and the deployed URL, health check, configuration instructions and hosted-workflow evidence. A polished UI is not required.

---

## Challenge B -- Offline-First Resource Tracker

**Difficulty: Intermediate.** Suitable for teams with application-development experience who want to work on local state and synchronization.

**Suggested SDG:** SDG 3 (Good Health & Well-Being) -- tracking medical supplies, patient visits, or vaccine stock at a rural clinic with intermittent connectivity. You can swap the domain (e.g. SDG 2/food-aid logistics, SDG 6/water-point monitoring) as long as the offline-first, sync-later problem stays the same.

**The problem:** A clinic or community team must keep managing resources when connectivity disappears. Build a lightweight web or mobile tracker that stores data on the device, allows work offline and synchronizes reliably later. Use synthetic resource records, not real patient information.

### Original core functionality (mandatory)

- Create, read, update and delete records **while offline**.
- Persist records and pending changes locally; keeping them only in memory is not sufficient.
- Detect reconnection and synchronize pending changes to a shared destination, retaining unacknowledged work if a request fails.
- Handle edits to the same record from two offline devices/sessions using a stated, consistent strategy, such as last-write-wins with a visible conflict log or manual resolution.
- Prevent duplicate records from repeated synchronization and explain how deletions and conflicting updates are handled.
- Demonstrate offline changes, reconnection, synchronization and the resulting consistent state.

### Mandatory DSA: Efficient Offline Synchronization and Conflict Management

Implement and integrate these structures:

1. **Durable FIFO pending-operation queue:** record create, update and delete
   operations in order, each with a stable unique operation ID, record ID,
   operation type, payload and relevant version/change metadata. Failed work
   stays pending with the same ID for retry. Remove it only after successful
   synchronization acknowledgment, not merely after sending a request.
2. **Record hash map keyed by record ID:** track local record state, latest
   pending changes, versions/change metadata and outstanding work. The map
   must not silently replace earlier queued operations with only the latest
   state.
3. **Operation-ID set:** track processed/acknowledged IDs and prevent duplicate
   processing. Persist the relevant state across reloads. Backend deduplication
   must also survive retries/restarts: a client-only set cannot prevent a
   repeated server mutation when the first response is lost. Apply the mutation
   and durable deduplication decision atomically or use an equivalent
   idempotent mechanism.
4. **Conflict-resolution algorithm:** use last-write-wins with a visible
   conflict log, or manual resolution. Explain the version/timestamp and
   deterministic tie policy, rejected/merged values and interaction with the
   queue and record map. Unresolved conflicts remain visible and pending.

Preserve FIFO processing; do not discard a failed head operation or silently
skip it to apply later dependent work. Retain deletion metadata/tombstones as
needed so retries or stale copies do not resurrect deleted records.

Standard collections are allowed. Expected in-memory costs are O(1) queue
enqueue/dequeue, or amortized O(1), and average O(1) map lookup/update and set
membership/insertion. Explain persistence/network costs separately. Advanced
distributed consensus and vector clocks are not required.

### Development steps

1. **Set up the architecture:** choose the app, local storage and backend. Obtain approval for the PrimeCloud remote persistence arrangement; a local development API is not the final deployment.
2. **Implement CRUD:** define stable record IDs and a usable resource interface.
3. **Persist locally:** use IndexedDB, PouchDB or equivalent device storage; retain records across reloads and make needed application assets available offline.
4. **Implement the durable FIFO queue:** capture offline create/update/delete operations and retain failed/unacknowledged work.
5. **Implement the record map:** maintain local state, versions and outstanding changes without losing queued history.
6. **Implement operation-ID tracking:** use the set and durable backend deduplication to make retries safe.
7. **Implement synchronization:** detect reconnection, process queued work in order and acknowledge only successful operations. A device reporting "online" does not guarantee a request succeeds.
8. **Resolve conflicts:** apply the selected strategy consistently to two independently edited copies; expose outcomes and rejected values.
9. **Test retries and duplicates:** include a failed request, a lost acknowledgment and repeated submission of the same operation ID.
10. **Test separate sessions:** perform offline edits and deletion from two devices or isolated browser profiles, including reload/restart.
11. **Deploy a minimal backend early:** validate its hosted sync interface and approved persistent store with sample operations.
12. **Document DSA and synchronization:** explain structures, complexity, IDs, acknowledgments, conflict/deletion policy and observed limitations.
13. **Deploy the completed application and sync service to PrimeCloud:** include the accessible interface, health check and approved remote persistence.
14. **Repeat the complete hosted workflow:** online use, offline use/reload, reconnect, sync, conflict handling and duplicate prevention.

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

### DSA acceptance checks

Show ordered enqueue/dequeue, record-map lookup/update and operation-ID set
membership. Demonstrate that failed operations remain pending, retries keep
the same IDs and a lost acknowledgment does not duplicate a server change.
Use two independently modified copies of one record to prove consistent
conflict handling. Verify deletion and explain the complexity assumptions.
Framework replication alone is not evidence of your queue/map/set integration.

### PrimeCloud acceptance checks

Provide the accessible application interface, cloud-hosted synchronization
endpoint, `GET /healthz` and an **organizer-approved persistent remote store**.
Do not rely on ephemeral container-local files for synchronized records or
processed-operation IDs.

Demonstrate loading the deployed app, online create/edit, working offline,
persisting offline changes across a reload, restoring connectivity and syncing
with the deployed backend. Then show conflicts, deletion and duplicate/retry
handling. Verify remote persistence across a permitted backend restart or
redeployment. Local persistence and remote synchronization are separate checks;
hosting does not replace offline-first behavior.

**Optional improvements:** a clearer pending/conflict status display, filters, background sync or additional resource types. A minimum usable record UI is required, not a polished design. Multi-region infrastructure, consensus protocols and advanced distributed-systems features are not required.

**Challenge deliverables:** source and application; local/remote storage and sync setup; sample resource records; queue/map/set implementation and complexity notes; operation-ID and conflict/deletion policy; two-session, FIFO, retry/lost-acknowledgment and persistence evidence; and the deployed interface/sync URLs, health check and deployment evidence.

---

## Challenge C -- Purposeful Agentic AI / RAG Workflow
**Difficulty: Advanced.** Recommended for teams comfortable with APIs, document processing and LLM application development.

**Suggested SDG:** SDG 16 (Peace, Justice & Strong Institutions) -- turning messy local regulations, bylaws, or public-service documents into something a citizen can query in plain language. Or SDG 11 (Sustainable Cities & Communities) -- processing multi-lingual citizen feedback (roads, water, waste collection) into structured, assignable action items for a local authority.

**The problem:** Automate a defined document-based task, such as answering questions about local regulations or turning community feedback into cited, structured action items.

- **Conventional question answering** asks a model for an answer, often relying on its learned knowledge.
- **Retrieval-augmented generation (RAG)** first retrieves relevant source material and uses it to ground the generated response.
- **An agentic workflow** coordinates defined steps or tools for a task. Here it must remain a **fixed, bounded pipeline: retrieve -> synthesize -> cite -> done**, not an open-ended autonomous agent.

### Original core functionality (mandatory)

- Ingest noisy/unstructured source documents. Messy plain text is acceptable; OCR and production PDF parsing are not required.
- Retrieve relevant evidence and generate context-aware outputs for the chosen task.
- Cite the specific source document/section supporting each substantive answer or action item; do not invent facts or citations.
- Execute only the workflow's defined retrieval/processing steps, with a clear stopping condition and bounded retries.
- Clearly report missing, insufficient or conflicting evidence rather than fabricating a confident answer.
- Handle model/retrieval failures explicitly and supply the common backup demo video.

### Mandatory DSA: Efficient Top-K Document Retrieval and Ranking

Implement a **bounded binary min-heap** in the actual retrieval pipeline.
Receive candidate chunks and relevance scores from your chosen keyword,
similarity or embedding method; the heap-based selection must be your
implemented algorithm, not merely a database/library's ready-made top-K output.
You do not need to implement an LLM, embedding model or vector database.

1. Validate K as a positive integer and retain each candidate's document ID,
   chunk ID, section metadata and score.
2. Insert candidates until the heap contains K entries.
3. Keep the least desirable selected candidate at the root. When a better
   candidate arrives, replace the root and restore the binary heap property.
4. Use a deterministic total ordering for equal scores, such as document ID
   then chunk ID. Apply the same preference to heap replacement and output
   sorting; tied results must not depend on input order.
5. Return the selected chunks in descending relevance order, with the
   deterministic tie order and intact citation metadata.
6. Feed these selected chunks into synthesis and citation, not into a separate
   demonstration-only code path.

Define duplicate handling; a set of document/chunk identities may prevent the
same chunk appearing twice. Handle empty candidate sets, fewer than K valid
candidates and invalid/non-finite scores explicitly. Do not fill missing
evidence with invented chunks.

**Complexity:** heap insertion/replacement is O(log K), and selection over n
candidates is O(n log K) for K >= 2, or O(n) for K = 1. Heap storage is O(K).
Sorting the selected results adds O(K log K); score generation and any
duplicate-tracking set have their own costs. Compare against a full-sort
baseline using the same candidates, K, duplicate policy and tie ordering.

### Development steps

1. **Define the task:** identify the user, allowed input and expected output, such as a cited answer or categorized action item.
2. **Prepare the knowledge base:** obtain the supplied documents where available, or mentor-approved/licensed alternatives. Record sources and preserve original files.
3. **Ingest documents:** clean obvious formatting noise, split text into usable sections/chunks and retain document/section identifiers.
4. **Retain identifiers:** preserve document, section and chunk identities through scoring and retrieval.
5. **Generate candidate scores:** use keyword/similarity search or embeddings. A managed vector database is not required; check known supporting passages first.
6. **Implement the bounded heap:** add insertion, replacement and heap-property checks with deterministic tie handling.
7. **Select top-K evidence:** preserve metadata and supply the selected chunks to generation.
8. **Generate with context:** require grounded answers/action items, supporting document/section citations and accessible source excerpts.
9. **Bound the workflow:** keep retrieve -> synthesize -> cite -> done, with restricted tools, stopping conditions, bounded retries and output size.
10. **Evaluate relevance and citations:** compare with known answers/sources and record unsupported claims.
11. **Compare selection algorithms:** verify the heap returns the same ranked top-K as full sorting, and record dataset size, K, timings and complexity.
12. **Test failures:** cover absent/conflicting evidence, noisy input, invalid K, empty/tied candidates and unavailable model/retrieval; report limitations explicitly.
13. **Deploy the actual RAG API/application to PrimeCloud:** configure permitted documents and an approved model endpoint reachable from the hosted application.
14. **Verify the hosted workflow:** demonstrate ingestion or the supplied knowledge base, heap selection, grounded generation, citations and visible failure handling through the HTTPS URL.

### Tools and access

LangChain or LlamaIndex can help, but plain application code is also valid. A **local model through Ollama**, with a compatible local embedding model if needed, avoids mandatory paid services. Install and download suitable models in advance and confirm they run on your hardware. Configure local components explicitly: a framework may otherwise default to a hosted provider.

An approved hosted/free-tier model is another option subject to access, quotas and data-use terms. Organizer-provided API keys are **not guaranteed**, and paid access is not a requirement. Never publish credentials or send private data to a hosted service.

For the mandatory deployment, the application must have an approved inference
route reachable from PrimeCloud. Local Ollama is useful for development, but
a model running only on your laptop does not satisfy hosted delivery.
Do not expose an unsecured laptop model server to the internet. Confirm a
permitted inference arrangement early; neither a paid API nor organizer keys
are assumed. Hosting or training a full model in the trial container is not
required. Store credentials using the supported server-side configuration and
secret facilities described in the [deployment guide](deployment.md).

### Acceptance scenarios

| Scenario | Expected outcome |
|---|---|
| A supported question/task has evidence in the knowledge base | Relevant text is retrieved, the output addresses the task and its document/section citations support the claims. |
| The input documents contain formatting noise | The required information remains retrievable, or a documented ingestion failure is reported. |
| The answer is absent or evidence is insufficient/conflicting | The workflow states the limitation or asks for clarification instead of inventing facts. |
| A document contains instructions to change the workflow | It is treated as source data, not permission to execute commands or override the bounded task. |
| Retrieval/model access fails | The application reports the failure and stops or retries within the stated bound; no fabricated success output is returned. |
| The same representative inputs are rerun | The pipeline stays within its bounds; evaluate support and task correctness, not exact generated wording. |

### DSA acceptance checks

Show heap construction, insertion, replacement and the heap property after
each operation on a small trace. Verify the highest-scoring K candidates,
deterministic ties, duplicate policy and preserved citation metadata against
the full-sort baseline. Include K = 1, fewer than K candidates, empty input and
invalid K/score cases. Record timings and explain selection, final sorting and
storage complexity. Show that the same selection code supplies the live RAG
workflow.

### PrimeCloud acceptance checks

The deployed application/API must expose `GET /healthz` and execute the real
ingestion or supplied-knowledge-base workflow, heap-based retrieval, grounded
generation and source citations. Demonstrate a supported task and missing
evidence, plus explicit service-error handling. A static chatbot screen,
prewritten answer or health check alone is not a successful deployment.

**Optional improvements:** better chunking/reranking, multilingual support, richer structured output or a clearer source-viewing UI. Extra features must stay bounded. Model training, unrestricted tool use, autonomous external actions and a large model hosted in the trial container are not required.

**Challenge deliverables:** source and bounded workflow; run/model configuration; permitted sample documents and source metadata; heap-selection implementation, trace, full-sort comparison and complexity notes; example inputs and cited outputs; expected-answer/source references and failure tests; and the deployed URL, health check and hosted-workflow evidence. A generic chatbot or canned answers without retrieval do not meet the challenge.

---

## Mandatory PrimeCloud deployment for every challenge

Deploy the completed solution to [PrimeCloud](https://primecloud.cloud/).
Use the [official documentation](https://primecloud.cloud/docs),
[official quickstart](https://primecloud.cloud/docs/quickstart) and the separate
[Software Development deployment guide](deployment.md).

- Submit the **assigned PrimeCloud HTTPS application URL**, `GET /healthz`
  URL, GitHub repository and deployed commit/revision.
- Supply deployment-status evidence and actual core-workflow inputs/outputs
  from the hosted service, not just a successful build or static page.
- Document build/start commands, runtime port, required environment-variable
  names, dependencies, storage/model arrangements and limitations. Never submit
  secret values.
- A requires a lightweight reconciliation interface; B requires the accessible
  app and persistent hosted sync backend; C requires the functioning hosted RAG
  application/API with heap-selected evidence.
- Confirm organizer-approved account access, resources, persistence and any
  inference arrangements early. Public documentation is not a guarantee of
  event credits, trial availability or a particular resource allocation.

A custom domain and production-grade architecture are not required. Deployment
does not replace core functionality, DSA or testing. Missing access/services
must be raised with the Technical Lead and recorded, not silently treated as
an optional requirement or successful deployment.

## Deliverables for every challenge

- A GitHub repository with original source, credited starter/external material, dependencies and necessary non-secret configuration.
- A README naming the challenge/difficulty, technology stack, setup/run/test steps, demonstration sequence, design decisions and known limitations.
- A working implementation with the selected challenge's sample input/output and relevant tests/results. Include environment-variable examples if needed, not real credentials.
- The integrated DSA implementation, complexity explanation, relevant comparison/trace evidence and expected/observed test results.
- The PrimeCloud HTTPS URL, health-check URL, deployed revision, deployment-status evidence and proof that the core workflow works through the hosted application.
- The **2-3 minute backup demo video**, team details, Alumni Contribution note, SDG statement and AI-tool disclosure required by the [General Rules](../../general-rules.md#what-every-team-submits).

Keep results and explanations in the README or linked project documentation;
no separate duplicate report, slide deck or formal Track-Level pitch is
required. Have the implementation, DSA evidence and hosted workflow ready for
inspection; see the [rules](rules.md) for the submission channel/deadline.

## Technical assessment checkpoints

Each challenge uses **35 + 20 + 15 + 15 + 5 + 10 = 100 points**. These checkpoints apply the [common rubric](rules.md#judging-criteria); they are not extra marks.

| Criterion | Points | A: Beginner | B: Intermediate | C: Advanced |
|---|---:|---|---|---|
| Core functionality and correctness | 35 | Original reconciliation works through the hosted interface, including matching and review outputs. | Offline CRUD and cloud synchronization work, including conflicts, deletion and duplicate prevention. | Hosted ingestion/knowledge-base, heap-selected evidence and grounded, cited outputs work through the bounded pipeline. |
| Technical design and implementation | 20 | Correct normalized-key index and FIFO review queue integrated with fuzzy matching and traceable reconciliation. | Durable FIFO queue, record map, operation-ID set and consistent conflict/deletion algorithm. | Correct bounded binary min-heap, deterministic ranking and metadata-preserving retrieval integrated into generation. |
| Testing, reliability and edge cases | 15 | Original cases, multi-record keys, queue order, linear/index comparison and hosted workflow results. | Offline/reload, FIFO, retry/lost acknowledgment, duplicates, conflicting copies and remote persistence results. | Heap trace/full-sort comparison, ties/boundaries, citation/failure checks and hosted workflow results. |
| Code quality, documentation and reproducibility | 15 | Maintainable code, complexity explanation, sample outputs and reproducible local/deployment commands. | Organized code, complexity notes, storage/sync configuration and repeatable local/hosted scenarios. | Reproducible ingestion/model setup, heap complexity and deployment configuration, examples and limitations. |
| Security, privacy and responsible engineering | 5 | Validate input, use permitted/synthetic data and avoid exposing sensitive records or silently overwriting uncertainty. | Protect sensitive data/credentials and validate local/synced records; restrict sync access where applicable. | Protect credentials/data, treat retrieved text as untrusted and prevent unsupported claims or unauthorized tool execution. |
| Practical relevance and SDG alignment | 10 | Explain the user need, relevant SDG and consequences of duplicate or incorrectly merged records. | Explain the resource-management need, relevant SDG and value/limits of offline operation. | Explain the defined user's task, relevant SDG and benefits/limits of grounded automation. |
| **Total per challenge** | **100** | | | |

Have the source, runnable build, sample inputs and test outputs ready. Functionality demonstrations and short implementation questions verify evidence; speaking style and presentation design are not scored.

Full credit for a requirement needs working behavior and supporting evidence.
Show separate acceptance results for **original functionality, DSA,
PrimeCloud deployment, testing and documentation**. Partial or inconsistent
implementation earns partial credit; absent or unsupported work earns none for
the affected requirement. Missing a mandatory part means the full challenge
is not complete. Difficulty and optional features never increase the
100-point maximum.
