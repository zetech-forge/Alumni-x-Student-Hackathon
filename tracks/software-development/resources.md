---
title: Curated Resources
parent: Software Development
grandparent: Hackathon Tracks
nav_order: 2
---

# Software Development: Curated Resources

Use resources for **your selected challenge**; the tools below are alternatives, not a checklist of mandatory installations. All listed documentation is free to read. Hosted model/API usage may have costs or limits.

## Shared preparation

| Resource | Use it for |
|---|---|
| [GitHub: Pull requests](https://docs.github.com/en/pull-requests) | Collaborating, reviewing changes and resolving conflicts. |
| [UN Sustainable Development Goals](https://sdgs.un.org/goals) | Selecting a relevant goal and explaining the intended beneficiary and useful outcome. |

## Challenge A -- Backend Data Reconciliation & Fuzzy Search

**Beginner focus:** parsing two supported formats, consistent normalization, similarity thresholds and ambiguous-match review. Start with small synthetic examples before the full dataset.

| Resource | Use it for |
|---|---|
| [RapidFuzz documentation](https://rapidfuzz.github.io/RapidFuzz/) | Practical fuzzy-comparison functions and examples; use a library rather than implementing edit distance from scratch. |
| [pandas documentation](https://pandas.pydata.org/docs/) | Optional Python table/file loading, cleaning, joining and exporting. A simpler parser is also valid. |

Neither Python nor pandas is mandatory if your chosen language handles the required formats and matching correctly.

## Challenge B -- Offline-First Resource Tracker

**Intermediate focus:** durable local records, pending changes, reconnect/retry behavior and a tested conflict policy.

| Resource | Use it for |
|---|---|
| [MDN: IndexedDB API](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API) | Browser-native persistent structured storage. IndexedDB does not itself synchronize data to a server. |
| [PouchDB: Conflicts](https://pouchdb.com/guides/conflicts.html) | The alternative database/replication approach and why applications must still handle conflicts. Replication needs a compatible endpoint. |
| [web.dev: Offline Cookbook](https://web.dev/articles/offline-cookbook) | Supplementary patterns for keeping application assets available offline; distinguish caching from record synchronization. |
| [Tailwind CSS documentation](https://tailwindcss.com/docs) | Optional UI styling only; visual polish is not a separate assessment category. |

Use browser developer tools to simulate disconnection and separate profiles/devices to test independent offline edits. A small local sync service or compatible replication endpoint is sufficient; a production deployment is not required.

## Challenge C -- Purposeful Agentic AI / RAG Workflow

**Advanced focus:** relevant retrieval, source metadata, grounded generation/citations, bounded execution and failure evaluation.

| Resource | Use it for |
|---|---|
| [Pinecone: Retrieval-Augmented Generation](https://www.pinecone.io/learn/retrieval-augmented-generation/) | The retrieve/context/generate concepts. The explainer does not make a Pinecone account or managed database mandatory. |
| [LangChain: Retrieval](https://docs.langchain.com/oss/python/langchain/retrieval) | Optional retrieval/context components. Keep the challenge's workflow bounded rather than adopting unrestricted agent examples. |
| [LlamaIndex framework documentation](https://developers.llamaindex.ai/python/framework/) | An alternative document-ingestion/retrieval toolkit; configure the model and embedding provider deliberately. |
| [Ollama quickstart](https://docs.ollama.com/quickstart) | Install Ollama and follow the **local-model** route. Download a suitable model and confirm hardware capacity before relying on it. |
| [Ollama API introduction](https://docs.ollama.com/api/introduction) | Distinguish the local server from cloud endpoints when configuring your application. |

LangChain/LlamaIndex are optional open-source frameworks, **not free access to every model provider**. For a local-only setup, select local generation and embeddings explicitly and download what is needed beforehand. Hosted/free-tier alternatives are subject to approval, access and quotas; paid services are not required and organizer-supplied keys are not guaranteed. Never commit credentials or send private data to a hosted model.

## Setup and starter access

- Install Git, an editor and only your project's required runtime/dependencies. Follow its README and manifest; there is no universal install command for all three choices.
- The [starter-materials notice](challenges.md#starter-materials-and-setup) lists the original event-pack contents and the current download-availability gap. Ask the mentor for the pack or approved substitute inputs; these resource links are not a starter repository.
- Follow the [curriculum pathway](content.md) and [implementation/acceptance steps](challenges.md), then prepare the [required submission](rules.md#submission-and-assessment-preparation).
