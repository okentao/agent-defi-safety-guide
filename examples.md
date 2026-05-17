# Safe and Unsafe DeFi Agent Workflows

## Safe: Read-Only Risk Report

1. Agent receives a wallet address and protocol list.
2. Agent reads balances, allowances, lending health factor, pool exposure, and
   current market prices from public APIs or RPC calls.
3. Agent produces a report with risks and suggested next steps.
4. No wallet signature or token approval is requested.

Why safe: the agent never moves funds and does not need secrets.

## Safe With Human Approval: Bounded Swap Plan

1. Agent reads a quote from a trusted router.
2. Agent checks token addresses, chain ID, route, price impact, slippage, and
   deadline.
3. Agent simulates the call.
4. Agent presents the exact spender, token amount, min output, and deadline to
   the human.
5. Human signs only if the wallet prompt matches the summary.

Why safe: the agent prepares a bounded plan, but the human wallet remains the
approval gate.

## Unsafe: Unlimited Approval From Unknown Site

1. Agent follows a social link to a new DeFi page.
2. Page asks to approve unlimited USDC to an unknown spender.
3. There is no official contract source or simulation.

Required action: stop. Do not sign. Verify the protocol through official docs
or abandon the task.

## Unsafe: Bounty Requires Deposit First

1. A bounty claims payout is available after sending funds to a contract.
2. The task requires staking, buying a token, or paying gas to qualify.

Required action: stop unless the human explicitly chose to fund the workflow
after independent review. For earning tasks, this should normally be rejected.

## Unsafe: Agent Stores Recovery Material

1. User pastes a seed phrase so the agent can "help faster."
2. Agent logs or stores it in a state file.

Required action: refuse handling the secret and instruct the user to rotate the
wallet if the phrase was exposed.
