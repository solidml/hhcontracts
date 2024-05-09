# CoinSale Smart Contract

The `CoinSale` contract is a robust and feature-rich token sale system, designed to work with Chainlink's price feed for accurate token pricing. It supports flexible role-based access control, secure purchase mechanisms with referrals, and advanced recovery functionality.

## Table of Contents
- [Key Features](#key-features)
- [Roles](#roles)
- [Events](#events)
- [Errors](#errors)
- [Functions](#functions)
- [Usage](#usage)
- [Contributing](#contributing)

## Key Features
- **Chainlink Integration:** Utilizes Chainlink's AggregatorV3Interface for accurate real-time price feeds.
- **Referral System:** Allows referrers to receive rewards for successful referrals.
- **Access Control:** Administered via OpenZeppelin's `AccessControl`.
- **Reentrancy Guard & Pausable:** Prevents reentrancy attacks and allows pausing/unpausing.
- **On-ramp Purchases:** Supports secure token purchases via external roles.
- **Ether & ERC-20 Recovery:** Enables the recovery of unused tokens and Ether.

## Roles
- **DEFAULT_ADMIN_ROLE:** Administers the contract, controls pausing, and recovery functions.
- **ONRAMP_ROLE:** Manages token purchases on behalf of others.

## Events
- **PriceThresholdUpdated:** Triggered when the Chainlink price threshold is updated.
- **Erc20Recovered:** Emitted when unused ERC-20 tokens are recovered by the admin.
- **CoinRecovered:** Emitted when Ether is recovered by the admin.
- **TokensPurchased:** Emitted when tokens are purchased.

## Errors
- **ErrClosed:** Raised when the storage is not active.
- **ErrRoundClosed:** Raised if the current round is not open.
- **ErrNullAddress:** Raised if a specified address is null.
- **ErrInvalidPriceThreshold:** Raised if the price threshold is zero or invalid.
- **ErrRoundAllocation:** Raised if the current round exceeds its allocation.
- **ErrPriceThreshold:** Raised when the price feed's data is outdated.
- **ErrUserNullAddress:** Raised when a specified user address is null.
- **ErrAmountZero:** Raised when the purchase amount is zero.
- **ErrReferral:** Raised if the referral address is the same as the buyer.
- **ErrTransfer:** Raised if a transfer fails.
- **ErrMin:** Raised if the purchase amount is below the minimum limit.
- **ErrMax:** Raised if the purchase amount exceeds the maximum limit.

## Functions
- **Constructor:**
  Initializes the contract with storage, Chainlink price feed, and a price threshold.

- **pause()**:
  Pauses the contract operations, callable by `DEFAULT_ADMIN_ROLE`.

- **unpause()**:
  Resumes the contract operations, callable by `DEFAULT_ADMIN_ROLE`.

- **buy(Storage.Option option_, address ref_)**:
  Allows a user to buy tokens directly using Ether.

- **buyFor(Storage.Option option_, address user_, address ref_)**:
  Enables an external role with `ONRAMP_ROLE` to purchase tokens on behalf of others.

- **setPriceThreshold(uint256 priceThreshold_)**:
  Updates the Chainlink price data's allowable time threshold.

- **recoverCoin()**:
  Recovers unused Ether to the admin wallet.

- **recoverErc20(address token_, uint256 amount_)**:
  Recovers any unused ERC-20 tokens to the admin wallet.

- **getStorage()**:
  Returns the associated storage contract address.

- **getTotal()**:
  Retrieves the total Ether purchased.

- **getPriceThreshold()**:
  Returns the Chainlink price data's allowable time threshold.

## Usage
### Prerequisites
- Ensure OpenZeppelin's contracts are included in your project.
- Deploy the `Storage` contract first, specifying rounds, referral rates, etc.
- Deploy the `CoinSale` contract, providing the `Storage` address, Chainlink price feed address, and an initial price threshold.
- Assign roles using `AccessControl`.

### Buying Tokens
- **Direct Purchase:** Users call `buy()` to purchase tokens directly with Ether.
- **Third-Party Purchase:** External entities with `ONRAMP_ROLE` can purchase tokens on behalf of others using `buyFor()`.

## Contributing
Contributions are welcome! Please adhere to the code style and provide comprehensive tests for any new functionality.

**License:** MIT
