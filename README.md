# MD coins Smart Contracts
Public Repository for the MD Coins smart contracts



## Contracts
The Led Tokens are based on the `StandardToken` and `MintableToken` ERC20 contracts. Additional functionality is heavily inspired by the `MinimeToken` (https://github.com/Giveth/minime/blob/master/contracts/MiniMeToken.sol)

## How to use the tokensale contract
The following contracts will be hosted on this repository.
- The tokensale contract
- The Led token contract
- The token factory contract
- Several other interface contracts


## For the ICO team
There are not much of prerequisites for using the smart contract.

### Contract setup:

#### 1. Compile and migrate the contracts to the network.
This can be done with the `truffle migrate --network ethereum` command. The contract addresses will successively appear
on the console

### Critical Verifications:

#### 1. Verify the multisig address
The multisig refers to the wallet to which funds from the tokensale are transferred when a investor sends ether
#### 2. Verify the MD wallet
The MD wallet receives the MD Coins when upon completion of the tokensale
#### 3. Verify the start date and end date
Token purchase can be made only between the start block and the end block
#### 4. Verify the token the token cap, the cap, and the wei cap
The token cap is the maximum number of tokens that can be issued in ERC20 units (= number of tokens times 10^18)
The cap is the maximum number of tokens that can be issued
#### 5. Verify all the rest


- The token sale will start on the date indicated by the `startTime` variable. Alternatively, it is possible to force the starting of the token sale by calling the `forceStart` method. Only the tokensale controller can call this method.

- By default the MD Coins are not transferable at the start of the tokensale. The controller of the tokensale can call the 
`enableTransfers` and `lockTransfers` methods to make token transferables. After the endTime, anybody can make the tokens definitely transferables by calling the `enableTransfers` method. The `lockTransfers` method will fail after the end of the token sale.

- The token master wallet can be used to send tokens to certain addresses (ex: exchanges) without making transfers available to anyone before the end of the presale. The token sale controller can call the `enableMasterTransfers` and `lockMasterTransfers` to activate/deactivate this option.


### Token Sale Pause


- The tokensale can be paused with the `pause` function. In this case, token minting is paused and tokens can not be bought anymore. This does not affect whether tokens are transferable or not.


### Token Sale Finalization:

The token sale can be finalized in different ways.

- First if the end block is reached, no more tokens can be issued by the token sale. The rest of the functionality of the tokensale contract however remains available. It is necessary to manually enable transfers through the `enableTransfers` function (can only be called by the owner of the tokensale).


- The last and standard way to finalize the token sale is to call the `finalize` function. This function can only be called by the owner of the token sale contract and can only be called when the token sale is paused. This automatically finishes the minting of the led tokens and enables token transfers

Step-by-step instructions to finalize the token sale:

1. Pause the token sale with the `pause` function
2. Allocate Led Tokens with the `allocateLedTokens` function - step 1 needs to be completed
2. Finalize the token sale with the `finalize` function - step 1 and 2 need to be completed
3. Optionally, transfer the control of the Led token to another smart-contract


### Development and Testing Environment Setup

#### Requirements :
- OSX or Linux (Windows setup is likely possible but not covered in this guide)
- Node (version  (at least)  8.7.0 required for the testing environment)
- testrpc / geth

#### Testing Environment Setup :

- Clone the repository and install dependencies

```
git clone https://github.com/justdvnsh/MD-Coins.git
cd MD-Coins
npm install
```

- Install the latest version of truffle
```
npm install -g truffle
```

- Compile contracts
```
truffle compile
```

- Initialize testrpc (or geth)

```
testrpc
```

- Migrate contracts to chosen network

```
truffle migrate --network development
```

- Make sure you are using the latest version of node

```
nvm install 8.7.0
nvm use 8.7.0
```


- Fill in `truffle.js` and `deploy_contracts.js` with appropriate wallet addresses. Unlock the corresponding accounts.

- Verify all tests are passing

```
truffle test
```

- You can interact with the contracts via the console

```
truffle console
```



