---
sidebar_position: 2
---

# RTD Feed Interface Reference

This document provides a reference for the Real Time Data (RTD) Feeds interface and how to interact with Mozaik RTD Feeds.

:::tip[]
Feeds are currently in development and do not currently require the **MZK** token to use.
:::

## IRTDCoordinator.sol

Import the `IRTDCoordinator` interface to your contract and use it to request your RTD feed data.

```solidity

interface IRTDCoordinator {
    function requestRTD(bytes32 _feed) external;

    event RTDTriggered(bytes32 indexed feed, uint256 indexed requestId, address requester);
    event RTDFulfilled(uint256 indexed requestId, address indexed requester, address operator);

    error InvalidRequest(uint256 requestId);
    error InvalidCoordinatorId();
    error InvalidProof();
    error InvalidChainId();
    error ZeroRequester();

    function requestRTD(bytes32 _feed) external;
}

```

## RTDReceiver.sol

To receive RTD price data, your contract must inherit the `RTDReceiver` abstract contract. It is suggested to use the `onlyCoordinator` modifier to restrict access to your receiving function.

```solidity

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import {IRTDCoordinator} from "../interfaces/IRTDCoordinator.sol";

abstract contract RTDReceiver {
    IRTDCoordinator public coordinator;

    modifier onlyCoordinator() {
        require(msg.sender == address(coordinator), "RTDReceiver: Only coordinator can call this function");
        _;
    }

    constructor(address _coordinator) {
        coordinator = IRTDCoordinator(_coordinator);
    }

    function fulfillRequest(uint256 _requestId, bytes calldata _data) external virtual;
}

```

## Example Usage

Each RTD feed has a return value associated to it. The return value is a `bytes` type that can be decoded to the expected data type. Below is an example of how to receive RTD data in your contract.

```solidity
contract MockRTDReceiver is RTDReceiver {
    uint256 public data;
    uint256 public requestId;

    constructor(address _coordinator) RTDReceiver(_coordinator) {}

    function requestRTD(bytes32 _feed) external {
        coordinator.requestRTD(_feed);
    }

    function fulfillRequest(uint256 _requestId, bytes calldata _data) external override onlyCoordinator {
        data = abi.decode(_data, (uint256));
        requestId = _requestId;
    }
}

```
