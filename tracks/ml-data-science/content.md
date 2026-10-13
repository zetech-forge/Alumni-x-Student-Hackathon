---
title: Content & Curriculum
parent: Machine Learning & Data Science
nav_order: 1
---

# Content & Curriculum

This is the self-study plan to complete **before** competition day. The full lessons, with explanations, code and exercises, are on the [Course](course.md) page. This page tells you what to learn, in what order and how long it takes, depending on the challenge you plan to attempt. Links to external tutorials, datasets and tools are on [Curated Resources](resources.md).

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
- Package a project so another person can run it, and present it in 5 minutes
- Link a solution to at least one UN Sustainable Development Goal (SDG)

Beginners in Challenge 1 add: climate statistics (normals, anomalies, extremes, trends) and seasonal forecasting skill. Intermediate participants in Challenge 2 add: spatial statistics, uncertainty and epidemiology (prevalence mapping, presence-only data, meta-analysis of drug studies). Advanced participants in Challenge 3 add: multimodal AI (speech, image and text retrieval), access control for AI systems, and building a benchmark that measures hallucination.

## Prerequisite knowledge

| Level | What you should already know |
|---|---|
| **Beginner** | Basic computer skills and school-level maths. No programming experience is needed. |
| **Intermediate** | Some Python (variables, loops, functions) and experience with tables of data, or a first model built in a class or tutorial. |
| **Advanced** | Comfortable with Python, pandas and scikit-learn, and Git. Some experience with at least one of: language-model applications, speech or image models, or building web apps and APIs. |

Not sure where you fit? Try the Module 2 exercise on the Course page (load a CSV and summarize it by group). If it takes more than an hour, start at the beginning.

## Topic breakdown

Module numbers match the [Course](course.md) page. In the table, **●** means the module is needed for that challenge and **○** means it is helpful. Challenge 1 is Climate Sentinel, Challenge 2 is Malaria Atlas Lab and Challenge 3 is Product Copilot.

### Core modules (everyone)

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
| 11 | Ship it: repo, reproducibility, pitch | 3 h | ● | ● | ● | Package your work and deliver a 5-minute pitch |

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

### Beginners (Challenge 1): 14 days, about 2 hours a day

| Day | Study | Checkpoint |
|---|---|---|
| 0 | Setup | Run `print("hello")` and push a notebook to GitHub |
| 1 | Modules 0 and 1 | |
| 2 to 3 | Module 2 | |
| 4 | Module 3 | |
| 5 | Module 4 | |
| 6 | Module 5 | |
| 7 | Catch-up and **Checkpoint 1** | A short data story from weather data for one city |
| 8 | Module 6 | |
| 9 to 10 | Module 7 | |
| 11 | Module 12 (climate indicators) | |
| 12 | Module 9 and the agent part of Module 8 | |
| 13 | Module 10 | |
| 14 | Module 11 and **Checkpoint 2** | A mini Climate Sentinel, with README and a 5-minute pitch |

If you have less than two weeks, do Setup, Modules 1, 2, 5, 6, 7, 12 and 9 first. Those give you the biggest return for Challenge 1.

### Intermediate (Challenge 2): 2 weeks, 1 to 2 hours a day

| Week | Focus |
|---|---|
| Week 1 | Skim Modules 2, 5, 6 and 7 and fix gaps, especially honest validation (Module 7). Read Modules 8, 9 and 10. |
| Week 2 | Study Module 14 (spatial statistics and epidemiology) and the pipeline parts of Module 17. Build a half-day mini version: fit a prevalence model on a few dozen survey points with spatial cross-validation, and pool three made-up drug studies with a random-effects meta-analysis. |

### Advanced (Challenge 3): flexible

| Phase | Focus |
|---|---|
| Phase 1 | Study Module 15 (speech, OCR, image and text retrieval) and Module 8 (RAG). Build a retrieval prototype over five manuals and measure how often the right page is retrieved. |
| Phase 2 | Study Module 16 (evaluation and access control) and Module 9 (agents). Prototype the riskiest piece first: role-aware retrieval and the adversarial tests. |
| Phase 3 | Practice the one-command build and evaluation (Module 17), and draft your model card and limitations note. |

## Before competition day

- [ ] Python (or a Colab account) and Git are working
- [ ] You have a GitHub account and a project repository ready
- [ ] You can run a language model for your agent: a local open model through Ollama, or a free API tier
- [ ] You have read the [rules](rules.md) and the [challenges](challenges.md), and have chosen a challenge and a draft SDG
- [ ] Applied for any data that needs registration or approval (for example DHS, WWARN, MalariaGEN)
- [ ] Optional: QGIS installed for checking map layers, and a Streamlit account for hosting your demo
- [ ] Optional for Challenge 3: a Google Colab account for free GPU time (speech and vision models)