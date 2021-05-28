# CashCoin DAPP
The following requirements are associated with building a decentralized payment application on a Layer 2 platform.

## What is Layer 2?
The blockchain trilema: Decentralization, Security, Scalability. This was coined by Vitalik Buterin to explain the three main issues that developers strive to solve when building blockchains. It’s difficult to achieve all three, and most chains sacrifice one. 

In a move to Proof of Stake, Ethereum hopes to solve the scalability issue that has afflicted the blockchain since its inception. While the community awaits the switch to Proof of Stake, Layer 2 solutions have been researched, built and tested to alleviate the congestion and high fees associated with transactions on the main chain.

Layer 2 is a set of technologies or systems that run on top of Ethereum (Layer 1), inherit security properties from Layer 1, and provide greater transaction processing capacity (throughput), lower transaction fees (operating cost), and faster transaction confirmations than Layer 1.[*](https://entethalliance.org/how-ethereum-layer-2-scaling-solutions-address-barriers-to-enterprises-building-on-mainnet/)
The major categories of L2 Solutions are: state channels, side chains, plasma, sk-rollups, optimistic rollups, and validium.

## Mission
We'd like you to build an Ethereum smart contract-based payment application that can request and make payments, and display balances and outstanding payment requests, all on a Layer 2 platform. The app should also provide a bridge that allows users to move their balance from L2 to mainnet Ethereum.
Your solution should address the following user stories:

#### User - Payment - I can request payment from an address
*Scenario*
- A user wants to request payment from an address

*Acceptance Criteria*
- Maps payment amount to requester and requestee

#### User - Payment - I can make a payment
*Scenario*
- A user wants make a payment

*Acceptance Criteria*
- Must transfer payment
- Decreases amount due for user

#### User - Payment - I can view my outstanding payment requests

#### User - Payment - I can view my balance

#### User - Payment - I can move my funds to mainnet

## Resources:
* [LAYER 2 ROLLUPS](https://ethereum.org/en/developers/docs/scaling/layer-2-rollups/)
* [How Ethereum Layer 2 scaling solutions address barriers to enterprises building on Mainnet](https://entethalliance.org/how-ethereum-layer-2-scaling-solutions-address-barriers-to-enterprises-building-on-mainnet/)
* [Polygon](https://polygon.technology/)
* [Polygon Developer Docs](https://docs.matic.network/docs/develop/getting-started)
* [Zk.sync](https://zksync.io/)
* [Optimism](https://optimism.io/)




