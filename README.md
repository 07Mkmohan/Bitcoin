BitcoinLikeToken (BLT)

A minimal ERC-20–style token implemented in Solidity. This contract replicates Bitcoin-like fixed-supply behavior while providing common token mechanics: transfers, approvals, and allowance-based spending.

🚀 Features

Fixed total supply minted on deployment

Standard token metadata (name, symbol, decimals)

Balance + allowance tracking

ERC-20–style events (Transfer, Approval)

Lightweight, simple, and beginner-friendly

📝 Token Information
Property	Value
Name	BitcoinLikeToken
Symbol	BLT
Decimals	18
Total Supply	Defined at deployment
🔧 Deployment

Deploy with the constructor parameter:

constructor(uint256 _initialSupply)


Example:

new BitcoinLikeToken(1_000_000);


Creates:

1,000,000 × 10^18 tokens


All tokens are assigned to the deployer.

🧪 Functions Overview
transfer(address to, uint256 amount)

Transfers tokens from the caller to another address.

approve(address spender, uint256 amount)

Approves another address to spend tokens on the caller’s behalf.

transferFrom(address from, address to, uint256 amount)

Allows a spender (approved earlier) to transfer tokens.

checkBalance(address account)

Returns the token balance of any address.

📄 Contract Source
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract BitcoinLikeToken {
    string public name = "BitcoinLikeToken";
    string public symbol = "BLT";
    uint8 public decimals = 18;
    uint256 public totalSupply;

    mapping(address => uint256) public balanceOf;
    mapping(address => mapping(address => uint256)) public allowance;

    event Transfer(address indexed from, address indexed to, uint256 value);
    event Approval(address indexed owner, address indexed spender, uint256 value);

    constructor(uint256 _initialSupply) {
        totalSupply = _initialSupply * 10 ** uint256(decimals);
        balanceOf[msg.sender] = totalSupply;
    }

    function transfer(address recipient, uint256 amount) public returns (bool) {
        require(balanceOf[msg.sender] >= amount, "Insufficient balance");
        balanceOf[msg.sender] -= amount;
        balanceOf[recipient] += amount;
        emit Transfer(msg.sender, recipient, amount);
        return true;
    }

    function approve(address spender, uint256 amount) public returns (bool) {
        allowance[msg.sender][spender] = amount;
        emit Approval(msg.sender, spender, amount);
        return true;
    }

    function transferFrom(address sender, address recipient, uint256 amount) public returns (bool) {
        require(balanceOf[sender] >= amount, "Insufficient balance");
        require(allowance[sender][msg.sender] >= amount, "Allowance exceeded");
        balanceOf[sender] -= amount;
        balanceOf[recipient] += amount;
        allowance[sender][msg.sender] -= amount;
        emit Transfer(sender, recipient, amount);
        return true;
    }

    function checkBalance(address account) public view returns (uint256) {
        return balanceOf[account];
    }
}

📄 License

This project is released under the MIT License.
