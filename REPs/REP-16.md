```
REP: REP-16
Title: Staking Rewards Taxation Adjustment
Status: Candidate
Type: Core
Created: 21 Mar 2024
Author(s): Albert <iavl@proton.me>, HenryQW <hi@henry.wang>
Description: This REP describes the adjustment of Staking Rewards taxation formula.
Discussions: <https://forum.rss3.io/t/rep-pending-adjusting-staking-rewards-taxation/128>
```

# REP-16: Staking Rewards Taxation Adjustment

## Table of Contents

- [Abstract](#abstract)
- [Motivation](#motivation)
- [Specification](#specification)
- [Rationale](#rationale)
- [Reference Implementations](#reference-implementations)

## Abstract

This REP proposes to adjust the taxation of Staking Rewards.
The REP will update the Whitepaper first, and then the taxation will be adjusted on the VSL accordingly.

## Motivation

The proposed adjustment will simplify the taxation formula, making the computation more efficient and less error-prone.

## Specification

Current formula as [stated in the Whitepaper](https://github.com/RSS3-Network/Whitepaper/blob/d8a86712cad0c88846c659577e0848b422b90f14/current/sections/tokenomics/network_rewards.tex#L77-L83):

$$
T_{N,\epsilon} = \min(D_{N,\epsilon} * c_{\epsilon}, (R_{S|N,\epsilon} + R_{O|N,\epsilon}) * τ_{N,\epsilon})
$$

Current [description of the formula](https://github.com/RSS3-Network/Whitepaper/blob/d8a86712cad0c88846c659577e0848b422b90f14/current/sections/tokenomics/network_rewards.tex#L75):

```
The tax rate τ is set by the Node Operator of a Normal Node, and is applied to the Network Rewards allocated to its $P_s$.

The amount of tax collectible is capped at a maximum of $c$ times the amount of the current deposit, where $c$ is set by the Network.
```

Proposed new taxation formula:

$$
T_{N,\epsilon} = \min(P_{O|N,\epsilon} * c_{\epsilon}, (R_{S|N,\epsilon} + R_{O|N,\epsilon}) * τ_{N,\epsilon})
$$

Proposed new description of the formula:

```
A Normal Node's operator sets the tax rate τ which is imposed on the Network Rewards allocated to its $P_s$.

The amount of taxiable $R_s$ is capped at a maximum of $c$ times the amount of the current $P_o$, where $c$ is set by the Network.
```

Reflecting the changes in the Whitepaper, the VSL will be updated accordingly.
The tokenomics will then be adjusted to reflect the new formula:

Current tokenomics intepretation:

$$
D_{N} * 25 \geq T_{N,\epsilon} \quad \text{where} \quad D_{N} \geq 10,000
$$

Proposed new tokenomics intepretation:

$$
P_{o} * 25 \geq T_{N,\epsilon} \quad \text{where} \quad D_{N} \geq 10,000
$$

To improve the clarity on the tax rate for all Public Good Nodes, The current description of:

```
For the Public Good Pool, the tax rate is set by the Network to collect donations to support Public Good initiatives and clauses.
```

is proposed to be updated to:

```
The tax rate for all Public Good Nodes is determined by the Network. These funds are deposited into the Public Good Pool and are allocated to support various Public Good initiatives and clauses. The allocations of these resources will be collectively decided by all Network participants.
```

## Rationale

The Core Developers have derived fresh insights from the Mainnet Alpha, revealing that the existing formula is overly complex and inefficient for computation.
This complexity not only elevates the risk of implementation errors but also confuses Network participants.

The proposed adjustment will simplify the formula, without compromising the original design principles and the economic incentives of the Network.

The proposed adjustment also slightly lowers the entry barrier for new Node Operators and simplifies the management of the Node.

The proposed adjustment does not introduce any new development requirements, and the implementation is expected to be straightforward.

## Reference Implementations

1. Whitepaper: [RSS3-Network/Whitepaper#4](https://github.com/RSS3-Network/Whitepaper/pull/4)
