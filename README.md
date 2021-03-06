# Building Robust Smart Contracts with OpenZeppelin

See [OpenZeppelin tutorial](https://www.trufflesuite.com/tutorials/robust-smart-contracts-with-openzeppelin)

## Requirements
- [node.js](https://nodejs.org)
- [truffle](https://www.trufflesuite.com/truffle) : `npm install truffle -g
- [ganache](https://www.trufflesuite.com/ganache)
- [MetaMask](https://metamask.io/) browser plugin

## Unboxing the project

`truffle unbox tutorialtoken`

## Creating the "SDVToken" smart contract

- download OpenZeppelin : `npm install openzeppelin-solidity`
- as OpenZeppelin requires solidity 0.6.0, change compiler options to match OpenZeppelin Requirements by adding following lines in file `truffle.js`
```js
  ...
  ,
  compilers: {
    solc: {
      version: "0.6.0"  
    }
  }
```
- also change the line `pragma solidity ^0.4.24;` to `pragma solidity ^0.6.0;` in `contracts/Migrations.sol`
- create the file `contract/SdvToken.sol` and add the following lines :

```solidity
pragma solidity ^0.6.0;

import "openzeppelin-solidity/contracts/token/ERC20/ERC20.sol";

contract SdvToken is ERC20 {
  uint public INITIAL_SUPPLY = 12000;

  constructor() ERC20("SdvToken", "SDV") public
  {
    _setupDecimals(2);
    _mint(msg.sender, INITIAL_SUPPLY);
  }
}
```
- compile project:

```bash
$ truffle compile

Compiling your contracts...
===========================
> Compiling ./contracts/Migrations.sol
> Compiling ./contracts/SdvToken.sol
> Compiling openzeppelin-solidity/contracts/GSN/Context.sol
> Compiling openzeppelin-solidity/contracts/math/SafeMath.sol
> Compiling openzeppelin-solidity/contracts/token/ERC20/ERC20.sol
> Compiling openzeppelin-solidity/contracts/token/ERC20/IERC20.sol
> Artifacts written to /Users/matthieu/workspace/blockchain/sdvtoken/build/contracts
> Compiled successfully using:
   - solc: 0.6.0+commit.26b70077.Emscripten.clang
```

## Create front-End

- create file `migrations/2_deploy_contracts.js`and add the following lines :

```js
var SdvToken = artifacts.require("SdvToken");

module.exports = function(deployer) {
  deployer.deploy(SdvToken);
};
```


## Ganache configuration

- launch ganach app and click on "NEW WORKSPACE" (make sure ETHEREUM is selected)
- enter a workspace name (i.e: sdv-workspace)
- select tab "SERVER", copy the configuration below and then click on [save workspace]
![](https://raw.githubusercontent.com/matthieuaudemard/SdvToken/master/img/ganache-config-server.png)
