```
REP: REP-34
Title: Demotion and Slashing Mechanism
Status: Draft
Type: Core
Created: 23 Jul 2024
Author(s): polebug <polebugfly@gmail.com>
Description: This REP describes the demotion and slashing mechanisms to maintain the Network’s stability.
Discussions: https://forum.rss3.io/t/rep-draft-on-demotion-and-slashing-mechanism/175
```

# REP-34: Demotion and Slashing Mechanism

## Abstract

This proposal introduces demotion and slashing mechanisms to the RSS3 Network. Global Indexers (GIs) follow the mechanisms to manage RSS3 Nodes based on their operational reliability. The primary objective is to establish a structured protocol for maintain and improve the Network stability by incentivizing reliable Node operations.

## Motivation

Nodes are critical to network stability and efficiency. Unreliable Nodes compromise the Network’s functionality. Currently, there lacks a clear and consistent protocol to do so. The demotion and slashing mechanisms enable systematic performance oversight, ensuring only reliable Nodes handle requests, thus ensuring the Network stability.

## Specification

An Enforcer is introduced as a component of GIs in this proposal, it manages demotions and slashes.

### Demotion Mechanism

1. Nodes are required to send regular heartbeats to GIs. If no heartbeat is received by GIs within a 5-minute rolling interval, the Node is marked as offline until a new heartbeat is received. The Node’s demotion counter increases by 1.
2. GI routes requests to a selected number of Nodes (a minimal of 3).
    - If a Node fails to respond normally after a predetermined number of retries (default to 3), the Node’s demotion counter increases by 1.
    -  If a Node’s successful response fails to pass cross-validation with other Nodes:
       - If a Node’s response differs from the majority, the Node’s demotion counter increases by 1.
       - If no majority is reached, all responses are deemed invalid, but no one is demoted.
3. Each demotion reduces the Node’s reliability score, diminishing its chances of receiving requests.
   - The demotion counter and reliability score are reset at the end of each Epoch.

## Slashing Mechanism

1. If a Node's demotion counter hits the threshold (currently set to 3), it is slashed.
2. Slashed Nodes have a reliability score of 0, no requests will be routed to them.
   - The reliability score is reset at the end of each Epoch.
3. Slashed Nodes will be marked as `offline`, until the Node Operator manually confirms that the Node is ready to enter `online`state.
4. A slash temporarily freezes 1% of the Node’s Operation Pool **AND** 0.5% of its Staking Pool.
   - Slashed tokens are stored in the Slashing Pool.
   - A slash may be challenged by the Operator within a 3-Epoch challenge window.
       - A successful challenge revokes the corresponding slash and unfreezes the tokens.
       - A successful challenge does not distribute Network Rewards retrospectively.
   - After 3 Epochs, the slash is committed and finalized on-chain.
   - Failing to revoke a slash within the challenge window means that the slash will be committed permanently. The slashed tokens will be:
        - **Burn**: 50% of the slashed tokens will be burnt.
        - **Reward and Reimbursement**: 20% of the slashed tokens will be awarded to reporters. When the slash is automatically triggered without a reporter, 20% of the slashed tokens will be reimbursed to all developers who paid request fees during the Epoch in which the slashing occurred.
        - **Donation**: The remaining tokens will be donated to the Treasury and used for Public Good initiatives and clauses.

   Here is a figure showing what happens during an Epoch. The figure might be helpful for illustrating the Enforcer’s logic regarding slashing.

![RSS3 Mainnet Diagrams (1).png](REP-34%2FRSS3%20Mainnet%20Diagrams%20%281%29.png)


And here is a figure to assist in the understanding of cross-validation. `-1` leads to a demotion.

![3 responses [r1,r2,r3].png](REP-34%2F3%20responses%20%5Br1%2Cr2%2Cr3%5D.png)

# **Rationale**

The core of this proposal is to introduce demotion and slashing mechanisms for maintaining the RSS3 Network’s stability. These mechanisms will evaluate operational reliability, penalize non-compliance, and incentivize consistent high-quality Node operations.