---
title: Web3 starter kit
nav_exclude: true
search_exclude: true
---

# Web3 & Blockchain starter kit

Setup steps and walkthroughs for all three challenges are on the [Starter Kits](../starter-kits.md) page.

```bash
npm install
npm test
```

| Command | What it does |
|---|---|
| `npm test` | Runs the Solidity tests and the game page tests in `test/` |
| `npm run chain` | Starts the local practice chain |
| `npm run deploy:commons` | Deploys a fresh Commons game (set `ROUND_SECONDS` to change the round length) |
| `npm run game` | Serves the Commons game to phones on your network |
| `npm run build:game` | Rebuilds the game page after you edit `commons/web/src/` |
| `npm run deploy:agent` | Deploys the PolicyWallet for the Leashed Agent |
| `npm run data-api` | Starts the mock paid data API |
| `npm run agent -- "request"` | Runs the agent |
| `npm run owner -- pause` | Owner controls: pause, unpause, revoke, approve, allow, block, agent |

`contracts/Pledge.sol` and `contracts/PolicyWallet.sol` are skeletons, so their tests fail until you finish the TODOs. `contracts/Commons.sol` is a complete game with no mechanism yet.
