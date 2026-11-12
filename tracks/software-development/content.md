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
| B: Offline-First Resource Tracker - Intermediate | Application CRUD, JavaScript/browser concepts or comparable mobile development, and simple client/server requests. | Production cloud infrastructure or advanced distributed systems. |
| C: Purposeful Agentic AI / RAG Workflow - Advanced | Confident programming, APIs, document processing and basic retrieval/LLM concepts. | Training a language model, paid APIs or a managed vector database. |

Everyone needs basic Git usage and a working editor/runtime for their chosen stack. Use a supported runtime version compatible with your project's dependencies and record it in the README.

## Topic breakdown

### Module 1: Git & GitHub essentials (everyone)
Practice branches, commits, pull requests and resolving a simple merge conflict. Create your own repository, ignore secrets/generated files and record reused code. **Preparation exercise:** another team member can obtain your code and run a minimal example. Suggested focused practice: 1-2 hours if new to Git.

### Module 2: Follow your selected challenge pathway

**2A - Beginner: data reconciliation and fuzzy search**

- Learn parsing for two of CSV/JSON/XML, schema mapping, whitespace/case normalization and missing-field validation.
- Use a similarity library such as RapidFuzz; understand exact vs fuzzy matches, threshold choices and false matches.
- Separate confident reconciliations from human-review cases, retaining source traceability.
- Implement normalized-key hash-map buckets that retain multiple record references and a FIFO review queue; compare indexed and linear lookup.
- **Practice:** reconcile a few synthetic records with typos, a distinct near-match and an ambiguous pair; export reconciled/review results.
- Focus on the Challenge A section of [Curated Resources](resources.md). Suggested practice: 2-3 hours; the third format and a review UI are optional.

**2B - Intermediate: offline-first resource tracking**

- Learn IndexedDB/PouchDB or equivalent device storage; distinguish persistent state from in-memory UI state.
- Understand pending changes, stable IDs, acknowledgments/retries, deletions and a simple conflict policy.
- Implement the durable FIFO queue, record map and operation-ID set; test server-side deduplication when an acknowledgment is lost.
- For browser apps, learn how to keep needed assets available offline; a service worker is one option, not the record database.
- **Practice:** create/edit/delete offline, reload, reconnect and sync; repeat sync and resolve conflicting edits from two isolated sessions.
- Focus on the Challenge B section of [Curated Resources](resources.md). Suggested practice: 2-3 hours; background sync and richer UI are supplementary.

**2C - Advanced: purposeful agentic AI / RAG**

- Distinguish model-only answers from retrieval-grounded outputs and a defined, multi-step workflow.
- Learn chunking/source metadata, relevant retrieval, context-based generation and verifiable citations.
- Implement bounded binary min-heap top-K selection, deterministic ties and metadata retention; compare with full sorting on the same candidates.
- Bound tool execution and retries, handle absent evidence/service failure and treat document instructions as untrusted data.
- **Practice:** use a few permitted documents for one supported question, one missing-answer case and one model/retrieval failure; inspect the source support.
- Focus on the Challenge C section of [Curated Resources](resources.md). Suggested practice: 3-4 hours; install/download a usable local model beforehand if choosing Ollama for development, and confirm approved inference reachable from the cloud app. OCR, model training and advanced agents are supplementary, not prerequisites.

### Module 3: Preparing technical evidence (everyone)
Practice the selected challenge's [acceptance scenarios](challenges.md). Keep expected and observed results, sample inputs/outputs, configuration examples and limitations together with your code. Have another team member follow the README. Prepare the required 2-3 minute backup demo video and common submission details. Suggested focused practice: about 1 hour.

Follow the [PrimeCloud Deployment Guide](deployment.md) to prepare the HTTP
interface, runtime port, health check, secret configuration and any approved
persistence/inference dependencies. Practice the DSA trace/comparison and repeat
the core workflow through the assigned HTTPS URL, not only localhost.

Every challenge uses the [35/20/15/15/5/10 technical rubric](rules.md#judging-criteria), totaling **100 points**. No slides or formal Track-Level pitch are required; presentation quality earns no points.

## Suggested timeline

The event is **12-13 November 2026**. The practice durations above are learning estimates, not a requirement to complete all pathways before building.

- **Before starting:** confirm runtime/Git, the event materials or approved substitutes, and PrimeCloud access. For B, confirm remote persistence; for C, confirm cloud-reachable inference without assuming shared keys.
- **Day 1:** choose one challenge, divide work and deploy a minimal baseline early. Integrate the relevant DSA while addressing matching ambiguity, offline conflict handling or grounded retrieval.
- **Day 2:** complete mandatory behavior, DSA and hosted verification, document complexity/results/limits and submit before the announced freeze.

Use the [curated resources](resources.md) to fill gaps as needed. Do not spend the build window trying every framework.
