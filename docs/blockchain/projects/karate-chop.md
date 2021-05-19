# KARATE CHOP LIQUIDITY SWAP
The following requirements are associated with building a distributed application that can handle processing atomic swaps between Uniswap v3 concentrated liquidity position NFTs.

## What are Uniswap v3 concentrated liquidity positions?
Uniswap v3 gives individual LPs granular control over what price ranges their capital is allocated to. Individual positions are aggregated together into a single pool, forming one combined curve for users to trade against.

In other words, LP’s can concentrate their capital within custom price ranges, providing greater amounts of liquidity at desired prices. In doing so, LPs construct individualized price curves that reflect their own preferences.

As a byproduct of per-LP custom price curves, liquidity positions are no longer fungible and are not represented as ERC20 tokens in the core protocol. Instead, LP positions are represented by non-fungible tokens (NFTs).

Today, LP positions can be [bought and sold on NFT marketplaces like OpenSea](https://opensea.io/assets/uniswap-v3-positions) however, LPs do not have the ability to atomically swap their positions for other users positions.


## Mission
We’d like for you to build an Ethereum smart contract-based, non-custody solution that enables users to atomically swap their concentrated liquidity positions, represented as NFT. Your solution should address the following user stories:

#### Lister - Trade - I can list my concentrated liquidity position(s) that I am willing to trade
*Scenario*
- A user wants to list their concentrated liquidity positions - as NFTs - that they would be willing to swap

*Acceptance Criteria*
- Require the number of listed liquidity positions in the array of positions is greater than zero
- Require the token IDs in the array of positions listed exist and are associated with the [NonfungiblePositionManager](https://docs.uniswap.org/reference/periphery/NonfungiblePositionManager#collect) contract
- The user must approve the Trade contract in order to allow it to transfer their positions if a Swapper makes a trade offer that they’d like to accept

#### Lister - Trade - I can accept an offer
*Scenario*
- A user wants to accept an offer to swap their listed concentrated liquidity positions

*Acceptance Criteria*
- Require the offer includes only concentrated liquidity positions that I have listed
- The listed concentrated liquidity positions are transferred from the lister to the swapper

#### Lister - Trade - I can decline an offer
*Scenario*
- A user wants to decline an offer to swap their listed concentrated liquidity positions

*Acceptance Criteria*
- The offer if declined
- The listed concentrated liquidity positions are NOT transferred from the lister to the swapper

#### Swapper - Trade - I can create an offer
*Scenario*
- A user wants to issue an offer to a Lister that has listed their concentrated liquidity position(s) that they are willing to trade
*Acceptance Criteria*

- Require that the concentrated liquidity position(s) included in the offer are owned by the Swapper (or user initiating the offer)
- Require that the number of concentrated liquidity position(s) included in the offer are greater than zero
- Require the offer corresponds to a Lister’s corresponding concentrated liquidity position listings
- The Swapper must approve the Trade contract in order to allow it to transfer their positions if a Lister accepts their trade offer
- Creates an offer that the Lister can review and then accept or decline


## Resources:
* [Introduction Uniswap v3](https://uniswap.org/blog/uniswap-v3/)
* [Uniswap v3 Smart Contracts Overview](https://docs.uniswap.org/reference/smart-contracts)
* [What is an Automated Market Maker (AMM)](https://www.gemini.com/cryptopedia/amm-what-are-automated-market-makers)


