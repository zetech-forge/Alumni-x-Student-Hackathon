---
title: Curated Resources
parent: Web3 & Blockchain
grandparent: Hackathon Tracks
nav_order: 2
---

# Web3 & Blockchain: Curated Resources

Use these references to complete **one selected challenge**, not as a course
you must finish. The [curriculum](content.md) maps them to eight learning
modules; [Challenges](challenges.md) defines the required outcomes.
All references below are free to read and the listed developer tools are free.
Hosted model services may charge; local models use your own hardware and
require a model download.

## Start here: official kit and software

The official project is
**[zetech-forge/web3_starter-kit](https://github.com/zetech-forge/web3_starter-kit)**.
It contains contracts, tests, deployment scripts, the Commons frontend/server
and the Leashed Agent implementation. All project paths start at its root.
Do not clone the main hackathon repository to install the kit.

Use [Starter Kits](starter-kits.md) for the exact `npm ci`, test, deployment and
run commands. Follow that walkthrough before adapting instructions from an
external tutorial. Confirm repository access before the event; if GitHub
reports it cannot be found, contact the organizers.

| Challenge | Required setup | Additional installation |
| --- | --- | --- |
| **A: The Pledge - Beginner** | A browser and [Remix IDE](https://remix.ethereum.org), using Remix VM practice accounts. | **None** for the browser route. The complete kit is optional for local automated tests. |
| **B: The Commons - Intermediate** | Node.js **22.13+**, npm, Git, an editor, terminal access and the dedicated kit. | The kit installs Hardhat and viem. Phones need only a browser and the same network as the laptop. |
| **C: Leashed Agent - Advanced** | Everything required for B, plus a model option or the mock fallback. | Ollama for a local model; alternatively an approved hosted model, or **`LLM_FAKE=1` with no model installation or API key**. |

For B/C, download [Node.js](https://nodejs.org/en/download) (npm is normally
included) and [Git](https://git-scm.com/install/). Use
[Visual Studio Code](https://code.visualstudio.com/) or your preferred editor.
PowerShell on Windows and Bash/Zsh terminals on Linux/macOS are supported by
the starter walkthrough.

**AI access:** no organizer-provided or shared API credentials are assumed.
Only use hosted access approved for the event and credentials you are
authorized to use. Do not wait for a shared key: use Ollama or the supported
mock fallback if hosted access is unavailable.

## 1. Blockchain fundamentals

**For all challenges; Modules 1-4.** Start with the introduction, then read the
reference for the concept you need.

| Resource | Level | What to use it for |
| --- | --- | --- |
| [Technical introduction to Ethereum](https://ethereum.org/en/developers/docs/intro-to-ethereum/) | Beginner | Understand shared state, blocks and the role of smart contracts. |
| [Ethereum accounts](https://ethereum.org/en/developers/docs/accounts/) | Beginner | Distinguish signing accounts, contract accounts and their roles. |
| [Transactions](https://ethereum.org/en/developers/docs/transactions/) | Beginner | Understand how a signed action changes blockchain state. |
| [Gas and fees](https://ethereum.org/en/developers/docs/gas/) | Beginner | Separate execution fees from a pledge's stake or a wallet's payment. |
| [Ostrom's Nobel lecture](https://www.nobelprize.org/prizes/economic-sciences/2009/ostrom/lecture/) | Optional context for B | Explore real-world shared-resource governance; use it for mechanism ideas, not as required technical reading. |

## 2. Solidity and Remix

**Core preparation for A; a language refresher for B/C. Modules 4-5.**

| Resource | Level | What to use it for |
| --- | --- | --- |
| [Remix IDE](https://remix.ethereum.org) | Beginner | Write, compile and call Pledge entirely in a browser. Use Remix VM, not a production wallet. |
| [Remix Deploy & Run guide](https://remix-ide.readthedocs.io/en/latest/run.html) | Beginner | Select an environment/account, set transaction Value and interact with a deployed contract. |
| [Solidity: introduction to smart contracts](https://docs.soliditylang.org/en/latest/introduction-to-smart-contracts.html) | Beginner | Read a small contract and understand storage, functions and calls. |
| [Solidity: revert statements](https://docs.soliditylang.org/en/latest/control-structures.html#revert-statement) | Beginner-Intermediate | Understand `require`/reverts and why a rejected action must leave no successful state change. |

The official [`Pledge.sol`](https://github.com/zetech-forge/web3_starter-kit/blob/main/contracts/Pledge.sol)
and the [Remix walkthrough](starter-kits.md) are the shortest route to Challenge A.

## 3. Hardhat and viem

**For B/C; optional local tooling for A. Modules 6-7.**

| Resource | Level | What to use it for |
| --- | --- | --- |
| [Hardhat 3 getting started](https://hardhat.org/docs/getting-started) | Intermediate | Understand the project's build/test tools. Use the existing kit; do not initialize a new project inside it. |
| [Hardhat: local development node](https://hardhat.org/docs/guides/hardhat-node) | Intermediate | Understand the chain behind `npm run chain`, local accounts and reset behavior. |
| [viem documentation](https://viem.sh/docs/getting-started) | Intermediate-Advanced | Understand the clients used by the supplied game, deployment scripts and agent to read/write contract state. |
| [MDN JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide) | As needed for B/C | Look up functions, promises and asynchronous requests when reading frontend/agent code. |

The kit already supplies a frontend, server and agent loop. You do not need to
write them again or install a second blockchain framework.

## 4. Smart contract testing

**For all challenges; Module 6.** A browser-only Pledge submission may use the
manual test log described in the challenge. B/C teams should run and extend
the supplied automated tests.

| Resource | Level | What to use it for |
| --- | --- | --- |
| [Official starter tests](https://github.com/zetech-forge/web3_starter-kit/tree/main/test) | All levels | Begin with the test for your challenge; identify allowed, rejected and boundary actions. |
| [Hardhat: Solidity unit tests](https://hardhat.org/docs/guides/testing/using-solidity) | Intermediate | Understand the `.t.sol` tests and precise time/account controls used for contract checks. |
| [Hardhat: viem and Node.js tests](https://hardhat.org/docs/guides/testing/using-viem) | Intermediate-Advanced | Understand application-side tests using the same tooling family as the kit. |

Test contract behavior, not only page appearance. Important boundaries include
the Pledge deadline, Commons harvest limits, and the wallet threshold/window.
The current official baseline passes; unfinished instructor exercise copies
may contain TODOs whose tests fail until completed.

## 5. Smart contract security

**For all challenges; Module 6 and the challenge acceptance checks.**

| Resource | Level | What to use it for |
| --- | --- | --- |
| [Solidity security considerations](https://docs.soliditylang.org/en/latest/security-considerations.html) | Beginner-Advanced | Focus on external calls, reentrancy, state updates and common contract pitfalls. |
| [OpenZeppelin: access control](https://docs.openzeppelin.com/contracts/5.x/access-control) | Intermediate-Advanced | Understand authorization patterns for owner/agent and governance roles. Reading does not require adding a new dependency. |

Use practice funds only. Never commit keys, wallet exports or API credentials.
Default Hardhat keys are publicly known and must remain local-practice-only.
These references and a passing test suite do not make a prototype audited or
safe for real assets.

## 6. AI agents and local LLMs

**For C; Modules 7-8.** An LLM is a language model that can propose tool calls;
the wallet contract, not the model, enforces payment permission.

| Resource | Level | What to use it for |
| --- | --- | --- |
| [Ollama download](https://ollama.com/download) | Advanced pathway | Install a local model runner. The kit defaults to `qwen2.5:3b`; download it before relying on venue connectivity. |
| [Ollama OpenAI compatibility](https://docs.ollama.com/api/openai-compatibility) | Advanced | Understand the compatible API shape used by the agent. Use the local endpoint from the kit walkthrough, not cloud credentials copied from an example. |
| [x402 overview](https://www.x402.org/) | Optional advanced context | Learn the idea of HTTP payments. The supplied API only imitates an x402-style flow; production x402 integration is a stretch goal. |

Start with fake mode if model setup is a blocker. It is deterministic and
deliberately trusting, making it useful for demonstrating that malicious
instructions cannot override the wallet. It does not generate owner-approval
requests; use the local-console procedure in [Starter Kits](starter-kits.md)
to demonstrate `requestPayment()` followed by the owner's on-chain `approve()`.

Do not confuse that approval process with an off-chain cryptographic
co-signature. The challenge specification explains which payments count toward
the autonomous budget and which require explicit owner action.

## 7. UN Sustainable Development Goals

**For all challenges.**

| Resource | Level | What to use it for |
| --- | --- | --- |
| [The 17 UN Sustainable Development Goals](https://sdgs.un.org/goals) | All levels | Select a relevant goal and target; explain your problem, beneficiary and a plausible measure of impact. |

Name the connection in concrete terms. A practice prototype demonstrates a
workflow or mechanism; it does not by itself prove a real-world impact outcome.
