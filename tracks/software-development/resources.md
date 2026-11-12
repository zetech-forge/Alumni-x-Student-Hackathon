---
title: Curated Resources
parent: Software Development
grand_parent: Hackathon Tracks
nav_order: 2
---

# Software Development: Curated Resources

Start with shared basics, your selected challenge and the
[PrimeCloud Deployment Guide](deployment.md). Do not read every course or
install every listed tool.

**Essential** identifies a required concept or relevant deployment instruction,
not a mandatory programming language/library. Language-specific references
apply when using that language; equivalent implementations are allowed.
**Supplementary** means an optional tool, alternative or deeper explanation.
All references are free to read; hosted services can have costs and limits.
Follow documentation matching your project's declared runtime/dependencies.

## Shared resources

| Resource | What it covers | Supports | Priority |
|---|---|---|---|
| [Official Git tutorial](https://git-scm.com/docs/gittutorial) | Repository setup, snapshots, commits and basic branching/merging; pair with GitHub collaboration guidance. | A, B, C | Essential |
| [GitHub pull-request documentation](https://docs.github.com/en/pull-requests) | Branch-based collaboration, reviews and conflict resolution. | A, B, C | Essential |
| [Princeton: Analysis of Algorithms](https://algs4.cs.princeton.edu/14analysis/) | Algorithm cost models, growth rates, memory and empirical performance; examples use Java, but the concepts are language-independent. | A, B, C | Essential concepts |
| [UN Sustainable Development Goals](https://sdgs.un.org/goals) | Choose a relevant goal and connect the user problem, beneficiary and intended outcome. | A, B, C | Essential |

## Challenge A -- Backend Data Reconciliation & Fuzzy Search

**Beginner focus:** the hash-map index and FIFO review queue must support the
existing normalization, fuzzy matching and traceable human-review workflow.

| Resource | What it covers | Supports | Priority |
|---|---|---|---|
| [Python dictionaries](https://docs.python.org/3/builtins/stdtypes.html#dict) | Key-value indexing and updates. Store a list of record references per normalized key rather than overwriting duplicate-key records. | A; B backend alternative | Essential DSA reference |
| [Python deque](https://docs.python.org/3/library/collections.html#collections.deque) | Efficient queue insertion/removal and FIFO processing; choose an equivalent queue representation in another language. | A, B | Essential DSA reference |
| [RapidFuzz documentation](https://rapidfuzz.github.io/RapidFuzz/) | Similarity functions for fuzzy comparisons; thresholds and ambiguous decisions remain your application's responsibility. | A | Supplementary tool |
| [Python CSV parsing](https://docs.python.org/3/library/csv.html) | Reading structured CSV rows and handling format options. | A | Essential if CSV is selected |
| [Python JSON parsing](https://docs.python.org/3/library/json.html) | Loading/validating JSON structures and reporting parse failures. | A | Essential if JSON is selected |
| [Python ElementTree](https://docs.python.org/3/library/xml.etree.elementtree.html) | Parsing XML elements and mapping fields; follow its security guidance for untrusted input. | A | Essential if XML is selected |
| [pandas documentation](https://pandas.pydata.org/docs/) | Optional tabular data loading and transformation; not a replacement for the required index/review logic. | A | Supplementary tool |

Select at least two supported formats, not necessarily all three. Python,
pandas and a particular matching library are not mandatory. Begin with small
synthetic fixtures; compare linear/indexed lookup on identical keys and records.

## Challenge B -- Offline-First Resource Tracker

**Intermediate focus:** durable queued operations, record/change tracking,
operation-ID deduplication and consistent conflicts/deletions.

| Resource | What it covers | Supports | Priority |
|---|---|---|---|
| [MDN: IndexedDB API](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API) | Durable browser records and pending work; IndexedDB does not itself synchronize with a server. | B | Essential concepts; browser option |
| [MDN: Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) | JavaScript key-value record/state tracking. Keep queued history separately from a map's latest state. | B; A JavaScript alternative | Essential DSA reference |
| [MDN: Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set) | Unique operation-ID membership and duplicate detection; an in-memory set alone is not durable deduplication. | B | Essential DSA reference |
| [PouchDB getting started](https://pouchdb.com/guides/) | An alternative local database/replication approach and compatible server requirements. | B | Supplementary tool |
| [PouchDB conflicts](https://pouchdb.com/guides/conflicts.html) | Detecting and resolving conflicts; replication does not remove the need for a tested conflict policy. | B | Supplementary tool |
| [web.dev: Offline Cookbook](https://web.dev/articles/offline-cookbook) | Keeping necessary application assets available offline; caching is separate from the record database. | B | Essential concepts; browser examples |
| [MDN: Idempotent](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent) | Why repeating a request can repeat a state change; safe POST-based synchronization requires application-level operation IDs/deduplication. | B | Essential concepts |

Use the queue reference above or your language's equivalent. Persist pending
operations and deduplication state; a JavaScript array's front-removal operation
is not a constant-time queue implementation. Test two isolated sessions,
reconnection, lost acknowledgments and conflicts against the PrimeCloud-hosted
sync backend and approved persistent store. A local-only service is insufficient.

## Challenge C -- Purposeful Agentic AI / RAG Workflow

**Advanced focus:** implement the bounded heap selector inside retrieval,
preserve citation metadata and keep generation grounded and bounded.

| Resource | What it covers | Supports | Priority |
|---|---|---|---|
| [Princeton: Priority Queues](https://algs4.cs.princeton.edu/24pq/) | Binary heaps, min/max priorities and operation costs; apply these principles to bounded top-K selection. | C | Essential concepts |
| [Python heapq](https://docs.python.org/3/library/heapq.html) | Binary min-heap primitives and priority-queue considerations. Implement the bounded selection loop; a ready-made top-K call does not satisfy the task. | C | Essential DSA reference |
| [Pinecone: Retrieval-Augmented Generation](https://www.pinecone.io/learn/retrieval-augmented-generation/) | Retrieval/context/generation concepts; no Pinecone account or managed vector database is required. | C | Supplementary explainer |
| [LangChain retrieval](https://docs.langchain.com/oss/python/langchain/retrieval) | Optional document loading/splitting, retrieval and context integration; do not bypass the required heap selector. | C | Supplementary framework |
| [LlamaIndex framework documentation](https://developers.llamaindex.ai/python/framework/) | Alternative document ingestion, chunk/source metadata and retrieval components; configure model/embedding access deliberately. | C | Supplementary framework |
| [Ollama quickstart](https://docs.ollama.com/quickstart) | Local model setup; download a suitable model and check hardware capacity before relying on it. | C | Supplementary local-model route |
| [Ollama API introduction](https://docs.ollama.com/api/introduction) | Local-server API configuration and the distinction from a cloud inference endpoint. | C | Supplementary local-model route |

Use the shared algorithm-analysis resource for time/space reasoning and compare
heap/full-sort results on the same candidates and tie order. LangChain and
LlamaIndex are optional, not free access to all model providers. Local Ollama
does not alone satisfy cloud delivery: confirm approved inference reachable
from PrimeCloud. Paid AI access and organizer-supplied keys are not guaranteed.
Never commit credentials or send private data to a hosted model.

## PrimeCloud deployment resources

PrimeCloud deployment is mandatory for all three challenges. Start with the
[Software Development Deployment Guide](deployment.md), then consult only
the relevant official sections below.

| Resource | What it covers | Supports | Priority |
|---|---|---|---|
| [PrimeCloud official website](https://primecloud.cloud/) | Provider overview; confirm approved event/workspace access, not assumed free entitlements. | A, B, C | Essential orientation |
| [PrimeCloud documentation](https://primecloud.cloud/docs) | Platform documentation index and links to the required configuration topics. | A, B, C | Essential reference |
| [Quickstart](https://primecloud.cloud/docs/quickstart) | Basic deployment, runtime binding, health checks and initial verification. | A, B, C | Essential |
| [Application deployment](https://primecloud.cloud/docs/applications) | Git/source deployment, application lifecycle and runtime behavior. | A, B, C | Essential |
| [Configuration](https://primecloud.cloud/docs/configuration) | Build/start configuration, environment settings and relevant persistence controls. | A, B, C | Essential |
| [Security and secrets](https://primecloud.cloud/docs/security) | Supported secret/Vault facilities, credentials and access controls. | A, B, C | Essential |
| [System limits](https://primecloud.cloud/docs/limits) | Runtime/lifecycle limits and account-dependent constraints to check before assessment. | A, B, C | Essential relevant sections |
| [Production blueprints and troubleshooting](https://primecloud.cloud/docs/guides) | Optional deployment patterns and diagnostic runbooks; not a requirement for production-grade infrastructure or paid services. | A, B, C | Supplementary |

The Organising Committee must confirm workspaces, trials/credits, database or
storage allocations and permitted services. Do not purchase add-ons or assume
free upgrades. B needs approved persistent remote storage; C needs approved
cloud-reachable inference. The guide explains these dependencies without
requiring every team to master every platform subsystem.

## Setup and starter access

- Install Git, an editor and only your project's required runtime/dependencies. Follow its README and manifest; there is no universal install command for all three choices.
- The [starter-materials notice](challenges.md#starter-materials-and-setup) lists the original event-pack contents and the current download-availability gap. Ask the mentor for the pack or approved substitute inputs; these resource links are not a starter repository.
- Follow the [curriculum pathway](content.md) and [implementation/acceptance steps](challenges.md), then prepare the [required submission](rules.md#submission-and-assessment-preparation).
- The [100-point rubric](rules.md#judging-criteria) includes mandatory DSA and
  deployment. Prepare technical evidence, not a slide deck or formal Track-Level pitch.
