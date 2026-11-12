---
title: Track Rules & How to Compete
parent: Software Development
grand_parent: Hackathon Tracks
nav_order: 3
---

# Software Development: Track Rules & How to Compete

## Format
Each team picks **one** [challenge](challenges.md) and completes its original functionality, integrated DSA task and mandatory PrimeCloud deployment during the two-day event. You do not need to attempt all three challenges. Team size, eligibility, the Alumni/Finalist Collaborator requirement and conduct follow the [General Rules](../../general-rules.md). Explain your team's own contribution and the specific SDG your solution supports.

All three challenges have the same **100-point maximum**. Selecting Advanced
Challenge C instead of Beginner Challenge A does not automatically earn more
points. Complete the selected challenge's requirements, not only its optional
improvements.

## Mandatory Data Structures and Algorithms

DSA is a required technical component of every challenge. Integrate the
structures and algorithm into the **actual application**, not a disconnected
exercise or a theoretical description.

| Challenge | Required implementation | Required supporting evidence |
|---|---|---|
| A - Beginner | Hash-map-based record indexing and a FIFO queue for ambiguous-match review. | Normalized-key lookup, multiple records per key without overwriting, ordered review, and linear/indexed lookup comparison. |
| B - Intermediate | FIFO synchronization queue, hash map for record/change tracking and an operation-ID set for duplicate detection, integrated with the conflict strategy. | Durable pending work, FIFO processing, map/set use, failed-request retry, lost-acknowledgment deduplication and conflicting copies/deletion tests. |
| C - Advanced | Bounded binary min-heap top-K selection and ranking in the RAG retrieval pipeline. | Heap construction/insertion/replacement, heap-property checks, deterministic ties, metadata preservation and comparison with full sorting. |

Supply relevant tests and a short explanation of **time and space complexity**,
including assumptions and persistence/network costs where relevant. Standard
language-provided hash maps and queues are allowed; implementing them from
scratch is not required.

For C, implement and test the **binary heap selection algorithm** that supplies
the retrieved evidence. Merely accepting a library or database's ready-made
top-K result does not meet the requirement. Follow the
[challenge-specific DSA acceptance checks](challenges.md) for boundaries,
comparisons and integration evidence.

## Mandatory Cloud Deployment — PrimeCloud

Every team must deploy its completed solution to **PrimeCloud**:

- [PrimeCloud platform](https://primecloud.cloud/)
- [Official documentation](https://primecloud.cloud/docs)
- [Official quickstart](https://primecloud.cloud/docs/quickstart)

Follow the separate [PrimeCloud Deployment Guide](deployment.md):

1. Prepare and test a working local implementation.
2. Push the source and required non-secret project files to GitHub.
3. Access the authorized PrimeCloud account/workspace.
4. Connect the repository or use the officially supported CLI.
5. Configure build/start commands, runtime port, environment variables,
   secrets and any approved storage/model connections.
6. Deploy the application.
7. Verify deployment status, the intended revision, HTTPS access and health.
8. Test the main challenge functionality through the hosted URL.

| Challenge | Mandatory hosted functionality |
|---|---|
| A | Expose actual reconciliation through a cloud-accessible service/API, even if the core engine is a CLI or library. Return matching, reconciled and ambiguous-review results. |
| B | Deploy the offline-capable application and cloud synchronization service, with approved persistent remote storage. Hosting must not replace offline functionality. |
| C | Deploy the RAG application/API, including implemented heap-based top-K retrieval, grounded generation and citations. Approved inference must be reachable from the hosted application. |

A static landing page, repository, local-only application or healthy endpoint
without the real workflow is insufficient. Use PrimeCloud's **assigned HTTPS
URL**; no custom domain is required.

## Deployment security and data handling

- Never commit API keys, passwords or database credentials.
- Never upload real secret-bearing `.env` files to the repository, application
  image or submission. Supply example configuration without secret values.
- Configure credentials through PrimeCloud's supported application
  configuration and secret-management/Vault facilities; keep them server-side.
- Do not expose private database credentials in frontend code, URLs, logs,
  screenshots, health responses or README files.
- Use synthetic or approved sample datasets, not real sensitive personal
  information.
- Do not deploy unauthorized or harmful functionality. Work only within
  systems and services your team controls or is explicitly authorized to use.
- Expose a suitable health endpoint, normally `GET /healthz`, and follow the
  documented listen-address, target-port, health and shutdown requirements in
  the [deployment guide](deployment.md).

## Allowed tools & tech
- Any programming language, framework, or library.
- You may use third-party libraries, frameworks and APIs that you have permission to use; respect licenses, service terms and rate limits. Additional paid APIs are not required. Confirm approved PrimeCloud access and costs before provisioning; do not assume event credits or incur unapproved charges.
- Credit reused code, datasets, models and libraries. Disclose significant AI assistance and be able to explain your implementation.
- Use synthetic or appropriately licensed public sample data. Do not expose personal information, passwords or API keys in code, logs, demonstrations or hosted models.
- Keep secrets outside the repository; provide example environment variables and setup instructions without credentials.
- Develop and test only in environments your team controls or is explicitly authorized to use. For Challenge C, confirm model access before relying on an external API; organizer-provided credentials are not guaranteed.
- An original solution may build on starters and credited examples, but submitting someone else's project or a pre-existing finished solution as event work is not permitted. State what the starter already did and what your team implemented.
- For Challenge C, use a small, fixed workflow with bounded tool execution. Retrieved documents and model output are untrusted input, not permission to execute commands or change the workflow.

## Submission and assessment preparation

Submit through the announced event channel by the submission freeze in the [Schedule](../../schedule.md). Prepare:

1. An accessible GitHub repository.
2. Source code, required dependency manifests/lockfiles and non-secret configuration.
3. A README naming the challenge/difficulty, technology stack, implementation approach, setup/run/test/deployment steps and known limitations.
4. Relevant tests and expected/observed results, including failures and boundaries.
5. DSA implementation details, time/space complexity and required traces/comparisons.
6. The assigned PrimeCloud HTTPS application URL and health-check URL.
7. Sanitized deployment verification evidence, deployed revision and hosted-workflow results.
8. Challenge-specific outputs and evidence listed below.
9. A specific SDG statement explaining the user problem, beneficiary and intended impact.
10. Team details, Alumni Contribution note and relevant AI/external-resource acknowledgments required by the General Rules.

Challenge-specific evidence:

- **A:** inputs in at least two supported formats, reconciliation/review/matching outputs, accuracy/runtime results, index buckets, FIFO review and linear/indexed lookup comparison.
- **B:** an offline-capable build, two-session tests, queue/map/set implementation, sync/conflict/deletion policy, retry/deduplication and remote-persistence evidence.
- **C:** permitted documents, the bounded workflow, heap trace/full-sort comparison, cited outputs and missing-evidence/model/retrieval failure results.

Retain the required **2-3 minute backup demo video**. It supports the common
submission but **does not replace mandatory PrimeCloud deployment**.

Have the implementation ready to run. No slide deck or formal pitch is required for Track-Level Judging.

Follow the [challenge deliverable checklist](challenges.md#deliverables-for-every-challenge)
and [PrimeCloud Deployment Guide](deployment.md). A's engine may be a CLI/library
but needs a cloud-accessible interface; no polished frontend is required.
B needs the hosted application/sync backend and approved persistent remote
storage, not only a local sync service. C needs approved inference reachable
from the hosted RAG application, not only a laptop model. Training/hosting a
full model, buying AI API credits and a custom domain are not required.

## Judging criteria

Every selected challenge has the same maximum of **100 points**. Selecting a more demanding challenge does not multiply the score or award automatic extra points.

| Criterion | Points | What your team must demonstrate |
|---|---:|---|
| Core functionality and correctness | 25 | The selected challenge's original mandatory behavior works correctly: reconciliation and human review, offline resource tracking/sync, or bounded grounded and cited RAG outputs. |
| Data Structures and Algorithms implementation | 15 | Correct integrated structures/algorithm, relevant cases and tests, and an explanation of time/space complexity: A's index/queue, B's queue/map/set or C's binary min-heap selection. |
| PrimeCloud deployment and operational readiness | 15 | Successful deployment of the intended revision, assigned HTTPS access, working health check, actual hosted functionality, suitable runtime/secret/dependency configuration and availability for assessment. |
| Technical design and architecture | 10 | Suitable component boundaries, data flows, interfaces, integrations and justified implementation decisions for the selected problem. |
| Testing, reliability and edge cases | 15 | Repeatable core, DSA and hosted normal/failure/boundary tests, expected/observed results, required comparisons and honest limitations. |
| Code quality, documentation and reproducibility | 10 | Maintainable organization, clear README, dependencies/non-secret configuration, complexity notes and reproducible local/test/deployment steps. |
| Security, privacy and responsible engineering | 5 | Input validation, safe credentials/data handling, appropriate access controls and authorized, bounded behavior. |
| Practical relevance and SDG alignment | 5 | A specific intended user problem, useful demonstrated application and credible SDG link without unsupported impact claims. |
| **Total** | **100** | **Technical assessment only.** |

The [challenge checkpoints](challenges.md#technical-assessment-checkpoints)
provide checks for **all eight criteria for A, B and C**. Each criterion is
scored once within its allocation; evidence does not create bonus marks.
Core functionality, DSA and deployment are mandatory. Missing one means the
full challenge is incomplete. Partial or inconsistent work receives credit
only for supported requirements; unsupported claims receive no credit for the
affected requirement. Optional improvements do not replace mandatory work.

### What to expect

Every team undergoes technical inspection: judges may inspect the deployed application, test required functionality, review source/configuration and documentation, verify outputs and ask implementation questions. You may be asked to run the solution or repeat a test. A demonstration supplies technical evidence; it is **not a separately scored presentation**. Slides, speaking style and pitching quality earn no Track-Level points.

## Scoring and tie-breakers

Approximately **two to three judges** may assess each team. Each independently awards a score out of 100 using the rubric above. Your official Track-Level score is the **average** of those scores, and teams are ranked from highest to lowest average.

For example: `(85 + 90 + 88) / 3 = 87.67/100`.

Ties are resolved by the higher average **Core functionality and correctness** sub-score, then **Testing, reliability and edge cases**, followed by panel deliberation on technical evidence if needed. Presentation quality is not a tie-breaker.

The **top three teams** qualify for the **Grand Finale**. The highest-ranked team receives **Best Software Development Solution**.

## PrimeCloud support and resource allocation

Use the workspace, trial or resource allocation communicated by the organizers.
The Organising Committee must confirm event-provided access, credits, permitted
services, storage/databases, relevant limits and assessment-access arrangements.
Do not assume identical trial entitlements, paid services, databases or resource
upgrades, and do not incur unapproved charges.

Raise access, capacity or inference problems with the Technical Lead early;
record unresolved issues rather than claiming successful deployment. Follow
the [PrimeCloud Deployment Guide](deployment.md) for current official resources,
verification, troubleshooting and plan-lifecycle considerations.

## Day-of timeline

Use Day 1 to select a challenge, confirm cloud/storage/model access and deploy a minimal baseline early. Use Day 2 for the integrated DSA, complete local/hosted tests, documentation and technical verification. Follow the published schedule and announced freeze; do not rely on unconfirmed model access for Challenge C.
