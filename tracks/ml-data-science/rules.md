---
title: Track Rules & How to Compete
parent: Machine Learning & Data Science
nav_order: 3
---

# Track Rules & How to Compete

These rules cover what is specific to the Machine Learning & Data Science track. Team size, eligibility and conduct are in the general rules, so they are not repeated here.

## Format

- Each team chooses **one of the three challenges** (Beginner, Intermediate or Advanced) and builds a **working prototype** during the two-day event.
- **Day 1** is for ideation, data and a first working baseline. **Day 2** is for continued development, testing and pitch preparation, and it ends with **live demonstrations and pitches**.
- Every team delivers: a public code repository, a working demo, a short written limitations note, and a 5-minute live pitch.
- Teams choose the tier that fits their skills. Harder challenges carry more points, but they are also harder to finish. A complete, honest solution to an easier challenge can beat an unfinished solution to a harder one.
- Every team **must tie its solution to at least one UN Sustainable Development Goal (SDG)** of its own choosing, and explain who the users are and what decision the system supports.

## Allowed tools and technology

**Allowed**
- Any programming language, although the starter kits use Python.
- Any open-source library, free tool or free cloud tier (for example Google Colab, Streamlit Community Cloud, Hugging Face Spaces).
- **Pre-trained models**, including open language, speech and image models, and free API tiers for language models. Cite every model and say how you used it.
- Open data from any source whose license allows your use, including the starter kits in `assets/`.
- AI coding assistants, as long as you **disclose** their use in your README and can explain and defend every part of your solution in the Q&A. *(Organizers: confirm this matches the general rules.)*

**Not allowed**
- Real personal data, including real patient, household, customer or contact records. Use public aggregated data or synthetic data only.
- Passing private or sensitive data into hosted AI services.
- Committing passwords or API keys to your repository.
- Presenting simulated, modelled or synthetic results as real-world measurements.
- Giving clinical advice. In Challenge 2 the system supports programme planning only, and must refuse requests for individual diagnosis or dosing.
- Copying proprietary manuals, price lists or images that you do not have the right to use (Challenge 3). Respect every license and site's terms of use.
- Attacking, scanning or overloading any system you do not own, including the public data services and APIs you use. Security testing is limited to **your own system**.
- Using someone else's solution without credit.

**Data rules.** Record every data source, access date and license in `DATA.md`. Respect rate limits on public APIs. If a data service needs registration, register before the event. Some malaria and survey datasets need an application or an agreement to terms of use, so apply early.

## Submission requirements

Submit through the event submission channel *(organizers: add the form or platform here)*. A complete submission has:

| Item | Required for | Notes |
|---|---|---|
| **Public repository link** | All | README with the problem, users, chosen SDG, and how to run. `requirements.txt` (or equivalent) and `DATA.md` |
| **Working demo** | All | A running app, dashboard or notebook the judges can open, or a live demo on your machine |
| **Notebook or report with results** | All | The metrics asked for in your challenge, and honest comparisons with baselines |
| **Limitations and model card note** | All | One page: intended use, results overall and by group or area, known weaknesses, misuse risks |
| **Agent log** | Challenges 1 and 2 | Every tool call for the required test questions, including the human approval step |
| **Action playbook with citations** | Challenge 1 | Hazard levels and the cited actions the agent is allowed to recommend |
| **Assumptions file** | Challenge 2 | `ASSUMPTIONS.md`: data biases, covariate choices and modelling assumptions |
| **Evaluation benchmark, results and security note** | Challenge 3 | 60 or more questions with reference answers, adversarial results before and after defenses, and the access-control note |
| **One-command run** | Challenges 2 and 3 | A command or short script that rebuilds the main results |
| **5-minute pitch** | All | Live, at the end of Day 2 |

**Deadline.** Submissions close at the **code freeze on Day 2**, which is announced at the start of the event *(organizers: add the exact time; we suggest about two hours before the pitches start)*. Changes pushed after the freeze are not judged. Teams may use the remaining time to rehearse their pitch.

## Judging criteria and weights

All teams are scored out of 100 using this rubric.

| Criterion | Weight | What judges look for |
|---|---|---|
| **Technical rigor and functionality** | 30% | The core requirements work end to end. Validation is honest (time, spatial or group splits where needed), with no leakage, uncertainty is reported, and results are compared with a baseline |
| **SDG relevance and impact** | 15% | A clearly chosen SDG, a clear user and decision, and a realistic path to use |
| **Responsible AI and security** | 10% | Errors checked by group or area, privacy respected, safe refusals, limits stated honestly. For Challenge 3, mainly the access control, adversarial testing and human hand-off |
| **Reproducibility and documentation** | 10% | A judge can rerun your work. Clear README, pinned dependencies, data sources and licenses. For Challenges 2 and 3, also tests and a one-command run |
| **Creativity, approach and insight** | 10% | A sensible, original approach, and insight from the data beyond the minimum |
| **Pitch and presentation** | 25% | A clear 5-minute story: the problem, the approach, a live demo, the results, honest limits and the impact. Clear answers to questions |

**Challenge-specific notes** are in each challenge on the [Challenges](challenges.md) page. They explain how a criterion applies to that challenge, and they do not add new criteria.

## Scoring and tie-breakers

- **Final score** = (rubric score ÷ 100) × the challenge's points. For example, a team scoring 80 on Challenge 2 earns 0.80 × 200 = 160 points. A team scoring 90 on Challenge 1 earns 0.90 × 100 = 90 points.
- Scores are given by a panel of judges. Each judge scores independently, and the final rubric score is the **average**. Judges may adjust a score after Q&A if the team could not explain the work.
- **Stretch goals** earn credit through the rubric (mainly rigor, creativity and impact). They do not add separate points.
- A criterion is scored zero if the required item is missing (for example, no limitations note means no credit for the honest-limits part of Responsible AI).
- **Tie-breakers**, in order:
  1. Higher **Technical rigor and functionality** score
  2. Higher **Pitch and presentation** score
  3. Higher **SDG relevance and impact** score
  4. The judging panel's vote

**Integrity.** Judges may ask any team member to explain how any part of the solution works, to rerun a result or to show the agent log. Results that cannot be reproduced or explained will be scored down.

## Day-of timeline for this track

The track follows the general event schedule. These are the track's own checkpoints. *(Organizers: add clock times that match the general schedule.)*

| When | What happens |
|---|---|
| **Day 1, start** | Track briefing. Teams choose a challenge and an SDG. Starter kits are released |
| **Day 1, midday** | Teams have data loaded and a plan. Mentors visit teams |
| **Day 1, end: Checkpoint 1** | A working **baseline** with an evaluation: a first hazard indicator or map, a first model score, or a first working retrieval answer. Mentors check progress and help teams scope Day 2 |
| **Day 2, morning** | Build the remaining core requirements. Mentors available |
| **Day 2, midday: Checkpoint 2** | All core requirements working, even if rough. From here, work on testing, limitations and the demo. Do not start new features |
| **Day 2, code freeze** | Final push of code and submission of the repository link and documents |
| **Day 2, pitches** | Live 5-minute pitch per team, followed by questions from the judges |
| **Day 2, close** | Judges' deliberation and results |

**Advice for winning**
1. **Get an end-to-end baseline by the end of Day 1**, even a crude one, and improve it.
2. Build the **core requirements first**. Stretch goals count only if the core works.
3. **Compare with a baseline**, and be honest if your model does not beat it. Judges respect clear thinking.
4. **Split data the way the real world will test you**: by time for forecasts, by place for maps, by held-out items for retrieval and images.
5. **Show uncertainty and limits.** Say who the system might fail, and how you checked.
6. **Practice the pitch with a timer**, with the demo already running. Show one chart at a time, and say the finding aloud.