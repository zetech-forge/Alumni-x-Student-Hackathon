---
title: Curated Resources
parent: Software Development
nav_order: 2
---

# Software Development: Curated Resources

## General
| Resource | Type | Free/Paid | Why it's useful |
|---|---|---|---|
| [GitHub Docs: About pull requests](https://docs.github.com/en/pull-requests) | Reference | Free | You'll need this to collaborate as a team under time pressure |
| [UN Sustainable Development Goals](https://sdgs.un.org/goals) | Reference | Free | Read the 17 goals before picking your specific angle |

## Challenge A -- Data reconciliation & fuzzy search
| Resource | Type | Free/Paid | Why it's useful |
|---|---|---|---|
| [RapidFuzz docs](https://github.com/maxbachmann/RapidFuzz) | Library + docs | Free | Fast, ready-to-use fuzzy string matching -- don't write Levenshtein distance by hand |
| [Real Python: Fuzzy String Matching](https://realpython.com/fuzzywuzzy-python/) | Tutorial | Free | Practical walkthrough of fuzzy matching concepts and code |
| [pandas documentation](https://pandas.pydata.org/docs/) | Reference | Free | Handy for reading/merging CSV, JSON data if you're using Python |

## Challenge B -- Offline-first resource tracker
| Resource | Type | Free/Paid | Why it's useful |
|---|---|---|---|
| [MDN: IndexedDB API](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API) | Reference | Free | Browser-native local storage for offline-first apps |
| [PouchDB](https://pouchdb.com/) | Library + docs | Free | Higher-level offline storage with built-in sync -- faster to get working than raw IndexedDB |
| [web.dev: Offline-first design](https://web.dev/articles/offline-cookbook) | Guide | Free | Patterns for handling the offline/sync problem well |
| [Tailwind CSS docs](https://tailwindcss.com/docs) | Library + docs | Free | Quick, clean UI without hand-writing CSS |

## Challenge C -- Agentic AI / RAG workflow
| Resource | Type | Free/Paid | Why it's useful |
|---|---|---|---|
| [LangChain docs](https://python.langchain.com/docs/introduction/) | Framework + docs | Free (API calls may cost) | Common framework for building RAG pipelines fast |
| [LlamaIndex docs](https://docs.llamaindex.ai/) | Framework + docs | Free (API calls may cost) | Alternative to LangChain, often simpler for pure retrieval/citation use cases |
| [Ollama](https://ollama.com/) | Local model runner | Free | Run a model locally -- no API key or internet dependency during the event |
| [Pinecone: What is RAG?](https://www.pinecone.io/learn/retrieval-augmented-generation/) | Explainer | Free | Clear conceptual overview of retrieve → augment → generate |

## Tools & setup
Decide and install your team's stack in advance -- don't spend hackathon time on environment setup. If you're attempting Challenge C, confirm with organizers in advance whether a shared API key or a local Ollama setup will be available at the venue, since relying on live external API calls for ~150 participants on shared wifi is risky.
