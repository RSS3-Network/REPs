```
REP: REP-31
Title: Node State Transition
Status: Draft
Type: Core
Created: 19 Jul 2024
Author(s): KallyDev <kallydev@rss3.io>
Description: This REP outlines every potential Node state and the transitions between them.
Discussions: https://forum.rss3.io/t/proposal-on-node-state-transition/173
```

# REP-31: Node State Transition

## Table of Contents

- [Abstract](#abstract)
- [Motivation](#motivation)
- [Specification](#specification)
- [Rationale](#rationale)

## Abstract
This REP proposes a comprehensive set of states and their associated transitions for Node operating on the RSS3 Network.
It establishes a structured framework for Node operations, aiming to enhance clarity, consistency, and efficiency for Node management.

## Motivation

The Node states are currently not documented, potentially compromising network stability and complicating maintenance.
A comprehensive set of states and their associated transitions enhance clarity, consistency, and efficiency for Node management.
Clear definitions and guidelines will support the Network's current functionality and future scalability.

## Specification

A Node can be in 1 of the following 7 states:

1. **Registered**: The Node is registered on the VSL with a sufficient deposit.
2. **Initializing**: The Node is operating on the DSL. Automated tasks will be executed at this stage to ensure the Node is in a healthy condition. This state applies to the initial startup or the first startup following any change in the Node’s coverage.
3. **Online**: The Node is operational and actively participating in network activities.
4. **Offline**: The Node is not operational and not participating in network activities.
5. **Exiting**: The Node is in the process of exiting the Network.
6. **Exited**: The Node has successfully exited the Network.
7. **Slashed**: The Node has been slashed due to a violation of network rules or malicious behavior.

### Node State Transition Path

![](REP-31/node-state-transition-path.png)

1. **Registered** → **Initializing** → **Online**: Upon registration, a Node transitions to `Registered`.  `Initializing` is the state when the Node is started. After the automatic initialization is completed, it enters `Online` state.
2. **Registered** → (after 30 Epochs) → **Exited**: A `Registered` Node transitions to `Exited` state after 30 Epochs of inactivity.
3. **Online** → (current Epoch) → **Exiting**: An `Online` Node transitions to `Exiting` state upon announcing its intention to exit.
4. **Exiting** → (waiting period) → **Exited**: An `Exiting` Node transitions to `Exited` state after completing the waiting period.
5. **Exiting** → **Slashed**: An `Exiting` Node transitions to `Slashed` state if it prematurely exits during the waiting period.
6. **Online** → (current Epoch) → **Offline**: An `Online` Node transitions to `Offline` state immediately within the same epoch if its Operation Pool drops below the required threshold.
7. **Online** → (current Epoch) → **Slashed**: An `Online` Node transitions to `Slashed` state immediately within the same epoch if it is slashed.
8. **Slashed** → (next Epoch) → **Offline**: A `Slashed` Node transitions to `Offline` state in the next epoch if the Operator fails to manually re-online it by the end of the current epoch.
9. **Slashed** → (next Epoch) → **Online**: A `Slashed` Node transitions to `Online` state in the next epoch if the Operator manually re-online it by the end of the current epoch.
10. **Offline** → (next Epoch) → **Online**: An `Offline` Node transitions to `Online` state in the next epoch if the Operator manually re-online it by the end of the current epoch.
11. **Offline** →(after 30 Epochs) → **Exited**: An `Offline` Node transitions to `Exited` state after 30 Epochs of inactivity.
12. **Exited** → (anytime) → **Registered**: An `Exited` Node can re-register at any time.

## Rationale

The core of this proposal is aim to standardize Node states, improve clarity, and simplify maintenance.
This proposal will ensure consistent operations across the Network, enable efficient troubleshooting, and provide a solid foundation for future enhancements.
