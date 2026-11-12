---
title: Starter Kits
parent: Web3 & Blockchain
grandparent: Hackathon Tracks
nav_order: 5
---

# Web3 & Blockchain: Starter Kits

The official starter kit now lives in its own repository:
**[zetech-forge/web3_starter-kit](https://github.com/zetech-forge/web3_starter-kit)**.
It contains the Solidity contracts, automated tests, deployment scripts, Commons
game frontend and server, AI agent, owner controls, and mock paid data API.

All project files are at the root of the dedicated starter repository.
This page takes you from choosing a challenge to running a demo and creating
your own team's repository.

## 1. Choose your setup

| Challenge | What you need |
| --- | --- |
| **A: The Pledge** | A browser and [Remix IDE](https://remix.ethereum.org). You can complete this challenge without installing the full kit. The kit is optional if you want to run its automated tests locally. |
| **B: The Commons** | The dedicated starter kit installed on a laptop. Phones join the laptop's game server; players do not need to install wallets or developer tools. |
| **C: Leashed Agent** | The dedicated starter kit plus a local AI model, an approved OpenAI-compatible model service, or the supported `LLM_FAKE=1` mock fallback. The mock fallback needs no model or API key. |

Everything below uses practice funds, not real money. Read the
[security reminders](#7-security-reminders) before starting.

## 2. Install the kit (Challenges B and C; optional for A)

### Prerequisites

Install or have access to:

- [Node.js](https://nodejs.org/en/download) **22.13 or later**, preferably a
  supported even-numbered LTS release. npm is normally installed with Node.js.
- **npm**, the package manager used to install the locked dependencies.
- [Git](https://git-scm.com/downloads).
- [Visual Studio Code](https://code.visualstudio.com) or another code editor.
- A terminal: **PowerShell** on Windows, or a terminal running **Bash/Zsh** on
  Linux/macOS.
- An internet connection for cloning, downloading dependencies, and Hardhat's
  first Solidity compiler download.

Open a new terminal after installing the tools. Confirm that these commands
print versions rather than "command not found":

```text
node --version
npm --version
git --version
```

### Download and install

The following commands work in PowerShell, Linux and macOS:

```text
git clone https://github.com/zetech-forge/web3_starter-kit.git
cd web3_starter-kit
npm ci
npm test
```

If GitHub reports that the repository cannot be found, confirm the URL and
contact the organizers for repository access.

`npm ci` installs the exact dependency versions in `package-lock.json`. Keep
that file; do not delete it or regenerate it just to make installation succeed.
An audit warning is different from an installation failure. The migrated
lockfile has known dependency audit findings; keep this kit in the local
sandbox and do not run `npm audit fix --force` as a setup step.

Open the downloaded folder in your editor. **Run every project command below
from the folder containing `package.json`.** Each new terminal must also be in
that folder.

### What to expect from tests

`npm test` runs the Solidity tests and the frontend/Node.js tests. On the first
run, Hardhat may download the configured Solidity compiler before compiling.
You can compile separately with:

```text
npm run build
```

**The current dedicated repository is a working baseline:** the Pledge and
PolicyWallet TODOs were completed during migration and have automated regression
tests. A fresh copy of the current baseline should pass, including the
Commons and game-page tests.

If your instructor supplies an **unfinished exercise copy**, Pledge and
PolicyWallet tests initially fail until you implement that copy's relevant
TODOs. Use each failing test name as a checklist of the missing rule; a
compilation success alone does not mean those rules work. Commons baseline
tests should still pass before you introduce your own mechanism. Do not remove
tests or weaken safety assertions just to obtain a green result.

## 3. Challenge A: The Pledge in Remix

The Pledge holds a stake against a goal. A chosen referee confirms success and
returns the stake to the pledger. If the deadline is reached without success, the
stake can be sent to a charity.

### Open, compile and deploy

1. Open [the official `contracts/Pledge.sol`](https://github.com/zetech-forge/web3_starter-kit/blob/main/contracts/Pledge.sol).
   Use **Raw** to copy the Solidity source rather than the GitHub page.
2. Open [Remix IDE](https://remix.ethereum.org). In its file explorer, create
   `Pledge.sol` and paste in the source.
3. If you have an unfinished exercise version, implement the TODOs in `confirm`
   and `release`: check authorization, deadline and active status; update
   status before transferring the stake; emit the appropriate event. The
   official baseline implements confirmation strictly before the deadline
   (`block.timestamp < deadline`) and release at or after it
   (`block.timestamp >= deadline`).
4. Open **Solidity Compiler**, choose **0.8.34** (the kit's configured version)
   or another compatible version at least 0.8.24, then click **Compile Pledge.sol**.
5. Open **Deploy & Run Transactions**. Select a **Remix VM** environment, not
   Injected Provider or a real wallet. Remix VM supplies funded practice accounts.
6. Select the `Pledge` contract, leave **Value** at `0`, and click **Deploy**.
   Expand it under **Deployed Contracts**.

### Understand the pledge inputs

Before calling `create`, choose three distinct Remix VM accounts:

- **Pledger:** the selected Account that calls `create` and supplies the stake.
- **Referee:** a different account allowed to confirm the goal was achieved.
- **Charity:** the account that receives the stake if the goal is not confirmed.

Copy their addresses somewhere you can identify them during the demo.

| Input | Meaning | Example |
| --- | --- | --- |
| `goal` | A readable description of the promise. | `"Attend every lecture this week"` |
| Stake | The **Value** sent with `create`, not a function parameter. Choose the **ether** unit. | `1` practice ether |
| `durationSeconds` | How long from creation until the deadline, in seconds; not a date or timestamp. | `120` |
| `referee` | The referee's nonzero address, different from the pledger. | A second Remix VM account |
| `charity` | A nonzero address to receive a failed pledge's stake. | A third Remix VM account |

Set **Value** to `1` ether, select the pledger account, and call
`create(goal, durationSeconds, referee, charity)`. Then **reset Value to `0`**
before calling nonpayable functions such as `confirm` and `release`.

Pledge IDs start at **0** and increase with each successful `create`. Use
`count()` and `pledges(id)` to inspect them. The returned status is
`0 = Active`, `1 = Succeeded`, or `2 = Failed`.

### Demonstrate a successful pledge

1. Create a pledge with a duration long enough to finish the demo.
2. Note its ID and inspect its stored stake and status.
3. Switch Account to its referee and call `confirm(id)` before its deadline.
4. Show status `Succeeded` and that the stake returned to the pledger. Account
   balances also include transaction gas costs, so inspect the status as well.

### Demonstrate a failed pledge

**Create a separate pledge.** You cannot turn an already successful pledge into
a failed one.

1. Create another pledge with a short duration, such as 30 seconds; note its ID.
2. Do not confirm it. Wait until its stored deadline is reached or has passed.
3. From any VM account, call `release(id)`.
4. Show status `Failed` and that the charity received the stake.

Settlement does not happen automatically when time runs out: someone must call
`release`. If Remix still reports that the deadline has not been reached, wait longer
and send another transaction; contract time is the latest block's timestamp.

### Try to break the rules

Use fresh active pledges where necessary so one rejection does not hide another:

| Attempt | Expected result |
| --- | --- |
| The pledger or a stranger calls `confirm(id)`. | Reverts: only the chosen referee may confirm. |
| Anyone calls `release(id)` before the deadline. | Reverts: release is only allowed at or after the deadline. |
| The referee calls `confirm(id)` exactly at or after the deadline on an active pledge. | Reverts: confirmation is too late. |
| Anyone calls `release(id)` exactly at the deadline on an active pledge. | Succeeds: the charity receives the stake. Use automated tests to set this timestamp precisely. |
| Confirm a successful pledge again, release it after its deadline, or release a failed pledge again. | Reverts: a settled pledge cannot pay out twice. |

After changing source code in Remix, compile and **deploy a new instance**;
an existing deployment does not change. If you also installed the kit, copy
your edited source into `contracts/Pledge.sol` and run:

```text
npx hardhat test solidity test/Pledge.t.sol
```

## 4. Challenge B: The Commons

The Commons is a shared-resource game: the stock regrows each round, players
harvest, and excessive harvesting causes permanent collapse. Your team designs
the on-chain mechanism that makes the resource survive.

### Start a local game

Use three terminals, all in the starter-kit root.

**Terminal 1: start the practice blockchain**

```text
npm run chain
```

Leave it running. This is a blockchain on your laptop, with funded test accounts
and no real money. It listens at `http://127.0.0.1:8545`, using chain ID
**31337**. Printed RPC requests are normal. Restarting it resets its state, so
you must redeploy after every restart.

**Terminal 2: deploy the Commons contract**

```text
npm run deploy:commons
```

This deploys a fresh lake to the running local chain and writes local deployment
information to `deployments/commons.json`. Keep that generated file out of Git.

**Terminal 3: start the game server**

```text
npm run game
```

This builds the frontend automatically and starts the server. Leave it running.

- **Host dashboard:** open `http://localhost:3000/?host` on the laptop/projector.
  It shows the lake, round history, previous-round summary, top harvesters and a
  join QR code.
- **Mobile interface:** players open the LAN URL printed by the server, or scan
  the dashboard's join QR code. They choose a name and harvest from their phone
  browser; throwaway practice wallets are created automatically.
- **Do not give phones a `localhost` link.** On a phone, `localhost` refers to
  the phone itself, not the laptop.

The server funds at most three player wallets per device and restricts forwarded
transactions to the game contract. A person can still control multiple players;
do not assume that one wallet means one human.

### Change your game's rules

Use these files in the dedicated repository:

- **Resource-management mechanism:** [`contracts/Commons.sol`](https://github.com/zetech-forge/web3_starter-kit/blob/main/contracts/Commons.sol),
  specifically `_mechanism`. Enforce quotas, taxes, licences or governance
  on-chain, not only in the UI. Revert when a harvest breaks your rules.
- **Starting settings:** [`scripts/deploy-commons.ts`](https://github.com/zetech-forge/web3_starter-kit/blob/main/scripts/deploy-commons.ts)
  contains lake capacity, collapse threshold, regrowth, round duration and boat size.
- **Frontend:** [`commons/web/src/`](https://github.com/zetech-forge/web3_starter-kit/tree/main/commons/web/src)
  and [`commons/web/index.html`](https://github.com/zetech-forge/web3_starter-kit/blob/main/commons/web/index.html).

For example, a simple per-harvest quota inside `_mechanism` is:

```solidity
function _mechanism(address, uint256 amount) internal virtual {
    require(amount <= stock / players.length, "That is more than your fair share");
}
```

This is only an example, not a proven fair allocation: stock changes as people
harvest, and players can control multiple wallets. Design and test your own rules.

After contract changes, run:

```text
npm test
npm run deploy:commons
```

Keep the chain and game server running. The server and open pages pick up the
fresh deployment without a server restart. Your mechanism may intentionally
change expectations in `test/Commons.t.sol`; update the relevant game-behavior
tests and add tests for each new rule, while preserving safety checks.

After editing frontend source, run this and refresh the browser:

```text
npm run build:game
```

### Optional: shorter rounds

The default round length is 30 seconds. Set a shorter duration in the
**deployment terminal**, then deploy.

**Linux/macOS (Bash/Zsh):**

```bash
ROUND_SECONDS=15 npm run deploy:commons
```

**Windows PowerShell:**

```powershell
$env:ROUND_SECONDS = "15"
npm run deploy:commons
Remove-Item Env:ROUND_SECONDS
```

### Connect phones and troubleshoot

1. Connect the laptop and all phones to the **same Wi-Fi network**.
2. Use the laptop's LAN address shown by the server, with port `3000`.
3. Allow Node.js through the laptop firewall on **private/trusted networks**.
   Do not disable your firewall or open the blockchain RPC port to the network.
4. If venue Wi-Fi blocks device-to-device traffic, use a phone hotspot and
   connect both the laptop and players' phones to it. Recheck the printed LAN
   address after changing networks; restart the game server if needed.
5. If the server says no game is deployed, check that the chain is running and
   rerun `npm run deploy:commons`. If a port is already in use, stop your own
   earlier process with **Ctrl+C** rather than starting duplicate servers.

## 5. Challenge C: Leashed Agent

An agent buys data or pays suppliers through a PolicyWallet. The model may
misunderstand a request or accept a malicious prompt; the wallet must enforce
the spending policy regardless.

### Prepare the wallet rules

Open [`contracts/PolicyWallet.sol`](https://github.com/zetech-forge/web3_starter-kit/blob/main/contracts/PolicyWallet.sol)
and [`test/PolicyWallet.t.sol`](https://github.com/zetech-forge/web3_starter-kit/blob/main/test/PolicyWallet.t.sol).
The official migrated version is implemented. If you received an unfinished
exercise copy, complete `pay` and `approve` before attempting a purchase:

- `pay` must enforce the payee allowlist, owner-approval threshold and spending
  window; update spending before transferring funds and emit `Paid`.
- `approve` must be owner-only, recheck the payee allowlist, prevent duplicate
  settlement, mark a request done before transferring funds, and emit `Paid`.
- Preserve pause, agent authorization and revocation checks. The current
  baseline also blocks approvals while paused.

Run the focused tests until they pass:

```text
npx hardhat test solidity test/PolicyWallet.t.sol
```

The default autonomous budget is **0.05 practice ETH per one-hour window**.
Payments **above 0.02 ETH** need owner approval. Explicit owner-approved
requests are outside the autonomous budget in the provided baseline; the owner
is deliberately trusted to approve larger purchases. Do not describe that
autonomous limit as a cap on all owner-authorized spending.

### Start the services in order

Use four terminals in the starter-kit root. If the Commons practice chain is
already running, reuse it; do not start a second chain on the same port.

**Terminal 1: local practice chain**

```text
npm run chain
```

**Terminal 2: deploy and fund the wallet**

```text
npm run deploy:agent
```

The script deploys the wallet with **1 practice ETH**, allows the data seller,
and writes `deployments/agent.json`. Local account **0** is the owner, account
**1** is the agent, and account **2** is the seller. The agent must never hold
the owner's key.

**Terminal 3: mock paid data API**

```text
npm run data-api
```

Leave it running at `http://localhost:4021`. Its weather and market-price data
are mock data, not real forecasts or live prices.

**Terminal 4: choose one model option and run the agent**

#### Option A: supported mock fallback (no model or API key)

**Linux/macOS (Bash/Zsh):**

```bash
LLM_FAKE=1 npm run agent -- "What will the weather be in Kiambu this week?"
```

**Windows PowerShell:**

```powershell
$env:LLM_FAKE = "1"
npm run agent -- "What will the weather be in Kiambu this week?"
```

The deterministic fallback selects a tool from the request and intentionally
does not resist malicious instructions. It is useful for showing that the
contract, not the model, protects funds. A successful weather purchase should
print mock forecast data.

On Linux/macOS, repeat the `LLM_FAKE=1` prefix for **each** fallback command.
In PowerShell the variable stays set in that terminal until you remove it:

```powershell
Remove-Item Env:LLM_FAKE
```

#### Option B: local Ollama model

Install [Ollama](https://ollama.com/download), keep its service/application
running, then download the default model:

```text
ollama pull qwen2.5:3b
```

Model downloads can take time and need disk space. Ensure fake mode is off
before running the agent.

**Linux/macOS (Bash/Zsh):**

```bash
unset LLM_FAKE
npm run agent -- "What will the weather be in Kiambu this week?"
```

**Windows PowerShell:**

```powershell
$env:LLM_FAKE = "0"
npm run agent -- "What will the weather be in Kiambu this week?"
```

The default model is `qwen2.5:3b` at `http://localhost:11434/v1`. If you receive
a connection error, check that Ollama is running. If the model is unavailable,
finish the demo using Option A.

#### Option C: an approved hosted model

Use an OpenAI-compatible provider permitted by the organizers. Set the following
in the **agent terminal**, replacing the placeholders with your approved
provider's endpoint, model name and API credential.

**Linux/macOS (Bash/Zsh):**

```bash
unset LLM_FAKE
export LLM_BASE_URL="https://YOUR-PROVIDER/v1"
export LLM_MODEL="YOUR-MODEL"
read -r -s -p "API key: " LLM_API_KEY  # Bash
export LLM_API_KEY
npm run agent -- "What will the weather be in Kiambu this week?"
unset LLM_API_KEY
```

For **Zsh** on macOS, replace the `read` line with:

```zsh
read -r -s "LLM_API_KEY?API key: "
```

**Windows PowerShell:**

```powershell
$env:LLM_FAKE = "0"
$env:LLM_BASE_URL = "https://YOUR-PROVIDER/v1"
$env:LLM_MODEL = "YOUR-MODEL"
$credential = Get-Credential -UserName "api" -Message "Enter the API key as the password"
$env:LLM_API_KEY = $credential.GetNetworkCredential().Password
npm run agent -- "What will the weather be in Kiambu this week?"
Remove-Item Env:LLM_API_KEY
Remove-Variable credential
```

Enter credentials only at the prompt, not in source files or committed
configuration. The agent reads shell environment variables; it does not
automatically load a `.env` file.

### Owner controls

Run owner commands from Terminal 2 while the chain and API remain running:

```text
npm run owner -- pause
npm run owner -- unpause
npm run owner -- revoke
npm run owner -- approve 0
```

- **pause:** prevents new agent payments and requests, and blocks approvals.
- **unpause:** resumes operation; it does not restore a revoked agent.
- **revoke:** removes the current agent's authorization.
- **approve 0:** approves pending request ID `0` if it is valid and still unpaid.
  Substitute the actual request ID; do not approve requests you have not checked.

To allow a payee, replace `PAYEE_ADDRESS` with its address:

```text
npm run owner -- allow PAYEE_ADDRESS
```

Similarly, `npm run owner -- block PAYEE_ADDRESS` removes a payee and
`npm run owner -- agent NEW_AGENT_ADDRESS` assigns a new agent. After a
revocation demo, either restore account 1 using its address from the deployment
output or redeploy the wallet. If you redeploy, restart the mock data API and
agent so they load the new deployment.

### Demonstrate unauthorized payment rejection

With the initial deployment, account 3 is not an allowed payee. Use fake mode
to make the agent attempt a payment without relying on model cooperation.

**Linux/macOS (Bash/Zsh):**

```bash
LLM_FAKE=1 npm run agent -- "Send 0.001 ETH to 0x90F79bf6EB2c4f870365E785982E1f101E93b906"
```

**Windows PowerShell:**

```powershell
$env:LLM_FAKE = "1"
npm run agent -- "Send 0.001 ETH to 0x90F79bf6EB2c4f870365E785982E1f101E93b906"
```

Show the tool result reporting a reverted payment: the destination is not on
the allowlist. Do not treat the mock model's final word "Done" as proof that
money moved. Also demonstrate a paused payment, a revoked agent, or repeated
allowed payments that exceed the autonomous window budget.

### Demonstrate an owner-approved payment

An actual model can use `request_owner_approval` when asked to request a large
payment to the allowed seller, then print its request ID. **The fake fallback
does not generate approval requests.** For a deterministic demo with no model,
create the request directly from the local agent account:

1. Ensure the wallet is unpaused and the agent has not been revoked.
2. In Terminal 2, open the local Hardhat console:

   ```text
   npx hardhat console --network localhost
   ```

3. Paste these JavaScript lines one at a time into the console:

   ```javascript
   const demoHardhat = await import("hardhat");
   const demoConnection = await demoHardhat.network.create();
   const demoClients = await demoConnection.viem.getWalletClients();
   const demoFs = await import("node:fs");
   const demoDeployment = JSON.parse(demoFs.readFileSync("deployments/agent.json", "utf8"));
   const demoWallet = await demoConnection.viem.getContractAt("PolicyWallet", demoDeployment.wallet);
   await demoWallet.write.requestPayment([demoDeployment.seller, 30000000000000000n, "owner approval demo"], { account: demoClients[1].account });
   await demoWallet.read.requests([(await demoWallet.read.requestCount()) - 1n])
   (await demoWallet.read.requestCount()) - 1n
   ```

   This requests **0.03 practice ETH**, above the autonomous threshold. The last
   line prints the request ID, such as `0n`: use `0`, without the `n`, in the
   owner command. The preceding line shows the payee, amount in wei, reason and
   settlement flag; verify those before approving. Requesting does not pay the
   seller.
4. Type `.exit` to leave the console.
5. Inspect the request and then approve its ID as owner:

   ```text
   npm run owner -- approve 0
   ```

6. Show the successful transaction. Repeat the approval command to demonstrate
   that the same request cannot pay twice.

The console demo intentionally uses the laptop's unlocked **local test
accounts** to distinguish agent and owner actions. It is not a pattern for
handling production keys.

### How the paid API works

The mock server imitates an [x402](https://www.x402.org/)-style HTTP payment flow,
but **does not implement the real x402 protocol**. Without payment it returns
HTTP **402** and a price. The agent pays from the wallet, then retries with
`X-PAYMENT` containing the transaction hash and `X-PAYMENT-SIGNATURE` containing
the payer's signature of that hash. The server verifies payment before returning
mock data.

If an agent command cannot find the wallet deployment, run `npm run deploy:agent`.
If purchases fail, read the reported contract error, check that the wallet is
unpaused and the agent is authorized, and confirm the mock API is running.
Restart the API after changing or redeploying its wallet.

## 6. Create and submit your team's independent repository

Use the official kit as your **project template**, not as a shared workspace.
Every team must own and submit its own GitHub repository.

1. On GitHub, create a **new empty repository** under your account or team.
   Do not initialize it with a README, license or `.gitignore` if you are
   following the commands below.
2. In your existing local starter-kit clone, rename the official remote to
   `upstream`. Add **your team's** repository as `origin`, replacing both
   placeholders:

   ```text
   git remote rename origin upstream
   git remote add origin https://github.com/YOUR-TEAM/YOUR-PROJECT.git
   git remote -v
   ```

3. Confirm that **origin points to your repository**, not Zetech Forge's.
   Push the starting project to your empty repository:

   ```text
   git push -u origin HEAD
   ```

4. Develop in this clone. Update your project's README with your problem, SDG,
   setup, architecture, demo steps and team details. Keep tests and the lockfile.
5. Before each commit, inspect `git status` and ensure no generated files,
   wallet exports or credentials are included. Commit and push your work:

   ```text
   git add .
   git commit -m "Implement our challenge solution"
   git push origin HEAD
   ```

6. Submit **your own project repository URL**, along with the demo materials
   required by the [track rules](rules.md).

If GitHub's **Use this template** button is available on the official repository,
you may use it instead of the remote-renaming procedure: create your team
repository, clone **that repository**, then run `npm ci` in its root. The
clone-and-change-remotes procedure above also works when that button is absent.

**Never push your team's solution to the official
`zetech-forge/web3_starter-kit` repository or to its `upstream` remote.**
The official kit is the common starting point; your deliverable is your
independent project.

## 7. Security reminders

- **Practice funds only. Never use real wallets, real ETH or mainnet.**
- Default Hardhat accounts and their test mnemonic are public and unsafe for
  real assets. Use them only on the approved local practice chain. Never fund
  those accounts on a public network, including public testnets.
- The local chain binds to loopback. Keep blockchain RPC private. The Commons
  server listens on the LAN for phones; use trusted Wi-Fi/hotspots only and
  never publish the game server or mock API to the internet.
- Never upload real private keys, seed phrases, API credentials or wallet files
  to GitHub. Do not put credentials in screenshots, demo recordings or chat.
  `.gitignore` does not remove a secret that was already committed.
- Keep `node_modules/`, `artifacts/`, `cache/`, `deployments/`, generated bundles,
  build output, temporary data and environment files out of commits. Keep
  `package-lock.json` in commits.
- Only use the approved local practice chain or **testnets explicitly permitted
  by the organizers**. Public-testnet deployment is not needed for these local
  walkthroughs. If a permitted testnet is used, obtain network-specific
  instructions and use a fresh, disposable test-only wallet, never the default
  Hardhat accounts or a wallet that holds real assets.
- Keep agent and owner credentials separate. The agent must never receive the
  owner's signing key.
- These educational contracts and servers are not audited production systems.
  A passing test suite is not a security guarantee.

When finished, press **Ctrl+C** in the terminals running the game server, mock
API and local chain. Restarting the practice chain later requires redeploying
the relevant contracts.
