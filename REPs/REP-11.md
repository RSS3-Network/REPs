```
REP: REP-11
Title: Protocol Upgrade
Status: Candidate
Type: Protocol
Created: 22 Jan 2024
Author(s): BruceXC <xichang1510@gmail.com>, HenryQW <hi@henry.wang>, KallyDev <kallydev@gmail.com>, Nya Candy <github@candinya.com>, polebug <polebugfly@gmail.com>, pseudoyu <pseudoyu@connect.hku.hk>, Thomas <73341653+naaive@users.noreply.github.com>
Description: This REP describes the process of upgrading the RSS3 Protocol v0.4.0-rc.1 to v1.0.0.
Discussions: <https://forum.rss3.io/t/rss3-protocol-upgrade/65>
```

# REP-11: RSS3 Protocol Upgrade

## Table of Contents

- [Abstract](#abstract)
- [Motivation](#motivation)
- [Specification](#specification)
- [Rationale](#rationale)
- [Reference Implementations](#reference-implementations)

## Abstract

This REP proposes to upgrade the RSS3 Protocol, based on the RSS3 Unified Metadata Schemas.

## Motivation

The RSS3 Protocol v0.4.0-rc.1 was the last version released through community consensus.
Following this, the RSS3 Core Devs have been dedicating their efforts to the RSS3 Unified Metadata Schemas (UMS), which has been implemented as the structures for circulating Open Information on the RSS3 DSL > v0.4.

Upgrading the RSS3 Protocol with UMS means that the Protocol will see its first stable and production-grade version, and also align with ongoing advancements in the DSL.

## Specification

See [RSS3 Protocol v1.0.0](https://github.com/RSS3-Network/Protocol/blob/main/versions/v1.0.0/main.adoc) for the full specification.

## Rationale

The RSS3 Protocol v0.4.0-rc.1 was a file-based solution for storing and circulating Open Information.
The approach was chosen to navigate the uncertainties of the Open Web at that time.
It was designed to be simple and easy to use, but it also had its limitations:

1. Scalability - it simply could not handle large amounts of data
2. Performance - the query speed was slow
3. Storage Cost - the storage cost was high
4. Interoperability - it was difficult for developers to build on top of the Protocol

The landscape of the Open Web has also changed a lot since the release of v0.4.0-rc.1, and the RSS3 Core Devs have been working on the RSS3 Unified Metadata Schemas (UMS) to align with the new trends.

The UMS is essentially a set of JSON schemas that define the structures of Open Information.
The storage of Open Information is no longer limited to files, but can be stored in any relational database, in this case, the RSS3 Core Devs have chosen to use CockroachDB.

The UMS addresses all the problems of the RSS3 Protocol v0.4.0-rc.1:

1. Scalability - the current DSL hosts 1.5b+ pieces of Open Information
2. Performance - the query speed is lightning fast
3. Storage Cost - the storage cost is much lower
4. Interoperability - it provides a set of APIs for developers to build on top of the Protocol

## Reference Implementations

1. Protocol Specification: <https://github.com/RSS3-Network/Protocol/blob/main/versions/v1.0.0/main.adoc>
2. Protocol-Go - A Golang implementation: <https://github.com/RSS3-Network/Protocol-Go>
3. Node implementation with Protocol-Go <https://github.com/RSS3-Network/Node/blob/7c69c9fbd05e353c6fd5ecabf6657a772bff6282/go.mod#L58>
