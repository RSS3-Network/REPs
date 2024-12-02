```
REP: REP-54
Title: Network operation rewards distribution adjustment
Status: Draft
Type: Core
Created: 1 Dec 2024
Author(s): BruceXC <xichang1510@gmail.com>
Description: This REP proposes a new Network operation rewards distribution mechanism
Discussions: https://forum.rss3.io/t/rep-network-operation-rewards-distribution-adjustment/223
```

# REP-54: Network operation rewards distribution adjustment

## Table of Contents

- [Abstract](#abstract)
- [Motivation](#motivation)
- [Specification](#specification)
- [Rationale](#rationale)
- [Reference Implementations](#reference-implementations)

## Abstract

This REP proposes to adjust the Network operation rewards distribution mechanism.
The REP will update the Whitepaper first, and then the rewards distribution mechanism will be adjusted on the Global Indexer accordingly.

## Motivation

The proposed adjustment accounts for various aspects of Node contributions to the network, aiming to optimize the allocation of rewards to Nodes and help cover their operational costs.

## Specification

The current formula is based on various factors reflecting Node contributions to the network. The total score for Node $i$ is defined as $S_i$, calculated using the following formula:

$$
S_i = W_1 \cdot R_i + W_2 \cdot D_i + W_3 \cdot E_i
$$

Where:

- $W_1$, $W_2$, $W_3$ are the weights of the three factors, and $W_1 + W_2 + W_3 = 1$.
- $R_i$ is the request distribution score of Node $i$.
- $D_i$ is the data indexing score of Node $i$.
- $E_i$ is the stability score of Node $i$.

$$
R_i = \frac{\text{valid\_count}_i}{\max(\text{valid\_count})} - \alpha \cdot \frac{\text{invalid\_count}_i}{\max(\text{invalid\_count})}
$$

where:

- $\text{valid\_count}_i$ is the valid request count of Node $i$.
- $\text{invalid\_count}_i$ is the potential invalid request count of Node $i$.
- $\alpha$ is a constant factor, representing the weight of the invalid request count.

$$
D_i = \beta_1 \cdot \frac{\text{network\_count}_i}{\max(\text{network\_count})} + \beta_2 \cdot \frac{\text{worker\_count}_i}{\max(\text{worker\_count})} + \beta_3 \cdot \frac{\text{activity\_count}_i}{\max(\text{activity\_count})}
$$

where:

- $\text{network\_count}_i$ is the number of supported networks of Node $i$.
- $\text{worker\_count}_i$ is the worker count of Node $i$.
- $\text{activity\_count}_i$ is the activity count of Node $i$.
- $\beta_1$, $\beta_2$, $\beta_3$ are the weights of the three factors, and $\beta_1 + \beta_2 + \beta_3 = 1$.

$$
E_i = \gamma_1 \cdot \frac{\text{uptime}_i}{\max(\text{uptime})} + \gamma_2 \cdot \text{version\_score}_i
$$

where:

- $\text{uptime}_i$ is the continuous uptime of Node $i$.
- $\text{version\_score}_i = 1$ if the node uses the latest version, otherwise $0$.
- $\gamma_1$, $\gamma_2$ are the weights of the two factors, and $\gamma_1 + \gamma_2 = 1$.

## Rationale

The core goal of this proposal is to evaluate Node contributions from multiple perspectives to ensure a fair allocation of network operation rewards. This approach enables Node operators to receive Network operation rewards while reducing their operational costs.

## Reference Implementations
