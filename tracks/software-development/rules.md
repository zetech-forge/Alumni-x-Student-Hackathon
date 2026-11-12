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
- You may use third-party libraries, frameworks and APIs that you have permission to use; respect licenses, service terms and rate limits. A paid service is not required.
- Credit reused code, datasets, models and libraries. Disclose significant AI assistance and be able to explain your implementation.
- Use synthetic or appropriately licensed public sample data. Do not expose personal information, passwords or API keys in code, logs, demonstrations or hosted models.
- Keep secrets outside the repository; provide example environment variables and setup instructions without credentials.
- Develop and test only in environments your team controls or is explicitly authorized to use. For Challenge C, confirm model access before relying on an external API; organizer-provided credentials are not guaranteed.
- An original solution may build on starters and credited examples, but submitting someone else's project or a pre-existing finished solution as event work is not permitted. State what the starter already did and what your team implemented.
- For Challenge C, use a small, fixed workflow with bounded tool execution. Retrieved documents and model output are untrusted input, not permission to execute commands or change the workflow.

## Submission and assessment preparation

Submit through the announced event channel by the submission freeze in the [Schedule](../../schedule.md). Prepare:

- An accessible GitHub repository with source code, dependency manifest/lockfile where applicable, required non-secret configuration and a README naming the challenge and difficulty, technology stack, setup/run/test commands, approach and limitations.
- A runnable application or pipeline, sample inputs and relevant test results. Provide a live URL only if applicable.
- A **2-3 minute backup demo video**, the SDG statement, team details, Alumni Contribution note and AI/external-resource acknowledgments required by the General Rules.
- **Challenge A:** examples in at least two supported formats, reconciled output, unresolved/review output, matching results and accuracy/runtime evidence.
- **Challenge B:** an offline-capable build, two-device or equivalent test setup, sync/conflict evidence and your conflict-resolution policy.
- **Challenge C:** permitted source documents, the bounded workflow, cited sample answers and evidence for missing-source or model/API failures.

Have the implementation ready to run. No slide deck or formal pitch is required for Track-Level Judging.

Follow the [challenge deliverable checklist](challenges.md#deliverables-for-every-challenge). A command-line/backend solution is valid for A; a polished graphical interface is not required. B can use a local synchronization service or suitable replication endpoint, without a production cloud deployment. C does not require training a model, buying API credits or running an open-ended agent.

## Judging criteria

Every selected challenge has the same maximum of **100 points**. Selecting a more demanding challenge does not multiply the score or award automatic extra points.

| Criterion | Points | What your team must demonstrate |
|---|---:|---|
| Core functionality and correctness | 35 | The selected challenge's mandatory input-to-output behavior works, with correct records, synchronized state or grounded outputs. |
| Technical design and implementation | 20 | Suitable architecture, data structures and implementation decisions: matching/review policy, persistence/sync strategy or bounded retrieval workflow. |
| Testing, reliability and edge cases | 15 | Repeatable normal, failure and boundary tests, with actual results and relevant limitations. |
| Code quality, documentation and reproducibility | 15 | Maintainable source, dependency/configuration instructions and a repeatable way to run the solution and its tests. |
| Security, privacy and responsible engineering | 5 | Appropriate validation, safe data/credential handling and relevant access or tool-execution restrictions. |
| Practical relevance and SDG alignment | 10 | A specific user need, a useful demonstrated application and a credible SDG connection without unsupported impact claims. |
| **Total** | **100** | **Technical assessment only.** |

The [challenge checkpoints](challenges.md#technical-assessment-checkpoints) explain how this rubric applies to each build. Partial or inconsistent implementations receive credit only for the requirements supported by evidence; unsupported claims receive no credit for the affected requirement.

### What to expect

Every team undergoes technical inspection: required functionality tests, source-code/configuration and documentation review, verification of outputs, and short questions about implementation decisions. You may be asked to run the solution or repeat a test. A demonstration supplies technical evidence; it is **not a separately scored presentation**. Slides, speaking style and pitching quality earn no Track-Level points.

## Scoring and tie-breakers

Approximately **two to three judges** may assess each team. Each independently awards a score out of 100 using the rubric above. Your official Track-Level score is the **average** of those scores, and teams are ranked from highest to lowest average.

For example: `(85 + 90 + 88) / 3 = 87.67/100`.

Ties are resolved by the higher average **Core functionality and correctness** sub-score, then **Testing, reliability and edge cases**, followed by panel deliberation on technical evidence if needed. Presentation quality is not a tie-breaker.

The **top three teams** qualify for the **Grand Finale**. The highest-ranked team receives **Best Software Development Solution**.

## Day-of timeline

Use Day 1 to select a challenge and get a baseline running. Use Day 2 for core functionality, tests, documentation and a reproducible technical demonstration. Follow the published schedule and announced freeze; do not rely on unconfirmed model access for Challenge C.
