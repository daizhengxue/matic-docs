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

The **Milestone feature is a crucial component that offers a high level of determinism and finality within a relatively short timeframe, averaging between 80 to 100 seconds**. It guarantees the immutability and irreversibility of a specific block in a distributed consensus system like the Polygon PoS network. The consensus algorithm requires the active participation of validator nodes within the network to achieve this.

When a new block is proposed, all validator nodes in the network engage in a voting process to determine its validity and ultimate finalization. Each validator node casts its vote based on the block hash of the proposed block. **If the proposed block receives more than two-thirds (2/3) of all votes, it reaches a supermajority, which is the requisite level of consensus for finality.**

When a block achieves finality through majority consensus, it is added to the blockchain and becomes **unalterable, irreversible, and immune to any form of tampering**.

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

**&rarr;** If the proposed `Milestone` receives more than (⅔+1) votes in favor, it is committed in the Heimdall database and can never be reverted back in the future.

**&rarr;** Finally, the Bor chain queries the latest `Milestone` from Heimdall and stores it in the Bor database.

## Use Cases of Milestones in Bor

1. **Chain Validation during Block Imports**: When a Bor node receives incoming blocks, it uses Milestones as a key validation tool. The node compares the latest stored Milestone with the incoming blocks. Only if the incoming blocks align with the latest Milestone—indicating its validity and consistency with the existing blockchain—does the Bor node accept and add it to the chain.

2. **Finalized Block Delivery to Users**: In addition to chain validation during block imports, the latest Milestone in Bor serves as a reference point for delivering finalized blocks to users.
