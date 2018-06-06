# Ecomi Token Sale contracts Audit Report

## Preamble
This audit report was undertaken by **[BlockchainLabs.nz](https://blockchainlabs.nz)** for the purpose of providing feedback to **[Ecomi](https://www.ecomi.com/)**.

It has subsequently been shared publicly without any express or implied warranty.

Solidity contracts were sourced from GitHub [`17b96f`](https://github.com/BlockchainLabsNZ/tge-contract-audit/commit/17b96ff760471c174d8edbeacc6b8cd2cf2c6b82)

We would encourage all community members and token holders to make their own assessment of the contracts.






<br><!-- *********************************************** -->

## Scope
The following contracts were subject for static analysis:

- [OMICrowdsale.sol](https://github.com/BlockchainLabsNZ/tge-contract-audit/blob/master/contracts/OMICrowdsale.sol)
- [OMIToken.sol](https://github.com/BlockchainLabsNZ/tge-contract-audit/blob/master/contracts/OMIToken.sol)
- [OMITokenLock.sol](https://github.com/BlockchainLabsNZ/tge-contract-audit/blob/master/contracts/OMITokenLock.sol)

### Framework used

This project is using [openzeppelin-solidity v1.8.0](https://github.com/OpenZeppelin/openzeppelin-solidity/releases/tag/v1.8.0), which is not the latest version and lacks some of the useful features of latest Solidity releases, such as constructors, reverting reasons and emitting events.

Repository "zeppelin-solidity" was renamed to the "openzeppelin-solidity" in May, 2018.<br>If One uses `yarn` to install dependencies, the changes in the contracts "import" statements are required, since `yarn` distinguish these repos and import paths from the contract won't be found. 

On the contrary, `npm` warn about this situation, but install old "zeppelin-solidity" repository, so no extra actions are required. 

No original OpenZeppelin Solidity framework contracts were changed.





<br><!-- *********************************************** -->

## Checklist

### Gas Optimization
* [ ] Using string in struct costs more gas than bytes32. [example](https://github.com/BlockchainLabsNZ/mothership-sen/issues/3)
* [ ] Avoid checking if a uint is greater than 0 [example](https://github.com/BlockchainLabsNZ/wings-private-contracts/issues/6)
* [ ] Don't assign a variable which is about to be returned [example](https://github.com/BlockchainLabsNZ/wings-private-contracts/issues/5)
* [ ] Avoid assigning global variables to a local variable. [example](https://github.com/BlockchainLabsNZ/wings-private-contracts/issues/2)
* [ ] uint256 can be used instead of uint8 to save gas. [example](https://github.com/BlockchainLabsNZ/bankorus_contracts_audit/issues/2) and the [reason](https://ethereum.stackexchange.com/questions/3067/why-does-uint8-cost-more-gas-than-uint256)


### Best Practices
* [ ] Have all declared variables/modifiers/functions/events/files been used? [example_1](https://github.com/BlockchainLabsNZ/zipper-contracts/issues/4), [example_2](https://github.com/BlockchainLabsNZ/gifto-contracts/issues/13)
* [ ] Prefer explicit declaration of variable types. [example_1](https://github.com/BlockchainLabsNZ/staking-contracts-audit/issues/3), [example_2](https://github.com/BlockchainLabsNZ/gifto-contracts/issues/9)
* [ ] Prefer explicit declaration of variables access modifiers. [example](https://github.com/BlockchainLabsNZ/gifto-contracts/issues/8)
* [ ] Always use latest stable version of the compiler. [example](https://github.com/BlockchainLabsNZ/staking-contracts-audit/issues/1)
* [ ] Dead code should be removed. [example](https://github.com/BlockchainLabsNZ/wings-private-contracts/issues/7)
* [ ] Consistent naming convention (normally CamelCase). [example_1](https://github.com/BlockchainLabsNZ/wings-private-contracts/issues/4), [example_2](https://github.com/BlockchainLabsNZ/wings-private-contracts/issues/3)
* [ ] Avoid magic numbers. [example](https://github.com/BlockchainLabsNZ/bluzelle-contracts/issues/3)
* [ ] Comments needs should be up to date and reflect code logic. [example](https://github.com/BlockchainLabsNZ/gifto-contracts/issues/11)
* [ ] Prefer require over revert [example](https://github.com/BlockchainLabsNZ/wings-private-contracts/issues/13)
* [ ] Token delivery should be decentralized, an owner should not have to "push" them to the investor [example](https://github.com/BlockchainLabsNZ/gifto-contracts/issues/12)
* [ ] Use only english in comments [example](https://github.com/BlockchainLabsNZ/LAToken-Contracts-Audit/issues/25)
* [ ] Recommend using braces for single line if/for statement. [example](https://github.com/BlockchainLabsNZ/etheal-contracts/issues/5). [discussion](https://stackoverflow.com/questions/2125066/is-it-bad-practice-to-use-an-if-statement-without-brackets)
* [ ] Improve code readability by making use of solidity time uints. [example](https://github.com/BlockchainLabsNZ/leverj-contracts/issues/8)
* [ ] If you are implementing from an interface then it should be declared. [example](https://github.com/BlockchainLabsNZ/poa-popa/issues/2)
* [ ] Repeated safety checks can be replaced by modifier. [example](https://github.com/BlockchainLabsNZ/poa-popa/issues/1)
* [ ] A function should return a result if it's declaration says that it's going to. [example](https://github.com/BlockchainLabsNZ/LINA-TokenERC20/issues/1)
* [ ] Public variables and functions should have different names to avoid duplicates. [example](https://github.com/BlockchainLabsNZ/LINA-TokenERC20/issues/2)


### Code Correctness
* [ ] Token state changes should log an event e.g transfer/mint/burn/change owner, etc [example_1](https://github.com/BlockchainLabsNZ/zipper-contracts/issues/1), [example_2](https://github.com/BlockchainLabsNZ/staking-contracts-audit/issues/2)
* [ ] Contract fully implements the ERC20 standard. [Standard definition](https://theethereum.wiki/w/index.php/ERC20_Token_Standard)
* [ ] Convention is to use capital letters for the token "symbol". [example](https://github.com/BlockchainLabsNZ/gifto-contracts/issues/6)
* [ ] The declaration of pragma version should be at the top of the file, before any imports happen. [example](https://github.com/BlockchainLabsNZ/staking-contracts-audit/issues/1)
* [ ] Enforce the use of specific Solidity compiler version. [example_1](https://github.com/BlockchainLabsNZ/wings-private-contracts/issues/10), [example_2](https://github.com/BlockchainLabsNZ/leverj-contracts/issues/5)
* [ ] Safemath should be used [example](https://github.com/BlockchainLabsNZ/leverj-contracts/issues/4)
* [ ] Use .transfer instead of .send. [example](https://github.com/BlockchainLabsNZ/gifto-contracts/issues/10)
* [ ] Functions should throw an error instead of returning false. [example](https://github.com/BlockchainLabsNZ/mobilego-contracts-audit/issues/1)
* [ ] Measure time milestones with timestamps, not block height. [example](https://github.com/BlockchainLabsNZ/leverj-contracts/issues/6)
* [ ] Favour require() over if( throw; ) statements. [example](https://github.com/BlockchainLabsNZ/mothership-sen/issues/1)

### Known Security Weaknesses
* [ ] Integer Overflow or Underflow [example](https://ethereumdev.io/safemath-protect-overflows/)
* [ ] Re-entrancy attacks [example](https://medium.com/@gus_tavo_guim/reentrancy-attack-on-smart-contracts-how-to-identify-the-exploitable-and-an-example-of-an-attack-4470a2d8dfe4)
* [ ] DoS with reverts [example](https://consensys.github.io/smart-contract-best-practices/known_attacks/#dos-with-unexpected-revert)
* [ ] DoS with Block Gas Limit [example](https://consensys.github.io/smart-contract-best-practices/known_attacks/#dos-with-block-gas-limit)

### Documentation
* [ ] Whitepaper/high level overview
* [ ] Business logic described
* [ ] Code is well documented, comments are relevant
* [ ] Meaningful variables and function names





<br><!-- *********************************************** -->

## Issues

### Severity Description
<table>
<tr>
  <td>Minor</td>
  <td>A defect that does not have a material impact on the contract execution and is likely to be subjective.</td>
</tr>
<tr>
  <td>Moderate</td>
  <td>A defect that could impact the desired outcome of the contract execution in a specific scenario.</td>
</tr>
<tr>
  <td>Major</td>
  <td> A defect that impacts the desired outcome of the contract execution or introduces a weakness that may be exploited.</td>
</tr>
<tr>
  <td>Critical</td>
  <td>A defect that presents a significant security vulnerability or failure of the contract across a range of scenarios.</td>
</tr>
</table>

### Minor
- **Dead code should be removed** `best practice` <br>
There are some dead code should be removed. <br>
XonioToken.sol, Line 18-19:
  ```
  //uint256 public constant INITIAL_SUPPLY = 1000000 * (10 ** uint256(decimals));
  //uint256 public constant INITIAL_SUPPLY = 0;
  ```
  And line 25-26:
  ```
  //balances[msg.sender] = INITIAL_SUPPLY;
  //emit Transfer(0x0, msg.sender, INITIAL_SUPPLY);
  ```
  [View on GitHub](https://github.com/BlockchainLabsNZ/xonio-contracts-audit/issues/2)

- **Crowdsale only lasts 5 minutes but comment says 30 days** `bug` ` correctness` <br>
XonioCrowdsale.sol line 26. It says the crowdsale will only last 5 minutes.
  ```
  TimedCrowdsale(now, now + 5 minutes)
  ```
  This should be a mistake or testing setting cause at the line 10 it says will run for 30 days. <br>
Just a remindar to change it to the correct value before deployment to the Ethereum.
[View on GitHub](https://github.com/BlockchainLabsNZ/xonio-contracts-audit/issues/1)


- **Explicitly declare your variables access modifiers** `best practice` <br>
You should explicitly declare public on the variables that are meant to be public. If not, it can cause unexpected behaviour. And to do this can help to avoid errors.
  ```
  XonioToken mToken;
  ```
  [View on GitHub](https://github.com/BlockchainLabsNZ/xonio-contracts-audit/issues/3)

- **SafeMath.sol is excluded in the repo** `bug` <br>
Several files import SafeMath.sol, but this library is not included in the repo. <br>
[View on GitHub](https://github.com/BlockchainLabsNZ/xonio-contracts-audit/issues/4)

- **Enforce the use of solc 0.4.23** `best practice` <br>
The code is declaring the following `pragma solidity ^0.4.23;`. <br>
The use of `^` states that any solc compiler greater or equal to `0.4.23` and lower than `0.5.0` can be used to run the code. <br>
However, there were some discrepancies in the compiled code and the expected behaviour when using `0.4.24`. <br>
Therefore we recommend using `pragma solidity 0.4.23;` without the `^` and adding `"solc": "0.4.23"` to the dependencies to enforce testing, compiling and deploying with that compiler. <br>
[View on GitHub](https://github.com/BlockchainLabsNZ/xonio-contracts-audit/issues/5)
### Moderate

- None found

### Major

- None found

### Critical

- None found





<br><!-- *********************************************** -->

## Observations

### No real token transfers

TockenLock contract doesn't suppose real token transfer during the Sale.
All tokens are virtually deposited to the Lock contract and could be transferred to the customers after 7 days after the Sale is finished. 

The process of sending tokens is possible only when particular AllowanceProvider Contract has that tokens on its balance.

That contract is not under audit, so we can not grant that AllowanceProvider will have required amount of tokens to distribute to buyers.

### Exchange rate updated from outside

The token exchange rate is a subject to external changes and could be set by Contract Owner to any value. We encourage customers to check the rate thoroughly before buying.

### WhitelistedCrowdsale.sol

Only whitelisted account allowed to check the token purchases from its own and other accounts, but Ethereum blockchain is transparent to everyone and anyone could check token purchases history for this project. 

Nevertheless, WhitelistedCrowdsale.sol contract modifier `isWhitelisted` was used, just once and just to restrict purchase history check. 



<br><!-- *********************************************** -->

## Conclusion
Overall we have not identified any potential vulnerabilities and satisfied that this Smart Contract does not exhibit any known security vulnerabilities. This contract has a low level risk of XXX02 being hacked or stolen.  

___

### Disclaimer

Our team uses our current understanding of the best practises for Solidity and Smart Contracts. Development in Solidity and for Blockchain is an emerging area of software engineering which still has a lot of room to grow, hence our current understanding of best practices may not find all of the issues in this code and design.

We have not analysed any of the assembly code generated by the Solidity compiler. We have not verified the deployment process and configurations of the contracts. We have only analysed the code outlined in the scope. We have not verified any of the claims made by any of the organisations behind this code.

Security audits do not warrant bug-free code. We encourage all users interacting with smart contract code to continue to analyse and inform themselves of any risks before interacting with any smart contracts.
