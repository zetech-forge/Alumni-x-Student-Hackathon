---
title: Challenges
parent: Web3 & Blockchain
grandparent: Hackathon Tracks
nav_order: 4
---

# Web3 & Blockchain: Challenges

Choose **one challenge** for the two-day hackathon. Each offers a different
technical starting point, not a different scoring scale. All use the shared
[track rules and judging rubric](rules.md).

| Challenge | Difficulty | Recommended starting knowledge | Main contribution |
| --- | --- | --- | --- |
| A: The Pledge | **Beginner** | Basic programming; no blockchain experience required. | Understand, adapt and demonstrate a stake-backed commitment contract. |
| B: The Commons | **Intermediate** | Comfortable editing code and running terminal commands; basic Solidity helps. | Add and test an original governance mechanism in a working resource simulation. |
| C: Leashed Agent | **Advanced** | Solidity transactions and JavaScript/API experience within the team. | Configure and demonstrate a useful agent whose payments remain constrained by a contract. |

## Shared expectations

Judges use the [challenge-specific technical checklists](judging.md) for the
100-point, technical-only Track-Level assessment. Only Grand Finale qualifiers
complete [From Prototype to Real-World Impact](../../real-world-impact.md);
its common 30-point rubric and five-slide presentation are separate.

### Baseline behavior and trust boundaries

- **The Pledge:** demonstrate success and failure with separate pledges.
  The blockchain cannot independently verify a personal goal; it trusts the
  designated referee. The contract only checks that the charity address is
  nonzero: it **does not verify that it belongs to a registered charity**.
  Use sandbox addresses, not real charity wallets.
- **The Commons:** regeneration processes all elapsed rounds, stopping early
  only when integer-rounded growth is zero and further rounds cannot change
  stock. There is no 100-round truncation. Custom simulations with very slow
  growth and large capacities require gas assessment; this is a local learning
  game, not a production-scale resource simulator.
- **Leashed Agent:** the owner configures policy; the agent has its own signing
  account and can only pay or request approval; approved recipients receive
  funds but gain no policy authority. Never supply the owner's private key to
  the AI agent or model. The public local mnemonic is not secret isolation and
  must never secure real funds. Owner-approved payments bypass the autonomous
  budget and do not increase its counter. A payment of exactly 0.02 ETH and
  cumulative autonomous spending of exactly 0.05 ETH are allowed; one wei over
  either requires approval or is rejected, respectively. The one-hour window
  starts at deployment and resets on the next successful autonomous payment
  when at least 3,600 seconds have elapsed; it is neither a sliding window nor
  aligned to clock hours. Pause blocks payments, requests and approvals.
  Revocation blocks new agent payments/requests but does not cancel pending
  requests: the owner may still approve them while unpaused and allowlisted.

- **Work from the dedicated kit:** [zetech-forge/web3_starter-kit](https://github.com/zetech-forge/web3_starter-kit).
  Do not clone the main hackathon repository for project files. Follow
  [Starter Kits](starter-kits.md) for installation, cross-platform commands,
  troubleshooting and creating your team's independent repository.
- **Build on what is supplied.** The current kit has working Pledge and
  PolicyWallet implementations, tests, a Commons game and an agent loop.
  Completing TODOs applies only if an instructor provides an unfinished
  exercise copy. You are not expected to recreate infrastructure already given.
- **Connect to an SDG.** State a real user problem and its relationship to a UN
  Sustainable Development Goal. Suggested SDGs below are examples, not limits.
- **Explain why a blockchain helps.** Describe what a shared, enforceable record
  adds and what still depends on trust outside the chain.
- **Enforce rules in the contract.** A disabled button or a model instruction
  is not protection: judges may call the contract directly.
- **Stay in the sandbox.** Use Remix VM or the approved local practice chain.
  Only use an organizer-permitted testnet with separate disposable test-only
  accounts. Never use mainnet, real wallets, real funds or real personal data.
  Never commit private keys, seed phrases or API credentials.
- **Submit your own repository**, not a push to the official starter. Include
  setup steps, your changes, test evidence, known limitations, SDG rationale and
  disclosure of AI coding tools. Every challenge also follows the full
  submission package in the [track rules](rules.md), including a **2-3 minute
  backup demo video**; challenge-specific demo checklists do not replace it.

**Two-day scope:** on Day 1, get the baseline running, choose one focused
contribution and verify its rules. On Day 2, finish tests, document limitations
and rehearse a reproducible demo. Stretch goals are optional; prioritize a
correct, explainable minimum over a large unfinished feature set.

---

## Challenge A: The Pledge

**Difficulty: Beginner.** A complete demonstration can be built in a browser
using Remix IDE. A custom frontend is optional.

### Background, problem and real-world context

People make commitments to attend classes, exercise or care for their
environment, but motivation can fade. A stake-backed pledge gives a promise a
consequence: success returns the stake; an unfulfilled pledge funds a chosen
charity.

Build a personal-goal commitment that is understandable to both the person
making it and the person verifying it. Suggested connections include **SDG 4:
Quality Education**, **SDG 3: Good Health and Well-Being**, and **SDG 13: Climate
Action**.

**Trust boundary:** the blockchain cannot know whether someone attended a
lecture or completed a run. It records the pledge and enforces settlement, but
the chosen **referee** decides whether the goal was achieved. Explain the risk
of a mistaken or dishonest referee; do not claim that blockchain verifies the
real-world activity.

### What to build and learn

Deliver a working contract demonstration in a specific goal-setting context,
using the provided contract as a baseline. Learn to:

- Send test ETH to a contract and distinguish the stake from transaction fees.
- Store and retrieve a pledge's details.
- Use caller authorization and blockchain timestamps.
- Move a pledge from active to a final status exactly once.
- Test both intended actions and attempts that must be rejected.

Personalizing the goal, explaining the trust model and supplying clear
validation evidence are sufficient for the minimum. New contract features are
optional; identify which behavior came from the starter.

### Tools and provided starting point

Required: a browser, [Remix IDE](https://remix.ethereum.org), Solidity and a
**Remix VM** practice environment. No npm installation, browser wallet or faucet
is needed for the browser-only route.

The official [`contracts/Pledge.sol`](https://github.com/zetech-forge/web3_starter-kit/blob/main/contracts/Pledge.sol)
provides pledge storage, creation, referee confirmation, charity release,
readable status and settlement events. The kit also includes
[`test/Pledge.t.sol`](https://github.com/zetech-forge/web3_starter-kit/blob/main/test/Pledge.t.sol)
for automated validation if you install the optional local setup.

### Numbered implementation steps

1. **Define your scenario.** Write one measurable goal, name the referee's role
   and explain why the beneficiary is appropriate. Use VM accounts in place of
   real people or charity wallets.
2. **Open Remix.** Create `Pledge.sol` and paste the raw source from the official
   contract link above. Read `create`, `confirm`, `release` and the status enum.
3. **Check the rules.** For an unfinished exercise copy, complete the TODOs.
   For the working baseline, trace the existing checks and adapt only what
   your scenario needs. Preserve the mandatory behavior below.
4. **Compile.** Use Solidity **0.8.34**, as configured in the kit, or another
   compatible version at least 0.8.24.
5. **Deploy in Remix VM.** Select three distinct practice accounts for pledger,
   referee and charity. Deploy with Value `0`; no real wallet is required.
6. **Create a pledge.** Select the pledger, set Value to a positive amount such
   as **1 test ether**, and call `create` with:
   - `goal`: the text describing the promise;
   - `durationSeconds`: a positive **duration in seconds**, such as `120`;
   - `referee`: another account's nonzero address;
   - `charity`: a nonzero beneficiary address.
   The stake is supplied as the transaction's Value, not as another function
   parameter. The contract calculates `deadline = block.timestamp + durationSeconds`.
7. **Inspect it.** Note the returned/emitted ID; IDs start at `0`. Read
   `pledges(id)` and `count()`. Status values are Active (`0`), Succeeded (`1`)
   and Failed (`2`). Reset Value to `0` before nonpayable calls.
8. **Exercise both outcomes.** Use one pledge for successful confirmation and
   a **separate pledge** for expiry and charity release. Run the acceptance
   scenarios below using the relevant VM accounts.
9. **Package the work.** Save your Solidity source, scenario, expected outcomes
   and test evidence in your own repository. If you edit source after deploying,
   compile and deploy a new instance before testing the changes.

### Mandatory functionality and on-chain enforcement

Anyone must be able to create a pledge and read its pledger, goal, stake,
deadline, referee, charity and status. Creation requires a positive stake and
duration, a nonzero referee different from the pledger, and a nonzero charity.

Use the following deadline boundary consistently in code, tests and explanations:

| Blockchain timestamp | Referee confirmation of an active pledge | Charity release of an active pledge |
| --- | --- | --- |
| **Before** the deadline: `block.timestamp < deadline` | Allowed; returns the stake to the pledger. | Rejected. |
| **Exactly at** the deadline: `block.timestamp == deadline` | Rejected. | Allowed. |
| **After** the deadline: `block.timestamp > deadline` | Rejected. | Allowed. |

Only the designated referee may confirm. **Anyone** may trigger release once
the deadline is reached; only the charity receives the released stake. Reaching
the deadline does not send money automatically: someone must submit `release`.

Both settlement paths must require Active status, update status before the
external transfer, and prevent any second payout. A pledger must not be able
to withdraw early through either path.

### Testing and minimum acceptance criteria

Use the following as a checklist; a revert means the contract rejects the
transaction rather than merely showing a warning in the UI.

| Scenario | Evidence required |
| --- | --- |
| Create a valid pledge. | Stored fields match the inputs; stake is held by the contract; deadline uses the creation block timestamp plus the duration in seconds. |
| Create with zero stake, zero duration or an invalid referee/charity. | Transaction reverts. |
| Referee confirms an active pledge before its deadline. | Status becomes Succeeded, the pledger receives the stake, and a success event is emitted. |
| Pledger or stranger attempts confirmation. | Transaction reverts and the pledge remains active. |
| Referee confirms exactly at or after the deadline. | Transaction reverts. |
| Anyone attempts release before the deadline. | Transaction reverts. |
| Anyone releases an unconfirmed pledge at or after the deadline. | Status becomes Failed, the charity receives the stake, and a failure event is emitted. |
| Repeat confirmation, repeat release, or release an already successful pledge. | Each attempt reverts; no duplicate transfer occurs. |
| Read either settled pledge. | Details remain retrievable with the correct final status. |

For browser-only submissions, keep a reproducible Remix test log with account,
pledge ID, action and result. Balance comparisons must account for gas fees.
Do not try to prove the exact-second boundary by clicking at the right moment:
the supplied automated tests set block time precisely. If using the installed
kit, run:

```text
npx hardhat test solidity test/Pledge.t.sol
```

Keep tests for one second before, exactly at, and one second after the deadline.
Remix-only teams must still show the strict `<` confirmation and `>=` release
conditions in their submitted contract and explain the boundary table.

### Deliverables and demonstration

Submit your own repository with Solidity source, a short user scenario,
setup/deployment steps, test evidence and the referee trust limitation.

In the live demo:

1. Create and inspect a pledge.
2. Show unauthorized confirmation and early release being rejected.
3. Confirm one pledge successfully as its referee.
4. Use a separate expired pledge to show late confirmation rejected and charity
   release succeeding.
5. Attempt a duplicate settlement and show the final stored statuses.

A Remix-only demo satisfies the interface requirement.

### Explicit judging checkpoints

- Can the team explain every input, the duration in seconds and the timestamp boundary?
- Do the correct recipients receive the stake in both outcomes?
- Do unauthorized, early, late and duplicate actions fail when called directly?
- Is the referee's real-world authority and potential dishonesty acknowledged?
- Is the team's scenario and contribution clearly distinguished from starter code?

### Optional extensions

Multiple referees, signed attendance evidence, group pledges, a goal dashboard,
or a dispute process. Explain additional trust assumptions and test any new
settlement path; none of these features is required.

---

## Challenge B: The Commons

**Difficulty: Intermediate.** Extend a working simulation; do not rebuild the
game infrastructure.

### Background, problem and real-world context

A fishery, community forest or aquifer can be depleted when each user gains by
taking more while everyone shares the cost. The Commons makes that tension
visible: players harvest a shared stock that regenerates between rounds and
collapses if depleted too far.

Your problem is to design an enforceable governance rule that changes player
incentives or access, then demonstrate its effect. Suggested connections:
**SDG 14: Life Below Water**, **SDG 15: Life on Land**, or **SDG 6: Clean Water
and Sanitation**. Explain that this is a simplified simulation, not a validated
ecological model.

### What to build and learn

Implement **at least one original resource-governance mechanism** on top of the
provided game. "Original" means your team selects, implements and explains its
own rule or adaptation; it need not invent a new research field.

Learn to read existing Solidity, reason about shared state over time, express a
rule as a contract check, write adversarial tests and compare outcomes under
the same player behavior.

Suitable scoped mechanisms include:

- **Harvest quotas:** allocate a share to each eligible player.
- **Conservation reserves:** reject harvests that would breach a protected stock.
- **Licensing:** make eligibility depend on a contract-managed permission.
- **Community voting:** allow a defined vote, not unilateral administration, to
  change a rule.
- **Dynamic limits:** reduce allowed harvesting as stock falls.

Choose one achievable mechanism first. Merely changing the starting capacity,
using the built-in boat limit, or adding a frontend warning is not a custom
governance mechanism.

### Tools and provided starting point

Required: Node.js **22.13 or later**, npm, Git, an editor, terminal access, the
dedicated starter kit and a phone/browser on the laptop's network. Use Hardhat's
local practice chain and Solidity; all installation commands are in
[Starter Kits](starter-kits.md).

The supplied [`contracts/Commons.sol`](https://github.com/zetech-forge/web3_starter-kit/blob/main/contracts/Commons.sol)
already implements registration, one harvest per player per round, a built-in
harvest limit, stock tracking, regeneration, collapse and readable scores.
Tests, deployment scripts, a game server, a host dashboard, QR joining and
mobile pages with throwaway practice wallets are provided.

Default settings in
[`scripts/deploy-commons.ts`](https://github.com/zetech-forge/web3_starter-kit/blob/main/scripts/deploy-commons.ts):

| Parameter | Default | Meaning |
| --- | --- | --- |
| Resource capacity | **1,000 units** | Starting stock and maximum capacity. |
| Collapse threshold | **100 units** | Collapse occurs when harvesting leaves stock **below** 100; exactly 100 is not collapsed. |
| Regrowth percentage | **50%** | A growth coefficient, not a flat 50% refill each round. |
| Round duration | **30 seconds** | How long each harvesting round lasts. |
| Maximum harvest per player per round | **50 units** | At most one successful harvest of up to 50 units in a round. |

For each elapsed round, growth uses integer arithmetic:
`stock += stock * growthPercent * (capacity - stock) / (capacity * 100)`.
For example, stock 900 becomes 945 after one default round. The contract
calculates elapsed growth when reading `stockNow()` and synchronizes stored
stock on harvesting; no new background blockchain scheduler is required.
Once collapsed, the stock does not recover.

### Numbered implementation steps

1. **Install and test.** Clone the dedicated kit, enter its root, run `npm ci`
   and `npm test`. Save the baseline result before changing any rules.
2. **Read the supplied contract.** Trace `join`, `harvest`, `_sync`, `stockNow`
   and `_mechanism`. Identify the checks already enforced before the hook.
3. **Choose one mechanism.** State the exact rule, which harvests it allows or
   rejects, and why it should help. Consider that one person may control
   several player wallets.
4. **Implement it in `_mechanism(address player, uint256 amount)`.** This
   initially empty internal function is called after stock synchronization and
   the built-in checks, but before harvest state changes. Use it to reject
   forbidden harvests or maintain your mechanism's state. Add helpers, storage
   or governed functions only as needed.
5. **Write tests.** Cover an allowed action, a prohibited action, boundary
   values and the effect across multiple players/rounds. Retain the supplied
   safety checks; explain any intentional changes to game-behavior assertions.
6. **Start the chain and deploy.** In Terminal 1 run `npm run chain`. Leave it
   running. In Terminal 2 run `npm run deploy:commons`.
7. **Launch the server.** In Terminal 3 run `npm run game`. Open
   `http://localhost:3000/?host` on the laptop/projector.
8. **Join from phones.** Connect laptop and phones to the same Wi-Fi or
   hotspot, then use the server's LAN URL/QR code. Players choose names; wallet
   installation is not needed. A phone must not use the laptop's `localhost` URL.
9. **Compare outcomes.** Show a baseline run without your mechanism and a fresh
   run with it under a comparable harvesting pattern. Record stock, accepted
   harvests and rejected harvests over a few rounds.
10. **Iterate and rehearse.** After contract edits run `npm test`, then
    `npm run deploy:commons`; the server picks up the new game. Restarting the
    chain also requires redeployment. Save the mechanism's rules and results.

Modify `_mechanism` and the settings needed for your experiment. Retain
registration, readable game state, stock accounting, event reporting,
regeneration, collapse and baseline safety restrictions. Do not remove
restrictions just to make the mechanism appear successful.

**Frontend changes are optional** unless a new interaction, such as voting, is
necessary to operate your mechanism. The existing controls are sufficient for
quotas or reserve rules. After frontend edits, run `npm run build:game` and
refresh the page.

### Mandatory functionality and on-chain enforcement

The built-in rules and your team's custom rule are separate requirements:

- Players can join and eligible players can harvest.
- Each harvest reduces stock and updates the player's total.
- Regeneration works between rounds; collapse remains permanent.
- An unregistered player, a second harvest in the same round, a harvest above
  the built-in limit, or a harvest above available stock must be rejected.
- At least one **additional team-designed rule** changes allowed behavior.
  Harvests violating it must revert even when sent directly to the contract.
- Neither the deployer nor a player may arbitrarily bypass or change the
  mechanism mid-game. If changes are allowed, enforce the declared governance
  procedure on-chain.

### Testing and minimum acceptance criteria

| Check | Evidence required |
| --- | --- |
| Join and harvest. | Multiple players can register; a permitted harvest changes stock and player totals. |
| Built-in restrictions. | Direct calls show rejection of unregistered, duplicate-round and excessive harvests. |
| Regeneration. | A known stock level grows according to the supplied formula after elapsed rounds. |
| Collapse. | Baseline tests prove collapse below the threshold and no recovery; the protected game retains that behavior if the threshold is reached. |
| Custom rule. | At least one harvest otherwise allowed by the baseline is rejected or constrained by your mechanism. |
| Boundary and multi-player behavior. | Tests cover the mechanism's limit and competing players, not only one successful call. |
| Behavioral effect. | A short comparison shows how the rule changes extraction, access or survival; report results rather than claiming universal sustainability. |
| Rule integrity. | No undeclared administrator/player shortcut bypasses the policy. |

Run `npm test`; for focused Solidity checks use:

```text
npx hardhat test solidity test/Commons.t.sol
```

A conservation mechanism may deliberately prevent a baseline depletion
sequence. Adapt that scenario or retain a separate baseline fixture for the
comparison; do not delete the rule checks or claim an untested collapse path.
List intentional changes to starter tests in your README.

### Demonstration, deliverables and network troubleshooting

Submit your own repository, mechanism specification, automated tests, setup
commands, SDG rationale and a brief baseline-versus-mechanism comparison.
Demonstrate the host dashboard, players joining from phones, harvesting,
regeneration and an on-chain rejection caused by your mechanism. Explain the
game in under a minute before inviting the audience to play.

Phones and laptop must share a network that permits device-to-device access.
If joining fails, verify the LAN URL/port, allow Node.js on a trusted private
network in the laptop firewall, or move all devices to one phone hotspot.
Do not expose blockchain RPC or disable the firewall. The existing game server
provides the phone-facing connection. Keep a short recording as backup if the
venue network is unreliable.

### Explicit judging checkpoints

- Can the team identify what the starter already enforced and what they added?
- Is the custom rule enforced by direct contract calls, not only the interface?
- Does a comparable before/after run support the claimed behavioral effect?
- Are stock accounting, growth, collapse and multi-player limits still correct?
- Can the team explain fairness trade-offs, multi-wallet abuse and the limits
  of its sustainability claim?

### Optional extensions

Voting, transferable licences, richer incentive experiments, a redesigned UI,
or comparisons across several strategies. Do not add a governance system or
frontend merely for complexity; one well-tested mechanism meets the scope.

---

## Challenge C: Leashed Agent

**Difficulty: Advanced.** Use a supplied agent and wallet to demonstrate that
contract policy remains effective even when model instructions are malicious.

### Background, problem and real-world context

An assistant that buys weather information for a farmer or supplies for a
clinic can save time, but permission to act must not become permission to spend
without limits. Prompts can be misleading, and a model can select the wrong
recipient or amount.

Build a useful payment workflow in which the model proposes actions but an
on-chain wallet controls what can actually be paid. Suggested connections:
**SDG 2: Zero Hunger**, **SDG 3: Good Health and Well-Being**, or **SDG 8: Decent
Work and Economic Growth**.

### What to build and learn

Configure the supplied agent for one concrete purchasing task, exercise its
wallet policies and demonstrate both allowed and rejected payments. Learn
role separation, spending-state accounting, on-chain authorization, payment
events and adversarial validation. You do not need to train a model, build an
agent framework or implement production payment infrastructure.

| Role | Authority |
| --- | --- |
| **Wallet owner** | Funds the wallet, manages the allowlist and agent, pauses operation and approves pending payment requests. The owner is trusted. |
| **AI agent** | Uses a separate limited signing account to pay within policy or submit a request. It cannot grant itself owner permissions. |
| **Approved recipients** | Addresses permitted to receive wallet payments, such as the mock data seller. Being approved does not grant owner or agent powers. |

The agent must never hold the owner's key. For the local demo, account **0** is
owner, account **1** is agent, and account **2** is data seller.

### Tools and provided starting point

Required: Node.js **22.13 or later**, npm, Git, an editor, terminal access, the
dedicated kit and Hardhat's local practice chain. Use either local
[Ollama](https://ollama.com/download), an approved OpenAI-compatible provider,
or the **`LLM_FAKE=1` fallback**; paid API access is not a prerequisite.

The kit supplies
[`contracts/PolicyWallet.sol`](https://github.com/zetech-forge/web3_starter-kit/blob/main/contracts/PolicyWallet.sol),
wallet tests, a deployment script, a working agent loop, command-line owner
controls and a mock paid data API. The current wallet implementation works;
complete TODOs only in an unfinished exercise copy. Your work is the chosen
use case, configuration, policy understanding, security evidence and any
clearly identified extensions.

### Default policy and approval semantics

Defaults from
[`scripts/deploy-policy-wallet.ts`](https://github.com/zetech-forge/web3_starter-kit/blob/main/scripts/deploy-policy-wallet.ts):

| Setting | Default |
| --- | --- |
| Initial practice wallet balance | **1 ETH** |
| Maximum autonomous spending | **0.05 ETH per one-hour window** |
| Owner approval threshold | **0.02 ETH per payment** |
| Initial allowed recipient | The local mock data seller |

These are practice amounts, not a requirement to obtain real ETH.

- A direct agent payment via `pay` must target an allowed recipient, be
  **at most 0.02 ETH**, and keep autonomous spending **at or below 0.05 ETH**
  in the current window.
- A new autonomous window starts on the next payment once at least one hour
  has elapsed from the current window's start; it is not a sliding-window sum.
- For a larger payment, the agent calls **`requestPayment()`**, which creates a
  pending request without transferring funds. The owner checks the request
  and submits **`approve()`** as a separate on-chain transaction.
- **Owner-approved payments are outside the autonomous window budget** in the
  provided contract and tests. The baseline intentionally permits an approved
  0.3 ETH payment despite the 0.05 ETH autonomous limit. Preserve and explain
  this distinction; do not silently make the window limit apply to approvals.
- Approval must still recheck the recipient allowlist, reject an already
  settled request and respect the paused state. The wallet also needs enough
  balance to transfer the amount.

**This is on-chain owner approval, not an off-chain cryptographic
co-signature.** Some legacy code identifiers use `coSignAbove` or `coSigned`;
they denote this request/approval flow, not a second signature collected by
the agent. The owner can approve a pending request even after revoking the
agent, provided other approval checks pass; revocation blocks new agent actions,
not the owner's authority.

### Numbered implementation steps

1. **Install and choose a task.** Follow [Starter Kits](starter-kits.md), run
   `npm ci`, and choose a small scenario such as buying mock weather or crop
   price data for a named location.
2. **Read and complete the wallet rules.** If your copy has TODOs, implement
   allowlist checks, autonomous budget accounting, approval enforcement and
   single settlement. In the working baseline, trace these paths rather than
   replacing them. Update state before sending funds and preserve events.
3. **Run wallet tests.** Use the focused command below. Verify the policy
   semantics before connecting the model; a cooperative model cannot fix a
   broken wallet.
4. **Deploy locally.** In Terminal 1 run `npm run chain`. In Terminal 2 run
   `npm run deploy:agent`. Keep the chain running; deployment funds the wallet
   and records role addresses in `deployments/agent.json`.
5. **Connect the mock API.** In Terminal 3 run `npm run data-api`. Leave it
   running at its default `http://localhost:4021`. Restart it after wallet
   redeployment so it reads the new deployment.
6. **Configure the agent.** In Terminal 4 use Ollama or the fake-mode commands
   below. For Ollama, install/start it and run `ollama pull qwen2.5:3b`; the
   default endpoint is `http://localhost:11434/v1`. Follow Starter Kits for
   shell-specific hosted-model configuration without committing credentials.
7. **Execute an authorized payment.** Ask for weather or market data. Show the
   allowed recipient, payment amount, successful transaction, recorded reason
   and returned mock data.
8. **Request a larger payment.** Use `request_owner_approval` with a real model,
   or the deterministic local-console procedure in Starter Kits, to submit
   `requestPayment` for the allowed seller. The fake fallback does **not**
   generate approval requests. Inspect the request and approve its actual ID
   through the owner command; verify it settles once.
9. **Exercise owner control.** The baseline already implements pause and
   revocation. Complete these only if missing from an exercise copy; demonstrate
   them with the commands below. Unpause does not restore a revoked agent.
10. **Attack and document.** Try unauthorized recipients, repeated payments,
    oversized payments and instructions to ignore the policy. Capture the
    contract's result, not only the model's response. Run the acceptance
    matrix, document the trust boundary and rehearse a backup demo.

Focused wallet tests:

```text
npx hardhat test solidity test/PolicyWallet.t.sol
```

**Fake mode on Linux/macOS (Bash/Zsh):**

```bash
LLM_FAKE=1 npm run agent -- "What will the weather be in Kiambu this week?"
```

**Fake mode on Windows PowerShell:**

```powershell
$env:LLM_FAKE = "1"
npm run agent -- "What will the weather be in Kiambu this week?"
```

For Ollama, disable fake mode first: `unset LLM_FAKE` in Bash/Zsh or
`$env:LLM_FAKE = "0"` in PowerShell, then run the same agent command without
the `LLM_FAKE=1` prefix.

Owner commands, from the kit root in another terminal:

```text
npm run owner -- pause
npm run owner -- unpause
npm run owner -- revoke
npm run owner -- approve 0
npm run owner -- allow PAYEE_ADDRESS
```

Replace `0` with the actual pending request ID and `PAYEE_ADDRESS` with the
intended sandbox recipient. `block PAYEE_ADDRESS` removes an allowed recipient;
`agent NEW_AGENT_ADDRESS` assigns a new agent. Do not run these commands
blindly in sequence: restore authorization or redeploy before continuing a
demo after revocation.

### Mandatory functionality and on-chain enforcement

Your demonstration must include a plain-language request leading to an allowed
payment, a separate owner-approved request, owner control and recorded payment
reasons. The wallet, not the prompt, must enforce role authorization, recipient
allowlisting, autonomous spending limits, the approval threshold and
single settlement.

The supplied data API **imitates an x402-style payment mechanism; it is not a
full production x402 implementation**. It returns HTTP 402 with a price, then
checks the payment transaction and payer signature before serving mock data.
Those payer signatures are separate from the wallet's on-chain owner approval.
Do not claim production x402 interoperability or real-world data accuracy.

### Security tests and minimum acceptance criteria

| Test | Required outcome |
| --- | --- |
| Allowed small payment. | Pays the approved recipient within threshold and budget; emits `Paid` with amount, recipient and reason. |
| Unauthorized recipient. | Direct payment and new payment request are rejected. Blocking a payee before approval also prevents settlement. |
| Autonomous overspending. | Several individually permitted payments exceeding 0.05 ETH in the same window are rejected; spending can resume in a new window. |
| Approval threshold. | A direct payment above 0.02 ETH is rejected even if the remaining autonomous budget is sufficient. |
| Owner-approved payment. | Request alone moves no funds; only the owner can approve. A valid large approval succeeds outside the autonomous budget. |
| Paused agent. | New payments and requests are rejected; approvals are also blocked until unpaused. |
| Revoked agent. | The old agent cannot make new payments or requests after revocation. |
| Duplicate approval. | Reapproving a settled request reverts and sends no additional funds. |
| Unauthorized policy change. | Agent/stranger cannot change payees, pause state or agent authorization, or approve requests. |
| Malicious instruction. | A tool may attempt an invalid transaction, but the wallet rejects it and balances/spending state do not reflect a successful payment. |
| Payment reason. | Successful direct and owner-approved payments record the stated reason on-chain; this is a log, not proof the statement is true. |

Use contract tests for precise window/threshold cases and agent runs for
end-to-end evidence. Test **exactly 0.02 ETH**, exactly the remaining autonomous
budget and the first action after a window expires. Keep existing wallet test
semantics; do not bypass the wallet or remove failing assertions.

The fake fallback deliberately follows simple request patterns. It is an
acceptable model substitute, not an intelligent or safe assistant. Its final
text may say "Done" even when the tool reports an error: judges should inspect
the transaction/tool result and wallet state.

### Deliverables and demonstration

Submit your own repository with reproducible commands, tests, a role/policy
explanation, the purchasing use case, model/fallback configuration, known risks
and the **2-3 minute backup demo video** required by the track submission rules.

Demonstrate:

1. A useful authorized purchase and its on-chain reason.
2. An unapproved recipient or excessive autonomous payment being rejected.
3. A pending large request, owner approval and duplicate-approval rejection.
4. Pause and revocation stopping the agent's new actions.
5. A malicious instruction failing to bypass the wallet, even if the model
   agrees with the instruction.

### Explicit judging checkpoints

- Are owner, agent and recipient roles genuinely separate?
- Can the team explain the autonomous budget versus explicit owner approval?
- Do restrictions hold for direct contract calls and malicious model outputs?
- Do the request, approval, events and returned data form a reproducible flow?
- Are credentials absent from the repository and production-security claims avoided?
- Is the team's contribution identified separately from supplied infrastructure?

### Optional extensions

A new mock purchasing task, tighter policy controls, several agent roles,
request expiry, a read-only audit dashboard, or genuine x402 integration.
Any change to owner-approved spending semantics must be explicitly described
as an extension, with separate tests and updated documentation; it is not
required for the baseline challenge.
