---
title: Content & Curriculum
parent: Web3 & Blockchain
grandparent: Hackathon Tracks
nav_order: 1
---

# Web3 & Blockchain: Content & Curriculum

Prepare for the **12-13 November 2026** hackathon by learning what your selected
challenge needs, not by trying to complete an entire blockchain course.
Choose **one challenge** and use the eight modules below as a practical guide.
[Curated Resources](resources.md) provides the short reading list;
[Starter Kits](starter-kits.md) provides installation and demo commands.

The Day 1 bootcamp introduces the core workflow. It is not a substitute for
all the programming experience needed by an intermediate or advanced team.
Arrive with a working setup where possible, or use the opening preparation
checklist when you arrive.

## Learning objectives

By the end of your chosen pathway, you should be able to:

- Explain what the blockchain records, what a wallet signs and what a contract
  can enforce.
- Deploy and call a contract using practice funds.
- Distinguish a read-only call from a transaction, and understand gas costs.
- Test successful actions, rejected actions and important boundary cases.
- Explain the supplied infrastructure and your team's own contribution.
- Identify a real beneficiary, an SDG connection and a reason to use a blockchain.
- State the trust and security limits of your prototype.

## Prerequisites by difficulty

| Pathway | Knowledge to bring | Software and access |
| --- | --- | --- |
| **Beginner: The Pledge** | Variables, functions, conditions and basic debugging in any language. No previous blockchain experience required. | A browser and Remix IDE. The complete starter kit is optional. |
| **Intermediate: The Commons** | Comfortable editing files, using a terminal and reading simple tests. Basic Solidity is helpful; work through Modules 4-6 if it is new. | Node.js **22.13+**, npm, Git, an editor, terminal access and the dedicated kit. Phones need a browser and the same network as the host laptop. |
| **Advanced: Leashed Agent** | Solidity transactions and JavaScript/API experience within the team; familiarity with asynchronous requests and environment variables. | The same local tools as Intermediate, plus Ollama, an approved hosted model, or the supported mock fallback. |

No pathway requires mainnet, real wallets, real ETH or a paid AI account.
For local development, npm normally comes with Node.js. Follow the versions
and commands in the kit rather than creating a different project from a tutorial.

## Which modules should you study?

| Challenge | Recommended pathway | Ready-to-build checkpoint |
| --- | --- | --- |
| **A: The Pledge - Beginner** | Modules **1-5**, then the browser-based testing/security activities in **6**. Module 7 is optional; Module 8 is not needed. | Create and inspect a pledge in Remix; explain the referee role, settlement paths and timestamp boundary. |
| **B: The Commons - Intermediate** | Modules **1-7**; review familiar fundamentals quickly. Module 8 is not needed. | Run the baseline game and tests; locate `_mechanism` and specify one additional on-chain rule. |
| **C: Leashed Agent - Advanced** | Modules **1-8**, focusing on **6-8** once fundamentals are secure. Module 7 applies to the agent's contract connection, not a required new frontend. | Explain owner/agent separation, run the wallet tests and complete an authorized mock-data purchase. |

The eight modules cover nine practical learning areas. Module 6 combines
local development with testing/security:

| Practical learning area | Module |
| --- | --- |
| 1. Blockchain fundamentals | 1 |
| 2. Wallets, keys and transactions | 2, with transaction execution in 3 |
| 3. Gas and transaction fees | 3 |
| 4. Smart contracts | 4 |
| 5. Solidity programming using Remix | 5 |
| 6. Local blockchain development using Hardhat | 6 |
| 7. Smart contract testing and security | 6 |
| 8. Connecting applications to smart contracts | 7 |
| 9. AI agents and programmable wallet policies | 8 |

## Eight practical learning modules

### Module 1: What is a blockchain?

**Learn:** blocks, shared state and the difference between a blockchain and a
database controlled by one service. A shared record does not make information
from the real world automatically true.

**Practice:** describe your selected challenge in two sentences: what should
be recorded/enforced on-chain, and who or what must still be trusted. For
example, The Pledge trusts a referee to assess the real-world goal.

**Ready when:** you can justify using a blockchain without claiming it solves
every trust problem. Relevant to **all challenges**.

### Module 2: Wallets and keys

**Learn:** account addresses, private keys, signatures and the distinction
between a user account and a contract account. A wallet helps sign transactions;
funds and state are recorded on the chain, not inside a browser extension.

**Practice:** switch among funded Remix VM accounts or identify the local
Hardhat accounts. Map them to roles: pledger/referee/charity for A,
players for B, or owner/agent/seller for C.

**Ready when:** you can explain who signs an action and why another account
must not have that authority. Never share real keys or use production wallets.
Default Hardhat accounts are public test accounts for the **local chain only**.
Relevant to **all challenges**.

### Module 3: Transactions and gas

**Learn:** read-only calls, signed state-changing transactions, receipts and
gas. Gas measures execution work; the transaction fee is separate from the
test ETH stake or payment. A reverted transaction rolls back its state changes
but can still consume gas.

**Practice:** inspect one successful transaction and one rejected transaction.
Find the sender, recipient and result. Compare a read such as `pledges(id)`
with a write such as `create`.

**Ready when:** you check the actual receipt/tool result rather than assuming
that a button click or model response proves success. Relevant to
**all challenges**.

### Module 4: Smart contracts

**Learn:** contract storage, functions, caller identity (`msg.sender`),
transferred value (`msg.value`), events and authorization. Contracts enforce
only the rules actually written; hiding a UI control does not prevent a direct
contract call.

**Practice:** trace a supplied contract's inputs, checks, state changes and
events. Identify its valid states and the actions each role is allowed to take.

**Ready when:** you can point to the on-chain check for an important rule.
Changing local source does not update an existing deployment: compile and
redeploy to test new code. Relevant to **all challenges**.

### Module 5: Solidity basics in Remix

**Learn:** Solidity types, structs, mappings/arrays, functions, payable calls,
`require`, status enums and events. Use the actual Pledge interface:
`create(goal, durationSeconds, referee, charity)`, with the stake supplied as
the transaction's Value.

**Practice:** open the official Pledge source in Remix, compile and deploy in
**Remix VM**. Create a pledge and read its stored details. Demonstrate success
and expiry using **separate pledges**, switching accounts for the relevant roles.

**Ready when:** you understand that `deadline` is the creation block timestamp
plus the **duration in seconds**. Confirmation requires
`block.timestamp < deadline`; release is allowed when
`block.timestamp >= deadline`. Each pledge settles only once.

This is the core coding module for **A** and a Solidity refresher for **B/C**.
The [starter walkthrough](starter-kits.md) supplies the detailed Remix steps.

### Module 6: Local Hardhat development, testing and security

#### Local development pathway

For **B/C**, use the dedicated kit to learn what each tool does:
`npm ci` installs locked dependencies, `npm run build` compiles contracts,
`npm test` runs the tests, and `npm run chain` starts the local practice chain.
Deploy with the relevant kit script and locate generated deployment metadata.

Keep commands in the project root and use separate terminals for long-running
services. Restarting the practice chain resets its state, so redeploy afterward.
Do not run a tutorial's project initializer inside the downloaded kit.

#### Testing and security pathway

For **all challenges**, define one expected outcome per test: allowed action,
unauthorized action, boundary value and repeated settlement/action. A contract
that compiles is not necessarily correct.

- **A:** test creation, the chosen referee, early/late actions, the exact
  deadline and duplicate settlement. Remix-only teams can keep a reproducible
  manual test log; supplied automated tests set exact block timestamps.
- **B:** retain baseline registration, stock, regeneration and collapse checks;
  add tests proving your custom mechanism permits and rejects the right harvests.
- **C:** test recipient restrictions, threshold/window boundaries, owner
  approval, pause, revocation, duplicate approvals and payment reasons.

Discuss authorization, updating state before external transfers, and
**reentrancy**: a recipient contract calling back during a transfer. Never
commit keys, API credentials, environment files or generated deployment state.
Passing tests do not mean a contract has been professionally audited.

**Ready when:** you can reproduce a failure and identify the contract check
responsible. A teams need the browser-based testing portion; B/C teams need
both portions. The official baseline passes; TODO-related failures apply only
to unfinished exercise copies.

### Module 7: Connecting an application to a contract

**Learn:** the RPC endpoint (how an application reaches a blockchain), contract
address, ABI (the description of callable functions/events), reads, signed
writes and receipts. The kit uses **viem** from JavaScript/TypeScript.

**Practice:** trace a Commons harvest from its mobile control to the contract,
or an agent payment from tool call to wallet transaction. Inspect how the
application loads the local deployment address and reports a revert.

**Ready when:** you can tell a network/setup error from a contract rejection.
For **B**, connect phones and laptop to the same trusted Wi-Fi/hotspot; phone
`localhost` is not the laptop. For **C**, trace the agent/API connection.
A custom web interface is **optional for A**; B/C teams need not rebuild the
supplied frontend or agent infrastructure.

### Module 8: AI agents with spending limits

**Learn:** how an agent turns a request into a tool call, why prompts are not
access control, and how the wallet distinguishes owner, agent and approved
recipients. The agent must never hold the owner's key.

**Practice:** use Ollama or `LLM_FAKE=1` to buy mock data, then attempt an
unauthorized payment. Show the difference between a model agreeing to act and
the contract actually permitting a transfer.

Trace the default policy: **0.05 practice ETH per one-hour autonomous window**,
with **owner approval above 0.02 ETH per payment**. Larger requests use
`requestPayment()` followed by the owner's on-chain `approve()` transaction,
not an off-chain co-signature. Owner-approved payments are outside the
autonomous window budget in the baseline. Demonstrate pause and revocation.

**Ready when:** you can explain a permitted purchase, a rejected purchase and
an owner-approved request. The mock data API imitates an x402-style payment
flow; it is not production x402 infrastructure.

This module is **recommended for Challenge C and optional for A/B**.
The fake fallback needs no model or API key and does not itself generate owner
approval requests; the starter walkthrough includes a deterministic local
console procedure for that part of the demo.

## Event-specific preparation checklist

Use this before **12 November 2026**, or at the start of Day 1 if you have
already arrived:

- Choose a likely challenge and review its prerequisites and acceptance tests.
- Identify a beneficiary and SDG; write down one realistic two-day outcome.
- **A:** open Remix and the official Pledge source; confirm you can compile
  and deploy in Remix VM without connecting a real wallet.
- **B/C:** install Node.js 22.13+, npm and Git; open the dedicated kit in your
  editor; run `npm ci`, `npm test` and `npm run build` while internet is available.
- Confirm access to the official repository. If GitHub reports it cannot be
  found, contact the organizers rather than using an old nested copy.
- **B:** check that a phone can reach the game server on the laptop's network;
  have a hotspot option if venue Wi-Fi blocks device-to-device access.
- **C:** test Ollama or an approved hosted model, or select `LLM_FAKE=1`.
  No shared organizer API credentials are assumed; the fallback is sufficient
  when no model service is available.
- Create your team's independent project repository using the starter
  instructions, and check that secrets/generated files are excluded.

## Realistic Day 1 preparation

Use the announced event timetable; the sequence below is a preparation
priority, not a promise of additional scheduled sessions.

1. **Shared foundations:** review Modules 1-4 and the sandbox rules. Identify
   the roles and transactions in your team's selected challenge.
2. **Guided contract exercise:** use Module 5 to deploy, call and deliberately
   trigger a rejection in Remix. Experienced teams can use this as a quick review.
3. **Challenge-specific setup:** A teams test both pledge outcomes; B teams
   launch the baseline game; C teams run wallet tests and a fake/local-model
   purchase. Use Modules 6-8 as needed, not as a required full-day course.
4. **Before implementation:** confirm one working baseline and write the
   team's change plus its acceptance tests. Ask the Technical Lead about
   blockers early; do not spend the build window on optional installations.
5. **During the build:** add one small change at a time, test the relevant
   behavior and record what the evidence demonstrates.

On **13 November**, prioritize acceptance tests, reproducible run instructions,
submission materials and a backup demo. Consult [Challenges](challenges.md) and
[Track Rules](rules.md) for what must be shown; reading every resource is not a
competition requirement.
