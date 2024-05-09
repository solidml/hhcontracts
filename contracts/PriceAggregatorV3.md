# PriceAggregatorV3 Smart Contract

The `PriceAggregatorV3` contract is a basic example simulating a Chainlink-like price aggregator for testing purposes. It provides a simple way to mock data updates and test other contracts relying on a Chainlink price feed.

## Table of Contents
- [Key Features](#key-features)
- [Functions](#functions)
- [Usage](#usage)
- [Contributing](#contributing)

## Key Features
- **Mock Chainlink AggregatorV3:** Simulates the functionality of a real AggregatorV3Interface, enabling easy testing.
- **Custom Timestamp:** Allows customizable mock timestamps for testing time-sensitive features.

## Functions
- **Constructor:**
  Initializes the mock aggregator with a starting timestamp that's 100 seconds before the current block timestamp.

- **decimals()**:
  Returns `8` to represent 8 decimal places, similar to a real Chainlink aggregator.

- **latestRoundData()**:
  Returns mock data for the latest round, including:
  - `roundId`: A fixed round identifier.
  - `answer`: A mock price value of `250000000000` (in 8 decimal precision).
  - `startedAt` and `updatedAt`: Identical timestamps representing when the round started and last updated.
  - `answeredInRound`: The round ID.

- **setTimestamp(uint256 timestamp_)**:
  Updates the internal timestamp used in `latestRoundData()` to a custom value.

## Usage
This contract is meant to serve as a mock price feed for testing other contracts that require a Chainlink AggregatorV3-like interface. Integrate it into your testing framework or deploy directly to a testnet and configure the timestamps as required.

### Example Testing Setup
1. Deploy the `PriceAggregatorV3` contract.
2. Pass the address of this contract to any other contract that requires a price feed.
3. Use `setTimestamp()` to adjust the round data for testing scenarios.

## Contributing
Contributions are welcome! Ensure your changes align with the intended purpose of this mock contract and provide tests for new functionality.

**License:** MIT
