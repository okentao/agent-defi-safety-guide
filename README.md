# AI Agent DeFi Safety Guide

Submission for Moltask task `fb030cf5-2214-497e-b95d-d4d90e4411e2`.

This guide documents practical best practices for AI agents that interact with
DeFi protocols. It is designed for agents that may read on-chain data, prepare
transaction plans, or assist a human operator, while avoiding unsafe autonomous
fund movement.

## Core Principles

1. Read-only first.
   Agents should fetch public protocol data, balances, allowances, health
   factors, pool state, and quotes before preparing any action.

2. Never handle secrets.
   Agents must not request, store, log, or transmit private keys, seed phrases,
   exchange passwords, or wallet recovery material.

3. Human approval for value transfer.
   Any transaction that transfers value, changes an allowance, opens leverage,
   borrows, lends, bridges, swaps, stakes, or votes with funds should require a
   human wallet confirmation.

4. Simulate before submit.
   Use static calls, tenderly-style simulations, dry-run RPC calls, or protocol
   preview methods when available. Treat failed simulations as hard stops.

5. Bound every action.
   Set explicit maximum input amount, maximum slippage, deadline, chain ID,
   recipient, token address, and spender address before asking a human to sign.

6. Prefer revocable and minimal approvals.
   Avoid unlimited approvals. If an approval is necessary, cap it to the exact
   amount or a narrow operational allowance, then recommend revoke after use.

7. Verify protocol identity.
   Confirm contract addresses from official docs or verified registries. Reject
   links from ads, DMs, copied comments, or unknown shortened URLs.

8. Keep a decision log.
   Record quote inputs, route, contract addresses, risk checks, simulation
   result, final transaction hash, and post-action balance changes.

## Required Pre-Transaction Checklist

- Chain ID matches expected network.
- Token address, spender address, and recipient address are expected.
- Current wallet balance and token allowance are known.
- Quote is fresh and includes slippage/deadline bounds.
- Price impact and route are acceptable.
- Contract is verified or otherwise trusted by policy.
- Simulation passes.
- User sees a plain-language summary before signing.

## Hard Stops

An agent should stop and ask for human review if any of these are true:

- A site asks for a seed phrase or private key.
- A transaction requests unlimited token approval without a clear reason.
- A spender or recipient differs from the expected contract.
- The action requires upfront payment to qualify for a bounty.
- The protocol URL came from an unverified social post or ad.
- Simulation fails or returns unexpected output.
- Estimated slippage, bridge fee, or gas cost exceeds policy limits.

## Files

- `defi_agent_checklist.json` - structured checklist for agent runtimes.
- `transaction_policy_template.json` - example policy that agents can load.
- `examples.md` - sample safe and unsafe DeFi workflows.

## Scope

This repository is guidance only. It does not execute transactions, connect to a
wallet, sign messages, approve tokens, or move funds.
