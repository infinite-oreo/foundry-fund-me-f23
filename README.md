# Foundry Fund Me

A simple crowdfunding contract built with Foundry. It accepts ETH contributions, enforces a minimum USD value using a Chainlink price feed, and allows only the owner to withdraw. Includes deployment and interaction scripts plus unit/integration tests.

## About

Key pieces:
- `src/FundMe.sol`: main contract with `fund`, `withdraw`, and `cheaperWithdraw`.
- `src/PriceConverter.sol`: library that converts ETH to USD using a Chainlink feed.
- `script/DeployFundMe.s.sol`: deploys `FundMe` with a network-appropriate price feed.
- `script/Interactions.s.sol`: helper scripts to fund and withdraw.
- `test/unit/*`: unit tests for core logic and zkSync devops checks.
- `test/integration/*`: integration test that runs the scripts end-to-end.

## Requirements

- Foundry (`forge`, `anvil`)
- Node.js (only needed for `zk-anvil`)
- A `.env` file if deploying to live networks

## Getting Started

### Install dependencies

```bash
forge install
```

Or use the Makefile:

```bash
make install
```

### Build

```bash
forge build
```

### Test

```bash
forge test
```

Run only integration tests:

```bash
forge test --match-path test/integration/*
```

## Quickstart (Local)

1) Start anvil:

```bash
anvil
```

2) Deploy:

```bash
make deploy
```

3) Fund/withdraw using scripts:

```bash
make fund
make withdraw
```

Note: `make fund` and `make withdraw` require `SENDER_ADDRESS` to be set in the Makefile or via environment.

## Deploying to Sepolia

Create a `.env` file with:

```bash
SEPOLIA_RPC_URL=...
ACCOUNT=default
ETHERSCAN_API_KEY=...
```

Then deploy with:

```bash
make deploy-sepolia ARGS="--network sepolia"
```

## zkSync Notes

There are zkSync-specific helpers and tests:

- Build: `make zkbuild`
- Test: `make zktest`
- Local zkSync dev node: `make zk-anvil`
- Deploy to local zkSync: `make deploy-zk`
- Deploy to zkSync Sepolia:

```bash
ZKSYNC_SEPOLIA_RPC_URL=...
make deploy-zk-sepolia
```

## Makefile Targets (Selected)

- `make build` / `make test`
- `make deploy` / `make deploy-sepolia`
- `make fund` / `make withdraw`
- `make anvil` / `make zk-anvil`
- `make format` / `make snapshot`
