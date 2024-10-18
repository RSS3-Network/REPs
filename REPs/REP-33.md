```
REP: REP-33
Title: Node State Transition
Status: Final
Type: Core
Created: 19 Jul 2024
Author(s): KallyDev <kallydev@rss3.io>, BruceXC <xichang1510@gmail.com>
Description: This REP outlines every potential Node state and the transitions between them.
Discussions: https://forum.rss3.io/t/proposal-on-node-state-transition/173
```

# REP-33: Node State Transition

## Table of Contents

- [Abstract](#abstract)
- [Motivation](#motivation)
- [Specification](#specification)
  - [Node State Transition Path](#node-state-transition-path)
  - [Reward Mechanism](#reward-mechanism)
- [Rationale](#rationale)
- [Reference Implementations](#reference-implementations)

## Abstract

This REP proposes a comprehensive set of states and their associated transitions for Nodes operating on the RSS3 Network. It establishes a structured framework for Node operations, aiming to enhance clarity, consistency, and efficiency in Node management.

## Motivation

The current lack of documentation for Node states potentially compromises network stability and complicates maintenance. A comprehensive set of states and their associated transitions enhances clarity, consistency, and efficiency in Node management. Clear definitions and guidelines will support both the Network's current functionality and future scalability.

## Specification

A Node can exist in one of the following 10 states:

1. **None**: The initial state of a Node.
2. **Registered**: The Node has been registered on the VSL with a sufficient deposit.
3. **Initializing**: The Node is operating on the DSL. Automated tasks are executed at this stage to ensure the Node is in a healthy condition. This state applies to the initial startup or the first startup following any change in the Node's coverage.
4. **Outdated**: The Node's version does not meet the minimum requirement.
5. **Online**: The Node is operational and actively participating in network activities.
6. **Offline**: The Node is non-operational and not participating in network activities.
7. **Exiting**: The Node is in the process of exiting the Network.
8. **Exited**: The Node has successfully exited the Network.
9. **Slashing**: The Node is about to be penalized for violating network rules or engaging in malicious behavior. It has a 3-epoch appeal period.
10. **Slashed**: The Node has been penalized due to a violation of network rules or malicious behavior.

### Node State Transition Path

![Node State Transition Path](REP-33/node-state-transition-path.png)

1. **None** → **Registered**: A `None` Node transitions to `Registered` state upon meeting the minimum deposit requirement.
2. **Registered** → **Initializing**: A `Registered` Node transitions to the `Initializing` state when it starts and begins indexing data but has not yet completed the process.
3. **Registered** → **Outdated**: A `Registered` Node transitions to the `Outdated` state when the Node is started and its version does not meet the minimum requirement.
4. **Registered**, **Outdated**, **Initializing**, **Slashed** → (anytime) → **Exited**: When a Node is in any of the `Registered`, `Outdated`, `Initializing`, or `Slashed` states, if the operator chooses to exit, the Node immediately enters the `Exited` state.
5. **Initializing** → (next Epoch) → **Online**: After the automatic initialization is completed, the Node enters the `Online` state at the next epoch.
6. **Online** → (current Epoch) → **Exiting**: An `Online` Node transitions to `Exiting` state upon announcing its intention to exit.
7. **Exiting** → (waiting period) → **Exited**: An `Exiting` Node transitions to `Exited` state after completing the waiting period.
8. **Online**, **Exiting** → **Slashing**: An `Online` or `Exiting` Node transitions to `Slashing` state if its demotion count reaches the threshold. The operator can appeal within 3 epochs.
9. **Online**, **Exiting** → (current Epoch) → **Offline**: An `Online` or `Exiting` Node transitions to `Offline` state immediately within the same epoch if the Node is detected to be unavailable.
10. **Offline**, **Slashed** → (current Epoch) → **Initializing**: An `Offline` or `Slashed` Node transitions to `Initializing` state if the Operator manually brings it back online.
11. **Slashing** → (after 3 epochs) → **Slashed**: A `Slashing` Node transitions to `Slashed` state after 3 epochs.
12. **Exited** → (anytime) → **Registered**: An `Exited` Node can re-register at any time.

### Reward Mechanism

Nodes in `Online`, `Initializing`, `Slashing` or `Exiting` states are eligible to provide services and receive rewards. Nodes in other states are ineligible.

## Rationale

The core objective of this proposal is to standardize Node states, improve clarity, and simplify maintenance. This proposal will ensure consistent operations across the Network, enable efficient troubleshooting, and provide a solid foundation for future enhancements.

## Reference Implementations

1. Upgraded contract : <https://scan.rss3.io/address/0x1FF6c3BC97841a3DF41e51Fc19223252ba373728>