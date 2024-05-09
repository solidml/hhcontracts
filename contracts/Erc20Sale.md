# Erc20Sale Smart Contract

The `Erc20Sale` contract is a customizable, ERC-20 compliant token sale mechanism, providing functionality for securely managing the purchase of tokens using other ERC-20 tokens. It ensures proper role-based access control, prevents reentrancy attacks, and integrates pausable functionality.

## Table of Contents
- [Key Features](#key-features)
- [Roles](#roles)
- [Events](#events)
- [Errors](#errors)
- [Functions](#functions)
- [Usage](#usage)
- [Contributing](#contributing)

## Key Features
- **Token Sale Management:** Allows users to purchase tokens using various ERC-20 tokens with referral options.
- **Access Control:** `ONRAMP_ROLE` to manage external token purchases, `DEFAULT_ADMIN_ROLE` to control pausing/unpausing.
- **ReentrancyGuard & Pausable:** Protects against reentrancy attacks and supports emergency stopping.
- **ERC-20 Recovery:** Allows administrators to recover any unused or mistakenly sent ERC-20 tokens.

## Roles
- **DEFAULT_ADMIN_ROLE:** Manages pausing and recovery functions.
- **ONRAMP_ROLE:** Manages external token purchases.

## Events
- **Erc20Recovered:** Emitted when ERC-20 tokens are recovered by the admin.
- **CoinRecovered:** Emitted when native coins are recovered.
- **TokensPurchased:** Emitted when tokens are purchased.

## Errors
- **ErrClosed:** Raised when the storage is not active.
- **ErrRoundClosed:** Raised if the current round is not open.
- **ErrRoundAllocation:** Raised if the current round exceeds its allocation.
- **ErrNullAddress:** Raised if a specified address is null.
- **ErrAmountZero:** Raised when the purchase amount is zero.
- **ErrReferral:** Raised when the referral is the same as the buyer.
- **ErrMin:** Raised if the purchase amount is below the minimum.
- **ErrMax:** Raised if the purchase amount exceeds the maximum.
- **ErrTokenUndefined:** Raised if the token is not defined in the list.
- **ErrTransfer:** Raised if a token transfer fails.

## Functions
- **Constructor:**
  Initializes the contract with specified storage and allowed tokens.

- **pause()**:
  Pauses the contract operations, callable by `DEFAULT_ADMIN_ROLE`.

- **unpause()**:
  Resumes the contract operations, callable by `DEFAULT_ADMIN_ROLE`.

- **buy(address token_, uint256 amount_, Storage.Option option_, address ref_)**:
  Allows a user to purchase tokens directly using an ERC-20 token.

- **buyFor(address token_, uint256 amount_, Storage.Option option_, address user_, address ref_)**:
  Allows a purchase for another user with the `ONRAMP_ROLE`.

- **recoverErc20(address token_, uint256 amount_)**:
  Recovers any unused ERC-20 tokens to the admin wallet.

- **isToken(address token_)**:
  Checks if a given ERC-20 token is supported.

- **getStorage()**:
  Returns the associated storage contract address.

- **getTotal(address token_)**:
  Retrieves the total tokens purchased using the specified ERC-20 token.

## Usage
To deploy and utilize the contract:
1. Ensure OpenZeppelin's contracts are included in your project.
2. Deploy the `Storage` contract first.
3. Deploy the `Erc20Sale` contract, providing the address of `Storage` and the initial list of supported tokens.
4. Assign appropriate roles using the `AccessControl` functions.

### Buying Tokens
- **Direct Purchase:** Users call `buy(token_, amount_, option_, ref_)` to purchase tokens.
- **Third-Party Purchase:** Users with `ONRAMP_ROLE` can purchase tokens on behalf of others using `buyFor()`.

## Contributing
Contributions are welcome! Please adhere to the code style used and provide comprehensive tests for any new functionality.

**License:** MIT
