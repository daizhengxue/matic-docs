---
id: milestone
title: Milestones
sidebar_label: Milestones
description: Milestone is a feature implemented in the Polygon PoS architecture to improve the deterministic finality time for the blockchain.
keywords:
  - docs
  - polygon
  - heimdall
  - bor
  - milestone
  - ethereum
  - mainnet
---

import useBaseUrl from '@docusaurus/useBaseUrl';

The **Milestone feature is a crucial component that offers a high level of determinism and finality within a relatively short timeframe, averaging between 80 to 100 seconds**. It guarantees the immutability and irreversibility of a specific block in a distributed consensus system like the Polygon PoS network. To achieve this, the consensus algorithm requires the active participation of validator nodes within the network.

When a new block is proposed, all validator nodes in the network engage in a voting process to determine its validity and ultimate finalization. Each validator node casts their vote based on the block hash of the proposed block. **If the block receives more than two-thirds (2/3) of the total votes from the participating validator nodes, it attains the required threshold for finality**.

When a block obtains this majority consensus and becomes final, it secures its place within the blockchain. **This means that the finalized block cannot be altered, reversed, or tampered with in any manner going forward**.

The determination of finality through the Milestone feature ensures the integrity and immutability of the blockchain, fostering a robust and secure environment. It establishes a clear and unalterable history of transactions and events, enabling participants to rely on the validity and permanence of the data stored within the blockchain.

## Types

A typical structure of Milestone looks similar to this when implemented in the Polygon PoS network:

```go
type Milestone {
    Proposer types.HeimdallAddress `json:"proposer"`

    // the block number on Bor when this checkpoint starts
    StartBlock uint64 `json:"startBlock"`

    // the block number on Bor when this checkpoint ends
    EndBlock uint64 `json:"endBlock"`

    // the block hash of the ending block
    Hash types.HeimdallHash `json:"hash"`

    // unique ID for each milestone
	MilestoneID string `json:"milestone_id"`

	// timestamp when milestone was created on Heimdall
    TimeStamp uint64 `json:"timestamp"`
}
```

## Flow of the Milestone Feature

**&rarr;** One of the validator is selected as **Proposer** based on their stake. Their task is to propose a `Milestone` using the `Start Block`, `End Block`, and `Hash` data obtained from the local Bor chain.

**&rarr;** Next, all the validators cross-check the proposed `Milestone` using the data from their local Bor chain and vote `YES` if it's correct.

**&rarr;** If the proposed `Milestone` receives more than (⅔+1) votes in favour, it is committed in the Heimdall database and can never be reverted back in future.

**&rarr;** Fianlly, the Bor chain queries the latest `Milestone` from Heimdall and stores it in the Bor database.

## Usecase of Milestones in Bor

1. **Chain Validation during Block Import**: When a Bor node receives incoming blocks to be added to its blockchain, it performs a thorough validation process to ensure the consistency and correctness of the chain. One key step in this validation is checking the incoming chain against the latest stored Milestone. It only accepts the incoming chain if it matches with the latest Milestone.

2. **Finalized Block Delivery to Users**: In addition to chain validation during block import, the latest Milestone in Bor serves as a reference point for delivering finalized blocks to users. Once a block achieves finality through the consensus mechanism, it becomes an immutable part of the blockchain and can be considered fully validated.
