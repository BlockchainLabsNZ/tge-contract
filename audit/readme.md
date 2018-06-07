# Ecomi Token Sale contracts Audit Report

Prepared by: 

- Alex Tikonoff, [alex.tikonoff@blockchainlabs.nz](alex.tikonoff@blockchainlabs.nz)
- Matt Lough, [matt.lough@blockchainlabs.nz](alex.tikonoff@blockchainlabs.nz)

Report: 

- June 06, 2018 – date of delivery 
- June 07, 2018 – last report update


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


### Documentation

 - [ ] Whitepaper, presentations, high level overview
 - [ ] Business logic workflow is described
 - [ ] Variables and constants are described
 - [x] Code is documented well enough, comments are helpful and reflect code logic
 - [ ] Completely commented code
 - [x] Meaningful variables and functions names
 - [ ] No typos in documentation/comments


### Code 

- #### Logic

 - [ ] Contract-driven token distribution (no dependency on external actors)
 - [ ] No Front-end dependencies (distribution scripts, running nodes, bridges, ... )
 - [x] No upgradeable contracts
 - [x] No Oracles


- #### Simplicity

 - [x] No custom approaches in business logic implementation
 - [x] No Assembly calls
 - [x] No Internal call with user content (such as bytes32 parameters)
 - [x] Insignificant number of internal calls, cross-links and other self-dependencies
 - [x] Low overall code complexity (non-expert developers can understand)



- #### Correctness

 - [x] Adherence to adopted standards such as ERC20
 - [ ] Latest version of pragma
 - [ ] Latest syntax (constructors, emit, ... )
 - [x] Common and well tested libraries and frameworks are used (e.g. Open Zeppelin)  
 - [x] Variable types declared explicitly (uint256 vs uint)
 - [x] Access modifiers declared explicitly
 - [x] Consistent naming convention (CamelCase/pascalCase, underscores, ...) 
 - [ ] No magic numbers (variables defined with any "obvious" numbers without explanation) – [example](https://github.com/BlockchainLabsNZ/bluzelle-contracts/issues/3)
 - [ ] Solidity variables are used (`1 year` vs `365*24*60*60`) – [list](https://solidity.readthedocs.io/en/v0.4.24/units-and-global-variables.html)
 - [x] Functions explicitly returns boolean if it was declared
 - [x] Tight struct packing
 - [ ] Fallbacks function logging events
 - [ ] Latest(ish) (of stable) version of 
	 - [ ] Solidity compiler
	 - [x] Frameworks
	 - [ ] Development/testing environment

- #### Testability
*[not audited  yet]*

		 - [ ] Test coverage across all functions and events
		 - [ ] Test cases for both expected behaviour and failure modes
		 - [ ] Settings for easy testing of a range of parameters
		 - [ ] No reliance on nested callback functions or console logs
		 - [ ] No test scenarios calling other test scenarios



### Gas Optimization

 - [x] No string used in structs (which is more expensive than bytes32) – [example](https://github.com/BlockchainLabsNZ/mothership-sen/issues/3)
 - [ ] No variables assigned when it's possible to avoid without losing the meaning – [example](https://github.com/BlockchainLabsNZ/wings-private-contracts/issues/2) *[not audited  yet]*
 - [x] No uint8/16/32/... used, only uint256 – [gas saving reason](https://ethereum.stackexchange.com/questions/3067/why-does-uint8-cost-more-gas-than-uint256)
 - [x] No dead code found. All declared variables/modifiers/functions/events/files have been used



### Other Best Practices

 - [x] The pragma version declaration is on the top of the code
 - [ ] Solidity compiler has strict version (not a range) [example_1](https://github.com/BlockchainLabsNZ/wings-private-contracts/issues/10), [example_2](https://github.com/BlockchainLabsNZ/leverj-contracts/issues/5)
 - [x] Safemath is used (if  [example](https://github.com/BlockchainLabsNZ/leverj-contracts/issues/4)
 - [x] Require over revert/throw – [example](https://github.com/BlockchainLabsNZ/wings-private-contracts/issues/13)
 - [x] English comments only
 - [x] Single line if/for statements are wrapped with curly braces – [discussion](https://stackoverflow.com/questions/2125066/is-it-bad-practice-to-use-an-if-statement-without-brackets)
 - [x] Contracts are explicit about interface they implement (if any) – [example](https://github.com/BlockchainLabsNZ/poa-popa/issues/2)
 - [x] No repeated code
 - [x] Names of public variables and functions help to differentiate them (to avoid misunderstanding on Etherscan) – [example](https://github.com/BlockchainLabsNZ/LINA-TokenERC20/issues/2)
 - [x] Token state changes emit log events (e.g transfer/mint/burn/change owner, etc)
 - [x] Contract fully implements the ERC20 standard. [Standard definition](https://theethereum.wiki/w/index.php/ERC20_Token_Standard)
 - [x] Token symbol consist of capital letters only
 - [x] No `.send` instructions (only `.transfer`, if any)
 - [x] No just `return false` instructions, there is an appropriate error handling or throwing errors at least




  
### Known Security Weaknesses 
*[not audited  yet]*

	 - [ ] Integer Overflow or Underflow [example](https://ethereumdev.io/safemath-protect-overflows/) 
	 - [ ] Re-entrancy attacks [example](https://medium.com/@gus_tavo_guim/reentrancy-attack-on-smart-contracts-how-to-identify-the-exploitable-and-an-example-of-an-attack-4470a2d8dfe4)
	 - [ ] DoS with (unexpected)reverts [example](https://consensys.github.io/smart-contract-best-practices/known_attacks/#dos-with-unexpected-revert) 
	 - [ ] DoS with Block Gas Limit [example](https://consensys.github.io/smart-contract-best-practices/known_attacks/#dos-with-block-gas-limit) 
	 - [ ] Honey pots 
	 - [ ] proxyOverflow
	 - [ ] Transaction-Ordering Dependence (TOD) / Front Running 
	 - [ ] Timestamp Dependence
	 - [ ] Forcibly Sending Ether to a Contract
	 - [ ] Race conditions 
		- [ ] Re-entrancy 
		- [ ] Cross-function race condition
		- [ ] Race conditions bad solutions




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

<br>

### Minor
- **Contract defining variables are not defined by default** `best practice`
<br>There is no check that `tokenAllowance`, `allowanceProvider`, `crowdsale` are valid.
<br>Consider to add them to the contract constructor. 
<br>[View on GitHub](https://github.com/BlockchainLabsNZ/tge-contract-audit/issues/1)

- **Multiple reverting** `correctness`
<br>If require(_release(_beneficiary)) fails by some reason, allreleaseAll()` function will fail.
Probably, it could be better to log failed release and continue the loop.
<br>[View on GitHub](https://github.com/BlockchainLabsNZ/tge-contract-audit/issues/2)

- **Old Solidity version** `best practice`
<br>The current Solidity release version is 0.4.24. The project is using 0.4.18, which lacks some of the useful features of latest releases, such as constructors, reverting reasons and emitting events.
<br>[View on GitHub](https://github.com/BlockchainLabsNZ/tge-contract-audit/issues/3)

- **Zeppelin Solidity framework was renamed** `testability`
<br>Repository "zeppelin-solidity" was renamed to the "openzeppelin-solidity" in May, 2018.
If One uses yarn to install dependencies, the changes in the contracts "import" statements are required, since yarn distinguish these repos and import paths from the contract won't be found.
<br>[View on GitHub](https://github.com/BlockchainLabsNZ/tge-contract-audit/issues/4)

- **Unnecessary limits checking** `correctness`
<br>```
  for (uint256 i = 0; i < lock.locks.length; i = i.add(1)) {
     ...
```     
There is no necessity to use SafeMath.sol lab in this case since there is limits check already presented: `... ; i < ....;`
<br>[View on GitHub](https://github.com/BlockchainLabsNZ/tge-contract-audit/issues/5)

- **require() vs. modifiers** `best practice`
<br>`require(!isFinalized);`
These lines use approach which is different to the rest of project with `whenNotPaused` and `whenNotFinalized` modifiers in the same contract.
<br>[View on GitHub](https://github.com/BlockchainLabsNZ/tge-contract-audit/issues/6)

<br>

### Moderate

- **Any address could be used as Crowdsale or AllowanceProvider addresses** `correctness`
<br>

	```
	function setCrowdsaleAddress (address _crowdsale) public onlyOwner returns (bool) {
   		crowdsale = _crowdsale;
    	return true;
  	}
```
Consider to validate that crowdsale contract is an actual crowdsale contract, not just an address.
<br>[View on GitHub](https://github.com/BlockchainLabsNZ/tge-contract-audit/issues/7)

- **Finalization crowdsale could be incomplete** `correctness`
<br>The Crowdsale `_finalization()` is an internal function and could be called only that lines 166, 170, 174.
<br>But, `_updatePurchasingState()` could be called only from `buyToken()` from Crowdsale.sol.
<br>That means if there are not enough purchases, the developers will be forced to buy their tokens themselves.
<br>[View on GitHub](https://github.com/BlockchainLabsNZ/tge-contract-audit/issues/1)

<br>
### Major

- None found

<br>

### Critical

- **Token transfer to the wrong account** `best practice`
<br>The `transferFrom()` sends tokens to the `msg.sender`, which is ok if the internal function `_release()` called from public function `releaseToken()`. 
<br>But when `_release()` called from the `releaseAll()`, then msg.sender is an owner (not the actual beneficiary) and the token will be transferred to that owner's (contract) account.
<br>[View on GitHub](https://github.com/BlockchainLabsNZ/tge-contract-audit/issues/1)






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
<!--Overall we have not identified any potential vulnerabilities and satisfied that this Smart Contract does not exhibit any known security vulnerabilities. This contract has a low level risk of XXX02 being hacked or stolen.  -->

TBD



<br>
___

### Disclaimer

Our team uses our current understanding of the best practises for Solidity and Smart Contracts. Development in Solidity and for Blockchain is an emerging area of software engineering which still has a lot of room to grow, hence our current understanding of best practices may not find all of the issues in this code and design.

We have not analysed any of the assembly code generated by the Solidity compiler. We have not verified the deployment process and configurations of the contracts. We have only analysed the code outlined in the scope. We have not verified any of the claims made by any of the organisations behind this code.

Security audits do not warrant bug-free code. We encourage all users interacting with smart contract code to continue to analyse and inform themselves of any risks before interacting with any smart contracts.
