---
title: Content & Curriculum
parent: Machine Learning & Data Science
nav_order: 1
---

# Content & Curriculum

This is the self-study plan to complete **before** competition day. The full lessons, with explanations, code and exercises, are on the [Course](course.md) page. This page tells you what to learn, in what order, and how long it takes. Links to external tutorials, datasets and tools are collected on [Curated Resources](resources.md).

## Learning objectives

By the end of the prep period, a participant should be able to:

- Load, clean, merge and summarize open data with Python and pandas
- Choose and build a clear chart, map or dashboard, and tell a short data story
- Test whether a difference is real, and report its size and uncertainty
- Pull data from open files and APIs without exposing keys or ignoring licenses
- Read and map geospatial data, and avoid common projection and join mistakes
- Train a baseline model, validate it honestly (by time, place or group), and explain it
- Build a simple retrieval-augmented (RAG) chatbot and an AI agent that uses tools
- Test a system for fairness, privacy and basic AI security risks, and document limits
- Package a project so another person can run it, and present it in 5 minutes
- Link a solution to at least one UN Sustainable Development Goal (SDG)

Intermediate and advanced participants add one or more specialist skills: satellite imagery, forecasting, deep learning and edge deployment, optimization and simulation, data and streaming engineering, anomaly detection, reinforcement learning, advanced AI security, and uncertainty and MLOps.

## Prerequisite knowledge

| Level | What you should already know |
|---|---|
| **Beginner** | Basic computer skills and school-level maths. No programming experience is needed. |
| **Intermediate** | Some Python (variables, loops, functions) and experience with tables of data, or a first model built in a class or tutorial. |
| **Advanced** | Comfortable with Python, pandas and scikit-learn, and Git. Experience with at least one specialist area (geospatial, deep learning, NLP, data engineering or reinforcement learning). |

Not sure where you fit? Try the Module 2 exercise on the Course page (load a CSV and summarize it by group). If it takes more than an hour, start at the beginning.

## Topic breakdown

Module numbers match the [Course](course.md) page. "Core" modules suit every participant. "Specialist" modules are for intermediate and advanced participants, and you pick the ones that match your target challenge.

### Core modules

| Module | Topic | Time | You will be able to |
|---|---|---|---|
| Setup | Python, Jupyter or Colab, Git | 1 h | Run code and save work to GitHub |
| 0 | The SDGs and a problem-solving loop | 0.5 h | Pick an SDG indicator and say what it can and cannot tell you |
| 1 | Python and notebooks | 2 h | Read and write short scripts |
| 2 | Data wrangling with pandas | 4 h | Clean, group, merge and resample data |
| 3 | Charts, dashboards and storytelling | 2 h | Make honest charts and a simple dashboard |
| 4 | Statistics you actually need | 2 h | Run a hypothesis test and report effect size |
| 5 | Finding and using open data | 2 h | Call an API, keep keys safe, check licenses |
| 6 | Geospatial basics | 4 h | Join data to a map and compute population affected |
| 7 | Machine learning fundamentals | 4 h | Train, validate and explain a model without leakage |
| 8 | LLMs and RAG | 4 h | Build a chatbot that cites sources and says "I don't know" |
| 9 | AI agents and tool use | 3 h | Build an agent with traceable tool calls |
| 10 | Responsible AI, privacy and security basics | 2 h | Audit errors by group and write a model card |
| 11 | Ship it: repo, reproducibility, pitch | 3 h | Package your work and deliver a 5-minute pitch |

### Specialist modules

| Module | Topic | Time | Most useful for challenges |
|---|---|---|---|
| 12 | Satellite imagery and remote sensing | 6 h | 3, 9, 10, 14, 17, 20, 21, 24 |
| 13 | Time series and forecasting | 5 h | 6, 11, 21 |
| 14 | Deep learning, computer vision and edge deployment | 6 h | 13, 14, 15, 20, 21 |
| 15 | Optimization and simulation | 5 h | 9, 12, 22 |
| 16 | Data engineering, streaming and observability | 6 h | 7, 13, 19, 22, 23 |
| 17 | Anomaly detection and trajectory analysis | 5 h | 19, 23 |
| 18 | Reinforcement learning for control | 6 h | 22 |
| 19 | Advanced AI security and multi-agent systems | 6 h | 18, 23, 24 |
| 20 | Uncertainty, fairness and MLOps | 5 h | 11, 15, 17, 19, 20, 21 |

The Course page ends with a **Challenge-to-Module Map** showing the core modules for each of the 24 challenges.

## Suggested timeline

### Beginners: 14 days, about 2 hours a day

| Day | Study | Checkpoint |
|---|---|---|
| 0 | Setup | Run `print("hello")` and push a notebook to GitHub |
| 1 | Modules 0 and 1 | |
| 2 to 3 | Module 2 | |
| 4 | Module 3 | |
| 5 | Module 4 | |
| 6 | Module 5 | |
| 7 | Catch-up and **Checkpoint 1** | A 5-chart data story from air-quality data |
| 8 | Module 6 | |
| 9 to 10 | Module 7 | |
| 11 | Module 8 | |
| 12 | Module 9 | |
| 13 | Module 10 | |
| 14 | Module 11 and **Checkpoint 2** | A mini version of a Beginner challenge, with README and 5-minute pitch |

If you have less than two weeks, do Setup, Modules 1, 2, 3, 5 and 11 first. Those give you the biggest return for a Beginner challenge.

### Intermediate: 2 weeks, 1 to 2 hours a day

| Week | Focus |
|---|---|
| Week 1 | Skim Modules 2 to 7 and fix gaps, especially honest validation (Module 7). Read Modules 10 and 11. |
| Week 2 | Pick two specialist modules that match your target challenge and complete their exercises. Build a half-day mini version of your challenge. |

### Advanced: flexible

| Phase | Focus |
|---|---|
| Phase 1 | Use the Challenge-to-Module Map. Study the core modules for your target challenge in full. |
| Phase 2 | Prototype the riskiest part first (data access, validation design, or the security test). |
| Phase 3 | Draft your limitations, failure-mode analysis and monitoring plan. |

## Before competition day

- [ ] Python (or a Colab account) and Git are working
- [ ] You have registered for any services your chosen challenge needs: OpenAQ (API key), Global Fishing Watch, the DHS Program (GPS data takes time to approve), Google Earth Engine, Copernicus
- [ ] You have read the [rules](rules.md) and the [challenges](challenges.md)
- [ ] You have chosen two or three challenges that fit your team's skills
- [ ] You have a GitHub account and a project repository ready
