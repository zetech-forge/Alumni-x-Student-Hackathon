---
title: Technical Judging Checklists
parent: Web3 & Blockchain
grandparent: Hackathon Tracks
nav_order: 6
---

# Web3 Technical Judging Checklists

Use the checklist for the team's **ONE** selected challenge:
**The Pledge (Beginner)**, **The Commons (Intermediate)**, or
**Leashed Agent (Advanced)**. Difficulty earns no bonus points.
This is **Stage 1: a 100-point technical assessment**, not a formal pitch.
Short technical demonstrations and clarification questions provide evidence;
slide quality and speaking style earn no marks.

Use an [individual printable judge score sheet](judge-score-sheet.html) for
each judge/team. Record check IDs, command or transaction evidence, actual
outcomes, failures and comments. Run checks against the submitted code,
not only an untouched starter. Credit demonstrated understanding and clearly
attributed changes; the supplied working baseline is not original team work.

## Scoring and evidence

Each challenge has **20 checks worth 5 points each**:

| Category | Check IDs | Maximum |
|---|---|---:|
| Core challenge functionality and completion | F1-F8 | 40 |
| On-chain rule enforcement and correctness | E1-E5 | 25 |
| Testing, security and failure handling | T1-T3 | 15 |
| Code quality and technical documentation | Q1-Q2 | 10 |
| Problem relevance, SDG alignment and blockchain justification | R1-R2 | 10 |
| **Total** | **20 checks** | **100** |

Apply these conditions to **each check**, then sum within categories:

| Points | Condition |
|---|---|
| **5: full** | All listed expected outcomes are reproducible, supported by evidence and correctly explained. |
| **4: partial** | Required behavior works; one minor documentation or evidence gap remains, with no demonstrated invariant violation. |
| **3: partial** | Main behavior works, but relevant edge-case or rejection evidence is incomplete. |
| **2: partial** | A substantial subset works, but an important part of the stated check is missing. |
| **1: partial** | Minimal relevant implementation/evidence exists but does not demonstrate a complete outcome. |
| **0: zero** | Missing, nonfunctional, unsupported, or demonstrably contrary to the stated requirement. |

**A reproduced on-chain bypass earns zero on the affected enforcement check**,
even if the frontend blocks it. Do not award partial enforcement points for
successful authorized calls when the prohibited action also succeeds.
Apply event safety/disqualification procedures separately, not as invented
scoring penalties.

Use only Remix VM, a local practice chain or an approved testnet with
disposable test accounts. Never request real keys or real-money evidence.
Judges may run precise timestamp and adversarial tests in their own local
environment; browser-only Pledge teams are not required to install Node.js.
See [setup and test commands](starter-kits.md) and
[participant acceptance cases](challenges.md).

## A: The Pledge - Beginner

Use separate successful and failed pledges, distinct signing roles and short
durations. With the official kit, run
`npx hardhat test solidity test/Pledge.t.sol` against the submitted contract.

| ID | Required functionality / judge action | Expected outcome for full points |
|---|---|---|
| F1 | Create a funded pledge with a goal, duration, referee and beneficiary. | Correct creator, stake, duration-derived deadline and active status are stored. |
| F2 | Try zero stake/duration, zero addresses and a self-appointed referee. | Invalid inputs revert without creating a pledge. |
| F3 | Read pledge details and count using the submitted interface. | Stored values, IDs and status are understandable and consistent. |
| F4 | Designated referee confirms one active pledge before expiry. | Status becomes Succeeded and the original stake returns to the pledger once. |
| F5 | Release a different expired active pledge. | Status becomes Failed and only its nominated beneficiary receives the stake. |
| F6 | Run both outcomes from fresh state, retaining receipts. | Separate pledge IDs prove both outcomes; neither pledge has contradictory outcomes. |
| F7 | Inspect creation and settlement events and balances. | Events identify the correct pledge/outcome; balance changes match transfers, accounting for gas. |
| F8 | Follow the team's reproducible Remix/local walkthrough. | Correct compiler, VM/network, roles, transaction value and calls reproduce the demonstration. |
| E1 | Confirm as pledger, stranger and designated referee. | Only the designated referee can confirm. |
| E2 | Confirm at deadline minus one second, exactly at it and one second later. | Only the first succeeds, on independent active pledges. |
| E3 | Release at deadline minus one second, exactly at it and one second later. | First fails; at/after expiry anyone may release to the fixed beneficiary. |
| E4 | Repeat and cross-call settlement after success/failure. | No second payout or status manipulation is possible. |
| E5 | Inspect state-before-transfer and exercise rejecting/callback recipients. | Terminal status is visible before transfer; re-settlement fails; a failed transfer rolls back settlement. |
| T1 | Inspect/run positive and unauthorized/invalid-input tests. | Assertions verify state and balances, not merely transaction submission. |
| T2 | Inspect/run exact timestamp boundary tests. | Evidence distinguishes `< deadline` from `>= deadline`, without wall-clock guessing. |
| T3 | Inspect/run callback and failed-transfer tests; check safety instructions. | No duplicate payout; rollback is tested; only sandbox funds/accounts are used. |
| Q1 | Inspect Solidity and attribution of baseline versus changes. | Clear names, coherent checks-effects-interactions and accurately disclosed contributions. |
| Q2 | Read setup, role map, tests, demo and limitations. | Another person can reproduce results without hidden credentials or missing steps. |
| R1 | Ask for the beneficiary/problem, SDG target and one measurable outcome. | A specific plausible use case, affected users and measure are identified. |
| R2 | Ask what blockchain proves and what it cannot verify. | Team justifies on-chain settlement, referee trust and the absence of independent goal or registered-charity verification. |

## B: The Commons - Intermediate

Deploy fresh state, join with at least two player accounts, and retain a
baseline-versus-mechanism comparison. Run
`npx hardhat test solidity test/Commons.t.sol` and relevant frontend tests.

| ID | Required functionality / judge action | Expected outcome for full points |
|---|---|---|
| F1 | Register two distinct players and try a repeat registration. | Players are identifiable; duplicate registration is rejected. |
| F2 | Perform a valid harvest and read stock/player totals. | Resources decrease and the correct player's harvested total increases by the same amount. |
| F3 | Read the game/scoreboard using two clients. | Contract-backed state and totals agree; display is not fabricated local state. |
| F4 | Advance rounds and compare growth with the integer logistic formula. | Stock follows the configured capacity/growth and rounds, including integer rounding. |
| F5 | Advance over 100 rounds in a slow-growth fixture, then harvest. | No missed rounds are discarded; recorded round, stock and subsequent growth agree. |
| F6 | Drive stock to the collapse boundary and below it. | Equality with the threshold survives; stock strictly below it permanently collapses. |
| F7 | Exercise at least one original team governance mechanism. | Mechanism runs on-chain and its intended resource protection is observable. |
| F8 | Compare baseline and mechanism under a stated comparable scenario. | Evidence explains the effect/trade-offs rather than claiming protection from one cherry-picked move. |
| E1 | Harvest unregistered, zero, above maximum and twice in one round. | Every prohibited direct call reverts without corrupting accounting. |
| E2 | Attempt to harvest beyond available stock. | Stock cannot underflow or exceed configured capacity during regeneration. |
| E3 | Bypass the UI and violate the team's governance rule directly. | The contract itself rejects the action. |
| E4 | Attempt harvesting after collapse and after advancing more rounds. | Harvest remains rejected and collapse cannot be undone by regeneration. |
| E5 | Combine custom-rule attempts with base restrictions. | The mechanism cannot bypass membership, per-round/max-harvest, stock or collapse checks. |
| T1 | Run positive, unauthorized and invalid-harvest tests. | State/player totals are asserted and rejections leave state unchanged. |
| T2 | Run regeneration, >100-round and fixed-point tests. | Exact growth is preserved; zero-growth fixed points terminate safely without losing growth. |
| T3 | Run collapse and mechanism-specific adversarial tests. | Both boundaries and direct-call bypass attempts are covered; remaining gas/scale limits are disclosed. |
| Q1 | Inspect mechanism code and baseline attribution. | Small, readable on-chain changes reuse existing checks and identify original work. |
| Q2 | Follow setup, deployment, frontend and test instructions. | Judges reproduce the game and comparison; configured parameters and limitations are documented. |
| R1 | Ask for the shared-resource problem, SDG target and success measure. | Realistic users, competing incentives and measurable sustainability outcomes are identified. |
| R2 | Ask why enforcement belongs on-chain. | Team explains shared rules/transparency, off-chain limitations and governance trade-offs. |

The starter's catch-up loop processes all rounds until the requested round or
an integer-growth fixed point. Extremely slow-growth custom configurations can
still need substantial gas; assess them explicitly rather than restoring a
silent 100-round cap.

## C: Leashed Agent - Advanced

Use separate owner, agent and recipient roles, a fresh funded local wallet,
and Ollama, an approved hosted model, or the supported mock fallback. Run
`npx hardhat test solidity test/PolicyWallet.t.sol`. Tool-call and receipt
evidence matters more than a model's text claiming success.

| ID | Required functionality / judge action | Expected outcome for full points |
|---|---|---|
| F1 | Inspect deployment and accounts. | Owner controls policy, agent signs its own actions, wallet is funded and recipient is separately identified. |
| F2 | Make a plain-language request with the chosen model/fallback. | The tool workflow selects a supported action and reports actual success/failure. |
| F3 | Purchase allowed mock data. | On-chain receipt and returned data prove the purchase using only practice funds. |
| F4 | Inspect payment reason and activity evidence. | Recipient, amount and useful reason are recorded consistently. |
| F5 | Request a large payment and inspect balances before approval. | A readable pending request exists; requesting alone transfers no funds. |
| F6 | Owner approves a valid request larger than the autonomous budget. | One transfer succeeds; autonomous spent counter and window are unchanged. |
| F7 | Pause, try actions, then unpause. | Pay/request/approval are blocked while paused; authorized operation resumes when unpaused. |
| F8 | Revoke/replace the agent and examine an existing request. | Old agent loses pay/request access; replacement works; owner may approve a pending request while unpaused and allowlisted. |
| E1 | Agent/stranger try policy changes or approval; stranger requests payment. | Owner-only controls and agent-only request/pay are enforced; AI has no owner key or owner-control tool. |
| E2 | Pay/request a blocked recipient; block a recipient after requesting, then approve. | Direct pay, new request and later approval all enforce the current allowlist. |
| E3 | Spend exactly 0.05 ETH autonomously, then try one wei more. | Exact budget is allowed; excess is rejected; owner-approved funds do not consume the autonomous budget. |
| E4 | Pay exactly 0.02 ETH, then one wei more; repeat an owner approval. | Equality is autonomous; above requires owner approval; duplicate settlement fails. |
| E5 | Try direct calls and hostile model instructions while paused/revoked. | Prompt text and UI cannot bypass on-chain authority, pause or revocation. |
| T1 | Run role, recipient, duplicate, pause, revoke and rotation tests. | Both authorized recovery and prohibited actions are asserted with state/balance evidence. |
| T2 | Test window start +3,599 and +3,600 seconds; inspect threshold equality. | Old budget applies before expiry; next successful autonomous payment resets at/after expiry; rejected calls roll back. |
| T3 | Inspect tool errors, transaction failures and sandbox tests. | Failures are explicit, not false successes; default agent and owner accounts reject non-loopback RPC; no production credentials are used. |
| Q1 | Inspect wallet/tools and attribution. | Readable policy code and minimal tool surface separate model decisions from owner authority. |
| Q2 | Follow model/fallback, API, deployment, approval and test instructions. | No assumed shared keys; reproducible requests, receipts and known limitations are documented. |
| R1 | Ask for the agent's user problem, SDG target and success measure. | A justified use case and measurable benefit are described without speculative impact claims. |
| R2 | Ask why programmable on-chain limits help. | Team explains bounded autonomy, owner trust, public local-key limitations and what still needs protection. |

## Scoring and qualification

Each judge independently assesses the selected challenge's 20 checks using
the five category totals, for a maximum of **100 points**. Approximately
two to three judges may assess each team. Their independent totals are
**averaged** for the official Track-Level score, not replaced by a single
panel total. For example: `(85 + 90 + 88) / 3 = 87.67/100`.
Teams rank by that average, with the
[published technical tie-breaker](rules.md#recording-scores-ranking-and-tie-breakers)
applied where needed.

The highest-ranked team receives **Best Web3 and Blockchain Solution**; the
top three advance. Do not add a pitch score here. Only finalists undertake
the common **[From Prototype to Real-World Impact](../../real-world-impact.md)**
challenge for 30 additional points.
