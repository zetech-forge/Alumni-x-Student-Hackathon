---
title: Content & Curriculum
parent: Software Development
grand_parent: Hackathon Tracks
nav_order: 1
---

# Software Development: Content & Curriculum

## Learning objectives
Prepare to build **one** of the [three challenges](challenges.md), not to master every tool in the track. You should be able to:

- Work as a team using Git/GitHub and credit external contributions.
- Reduce a two-day build to the mandatory behavior and relevant test scenarios.
- Implement the chosen workflow, explain design decisions and handle failures explicitly.
- Integrate the selected challenge's mandatory data structures/algorithm and explain complexity with trace/comparison evidence.
- Deploy the working solution to PrimeCloud and verify its health check and actual hosted workflow.
- Supply reproducible setup instructions, sample inputs/outputs and test evidence.
- Explain the user need, limitations and a specific SDG connection.

## Prerequisite knowledge

| Challenge | Preparation baseline | What you do not need |
|---|---|---|
| A: Backend Data Reconciliation & Fuzzy Search - Beginner | Basic programming, functions, lists/tables, file reading and simple validation. | AI frameworks, offline synchronization or a frontend framework. |
| B: Offline-First Resource Tracker - Intermediate | Application CRUD, JavaScript/browser concepts or comparable mobile development, and simple client/server requests. | Multi-region infrastructure, consensus protocols or advanced distributed systems. |
| C: Purposeful Agentic AI / RAG Workflow - Advanced | Confident programming, APIs, document processing and basic retrieval/LLM concepts. | Training a language model, paid APIs or a managed vector database. |

Everyone needs basic Git usage and a working editor/runtime for their chosen stack. Use a supported runtime version compatible with your project's dependencies and record it in the README.

## Learning modules

This is a preparation roadmap, not seven full courses to finish during a short
bootcamp. Everyone needs the shared foundations and basic deployment workflow;
study only the DSA and development pathway for your selected challenge.

### Module 1: Git and GitHub Essentials

- Create and manage your own repository; make understandable commits.
- Use branches, pull requests and reviews to divide work safely.
- Resolve a simple merge conflict and keep the selected deployment branch clear.
- Maintain a README with setup/run/test instructions, dependencies and credited
  external contributions.
- Ignore generated files and real secrets; use non-secret configuration examples.

**Practice:** another teammate clones the repository, follows the README and
runs a minimal example. Git/GitHub basics are recommended pre-event preparation.

### Module 2: Programming and Problem-Solving Fundamentals

- Decompose the problem into small steps with explicit inputs and outputs.
- Sketch an algorithm before choosing a framework; separate parsing,
  processing, state changes and output formatting.
- Validate inputs, preserve useful error information and handle failures explicitly.
- Introduce Big-O notation: distinguish time from space complexity, average
  from worst-case behavior, and algorithm cost from network/storage latency.
- Use small tests and debugging to trace incorrect output back to a specific step.

**Practice:** process a small valid/invalid input fixture, state the expected
output and trace how the implementation reaches it. Start with correctness
before comparing performance.

### Module 3: Data Structures and Algorithms

These are the structures used in the actual challenge implementations, not
unrelated coding exercises. Standard maps, sets and FIFO queues are allowed;
building a hash table from scratch is not required.

#### A - Beginner: Hash Maps and Queues

- Key-value indexing, insertion and lookup using normalized keys.
- Multiple record references per key without overwriting earlier records.
- FIFO enqueue/dequeue and traceable review decisions.
- Indexed versus linear search and basic time/space Big-O reasoning.
- Expected average map lookup O(1), index construction O(n), and queue
  operations O(1) or amortized O(1); account for result-list and matching costs.

**Practice:** build a lookup index with a repeated key and a missing-key case;
enqueue distinguishable ambiguous items and process them in FIFO order.
Compare indexed/linear results on the same probes. Use a proper queue
representation, not repeated linear-time removal from an array's front.

#### B - Intermediate: Queues, Hash Maps and Sets

- Ordered operation processing with a durable pending queue.
- Maps for record state, versions and outstanding changes.
- Sets and stable operation IDs for duplicate detection.
- Idempotency: retrying the same operation must not apply its effect twice.
- Deterministic conflict resolution, deletion handling and relevant complexity.

**Practice:** enqueue create/update/delete work, retain a failed operation,
retry with the same ID and demonstrate deduplication after a lost
acknowledgment. Resolve two independently edited copies consistently.
A browser-only acknowledged set does not establish server-side idempotency.

#### C - Advanced: Heaps and Priority Queues

- Binary heap structure/property and min-heap versus max-heap behavior.
- Insertion, root replacement and priority-based selection.
- Bounded top-K retrieval with deterministic score ties and citation metadata.
- Time/space analysis: O(n log K) selection for K >= 2, O(K) heap storage,
  and O(K log K) sorting of the selected output; identify other pipeline costs.

**Practice:** implement the bounded binary min-heap selection algorithm and
compare its ranked output with full sorting on the same scored candidates.
Test heap operations, ties, K = 1, fewer than K candidates, empty input and
invalid inputs. Using a ready-made library top-K result alone is insufficient.

### Module 4: Challenge-Specific Development

Follow one pathway and connect it to the corresponding Module 3 task.

| Challenge | Development pathway | Integrated DSA |
|---|---|---|
| A: Backend Data Reconciliation & Fuzzy Search - Beginner | Parsing, normalization, fuzzy matching, reconciliation and human review. | Normalized-key index and FIFO ambiguous-match queue. |
| B: Offline-First Resource Tracker - Intermediate | Offline CRUD, durable local data, synchronization and conflict/deletion policy. | Pending-operation queue, record map and operation-ID set. |
| C: Purposeful Agentic AI / RAG Workflow - Advanced | Document ingestion, relevant retrieval, grounded generation and citations. | Binary min-heap selecting top-K evidence for the live pipeline. |

**A - Data reconciliation**

- Parse at least two of CSV/JSON/XML; map fields and validate missing/malformed data.
- Normalize without erasing meaningful differences, retaining source identifiers.
- Use fuzzy comparisons and justified thresholds; distinguish confident,
  ambiguous and unrelated records. A score is not automatically a probability.
- Use indexed candidates without removing the fuzzy fallback and route
  ambiguity through the review queue.
- Expose the engine through a lightweight cloud HTTP interface.

**Practice:** reconcile small synthetic fixtures containing typos, a distinct
near-match and ambiguous pairs; export actual reconciliation/review results.
The third format and a polished review UI remain optional.

**B - Offline-first development**

- Use IndexedDB/PouchDB or equivalent device storage; distinguish durable
  records from in-memory UI state.
- Keep required app assets available offline; a service worker is one option,
  not the record database.
- Connect the queue/map/set to stable IDs, acknowledgments, retries and the
  selected conflict/deletion policy.
- Distinguish local persistence from the approved remote synchronization store.

**Practice:** create/edit/delete offline, reload, reconnect and sync against
the hosted backend; retry and resolve conflicts from two independent sessions.
Background sync and a polished UI are supplementary.

**C - Agentic AI and RAG**

- Distinguish model-only answers from retrieval-grounded outputs.
- Ingest permitted documents, handle formatting noise, chunk text and retain
  document/section metadata.
- Score candidate evidence, select it through the implemented heap, and
  generate grounded outputs with verifiable citations.
- Keep retrieve -> synthesize -> cite -> done bounded; treat retrieved
  instructions as untrusted data, not permission to execute commands.
- Report absent/conflicting evidence and model/retrieval failures explicitly.

**Practice:** evaluate a supported question, missing evidence and a service
failure against known sources. Ollama can support local development, but
confirm approved inference reachable from the hosted application. OCR,
model training, a managed vector database and unrestricted agents are not required.

### Module 5: Testing and Technical Validation

- **Unit tests:** check normalization, index buckets, queue/map/set operations
  or heap insertion/replacement and ranking.
- **Integration tests:** follow input through the real reconciliation,
  offline/sync or retrieval/generation workflow.
- **Boundary/failure tests:** cover malformed/missing input, empty results,
  duplicate IDs, retries, conflicts or heap K/tie cases as relevant.
- **Algorithm verification:** compare actual outputs with known expected
  results, not only whether the program ran.
- **Performance comparisons:** use the same inputs for indexed/linear lookup
  or heap/full-sort selection; record input size, timings and assumptions.
- **Repeatability:** preserve fixtures, configuration, commands and
  expected/observed results, including unsuccessful cases.

Use controlled test doubles for dependency-failure tests where appropriate
and label them. They do not replace evidence that the actual hosted workflow
works. Follow the [challenge acceptance checks](challenges.md).

### Module 6: Cloud Deployment with PrimeCloud

Learn the basic deployment workflow **before the hackathon where possible**,
then repeat it for your own application. You do not need to master every
PrimeCloud subsystem.

- Understand application containers and Git-based deployment from a known revision.
- Identify actual dependency/build/start commands and the application directory.
- Bind HTTP to `0.0.0.0:$PORT` and match the configured target port.
- Configure environment variables, protect credentials through supported
  secret facilities and provide a lightweight health check.
- Distinguish container-local files, persistent storage and managed database
  connections; confirm approved persistence for B.
- Confirm any inference connection required by C rather than assuming a
  laptop-only model is cloud-accessible.
- Verify deployment status, assigned HTTPS URL and real functionality;
  inspect build/runtime logs and relevant application monitoring.

**Practice:** deploy a minimal working interface with a health check, then
exercise one real challenge workflow from an independent browser/session.
Use the [PrimeCloud Deployment Guide](deployment.md) for the full procedure.
Confirm account/service allocations; no paid add-ons or shared keys are assumed.

### Module 7: Preparing for Technical Assessment

Prepare technical evidence, not a presentation:

- Working application and required challenge outputs.
- Integrated DSA code, complexity explanation and traces/comparisons.
- Tests, fixtures and expected/observed results, including failure cases.
- Accessible GitHub repository, README and declared dependencies/configuration.
- PrimeCloud live URL, health-check URL and deployed revision.
- Sanitized deployment-status and hosted-workflow evidence.
- SDG statement, team/contribution acknowledgments and the required
  2-3 minute backup demo video.

Have another teammate follow the README and repeat a representative test.
The backup video does not replace deployment. Every challenge uses the
[25/15/15/10/15/10/5/5 technical rubric](rules.md#judging-criteria), totaling
**100 points**, with dedicated DSA and deployment criteria.
**No slide deck or formal Track-Level oral pitch is required**;
presentation quality earns no points.

## Realistic two-day learning and build plan

The event is **12-13 November 2026**. Use these modules selectively; participants
are not expected to complete every pathway or all learning during the bootcamp.

- **Recommended pre-event preparation:** Git basics, programming/complexity
  foundations, the selected DSA task and a basic PrimeCloud deployment.
  Confirm runtime, starter materials or mentor-approved substitutes, account
  access and any required storage/inference.
- **Essential bootcamp focus:** explain the selected challenge's input/output,
  show how its DSA fits, and get a minimal HTTP/health-check deployment working.
  Use the remaining modules as references while building.
- **Day 1:** choose one challenge, divide work, build a small end-to-end
  baseline, integrate the DSA and deploy early.
- **Day 2:** complete functionality, repeat local/hosted failure and boundary
  tests, document results/limits and submit before the announced freeze.
- **Additional learning:** explore optional UI polish, deeper optimization or
  framework features only after mandatory functionality, DSA and deployment work.

Use the [curated resources](resources.md) for your pathway. They are references,
not a requirement to install every tool or read every subsystem guide.
