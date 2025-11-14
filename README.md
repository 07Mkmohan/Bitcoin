BitcoinLikeToken (BLT)

A minimal ERC-20–style token implemented in Solidity. This contract replicates core Bitcoin-like properties (fixed supply and no minting) while providing standard token functions such as transfer, approve, and transferFrom.

🚀 Features

Fixed supply minted at deployment

Standard token metadata (name, symbol, decimals)

Balance + allowance tracking

ERC-20–style events (Transfer, Approval)

Lightweight, easy for learning or testing

📝 Token Information
Property	Value
Name	BitcoinLikeToken
Symbol	BLT
Decimals	18
Total Supply	Set on deployment
🔧 Contract Deployment

In Remix or Hardhat, deploy with:

constructor(uint256 _initialSupply)


Example:

new BitcoinLikeToken(1000000);


This results in:

1,000,000 * 10^18 tokens


All tokens go to the deployer.

🧪 Available Functions
transfer(address to, uint256 amount)

Send tokens directly.

approve(address spender, uint256 amount)

Approve another address to spend your tokens.

transferFrom(address from, address to, uint256 amount)

Spend tokens via an allowance.

checkBalance(address account)

Return an address's token balance.
