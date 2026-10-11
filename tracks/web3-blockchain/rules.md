---
title: Track Rules & How to Compete
parent: Web3 & Blockchain
grandparent: Hackathon Tracks
nav_order: 3
---

> **This track feeds the "Best Web3 / Blockchain Solution" award.** Every team is also automatically eligible for Overall Hackathon Winner, Most Innovative Solution, Best Social Impact Solution, and Best Alumni-Student Collaboration. Remember: challenges must tie to a UN Sustainable Development Goal and fit the two-day build window (Day 1 build, Day 2 pitch).

# Web3 & Blockchain: Track Rules & How to Compete

## Format
Each team picks **one** of the three challenges in [Challenges](challenges.md) and builds it for the full two days. On Day 2 you give a live demo and a pitch. Each challenge lists "Must revert on-chain" rules. Judges will probe them live by calling your contract directly, so a rule that only exists in your web page does not count.

## Allowed tools & tech
- Any EVM chain and any language. Solidity is recommended, and the [Starter Kits](starter-kits.md) use it.
- AI coding assistants (e.g. Copilot, Cursor, ChatGPT, Claude) are allowed. Disclose which tools you used and roughly how much of the code they helped produce in your README. This is for transparency and is not penalized unless undisclosed.
- Deploy only to a practice chain (Remix's built-in chain or the starter kit's local chain) or a public testnet such as Sepolia. No mainnet deploys, no real money, and no real personal data.
- Any publicly available library or API is allowed.

## Safe sandbox (mandatory)
This is a university event -- every build must stay inside a safe sandbox:
- Testnets only. No real-money transactions.
- No real financial accounts or production wallets containing meaningful assets.
- Any smart contract risk must be disclosed in your submission.
- No unauthorized interaction with third-party contracts.

This rule is non-negotiable and applies regardless of what a challenge
otherwise allows.

## Submission requirements
Follow the standard submission package in [General Rules](/general-rules.md). Technical Leads: add anything specific to this track here.

## Judging criteria

| Criterion | Weight |
|---|---|
| Functionality / correctness | 30% |
| Code quality / documentation | 15% |
| Creativity / approach | 15% |
| SDG / social-impact alignment | 15% |
| Pitch / presentation | 25% |

Functionality is scored on behaviour judges see you demonstrate, not on what the team says it can do. It also depends on whether your must-revert rules actually hold when a judge tries to break them.

## Scoring and tie-breakers
Ties go to the team with the higher Functionality score. If still tied, the judges' panel decides.

## Day-of timeline
Follows the general two-day schedule. Two additions:

- Challenge B and C teams should have the starter kit installed and its tests running on at least one laptop by the end of the Day 1 bootcamp.
- Teams considering Challenge C should confirm LLM access during that session, before committing to the challenge.
