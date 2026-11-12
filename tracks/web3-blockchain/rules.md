---
title: Track Rules & How to Compete
parent: Web3 & Blockchain
grandparent: Hackathon Tracks
nav_order: 3
---

# Web3 & Blockchain: Track Rules & How to Compete

## Format and challenge selection

Each team selects **ONE** challenge for the two-day event:
**The Pledge (Beginner)**, **The Commons (Intermediate)**, or **Leashed Agent
(Advanced)**. Follow its [mandatory requirements and assessment checkpoints](challenges.md).
Difficulty does not provide bonus points or change the 100-point maximum.

Team size, eligibility, the Alumni/Finalist Collaborator requirement and
conduct follow the [General Rules](../../general-rules.md).

Build on the supplied baseline, identify your team's contribution, and connect
the solution to an SDG through its **problem, beneficiary and measurable
potential impact**. Explain why a blockchain is justified and disclose what it
cannot verify.

## Stage 1: Track-Level Judging

**All Web3 teams undergo a technical assessment out of 100 points.** Judges use
the approved challenge-specific rubric and the common categories below.
They may inspect source, run tests, call contracts directly and ask short
technical clarification questions. Teams may demonstrate their implementations.

**No formal slide presentation or pitch is required at this stage. No
presentation marks are included in the technical score.** Interface polish or
speaking style must not substitute for evidence of correct behavior.

### Technical scoring

| Criterion | Maximum points | Assessment focus |
| --- | --- | --- |
| Core challenge functionality and completion | **40** | Mandatory flows work; the team's contribution is complete and distinguishable from the starter. |
| On-chain rule enforcement and correctness | **25** | Authorization, state transitions and challenge-specific restrictions hold under direct contract calls. |
| Testing, security and failure handling | **15** | Positive, negative and boundary tests; safe credential handling; clear handling of rejected transactions and failures. |
| Code quality and technical documentation | **10** | Readable implementation, reproducible setup, documented decisions and limitations. |
| Problem relevance, SDG alignment and blockchain justification | **10** | A clear beneficiary, plausible impact and a reasoned explanation of blockchain's value and trust limits. |
| **Total** | **100** | **Technical assessment only; no pitch or presentation allocation.** |

### Challenge-specific checkpoints

Prepare the evidence in [Challenges](challenges.md) and the
[challenge-specific technical acceptance checklists](judging.md).
These explain reproducible checks and the conditions for full, partial or
zero credit, including:

| Challenge | Required technical evidence |
| --- | --- |
| **The Pledge** | Valid creation and readable details; referee-only confirmation strictly before the deadline; charity release at or after it; separate success/failure pledges; rejection of unauthorized, early, late and duplicate settlement; explanation of referee trust. |
| **The Commons** | Working registration, harvesting, stock accounting, regeneration and collapse; at least one original governance mechanism; direct-call rejection of prohibited harvests; tests and a comparable baseline-versus-mechanism demonstration. |
| **Leashed Agent** | Separate owner/agent roles; an allowed purchase and payment reason; recipient, autonomous-budget and approval checks; on-chain request/owner approval; pause, revocation and duplicate-approval rejection; malicious instructions cannot bypass policy. |

For Leashed Agent, preserve the baseline distinction: the **0.05 ETH per-hour
limit applies to autonomous spending**, while explicit owner-approved payments
are outside that budget. Payments above **0.02 ETH** require the
`requestPayment()` / `approve()` process, not an off-chain co-signature.

### Recording scores, ranking and tie-breakers

Approximately **two to three judges** may assess each team. Each independently
awards a score out of **100 points** using the selected challenge's technical
criteria. Your official Track-Level score is the **average** of those scores,
and teams rank from highest to lowest final average.

For example: `(85 + 90 + 88) / 3 = 87.67/100`.

For a Track-Level tie, compare the average **Core challenge functionality and
completion** sub-score first. If still tied, the panel deliberates on the
technical evidence. Do not introduce a pitch, difficulty multiplier or
unannounced presentation criterion to break a technical-stage tie.

The **top three Web3 teams qualify for the Grand Finale**. The
**highest-ranked Web3 team receives Best Web3 and Blockchain Solution**.

## Stage 2: Grand Finale Pitch & Awards Judging

The **top three teams from each of the five tracks** qualify: **15 finalists**
in total. Each finalist completes the mandatory challenge
**[From Prototype to Real-World Impact](../../real-world-impact.md)**,
worth an **additional 30 points**. The common brief contains the eight
assessment areas, agreed five-slide structure, recommended five-minute
presentation and complete 30-point rubric. It is not a Stage 1 requirement
or an additional Web3 technical scoring category.

```text
Combined Score = Track-Level Technical Score + Mandatory Challenge Score
Maximum Combined Score = 100 + 30 = 130
Normalized Score = (Combined Score / 130) * 100
```

Carry the confirmed Stage 1 score forward; do not reduce it to 70 points or
rescore the technical stage for presentation. Use the approved Grand Finale
rubric for the additional 30 points, not an invented Web3-specific pitch split.

The Grand Finale determines:

- **Overall Hackathon Winner**
- **Most Innovative Solution**
- **Best Social Impact Solution**
- **Best Pitch & Presentation**

Grand Finale award decisions and tie-breakers follow the official finale
guidelines; the track-level tie-breaker above applies only to Stage 1.

## Allowed tools and technologies

The official pathway is **Solidity**, **Remix VM** for the browser-based Pledge
workflow, and **Hardhat** for local compilation, tests and deployment.
The [dedicated starter repository](https://github.com/zetech-forge/web3_starter-kit)
includes JavaScript frontend/agent code, TypeScript scripts and Solidity/Node.js
tests. See [Starter Kits](starter-kits.md) for Node.js **22.13+**, npm and Git
setup; do not install the kit by cloning the main hackathon repository.

Alternative **EVM-compatible** languages, frameworks and tooling are permitted
if teams:

- Meet the same challenge behavior, acceptance tests and sandbox restrictions.
- Provide exact versions and reproducible build, test and deployment commands.
- Enable judges to inspect contract state and exercise the relevant rules
  directly; a frontend-only demonstration is insufficient.
- Confirm setup and assessment compatibility with the Technical Lead early,
  rather than relying on unavailable hardware, paid accounts or production access.

Libraries, public APIs and AI coding assistants may be used subject to their
licenses, event rules and safe credential handling. Disclose significant AI
tools, models, APIs and their contribution in the README. Leashed Agent may use
Ollama or the supported mock fallback; a paid model is not mandatory.

## Safe sandbox (mandatory)

These restrictions apply regardless of the tools or challenge selected:

- **Local practice chain or approved testnets only. No mainnet deployment.**
- **No real-money transactions or real financial accounts.**
- **No production wallets or production wallet credentials.**
- No unauthorized interaction with third-party contracts.
- Never expose private keys, seed phrases or API credentials in code, Git
  history, screenshots, recordings, logs or shared materials.
- Default Hardhat accounts are public test accounts for the local practice
  chain only; never fund them on public networks. For an approved testnet, use
  separate disposable test-only accounts.
- Keep blockchain RPC private. Use only a trusted LAN/hotspot for the Commons
  server; do not expose practice servers to the internet.
- Use synthetic/demo data, not real personal data. Disclose known contract
  risks and limitations; passing tests do not constitute a security audit.

Safety violations remain subject to the event's disqualification rules.

## Submission requirements

Follow the [general submission requirements](../../general-rules.md#what-every-team-submits),
including your team's code repository, setup/run README, **2-3 minute backup
demo video**, live URL if applicable, team details, named
Alumni/Finalist Collaborator and contribution note, SDG impact statement,
technology stack, AI-tool disclosure and known limitations.

**No slide deck or formal pitch is required for this Track-Level submission.**
Any Grand Finale presentation requirements apply only to qualifying finalists.

For this track, also include:

- Contract source, configuration, dependency lockfile and relevant scripts,
  frontend/agent files, plus a clear summary of your changes to the starter.
- Tests and results covering the selected challenge's acceptance criteria.
  Remix-only Pledge teams may supply the reproducible manual test log described
  in Challenges instead of installing the full kit.
- Local startup/deployment instructions, role/account descriptions and any
  network or model configuration needed to reproduce the demo.
- Evidence of successful flows and required on-chain rejections, including
  boundary cases and any intentional changes to baseline behavior.
- No installed dependencies (`node_modules/`), generated builds, deployment
  state, environment files, wallet exports or credentials committed to the
  repository.

Submit **your own independent project repository**, never push a solution to
the official starter. Follow the announced event submission channel and
deadline; a public deployment is not required for a local practice-chain demo.

## Two-day preparation

- **Day 1:** choose one challenge, run the baseline and begin the team's
  contribution. Commons and Leashed Agent teams should have the kit installed
  and tests running by the end of the bootcamp.
- **Before committing to Leashed Agent:** verify either local model access or
  the supported mock fallback; do not depend on unconfirmed shared API keys.
- **Day 2:** complete tests, document limitations, prepare the backup video and
  make the implementation available for technical assessment.
- **After track ranking:** the top three teams proceed to the mandatory
  Grand Finale challenge and pitch/awards stage.
