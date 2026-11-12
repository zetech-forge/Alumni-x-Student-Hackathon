---
title: Content & Curriculum
parent: Machine Learning & Data Science
nav_order: 1
---

# Content & Curriculum

Use this guide to prepare for your **selected challenge**, not to complete every module before building. The challenge scopes and technical minimums are unchanged. The modules below identify relevant skills; explanations and examples are linked from [Curated Resources](resources.md). There is no separate published Course page in this track.

The three challenges are **Climate Sentinel** (Beginner), **Malaria Atlas Lab** (Intermediate) and **Product Copilot** (Advanced). Read them on the [Challenges](challenges.md) page first, so you can see what you are preparing for.

## Learning objectives

By the end of the prep period, a participant should be able to:

- Load, clean, merge and summarize open data with Python and pandas
- Pull data from open files and APIs without exposing keys or ignoring licenses
- Read geospatial data, join it to a map, and measure area and distance correctly
- Train a baseline model, validate it honestly (by time, place or group), and explain it
- Build an AI agent that calls tools, cites its numbers, logs what it does and says "I don't know"
- Present results in a clear map, dashboard or story
- Audit a model for errors by group or area, protect privacy, and write a limitations note
- Package a project so another person can run it and reproduce its technical results
- Link a solution to at least one UN Sustainable Development Goal (SDG)

Beginners in Challenge 1 add: climate statistics (normals, anomalies, extremes, trends) and seasonal forecasting skill. Intermediate participants in Challenge 2 add: spatial statistics, uncertainty and epidemiology (prevalence mapping, presence-only data, meta-analysis of drug studies). Advanced participants in Challenge 3 add: multimodal AI (speech, image and text retrieval), access control for AI systems, and building a benchmark that measures hallucination.

## Prerequisite knowledge

| Level | What you should already know |
|---|---|
| **Beginner** | Basic Python, loading and summarizing tables, simple charts and school-level maths. Review the full weather/forecasting/mapping requirements before choosing Climate Sentinel. |
| **Intermediate** | Some Python (variables, loops, functions) and experience with tables of data, or a first model built in a class or tutorial. |
| **Advanced** | Comfortable with Python, pandas and scikit-learn, and Git. Some experience with at least one of: language-model applications, speech or image models, or building web apps and APIs. |

Not sure where to start? Load a small permitted CSV, inspect missing values and summarize it by group. If this is unfamiliar, begin with Python/pandas preparation and ask a mentor about the challenge workload.

## Topic breakdown

Module numbers are references within this guide. **●** marks a skill relevant to implementing that challenge and **○** marks supplementary study; neither means that every lesson must be completed before the event. Times are optional self-study estimates, not the Day 1 bootcamp agenda. Challenge 1 is Climate Sentinel, Challenge 2 is Malaria Atlas Lab and Challenge 3 is Product Copilot.

### Shared learning areas

| Module | Topic | Time | Ch. 1 | Ch. 2 | Ch. 3 | You will be able to |
|---|---|---|---|---|---|---|
| Setup | Python, Jupyter or Colab, Git | 1 h | ● | ● | ● | Run code and save work to GitHub |
| 0 | The SDGs and a problem-solving loop | 0.5 h | ● | ● | ● | Pick an SDG indicator and say what it can and cannot tell you |
| 1 | Python and notebooks | 2 h | ● | ● | ● | Read and write short scripts |
| 2 | Data wrangling with pandas | 4 h | ● | ● | ● | Clean, group, merge and resample data |
| 3 | Charts, dashboards and storytelling | 2 h | ● | ● | ● | Make honest charts and a simple dashboard |
| 4 | Statistics you actually need | 2 h | ● | ● | ○ | Compare groups and report the size of a difference |
| 5 | Finding and using open data | 2 h | ● | ● | ● | Call an API, keep keys safe, check licenses |
| 6 | Geospatial basics | 4 h | ● | ● | ○ | Join data to a map, use projections, compute population affected |
| 7 | Machine learning fundamentals | 4 h | ● | ● | ● | Train, validate and explain a model without leakage |
| 8 | LLMs and RAG | 4 h | ● | ● | ● | Prompt a model, ground answers in sources, say "I don't know" |
| 9 | AI agents and tool use | 3 h | ● | ● | ● | Build an agent with traceable tool calls |
| 10 | Responsible AI, privacy and security basics | 2 h | ● | ● | ● | Audit errors by group and write a model card |
| 11 | Ship it: repo, reproducibility, technical evidence | 3 h | ● | ● | ● | Package your work, reproduce results and demonstrate required functionality |

### Specialist modules (by challenge)

| Module | Topic | Time | Ch. 1 | Ch. 2 | Ch. 3 |
|---|---|---|---|---|---|
| 12 | Climate data, extremes and hazard indicators | 5 h | ● | ○ | |
| 13 | Time series and seasonal forecasting | 5 h | ● | ○ | |
| 14 | Spatial statistics, uncertainty and epidemiology | 6 h | ○ | ● | |
| 15 | Multimodal AI: speech, vision, OCR and retrieval | 6 h | | ○ | ● |
| 16 | Evaluating and securing LLM systems | 5 h | ○ | ● | ● |
| 17 | Data engineering and reproducibility | 4 h | | ● | ● |
| 18 | Uncertainty, fairness and MLOps | 4 h | ○ | ● | ● |

For Module 17, the parts about validation, idempotency, logging and one-command setup matter most.

## Suggested timeline

The event is **12-13 November 2026**. Prioritize a verified environment and data/model access, then build incrementally. A preparation exercise is not a reduced submission specification.

| Challenge | Essential preparation focus | Useful first checkpoint | Supplementary learning |
|---|---|---|---|
| Climate Sentinel - Beginner | Modules 1-7, 12-13 for data, weather indicators, maps and honest time-based evaluation; 8-11 for the required grounded advisory and delivery. | Load permitted weather data, document units/missing values, plot a climatology and compare an initial outlook with the required baselines. | Additional drought indices, vegetation signals and other listed stretch goals; do not download these before core inputs work. |
| Malaria Atlas Lab - Intermediate | Modules 2, 4-7, 14 and 17 for joins, projections, spatial validation and study uncertainty; 8-11 for the briefing workflow and delivery. | Map the available aggregate observations, verify joins/projections and reproduce a simple baseline with a spatial holdout. | Advanced MLOps, extra covariates, genomic clustering and other listed stretch goals. |
| Product Copilot - Advanced | Modules 2, 5, 8-11 and 15-17 for source metadata, multimodal inputs, role-aware retrieval and evaluation. | Ingest a few permitted product pages, verify role filtering before retrieval and run one text, image and audio example with source evidence. | Additional languages, offline optimization, mapping and other listed stretch goals. |

Across all pathways, Module 10's safety/privacy principles and Module 11's reproducible evidence are essential. Study additional modules as needed rather than treating the entire table as compulsory pre-event homework.

### Day 1 and Day 2

- **Before committing to a challenge:** inspect its full requirements and confirm the actual event pack, dataset permissions and model access. No starter bundle is currently published under this track; missing inputs need Technical Lead confirmation, not fabricated replacements.
- **Day 1:** verify the environment and sources, divide the work, inspect/clean inputs and establish an end-to-end baseline. Reserve time for the complete challenge, not just data downloads or model installation.
- **Day 2:** complete the specified functionality, evaluate using the required splits/metrics, test missing/unsafe inputs, document limitations and prepare the submission before freeze.

The retained research-heavy requirements depend on adequate preparation and accessible inputs. Ask the Technical Lead to resolve missing packs or access restrictions; these guidelines do not silently waive minimums or guarantee that a fresh data-access application will finish during the event.

## Before competition day

Track-Level Judging assesses each selected challenge out of **100 technical points**, without difficulty multipliers. Prepare the working implementation, data/sample inputs, evaluation results, logs and documents listed in the [rules](rules.md). You may demonstrate functionality and answer technical questions, but no slides or formal pitch are required and presentation quality earns no points.

The allocation is **30 technical methodology + 20 data quality/provenance + 15 evaluation + 15 responsible AI/safety + 10 reproducibility + 10 practical relevance/SDG alignment = 100**.

- [ ] Python (or a Colab account) and Git are working
- [ ] You have a GitHub account and a project repository ready
- [ ] You can run a language model for your agent: a local open model through Ollama, or a free API tier
- [ ] You have read the [rules](rules.md) and the [challenges](challenges.md), and have chosen a challenge and a draft SDG
- [ ] Confirmed access and permitted use for required data; an application alone does not guarantee availability, and patient-level records remain prohibited
- [ ] Optional: QGIS installed for checking map layers, and a Streamlit account for hosting your demo
- [ ] Optional for Challenge 3: Colab access if useful; free GPU capacity is not guaranteed, so confirm a workable model/runtime alternative