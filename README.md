# SimpleBankingSystem

## Overview

A basic smart contract for simulating a banking system. This contract includes functionality for minting tokens, withdrawing tokens, and checking balances. It incorporates Solidity's `require()`, `assert()`, and `revert()` for error handling.

## Features

- **Minting**: Allows the owner to mint new tokens to a specified address.
- **Withdrawal**: Users can withdraw tokens from their balance.
- **Balance Check**: Users can check their token balance.
- **Invariant Check**: Ensures the contract is in a valid state.
- **Custom Revert**: Demonstrates custom error messages.

## Contract Code

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SimpleBankingSystem {
    address public owner;
    mapping(address => uint256) private balances;

    // Sets the contract deployer as the owner
    constructor() {
        owner = msg.sender;
    }

    // Restricts access to the owner
    modifier onlyOwner() {
        require(msg.sender == owner, "Not authorized");
        _;
    }

    // Mints tokens to a specified address
    function mint(address to, uint256 amount) external onlyOwner {
        require(to != address(0), "Invalid address"); // Valid recipient
        require(amount > 0, "Amount must be > 0"); // Positive amount
        balances[to] += amount; // Update balance
    }

    // Withdraws tokens from the caller
    function withdraw(uint256 amount) external {
        require(amount > 0, "Amount must be > 0"); // Positive amount
        uint256 userBalance = balances[msg.sender];
        require(userBalance >= amount, "Insufficient balance"); // Enough balance
        balances[msg.sender] -= amount; // Update balance
        // Simulate withdrawal
    }

    // Returns the caller's balance
    function getBalance() external view returns (uint256) {
        return balances[msg.sender];
    }

    // Checks if the contract is valid
    function checkInvariant() external view returns (string memory) {
        assert(owner != address(0)); // Owner should not be zero address
        return "Invariant check passed";
    }

    // Custom revert with message
    function customRevert(bool condition) external pure {
        if (!condition) {
            revert("Custom revert error"); // Revert with message
        }
    }
}

```

## Usage
1.**Deploy the Contract:** Deploy SimpleBankingSystem using a Solidity development environment like Remix.

2.**Mint Tokens:** Call the mint() function with an address and amount. This function can only be executed by the contract owner.

3.**Withdraw Tokens:** Call the withdraw() function with the amount to withdraw. Ensure you have sufficient balance.

4.**Check Balance:** Call the getBalance() function to check your current token balance.

5.**Invariant Check:** Call checkInvariant() to verify the contract's state. It should confirm that the owner address is valid.

6.**Custom Revert:** Test the customRevert() function with different conditions to see how custom error messages are handled.

## License
This project is licensed under the MIT License. See the LICENSE file for details.
```sh

Feel free to customize the sections as needed for your project or audience!
```
