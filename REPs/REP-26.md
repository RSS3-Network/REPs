```
REP: REP-26
Title: Chip Mechanism Upgrade
Status: Candidate
Type: Core
Created: 9 Jul 2024
Author(s): BruceXC <xichang1510@gmail.com>
Description: This REP describes the upgrade of the chip mechanism to simplify the staking process and enhance the user experience.
Discussions: <https://forum.rss3.io/t/rep-pending-chip-mechanism-upgrade/169>
```

# REP-26: Chip Mechanism Upgrade

## Table of Contents

- [Abstract](#abstract)
- [Motivation](#motivation)
- [Specification](#specification)
- [Rationale](#rationale)
- [Reference Implementations](#reference-implementations)

## Abstract

This REP proposes an upgrade to the chip minting process for staking on the RSS3 Network. The main change is that each staking transaction will mint only one Chip, representing the total value staked, regardless of the amount. This approach is intended to streamline Chip management and enhance performance.

It is worth noting that the upgrade will not affect existing Chips in all aspects including their redemption, underlying stakes, future rewards allocation, except that they are now upgradable to the proposed new mechanism in which they will gain a new design. Existing Chips will remain valid until they are upgraded or redeemed, and will be considered a legacy version, with no new minting occurring.

## Motivation

The current staking mechanism, which mints a Chip for each unit of \$RSS3 staked based on the current Chip price, can be confusing and lead to high numbers of Chips being minted. This complexity has introduced challenges in transaction processing and data handling, which this proposal seeks to address.

## Specification

1. **Minting Mechanism**: A single Chip will be minted for each staking transaction, regardless of the amount of \$RSS3 staked.
2. **Chip Value Representation**: The Chip will embody the total value staked at the initiation of the transaction, adjusted according to the conditions at that epoch.
3. **Value Fluctuation**: The value assigned to each Chip will fluctuate based on the network's activities and the underlying public goods or staking pool size.

## Rationale

The core of this proposal is to reduce the number of Chips minted to one for each staking transaction, regardless of the amount staked, where each Chip will represent the total value staked.

## Reference Implementations

1. Whitepaper: [RSS3-Network/Whitepaper#7](https://github.com/RSS3-Network/Whitepaper/pull/7)
2. RSS3-Network-Contracts code update: <https://github.com/NaturalSelectionLabs/RSS3-Network-Contracts/pull/26>
