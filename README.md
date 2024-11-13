# Bitcoin

BitcoinLikeToken Smart Contract
This contract implements a basic ERC-20-like token with the name "BitcoinLikeToken" (BLT), following some of the essential rules for a fungible token. This token is similar to Bitcoin in terms of its properties, but it is built as an Ethereum-based ERC-20 token with customizable supply.

Code Explanation:
1. License Declaration
solidity
Copy code
// SPDX-License-Identifier: MIT
This line declares the open-source license under which the code is released. In this case, it’s the MIT license, which allows anyone to use, modify, and distribute the code with minimal restrictions.
2. Version Declaration
solidity
Copy code
pragma solidity ^0.8.0;
This line specifies that the code should be compiled using Solidity version 0.8.0 or higher. It ensures compatibility with features and syntax available in Solidity 0.8.x versions.
3. Contract Declaration
solidity
Copy code
contract BitcoinLikeToken {
This declares a new smart contract called BitcoinLikeToken. The contract will implement the functionality of a token that behaves similarly to Bitcoin, but it runs on the Ethereum blockchain.
4. State Variables
solidity
Copy code
string public name = "BitcoinLikeToken";
string public symbol = "BLT";
uint8 public decimals = 18;
uint256 public totalSupply;
name: The name of the token, "BitcoinLikeToken", which is a human-readable string.
symbol: The symbol for the token, "BLT", similar to how Bitcoin is represented by BTC.
decimals: The number of decimal places the token supports. 18 is typical in Ethereum-based tokens (same as Ether).
totalSupply: The total number of tokens that exist. This value will be set when the contract is deployed.
5. Mappings for Balances and Allowances
solidity
Copy code
mapping(address => uint256) public balanceOf;
mapping(address => mapping(address => uint256)) public allowance;
balanceOf: A mapping that stores the balance of each address. Each address (as a key) maps to its corresponding token balance (as a value).
allowance: A mapping that keeps track of how much a spender (second address) is allowed to withdraw from the owner's balance. It allows users to approve third parties to transfer tokens on their behalf.
6. Events
solidity
Copy code
event Transfer(address indexed from, address indexed to, uint256 value);
event Approval(address indexed owner, address indexed spender, uint256 value);
Transfer: An event emitted when tokens are transferred between addresses. This event includes the sender, the recipient, and the amount of tokens transferred.
Approval: An event emitted when a user approves another address to spend tokens on their behalf. It includes the owner, the spender, and the approved amount.
7. Constructor
solidity
Copy code
constructor(uint256 _initialSupply) {
    totalSupply = _initialSupply * 10 ** uint256(decimals);
    balanceOf[msg.sender] = totalSupply;
}
The constructor is executed once when the contract is deployed. It accepts an initial supply (_initialSupply) of the token and sets the total supply.
totalSupply: The total number of tokens created is multiplied by 10 ** uint256(decimals) to account for the decimal places (18 decimals).
The deploying address (msg.sender) is assigned the entire initial supply of tokens.
8. Transfer Function
solidity
Copy code
function transfer(address recipient, uint256 amount) public returns (bool) {
    require(balanceOf[msg.sender] >= amount, "Insufficient balance");
    balanceOf[msg.sender] -= amount;
    balanceOf[recipient] += amount;
    emit Transfer(msg.sender, recipient, amount);
    return true;
}
Purpose: Allows a token holder to transfer tokens to another address.
Logic:
First, it checks that the sender has enough tokens (require(balanceOf[msg.sender] >= amount)).
The sender’s balance is decreased, and the recipient’s balance is increased.
A Transfer event is emitted to notify the network of the transaction.
Finally, the function returns true to indicate the transfer was successful.
9. Approve Function
solidity
Copy code
function approve(address spender, uint256 amount) public returns (bool) {
    allowance[msg.sender][spender] = amount;
    emit Approval(msg.sender, spender, amount);
    return true;
}
Purpose: Allows a token holder to approve another address (spender) to spend a certain amount of their tokens.
Logic:
The function sets the allowance for the spender to the specified amount.
An Approval event is emitted to notify the network of the approval.
The function returns true to indicate the approval was successful.
10. TransferFrom Function
solidity
Copy code
function transferFrom(address sender, address recipient, uint256 amount) public returns (bool) {
    require(balanceOf[sender] >= amount, "Insufficient balance");
    require(allowance[sender][msg.sender] >= amount, "Allowance exceeded");
    balanceOf[sender] -= amount;
    balanceOf[recipient] += amount;
    allowance[sender][msg.sender] -= amount;
    emit Transfer(sender, recipient, amount);
    return true;
}
Purpose: Allows a spender (someone who has been approved to spend tokens) to transfer tokens on behalf of the owner.
Logic:
The function first checks if the sender has enough tokens and if the spender's allowance is enough (require(allowance[sender][msg.sender] >= amount)).
The sender’s balance is decreased, and the recipient’s balance is increased.
The allowance is reduced by the amount transferred.
A Transfer event is emitted to notify the network of the transaction.
The function returns true to indicate the transfer was successful.
11. Check Balance Function
solidity
Copy code
function checkBalance(address account) public view returns (uint256) {
    return balanceOf[account];
}
Purpose: This function allows anyone to check the balance of a particular address.
Logic:
The function takes an address as input and returns the balance stored in the balanceOf mapping.
Key Features:
Token Name: BitcoinLikeToken (BLT)
Decimals: 18 decimals, similar to Ether, allowing for a large precision in token amounts.
Total Supply: The total token supply is defined at deployment.
Transfer Functionality: Users can send tokens to others using the transfer function.
Approval and Delegated Transfer: Users can allow others to transfer tokens on their behalf with approve and transferFrom.
Transparency: The contract emits events like Transfer and Approval to enable external services (e.g., DApps) to track transactions.
How to Use:
Deploying the Contract:
To deploy this contract, an initial supply value (e.g., 1000 tokens) is passed to the constructor.
Interacting with the Contract:
Use the transfer function to send tokens to another address.
Use approve to authorize another address to spend a specific number of tokens on your behalf.
Use transferFrom to transfer tokens from one address to another if you’ve been approved.
This contract is a simple implementation of an ERC-20-like token with basic functionalities like transfer, allowance, and balance tracking. It does not implement all optional ERC-20 functions but is a good starting point for building a Bitcoin-like token on Ethereum.



