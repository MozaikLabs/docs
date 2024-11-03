---
sidebar_position: 1
---

# Getting Started

Mozaik’s **Push Data Feeds** provide an efficient and reliable solution for delivering off-chain data to smart contracts on a predetermined schedule or upon specific triggers. Designed for use cases where data updates are periodic or event-driven, Push Data Feeds ensure data consistency while minimizing latency and operational costs.

## How Mozaik Push Feeds Work

1. **Scheduled Data Collection**: Operators retrieve data from specified off-chain sources based on price deviations specific to the feed.

2. **Proof Generation**: Each data update includes a zero-knowledge (zk) proof, verifying the integrity of the compute. This zk-proof assures the blockchain of the data’s authenticity before it is published.

3. **On-Chain Delivery**: The verified data, along with its proof, is pushed directly to the smart contract, allowing applications to rely on atomic price data straight from on-chain data.

## Use Cases

Push Data Feeds are ideal for applications that require quick on-chain reads of off-chain data, such as:

- **DeFi Data**
- **TradFi Data**

With Mozaik’s Push Data Feeds, developers gain access to cryptographically provable compute, enabling secure and efficient data delivery for a wide range of decentralized applications.
