# MyToken Smart Contract

## Overview

MyToken is an ERC-20 compliant token smart contract implemented in Solidity. It allows minting, burning, and transferring tokens with owner restrictions on minting.

## Features

- **ERC-20 Compliance:** Implements standard ERC-20 functionality.
- **Owner-Controlled Minting:** Only the owner can mint new tokens.
- **Burnable Tokens:** Token holders can burn their own tokens.
- **Transferable Tokens:** Allows token holders to transfer tokens.
- **Event Logging:** Emits events for token transfers.

## Usage

### Deployment

Deploy the contract with an initial supply:

```solidity
constructor(uint256 initialSupply) ERC20("My Token", "MTK") {
    ownerAddress = msg.sender;
    _mint(ownerAddress, initialSupply);
}
```

### Minting Tokens

Only the owner can mint tokens:

```solidity
function mintTokens(address beneficiary, uint256 amount) external onlyOwner {
    _mint(beneficiary, amount);
    emit TokensTransferred(address(0), beneficiary, amount);
}
```

### Burning Tokens

Token holders can burn their tokens:

```solidity
function burnTokens(uint256 amount) external {
    require(balanceOf(msg.sender) >= amount, "Insufficient tokens balance to burn");
    _burn(msg.sender, amount);
    emit TokensTransferred(msg.sender, address(0), amount);
}
```

### Transferring Tokens

Token holders can transfer tokens:

```solidity
function transferTokens(address receiver, uint256 amount) external returns (bool) {
    _transfer(msg.sender, receiver, amount);
    emit TokensTransferred(msg.sender, receiver, amount);
    return true;
}
```

## License

This project is licensed under the MIT License.
