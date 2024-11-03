---
sidebar_position: 2
---

# Push Feeds Interface Reference

This document provides a reference for the Push Feeds interface and how to interact with Mozaik Push Feeds.

## IPushDataFeed.sol

Import this interface to your contract and use it to run functions for the specific feed contract.

```solidity
interface IPushDataFeed {
    function updateFeed(
        uint256[2] calldata _pA,
        uint256[2][2] calldata _pB,
        uint256[2] calldata _pC,
        uint256[4] calldata _pubSignals,
        uint256 _data
    ) external;
    function getLastRound() external view returns (Round memory);
    function getCurrentRound() external view returns (uint256);
    function latestAnswer() external view returns (uint256);
    function getFeedBinHash() external view returns (bytes32);
    function getConfig() external view returns (Config memory);

    struct Config {
        uint32 deviationThreshold;
        uint8 decimals;
        uint32 heartbeat;
        string description;
    }

    struct Round {
        uint256 roundId;
        uint256 data;
        uint256 timestamp;
    }

    event RoundUpdated(uint256 roundId, uint256 data, uint256 timestamp);

}
```
