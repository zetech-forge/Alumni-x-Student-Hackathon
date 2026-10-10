---
title: Challenges
parent: Web3 & Blockchain
nav_order: 4
---

# Web3 & Blockchain: Challenges

Pick **one** of the three challenges below and build it across both days. There are no per-challenge points: whichever you pick is judged against the shared rubric in [Track Rules & How to Compete](rules.md). Challenges A and B need no blockchain experience; the Day 1 bootcamp teaches enough to start. Challenge C is for teams that already have some.

Every team must connect its solution to a UN Sustainable Development Goal. Each challenge suggests one, but any SDG works if you can explain the link.

Three things apply to every challenge:

- **Why a blockchain?** Judges will ask why your solution needs a chain instead of a shared database. Have a one-sentence answer.
- **Judges will try to break your contract.** Each challenge lists rules that must be enforced on-chain, not just hidden in the UI. Expect a judge to call your contract directly during the demo and try to violate them.
- **Practice money only.** Challenge A runs on Remix's built-in test chain. Challenges B and C run a practice chain on your own laptop with the [starter kit](starter-kits.md). Wallets come funded, so nobody needs a faucet or real money. Deploying to a public testnet such as Sepolia as well is a plus.

---

## Challenge A: The Pledge

_Beginner. The whole contract can be built in Remix, in the browser, with nothing to install._

**Suggested SDG:** SDG 4 (Quality Education), SDG 3 (Good Health & Well-Being) or SDG 13 (Climate Action). People keep goals better when something is at stake: attend every lecture this month, run three times a week, plant ten trees. Put money behind the promise, and even a failed goal funds a good cause.

**The problem:** Build a contract where someone stakes money on a personal goal with a deadline, and a referee they choose confirms whether they did it. Succeed and the stake comes back. Fail and it goes to a charity.

**What "done" looks like:**

- Anyone can create a pledge with a goal, deadline, stake, referee and charity address
- Only the referee can confirm success before the deadline, which returns the stake
- After the deadline, anyone can send an unconfirmed pledge's stake to the charity
- Anyone can read every pledge and its status

**Must revert on-chain:** the pledger taking their stake back early, anyone but the referee confirming, confirming after the deadline, and paying out the same pledge twice.

**Constraints:** A web page is a plus; a clear demo in Remix is enough.

**Provided:** a [contract skeleton and a step-by-step Remix walkthrough](starter-kits.md#challenge-a-the-pledge-in-remix).

**Deliverable:** repo and a live demo.

**Judging note:** the chain can't see whether you went to class. It trusts the referee, and your friend might lie for you. Teams that name this and design around it (several referees, attendance signed by the lecturer) score higher on approach. Stretch goal: group pledges, where people who succeed split the stakes of those who don't.

---

## Challenge B: The Commons

_Beginner-friendly with a high ceiling. The starter game works out of the box; your job is to change its rules._

**Suggested SDG:** SDG 14 (Life Below Water), SDG 15 (Life on Land) or SDG 6 (Clean Water & Sanitation). A Lake Victoria fishery, a community forest and a shared aquifer all fail the same way: each user gains by taking a little more, and together they drain it.

**The problem:** Turn the provided on-chain game into one that survives its players. A shared resource regrows each round by rules in the contract, and players harvest from their phones. Overharvest, and it collapses for everyone. Your team designs the mechanism that keeps it alive: quotas, a harvest tax, licences, a vote, or something new.

**What "done" looks like:**

- The stock regrows each round by rules in the contract and collapses for good below a threshold
- Players join from a phone browser with no wallet setup, harvest once per round, and see everyone's harvests live
- At least one mechanism of your own design changes how players behave

**Must revert on-chain:** harvesting twice in a round, harvesting more than your mechanism allows, and anyone, including the deployer, changing the rules mid-game outside the mechanism itself.

**Constraints:** Players' phones join the game server on your laptop over the venue wifi, or over a phone hotspot if the wifi blocks it. Keep the game playable by a room of strangers in under a minute of explanation.

**Provided:** a [working starter game](starter-kits.md#challenge-b-the-commons): the lake contract with tests, a phone web page with throwaway wallets, a big-screen view with a join QR code, and a game server.

**Deliverable:** repo and a live game the audience plays during your demo.

**Judging note:** show the commons collapsing without your mechanism and surviving with it, using real players behaving selfishly. A mechanism that survives a greedy room beats a polished UI. Stretch goal: let players vote to change the mechanism mid-game.

---

## Challenge C: Leashed Agent

_Highest ceiling. Pick this only if someone on your team has written a smart contract or called an LLM API before._

**Suggested SDG:** SDG 2 (Zero Hunger), SDG 3 (Good Health & Well-Being) or SDG 8 (Decent Work & Economic Growth). An AI agent that buys weather and market-price data for a smallholder farmer, or restocks a rural clinic, saves hours of work. It also holds money, and anyone who can talk to it can try to talk it into spending.

**The problem:** Build an AI agent that pays for things on someone's behalf from a smart-contract wallet whose rules the agent cannot override, however it is prompted.

**What "done" looks like:**

- The agent takes a plain-language request and pays an allowed payee from the policy wallet
- The wallet enforces a payee allowlist, a spending limit per time window, and the owner's co-signature above a set amount
- The agent holds only a limited key that the owner can pause or revoke at any time
- Every payment is logged on-chain with the agent's stated reason

**Must revert on-chain:** a payment to a payee not on the allowlist, a payment over the window limit, and a payment above the threshold without the owner's co-signature, whatever the agent was told.

**Constraints:** Any LLM and any agent framework. The agent never holds the owner's key. Paying for a data API with x402, the HTTP payment standard for agents, is a plus but not required. _(TBD: confirm with organizers whether shared API keys or a local model are available at the venue.)_

**Provided:** a [policy wallet skeleton with tests, a working agent loop, owner controls and a mock paid data API](starter-kits.md#challenge-c-leashed-agent).

**Deliverable:** repo and a recorded backup demo (60 seconds is enough) in case the model misbehaves live.

**Judging note:** judges will try to talk your agent into overspending. A jailbreak that fools the agent is fine; a jailbreak that moves money is not. Score goes to the contract's guarantees, not the agent's cleverness.
