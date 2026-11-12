---
title: Software Development
nav_order: 1
parent: Hackathon Tracks
has_children: true
---

# Software Development

Build a working application or backend workflow for a specific user need during the two-day hackathon, **12-13 November 2026**. Teams practice implementation, data handling, testing and reproducible delivery, and explain how their solution supports a UN Sustainable Development Goal (SDG).

## Choose one challenge

Each team selects **ONE** challenge, not all three:

| Challenge | Difficulty | What you will build | Useful background |
|---|---|---|---|
| A: Backend Data Reconciliation & Fuzzy Search | Beginner | A backend or command-line workflow that normalizes inconsistent records, finds fuzzy matches and separates uncertain cases for human review. | Basic programming, functions, lists/tables and reading files. |
| B: Offline-First Resource Tracker | Intermediate | An application with persistent local records, offline CRUD and reliable synchronization/conflict handling when connectivity returns. | Application development, JavaScript/browser storage or equivalent mobile storage, and basic APIs. |
| C: Purposeful Agentic AI / RAG Workflow | Advanced | A bounded document-ingestion, retrieval, generation and citation workflow for a defined task. | Confident programming, APIs and basic document retrieval/LLM concepts; evaluation and failure handling matter more than model training. |

Beginners are welcome, but should be able to write and run a small program in their chosen language. Every team needs basic Git/GitHub collaboration skills. **Learn the tools for your selected challenge; beginners do not need to master offline synchronization or AI frameworks to attempt Challenge A.**

## Tools and expected outcomes

Any suitable language or framework is permitted. For A, Python with RapidFuzz/pandas is one option, not a requirement. For B, IndexedDB or PouchDB can support a browser app; comparable mobile tooling is acceptable. For C, LangChain or LlamaIndex are optional helpers, and Ollama supports local development; the deployed application needs approved inference access reachable from PrimeCloud. Paid AI access and organizer-supplied keys are not assumed. Use an editor, Git and the runtime required by your own project; not every participant needs every runtime.

Finish with accessible source code, a working implementation, reproducible setup instructions, relevant sample inputs/outputs and test evidence. The [challenge instructions](challenges.md) distinguish mandatory behavior from optional improvements and explain the status of the listed starter materials.

## Mandatory DSA and cloud delivery

Every team must complete the original challenge, its integrated **DSA task**
and a **working PrimeCloud deployment**:

- **A:** normalized-key hash-map indexing and a FIFO ambiguous-match review queue.
- **B:** a durable FIFO sync queue, record map, operation-ID set and conflict algorithm.
- **C:** bounded binary min-heap top-K selection integrated into the RAG pipeline.

Explain complexity and provide the required tests/comparisons. Submit the
assigned HTTPS URL, health check and hosted-workflow evidence. Follow the
[PrimeCloud Deployment Guide](deployment.md); confirm account access and any
storage/inference arrangements early. No polished A frontend, custom domain
or production-grade cloud architecture is required.

## Technical assessment

Every team receives a **100-point technical assessment** against its selected challenge's requirements, without a difficulty multiplier. Approximately two to three judges may inspect your implementation, tests, outputs and documentation; their independent scores are averaged to rank teams. You may demonstrate functionality and answer technical questions, but **no slides or formal pitch are required and presentation quality earns no points**. The top three teams qualify for the Grand Finale; the highest-ranked team receives **Best Software Development Solution**.

The common allocation is **25 functionality + 15 DSA + 15 PrimeCloud deployment +
10 technical design + 15 testing + 10 code/documentation + 5 security/privacy +
5 practical relevance = 100 points**. See the [full rubric](rules.md#judging-criteria)
and [challenge-specific checkpoints](challenges.md#technical-assessment-checkpoints).

See [Content & Curriculum](content.md) to prepare, [Curated Resources](resources.md) for tools and docs, [Track Rules & How to Compete](rules.md) for judging and submission details, and [Challenges](challenges.md) for the full problem statements.
