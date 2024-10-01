```
REP: 40
Title: Whitepaper Updates
Status: Draft
Type: Core
Created: 30 Jul 2024
Author(s): pseudoyu <pseudoyu@connect.hku.hk>
Description: This REP describes the updates to the RSS3 Network Whitepaper.
Discussions: https://forum.rss3.io/t/rep-draft-on-whitepaper-updates/179
```

# REP-40: Whitepapaer Updates

## Abstract

This REP proposes several updates to the RSS3 Network Whitepaper. These updates aim to enhance the clarity, consistency, and accuracy of the Whitepaper, reflecting the latest developments and improvements in the RSS3 Network.

## Motivation

The RSS3 Network Whitepaper serves as a foundational document, providing a comprehensive overview of the Network's design, architecture, and functionality. As the Network evolves, it is crucial to keep the Whitepaper aligned with the latest implementations.

This update aims to enhance clarity, correct outdated information, and ensure consistency across all RSS3 documentation. By maintaining an accurate Whitepaper, we provide a reliable reference for developers, users, and potential new participants, supporting the Network's ongoing development and adoption.

## Specification

### Section III. A Updates

1. changing the term “Permisionless Data Source (PDSs)” to “Open Data Protocols (ODPs)”.

### Section III. C Updates

1. The GIs perform critical duties to ensure the Network is robust and reliable.
2. GI has been changed to GIs where appropriate throughout the updates.
3. The GI components have been updated to match the current architecture:
   - Router: The routers ensure requests are routed and served with high performance and minimal latency.
   - Broadcaster: The broadcasters constantly monitor all Nodes' status for irregular behaviors.
   - Enforcer: The enforcers maintain records of demotion and slashing, and slash Nodes that fail to meet requirements.
   - Settler: The settlers initiate submissions of work records to the Value Sublayer.
   - Payment Processor: The payment processors ensure request fees are correctly distributed.
   - Taxer: The taxers calculate the Network's average tax rate and update the settlement contract.

## Rationale

The core of this proposal is to update the RSS3 Network Whitepaper to accurately reflect the current state of the Network. These updates focus on refining terminology, clarifying the role of Global Indexers, and providing more precise definitions. By implementing these changes, we aim to enhance the Whitepaper's accuracy and usefulness as a key reference document for the RSS3 ecosystem, ensuring it aligns with the latest developments and improvements in the Network.

And this is an informational REP which requires no code changes and has no empirical impact on anything.
