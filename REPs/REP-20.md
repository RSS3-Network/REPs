```
REP: REP-20
Title: Data Availability Layer Integration
Status: Candidate
Type: Core
Created: 23 Apr 2024
Author(s): Albert <iavl@proton.me>, HenryQW <hi@henry.wang>
Description: This REP describes the integration of the Data Availability Layer (DAL) into the VSL.
Discussions: <https://forum.rss3.io/t/data-availability-layer-integration/136>
```

# REP-20: Data Availability Layer Integration

## Table of Contents

- [Abstract](#abstract)
- [Motivation](#motivation)
- [Specification](#specification)
  - [DA Solutions](#da-solutions)
  - [Blob Space prices](#blob-space-prices)
  - [Conclusion](#conclusion)
- [Rationale](#rationale)
- [Reference Implementations](#reference-implementations)

## Abstract

This REP proposes to integration NEAR DA as the Data Availability Layer (DAL) into the VSL.

## Motivation

The proposed adjustment will adopt NEAR DA as the Data Availability Layer (DAL), as opposed to the original design in the Whitepaper, to reduce the operational cost and to align with the ongoing development of the RSS3 Network.

## Specification

[In the Whitepaper](https://github.com/RSS3-Network/Whitepaper/blob/d8a86712cad0c88846c659577e0848b422b90f14/current/sections/VSL.tex#L20-L24), Celestia is described as the Data Availability Layer (DAL) of the VSL.

### DA Solutions

A brief comparison of 4 viable DA solutions that have been explored:

| Solution | Security                         | Cost/Block | Major Advantage     | Major Drawback            |
| -------- | -------------------------------- | ---------- | ------------------- | ------------------------- |
| Avail    | Avail's own chain                | unknown    | unknown             | not production ready      |
| Celestia | Celestia shared security         | \~\$0.046  | ease of integration | not the cheapest solution |
| NEAR     | On NEAR with Nightshade          | \~\$0.0016 | huge blob space     | development not as active |
| EIP-4844 | the almighty monolithic Ethereum | \~\$7.73   | native DA           | expensive                 |

### Blob Space prices

EIP-4844 as the native solution suffers from limited blob space per block (as of proto-danksharding). As more and more L2s are competing for **768kb per block** (8,192kb for full-danksharding in the future), surging activities such as ethscription minting on L2s will drive up the blob prices and increase the cost of operating the VSL. NEAR DA promises a whopping blob space of **4,096kb per transaction**, effectively circumventing such issues. This may even accelerate our experiments with different use cases that demand additional onchain storage space.

In our tests, NEAR DA has shown to be the most cost-effective solution for the VSL, with a cost per block of \~\$0.0054 (higher than the claim but still remains the lowest).

### Conclusion

Based on these findings, this REP proposes to integrate NEAR DA as the DAL, to leverage the advantages of NEAR DA and to align with the ongoing development of the Network.
At the same time, the Whitepaper will be updated to reflect the changes.

## Rationale

The proposed adjustment will reduce:

1. Gas fee for all transactions taking place on the VSL.
2. DAL-related operational cost of the VSL.

## Reference Implementations

1. NEAR DA code contributions: <https://github.com/RSS3-Network/rollup-data-availability>
2. VSL Testnet DA submissions: <https://testnet.nearblocks.io/address/vsl-submitter.testnet>
3. VSL Mainnet DA submissions: `pending`
4. Whitepaper Data Availability subsection update: <https://github.com/RSS3-Network/Whitepaper/pull/5>
