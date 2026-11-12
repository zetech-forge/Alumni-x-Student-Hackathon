---
title: Track Rules & How to Compete
parent: Software Development
grandparent: Hackathon Tracks
nav_order: 3
---

# Software Development: Track Rules & How to Compete

## Format
Each team picks **one** [challenge](challenges.md) and builds a working implementation during the two-day event. You do not need to attempt all three. Team size, eligibility, the Alumni/Finalist Collaborator requirement and conduct follow the [General Rules](../../general-rules.md). Explain your team's own contribution and the specific SDG your solution supports.

## Allowed tools & tech
- Any programming language, framework, or library.
- You may use any third-party library or API as long as it's publicly available or provided by organizers.
- Credit reused code, datasets, models and libraries. Disclose significant AI assistance and be able to explain your implementation.
- Use synthetic or appropriately licensed public sample data. Do not expose personal information, passwords or API keys in code, logs, demonstrations or hosted models.
- Keep secrets outside the repository; provide example environment variables and setup instructions without credentials.
- Develop and test only in environments your team controls or is explicitly authorized to use. For Challenge C, confirm model access before relying on an external API; organizer-provided credentials are not guaranteed.

## Submission and assessment preparation

Submit through the announced event channel by the submission freeze in the [Schedule](../../schedule.md). Prepare:

- An accessible repository with source code, dependencies and a README naming the selected challenge, setup/run commands, approach and limitations.
- A runnable application or pipeline, sample inputs and relevant test results. Provide a live URL only if applicable.
- A **2-3 minute backup demo video**, the SDG statement, team details, Alumni Contribution note and AI/external-resource acknowledgments required by the General Rules.
- **Challenge A:** supported-format examples, unified output, match-accuracy/runtime results and ambiguous-match review examples.
- **Challenge B:** an offline-capable build, two-device or equivalent test setup, sync/conflict evidence and your conflict-resolution policy.
- **Challenge C:** permitted source documents, the bounded workflow, cited sample answers and evidence for missing-source or model/API failures.

Have the implementation ready to run. No slide deck or formal pitch is required for Track-Level Judging.

## Judging criteria

Every selected challenge has the same maximum of **100 points**. Selecting a more demanding challenge does not multiply the score or award automatic extra points.

| Criterion | Points | What your team must demonstrate |
|---|---:|---|
| Functionality and correctness | 30 | The selected challenge's required input-to-output workflow works, including its challenge-specific checkpoints. |
| Testing, reliability and responsible handling | 25 | Repeatable tests, relevant edge/failure cases, accurate results and safe handling of data, conflicts or unavailable services. |
| Code quality and documentation | 15 | Understandable implementation, reproducible setup and clear explanation of your code, dependencies and limitations. |
| Creativity and approach | 15 | A justified design that addresses the selected problem; useful improvements must actually work. |
| SDG and social-impact alignment | 15 | A specific user need, a relevant SDG and a credible explanation of how the demonstrated implementation helps. |
| **Total** | **100** | **Technical assessment only.** |

The [challenge checkpoints](challenges.md#technical-assessment-checkpoints) explain how this rubric applies to each build. Partial or inconsistent implementations receive credit only for the requirements supported by evidence; unsupported claims receive no credit for the affected requirement.

### What to expect

Every team undergoes technical inspection: required functionality tests, source-code/configuration and documentation review, verification of outputs, and short questions about implementation decisions. You may be asked to run the solution or repeat a test. A demonstration supplies technical evidence; it is **not a separately scored presentation**. Slides, speaking style and pitching quality earn no Track-Level points.

## Scoring and tie-breakers

Approximately **two to three judges** may assess each team. Each independently awards a score out of 100 using the rubric above. Your official Track-Level score is the **average** of those scores, and teams are ranked from highest to lowest average.

For example: `(85 + 90 + 88) / 3 = 87.67/100`.

Ties are resolved by the higher average **Functionality and correctness** sub-score, then **Testing, reliability and responsible handling**, followed by panel deliberation on technical evidence if needed. Presentation quality is not a tie-breaker.

The **top three teams** qualify for the **Grand Finale**. The highest-ranked team receives **Best Software Development Solution**.

## Day-of timeline

Use Day 1 to select a challenge and get a baseline running. Use Day 2 for core functionality, tests, documentation and a reproducible technical demonstration. Follow the published schedule and announced freeze; do not rely on unconfirmed model access for Challenge C.
