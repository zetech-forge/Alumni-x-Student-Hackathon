---
title: Web3 & Blockchain
nav_order: 2
parent: Hackathon Tracks
has_children: true
---

# Web3 & Blockchain

Web3 development connects applications to shared blockchain state and
wallet-based transactions. A blockchain maintains a record across computers;
a **smart contract** is a program on that chain that enforces rules for its
stored data and assets. In this track, you write or extend contracts, connect
them to a user interface or agent, and test who can do what.

Your two-day prototype must address a real problem linked to a UN Sustainable
Development Goal. Explain why a blockchain is useful, which rules it enforces,
and what still depends on trust outside the chain. All work uses practice
funds in the approved sandbox, never real money or mainnet.

## Who this track is for

The track offers entry points for beginners and experienced developers. Basic
programming in any language is the minimum starting point; choose a challenge
that fits your team's experience. The Day 1 bootcamp introduces the core
concepts, but the more advanced challenges require greater familiarity with
code, testing and APIs.

**Each team selects ONE challenge** and develops it across both days:

| Challenge | Level | What you will build | Recommended preparation |
| --- | --- | --- | --- |
| **The Pledge** | **Beginner** | A personal-goal commitment backed by test ETH, with referee confirmation and charity settlement. | Basic programming; no prior blockchain experience. Remix provides a browser-only route. |
| **The Commons** | **Intermediate** | An original resource-governance mechanism added to a working multiplayer harvesting simulation. | Comfortable editing code and using a terminal; basic Solidity and tests are helpful. |
| **Leashed Agent** | **Advanced** | A useful agent payment workflow constrained by a policy-controlled wallet, including owner approval and adversarial tests. | Solidity transactions and JavaScript/API experience within the team. |

You are not expected to rebuild supplied infrastructure. The
[challenge specifications](challenges.md) distinguish starter functionality,
required team contributions, acceptance tests and optional extensions.

## Languages, tools and starting point

The official pathway uses **Solidity** for contracts, **Remix IDE** for the
beginner browser workflow, and **Hardhat** for local compilation, testing and
deployment. The dedicated kit includes JavaScript frontend/agent code,
TypeScript scripts, Solidity tests and Node.js tests.

Challenges B and C use **Node.js 22.13 or later**, npm, Git, an editor and a
terminal. Challenge C supports Ollama, an approved model service, or the
provided mock fallback; a paid AI account is not required.

Use the dedicated [Web3 Starter Kit](https://github.com/zetech-forge/web3_starter-kit),
not a clone of the main hackathon repository. See [Starter Kits](starter-kits.md)
for setup and [Content & Curriculum](content.md) for preparation. Alternative
EVM-compatible tools must meet the same assessment and sandbox conditions in
the [track rules](rules.md).

## How you will be assessed

**Stage 1: Track-Level Judging.** All Web3 teams receive a technical assessment
out of **100 points**, using the approved challenge-specific checkpoints.
Judges inspect functionality, on-chain enforcement, tests, security, code,
documentation and problem relevance. You may demonstrate the implementation
and answer short technical questions. **No formal slide presentation or pitch
is required, and no presentation marks are included.**

Approximately **two to three judges** may assess each team independently.
Their scores are **averaged** for the official Track-Level score and ranking,
with no difficulty multiplier. For example:
`(85 + 90 + 88) / 3 = 87.67/100`.

The top **three Web3 teams** qualify for the Grand Finale. The highest-ranked
Web3 team receives **Best Web3 and Blockchain Solution**.

**Stage 2: Grand Finale Pitch & Awards Judging.** The top three teams from each
of five tracks form **15 finalists**. Each completes **From Prototype to
Real-World Impact**, worth an additional **30 points**. The combined maximum is
**130**, normalized as **(Combined Score / 130) * 100**.

The Grand Finale determines **Overall Hackathon Winner**, **Most Innovative
Solution**, **Best Social Impact Solution**, and **Best Pitch & Presentation**.
See [Track Rules & How to Compete](rules.md) for scoring, submissions and safety.
