# RocketSwap V2 Subgraph

# This repository is archived, you can find all the RocketSwap subgraph at [rocketswap/rocketswap-subgraph](https://github.com/rocketswap/rocketswap-subgraph)

[RocketSwap](https://rocketswap.finance/) is a decentralized protocol for automated token exchange on Binance Smart Chain.

This subgraph dynamically tracks any pair created by the rocketswap factory. It tracks of the current state of RocketSwap contracts, and contains derived stats for things like historical data and USD prices.

- aggregated data across pairs and tokens,
- data on individual pairs and tokens,
- data on transactions
- data on liquidity providers
- historical data on RocketSwap, pairs or tokens, aggregated by day

## Running Locally

Make sure to update package.json settings to point to your own graph account.

## Queries

Below are a few ways to show how to query the rocketswap-subgraph for data. The queries show most of the information that is queryable, but there are many other filtering options that can be used, just check out the [querying api](https://thegraph.com/docs/graphql-api). These queries can be used locally or in The Graph Explorer playground.

## Key Entity Overviews

#### RocketswapFactory

Contains data across all of RocketSwap v2. This entity tracks important things like total liquidity (in ETH and USD, see below), all time volume, transaction count, number of pairs and more.

#### Token

Contains data on a specific token. This token specific data is aggregated across all pairs, and is updated whenever there is a transaction involving that token.

#### Pair

Contains data on a specific pair.

#### Transaction

Every transaction on RocketSwap is stored. Each transaction contains an array of mints, burns, and swaps that occured within it.

#### Mint, Burn, Swap

These contain specifc information about a transaction. Things like which pair triggered the transaction, amounts, sender, recipient, and more. Each is linked to a parent Transaction entity.

## Example Queries

### Querying Aggregated RocketSwap Data

This query fetches aggregated data from all Rocketswap pairs and tokens, to capture activity throughout the entire protocol.

```graphql
{
  rocketswapFactories(first: 1) {
    pairCount
    totalVolumeUSD
    totalLiquidityUSD
  }
}
```
