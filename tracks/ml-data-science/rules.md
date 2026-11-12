---
title: Track Rules & How to Compete
parent: Machine Learning & Data Science
nav_order: 3
---

# Track Rules & How to Compete

These rules cover the Machine Learning & Data Science track. Team size, eligibility, the Alumni/Finalist Collaborator requirement and conduct follow the [General Rules](../../general-rules.md).

## Format

- Each team chooses **one of the three challenges** (Beginner, Intermediate or Advanced) and builds a **working prototype** during the two-day event.
- **Day 1** is for ideation, data and a first working baseline. **Day 2** is for continued development, evaluation, documentation and a reproducible technical demonstration.
- Every team prepares a public code repository, a working implementation, the challenge-specific results and a written limitations note. **No slides or formal pitch are required for Track-Level Judging.**
- Choose the tier that fits your skills. **Beginner, Intermediate and Advanced are each assessed out of 100 points.** Difficulty does not multiply the score or award automatic extra points; the expected technical outcomes of your selected challenge determine the assessment.
- Every team **must tie its solution to at least one UN Sustainable Development Goal (SDG)** of its own choosing, and explain who the users are and what decision the system supports.

## Allowed tools and technology

**Allowed**
- Any programming language, although the starter kits use Python.
- Any open-source library, free tool or free cloud tier (for example Google Colab, Streamlit Community Cloud, Hugging Face Spaces).
- **Pre-trained models**, including open language, speech and image models, and free API tiers for language models. Cite every model and say how you used it.
- Open data from any source whose license allows your use, including the starter kits in `assets/`.
- AI coding assistants, as long as you **disclose** their use in your README and can explain the implementation during technical clarification questions.

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

Submit through the announced event channel by the published code freeze. A complete submission has:

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
| **Common submission information** | All | Team details, SDG statement, Alumni Contribution note, AI/external-resource acknowledgments and the required 2-3 minute backup demo video |

**Assessment preparation.** Have the app/notebook, permitted data or retrieval instructions, sample inputs, result tables and agent logs accessible. Include dependency versions and example configuration variables, not API keys or private data. For Challenge 3, have both roles and image/audio examples ready. Be able to rerun the documented evaluation and explain failures.

**Deadline.** Follow the [Schedule](../../schedule.md) and announced Day 2 code freeze. Changes pushed after the freeze are not judged. No slide deck or formal pitch is required for this technical assessment.

## Judging criteria

All three challenges use this **100-point technical rubric**.

| Criterion | Points | What your team must demonstrate |
|---|---|---|
| **Core functionality** | 30 | The selected challenge's data pipeline, models, app and evidence-grounded agent work end to end. |
| **Validation and technical correctness** | 25 | Appropriate held-out/time/spatial splits, no leakage, baseline comparisons, required metrics and uncertainty or failure analysis. For Challenge 3, include multimodal and answer/citation evaluation. |
| **SDG relevance and impact** | 15 | A specific user, supported decision and relevant SDG, with a credible connection to the demonstrated results. |
| **Responsible AI and security** | 10 | Privacy, group/area error analysis, appropriate refusals and honest limits. Include role-aware access control, adversarial checks and human hand-off where required. |
| **Reproducibility and documentation** | 10 | Clear README, dependency versions, data licenses and provenance; results can be rerun. Challenges 2 and 3 include the required one-command run. |
| **Creativity, approach and insight** | 10 | Justified design choices and useful insight from the data beyond simply assembling tools. |
| **Total** | **100** | **No pitch, slide-design or presentation allocation.** |

The [challenge-specific checkpoints](challenges.md#technical-assessment-checkpoints) explain how these criteria apply; they do not add points.

### What to expect

Every team undergoes technical inspection of functionality, code, configurations, datasets, documentation, generated outputs and evaluation results. You may be asked to run a sample, reproduce a metric or explain an implementation decision. A technical demonstration is evidence, **not a separately scored presentation**. Speaking style and pitching quality do not affect the Track-Level score.

## Scoring and tie-breakers

- Approximately **two to three judges** may assess each team. Each independently awards a score out of 100 using the published rubric. Your official Track-Level score is the **average**, with no difficulty multiplier.
- Example: `(85 + 90 + 88) / 3 = 87.67/100`. Teams rank by their final average scores.
- **Stretch goals** earn credit through the rubric (mainly rigor, creativity and impact). They do not add separate points.
- Complete, reproducible evidence can earn full credit for a requirement; partial or inconsistent evidence earns partial credit. Missing or unsupported work earns no credit for the affected requirement.
- **Tie-breakers**, in order:
  1. Higher average **Core functionality** sub-score
  2. Higher average **Validation and technical correctness** sub-score
  3. Higher average **Responsible AI and security** sub-score
  4. Panel deliberation on technical evidence

**Integrity.** Judges may ask any team member to explain how any part of the solution works, to rerun a result or to show the agent log. Results that cannot be reproduced or explained will be scored down.

The **top three teams** qualify for the **Grand Finale**. The highest-ranked team receives **Best AI, Data Science and Machine Learning Solution**.

## Day-of timeline for this track

The track follows the published event schedule and announced freeze. These are its preparation checkpoints:

| When | What happens |
|---|---|
| **Day 1, start** | Track briefing. Teams choose a challenge and an SDG. Starter kits are released |
| **Day 1, midday** | Teams have data loaded and a plan. Mentors visit teams |
| **Day 1, end: Checkpoint 1** | A working **baseline** with an evaluation: a first hazard indicator or map, a first model score, or a first working retrieval answer. Mentors check progress and help teams scope Day 2 |
| **Day 2, morning** | Build the remaining core requirements. Mentors available |
| **Day 2, midday: Checkpoint 2** | All core requirements working, even if rough. From here, work on testing, limitations and the demo. Do not start new features |
| **Day 2, code freeze** | Final push of code and submission of the repository link and documents |
| **Day 2, Track-Level Judging** | Technical inspection, demonstrations and short implementation clarification questions; no formal pitch |
| **Day 2, close** | Judges' deliberation and results |

**Advice for winning**
1. **Get an end-to-end baseline by the end of Day 1**, even a crude one, and improve it.
2. Build the **core requirements first**. Stretch goals count only if the core works.
3. **Compare with a baseline**, and be honest if your model does not beat it. Judges respect clear thinking.
4. **Split data the way the real world will test you**: by time for forecasts, by place for maps, by held-out items for retrieval and images.
5. **Show uncertainty and limits.** Say who the system might fail, and how you checked.
6. **Rehearse the technical checks**, with the app running, sample inputs ready and evaluation outputs easy to locate.