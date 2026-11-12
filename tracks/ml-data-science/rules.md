---
title: Track Rules & How to Compete
parent: Machine Learning & Data Science
grand_parent: Hackathon Tracks
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

The [challenge specifications](challenges.md) retain their existing technical requirements and minimums. Choose after reviewing them, not from the difficulty label alone. Climate Sentinel needs basic Python/data analysis plus preparation for its weather, mapping and agent workflow; Malaria Atlas Lab adds spatial/statistical modelling; Product Copilot requires multimodal integration, retrieval and access-control evaluation. The [curriculum](content.md) maps preparation to those requirements.

## Allowed tools and technology

**Allowed**
- Any programming language; Python and its data-science libraries are the recommended pathway, not a requirement to use every listed tool.
- Any open-source library, free tool or free cloud tier (for example Google Colab, Streamlit Community Cloud, Hugging Face Spaces).
- **Pre-trained models**, including open language, speech and image models, and free API tiers for language models. Cite every model and say how you used it.
- Licensed public, aggregated or synthetic data appropriate to the selected challenge. No downloadable starter kit or `assets/` data directory is currently published under this track; obtain any event pack and its access instructions from the Technical Lead.
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

### Dataset and model access

- Inspect the actual event pack before assuming a dataset, notebook, pretrained model, image set or audio set is supplied. The [resource guide](resources.md) describes the existing sources and access conditions; it does not guarantee their inclusion in a pack.
- Confirm access before selecting a pipeline that depends on approval-only data. Ask the Technical Lead to confirm a suitable permitted alternative if access is unavailable; do not silently reduce the challenge minimums or invent observations.
- Use local/open models or an accessible approved free tier. Shared API keys, paid subscriptions and free GPU availability are **not guaranteed**. Hosted services can require your own credentials and have quotas; model weights also have licenses and hardware requirements.
- A local Ollama model and compatible local embeddings can avoid hosted-model credentials. Download what is needed and explicitly select local components; a framework may otherwise use a hosted provider by default.
- Read the supplied project's README/manifest for setup commands. Do not assume there is a universal install or run command for this track.

## Data quality, evaluation and responsible AI

- Record what each column represents, its units, spatial/temporal coverage and whether values are observed, modelled or synthetic. Check types, duplicates, joins, missing values and impossible values; explain exclusion or imputation.
- Define the analytical target and evaluation split before fitting. Fit preprocessing and learned thresholds on training data only. Use time-based splits for forecasts, spatial/group holdouts for geographic predictions and held-out examples for product/image/audio evaluation.
- Use the metrics and baseline comparisons required by the selected challenge. Report sample counts, per-location/group or modality failures and uncertainty where relevant. A high score without a valid methodology is not evidence of a better solution.
- Keep numerical calculations in code tools, retain provenance for agent claims, log tool calls and handle missing evidence honestly. Apply the required human approval/hand-off and refusal behavior.
- Test Product Copilot's permissions before retrieval, not only in a prompt. Evaluate whether citations support answers, whether calculations match code outputs and whether restricted information remains inaccessible.
- Treat weather results as planning support, malaria results as research/programme analysis and product answers as document-grounded assistance. Predictions do not establish medical causation or provide diagnosis, dosing, official warnings or certified engineering advice.
- Explain bias, uncertainty and deployment limits. Performance on a small benchmark or supplied dataset does not establish real-world validity; distinguish measured results from projections and model confidence from verified accuracy.

## Submission requirements

Submit through the announced event channel by the published code freeze. A complete submission has:

| Item | Required for | Notes |
|---|---|---|
| **Public GitHub repository link** | All | README with challenge/difficulty, problem, users, SDG, technology stack and setup/run/test steps. Dependency versions, non-secret configuration and `DATA.md` |
| **Working demo** | All | A running app, dashboard or notebook the judges can open, or a live demo on your machine |
| **Notebook or report with results** | All | The metrics asked for in your challenge, and honest comparisons with baselines |
| **Limitations and model card note** | All | One page: intended use, results overall and by group or area, known weaknesses, misuse risks |
| **Agent log** | All | Required tool calls and their outputs; include the specified question tests and approval step for Challenges 1 and 2, and Product Copilot's tool log |
| **Action playbook with citations** | Challenge 1 | Hazard levels and the cited actions the agent is allowed to recommend |
| **Assumptions file** | Challenge 2 | `ASSUMPTIONS.md`: data biases, covariate choices and modelling assumptions |
| **Evaluation benchmark, results and security note** | Challenge 3 | 60 or more questions with reference answers, adversarial results before and after defenses, and the access-control note |
| **Reproducible rebuild/run** | Challenges 2 and 3 | Challenge 2 permits one command or a short, clear sequence to rebuild main results. Challenge 3 requires its one-command knowledge-base build/evaluation; document app startup separately |
| **Common submission information** | All | Team details, SDG statement, Alumni Contribution note, AI/external-resource acknowledgments and the required 2-3 minute backup demo video |

**Assessment preparation.** Have the app/notebook, permitted data or retrieval instructions, sample inputs, result tables and agent logs accessible. Include dependency versions and example configuration variables, not API keys or private data. For Challenge 3, have both roles and image/audio examples ready. Be able to rerun the documented evaluation and explain failures.

Do not duplicate large organizer-supplied datasets in your repository. Reference their version/location and provide the code needed to regenerate processed outputs; redistribute data only when its license permits it. Include trained models or model identifiers/configuration only as needed to reproduce your results. Methodology, test results and limitations can live in notebooks/README sections rather than redundant separate reports; retain specifically required files such as `DATA.md` and `ASSUMPTIONS.md`.

**Deadline.** Follow the [Schedule](../../schedule.md) and announced Day 2 code freeze. Changes pushed after the freeze are not judged. No slide deck or formal pitch is required for this technical assessment.

## Judging criteria

All three challenges use this **100-point technical rubric**.

| Criterion | Points | What your team must demonstrate |
|---|---|---|
| **Technical functionality and methodology** | 30 | The selected challenge's required pipeline, analytical/model methods, app and evidence-grounded agent work correctly; choices and assumptions are explained. |
| **Data quality, provenance and validation** | 20 | Traceable licensed sources, understood units/coverage, appropriate cleaning and joins, missing-value handling and valid preprocessing/evaluation splits. |
| **Model/system evaluation and baseline comparison** | 15 | Required metrics, appropriate held-out tests and required baseline comparisons; inspect failures rather than reporting only the best aggregate score. |
| **Responsible AI, safety, privacy and uncertainty** | 15 | Safe data use, bias/uncertainty analysis, grounded claims, required refusals and human oversight; Product Copilot also enforces permissions and tests adversarial inputs. |
| **Reproducibility and documentation** | 10 | Clear README, dependency versions, data licenses and provenance; results can be rerun. Challenge 2 permits a command or short sequence; Challenge 3 requires the specified one-command build/evaluation. |
| **Practical relevance and SDG alignment** | 10 | A specific user and supported decision, a relevant SDG and realistic usefulness/limitations without unverified impact or clinical claims. |
| **Total** | **100** | **No pitch, slide-design or presentation allocation.** |

The [challenge-specific checkpoints](challenges.md#technical-assessment-checkpoints) explain how these criteria apply; they do not add points.

### What to expect

Every team undergoes technical inspection of functionality, code, configurations, datasets, documentation, generated outputs and evaluation results. You may be asked to run a sample, reproduce a metric or explain an implementation decision. A technical demonstration is evidence, **not a separately scored presentation**. Speaking style and pitching quality do not affect the Track-Level score.

## Scoring and tie-breakers

- Approximately **two to three judges** may assess each team. Each independently awards a score out of 100 using the published rubric. Your official Track-Level score is the **average**, with no difficulty multiplier.
- Example: `(85 + 90 + 88) / 3 = 87.67/100`. Teams rank by their final average scores.
- **Stretch goals** can provide stronger evidence within the same rubric. They do not add separate points or increase the maximum.
- Complete, reproducible evidence can earn full credit for a requirement; partial or inconsistent evidence earns partial credit. Missing or unsupported work earns no credit for the affected requirement.
- **Tie-breakers**, in order:
  1. Higher average **Technical functionality and methodology** sub-score
  2. Higher average **Model/system evaluation and baseline comparison** sub-score
  3. Higher average **Responsible AI, safety, privacy and uncertainty** sub-score
  4. Panel deliberation on technical evidence

**Integrity.** Judges may ask any team member to explain how any part of the solution works, to rerun a result or to show the agent log. Results that cannot be reproduced or explained will be scored down.

The **top three teams** qualify for the **Grand Finale**. The highest-ranked team receives **Best AI, Data Science and Machine Learning Solution**.

## Day-of timeline for this track

The track follows the published event schedule and announced freeze. These are its preparation checkpoints:

| When | What happens |
|---|---|
| **Day 1, start** | Track briefing. Confirm the selected challenge's data/model access and any event-pack distribution, then choose a challenge and SDG |
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