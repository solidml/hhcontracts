# Storage Smart Contract

The `Storage` contract acts as a central data management system, managing rounds, referrals, funds, and state changes for a broader token sale platform. It provides secure methods to administer and control different aspects of a token sale.

## Table of Contents
- [Key Features](#key-features)
- [Roles](#roles)
- [Events](#events)
- [Errors](#errors)
- [Functions](#functions)
- [Usage](#usage)
- [Contributing](#contributing)

## Key Features
- **Rounds Management:** Allows defining, opening, and closing rounds with price and supply updates.
- **Referral System:** Provides support for multi-level referral rates and enables/disable referrals.
- **Access Control:** Uses OpenZeppelin's `AccessControl` for robust role-based management.
- **Secure Transfers & Limits:** Safely handles transfers and enforces min/max limits per user.

## Roles
- **DEFAULT_ADMIN_ROLE:** Administers the contract, controls state changes, and manages limits.
- **OPERATOR_ROLE:** Manages rounds and referrals.

## Events
- **StateUpdated:** Emitted when the state of the entire sale is changed.
- **RoundOpened:** Emitted when a round is opened.
- **RoundClosed:** Emitted when a round is closed.
- **RoundAdded:** Emitted when a new round is created with specific prices and supply.
- **RoundPriceUpdated:** Emitted when a round's price is updated.
- **RoundSupplyUpdated:** Emitted when a round's supply is updated.
- **Erc20Recovered:** Emitted when ERC-20 tokens are recovered by the admin.
- **CoinRecovered:** Emitted when Ether is recovered by the admin.
- **AuthLimitUpdated:** Emitted when the authorization limit is updated.
- **AuthUserUpdated:** Emitted when a specific user's authorization status is updated.
- **MaxUpdated:** Emitted when the max limit is updated.
- **MinUpdated:** Emitted when the min limit is updated.
- **TreasuryUpdated:** Emitted when the treasury address is updated.
- **RefRateSetup:** Emitted when referral rates are set.
- **ReferralSetup:** Emitted when a referral is set up with specific rates.
- **ReferralEnabled:** Emitted when a referral is enabled.
- **ReferralDisabled:** Emitted when a referral is disabled.
- **ClaimedFunds:** Emitted when a referral successfully claims funds.

## Errors
- **ErrParamsInvalid:** Raised when input parameters are invalid.
- **ErrStarted:** Raised when attempting to start an already started process.
- **ErrClosed:** Raised when the process is closed or inactive.
- **ErrNullAddress:** Raised if a specified address is null.
- **ErrRoundUndefined:** Raised when a specified round index is undefined.
- **ErrRoundStarted:** Raised when trying to modify an already started round.
- **ErrRoundClosed:** Raised when trying to operate on a closed round.
- **ErrRoundSupply:** Raised when the supply of a round is inadequate.
- **ErrMin:** Raised when a value is below the minimum limit.
- **ErrMax:** Raised when a value exceeds the maximum limit.
- **ErrAuthLimit:** Raised when authorization limits are invalid.
- **ErrFirstRefFunds:** Raised when the first referral funds exceed the allowable rate.
- **ErrSecondRefFunds:** Raised when the second referral funds exceed the allowable rate.
- **ErrRefUndefined:** Raised when a specified referral is undefined.
- **ErrRefEnabled:** Raised if a referral is already enabled.
- **ErrRefDisabled:** Raised if a referral is already disabled.
- **ErrTokenUndefined:** Raised if no tokens are specified for referral claims.
- **ErrTransfer:** Raised if a transfer operation fails.

## Functions
- **Constructor:** Initializes the storage contract with the specified treasury address.

- **open()**:
  Opens the storage system for operation.

- **close()**:
  Closes the storage system for operation.

- **setRound(uint256 sPrice_, uint256 lPrice_, uint256 supply_)**:
  Adds a new round with specific short and long prices and supply.

- **setRefRate(uint256 firstRefRate_, uint256 secondRefRate_)**:
  Configures the global referral rates.

- **setupReferrals(address[] calldata refs_, uint256[] calldata firstRefRate_, uint256[] calldata secodRefFunds_)**:
  Configures individual referral rates for multiple addresses.

- **updateRoundPrice(uint256 index_, uint256 sPrice_, uint256 lPrice_)**:
  Updates a round's short and long prices.

- **updateRoundSupply(uint256 index_, uint256 supply_)**:
  Adjusts the supply for an existing round.

- **openRound(uint256 index_)**:
  Opens a specific round for operation.

- **closeRound(uint256 index_)**:
  Closes a specific round.

- **setAuth(address user_, bool value_)**:
  Assigns an authorization value to a user.

- **setAuthBatch(address[] calldata users_, bool[] calldata values_)**:
  Assigns authorization values in batch.

- **setMax(uint256 amount_)**:
  Updates the maximum limit.

- **setMin(uint256 amount_)**:
  Updates the minimum limit.

- **setAuthLimit(uint256 amount_)**:
  Sets the authorization limit.

- **setTreasury(address treasury_)**:
  Changes the treasury address.

- **setState(address user_, address token_, uint256 amount_, uint256 sold_, address ref_, uint256 fReward_, uint256 sReward_)**:
  Updates the state after a purchase with referral rewards.

- **enableReferral(address ref_)**:
  Enables a specific referral.

- **disableReferral(address ref_)**:
  Disables a specific referral.

- **claimRef(address[] calldata tokens_)**:
  Allows referrals to claim their earned funds.

- **recoverCoin()**:
  Recovers Ether to the admin wallet.

- **recoverErc20(address token_, uint256 amount_)**:
  Recovers ERC-20 tokens to the admin wallet.

- **getTreasury()**:
  Returns the treasury address.

- **getMax()**:
  Returns the maximum limit.

- **getMin()**:
  Returns the minimum limit.

- **getRoundsCount()**:
  Returns the count of available rounds.

- **getCurrentRound()**:
  Returns the currently active round index.

- **getRound(uint256 index_)**:
  Retrieves a round's details.

- **getTotalSold()**:
  Returns the total tokens sold.

- **balanceOf(uint256 round_, address user_)**:
  Returns the balance of a user in a specified round.

- **refBalanceOf(address token_, address user_)**:
  Returns the referral balance of a user for a specific token.

- **limitOf(address user_)**:
  Returns the available purchase limit for a user.

- **maxLimitOf(address user_)**:
  Returns the available maximum purchase limit for a user.

- **getAuthLimit()**:
  Returns the authorization limit.

- **getRefRates()**:
  Returns the global referral rates.

- **getRef(address user_, address ref_)**:
  Determines and returns a referral address for a user.

- **getRefRates(address ref_)**:
  Returns the referral rates for a specific referral.

- **isActive()**:
  Returns `true` if the system is active.

- **isInactive()**:
  Returns `true` if the system is inactive.

- **getPrice(Option option_)**:
  Returns the price for a specified option.

- **isAuth(address user_)**:
  Checks whether a user has authorization.

## Usage
### Prerequisites
- Ensure OpenZeppelin's contracts are included in your project.
- Deploy the `Storage` contract and configure rounds, limits, and referrals as needed.
- Assign roles using `AccessControl`.

## Contributing
Contributions are welcome! Please follow the code style used and provide tests for any new functionality.

**License:** MIT
