# Dynamic testing report

of Ecomi Crowdsale contracts

-

Prepared by: 

- Alex Tikonoff, [alex.tikonoff@blockchainlabs.nz](alex.tikonoff@blockchainlabs.nz)
- Matt Lough, [matt.lough@blockchainlabs.nz](alex.tikonoff@blockchainlabs.nz)

Report: 

- June 07, 2018 – date of delivery 
- June 07, 2018 – last report update


<br>

## Testing setup

1. Download, install and run docker.
2. Run terminal, cd to you project.
3. Run: `docker run --rm -a STDOUT -v $(pwd)/contracts:/audit/contracts -v $(pwd)/test:/audit/test nzblabs/dynamic-testing`
4. Interactive testing environment to play with: `docker run --rm -a STDOUT -v $(pwd)/contracts:/audit/contracts -v $(pwd)/test:/audit/test nzblabs/test-play`. Nano and Vim are installed.



<br>

## Testing results

```
  Contract: OMICrowsdale
    Basic Functions
      Settings
        ✓ should have the correct owners and addresses (176ms)
      Token Rate
        ✓ should allow the rate to be updated (78ms)
        ✓ should only allow the owner to update the rate
1 WEI can purchase: 6079 mOMI.
        ✓ should not allow rates below zero
      Update USD Raised
        ✓ should only allow owners to update the USD raised
        ✓ should store updated USD amounts (62ms)
      Pausable
        ✓ should only allow the owner to pause
        ✓ should only allow the owner to unpause (69ms)
        ✓ should not pause if already paused (67ms)
        ✓ should not unpause if already unpaused
      Whitelist
        ✓ should only allow owner to add accounts
        ✓ should be able to add accounts (73ms)
        ✓ should only allow owner to add many accounts at once (39ms)
        ✓ should be able to add many accounts at once (82ms)
        ✓ should only allow owner to remove accounts
        ✓ should be able to remove accounts
    Main Crowdsale
      ✓ should not allow purchases before the crowdsale start time (367ms)
      Token Lock
        ✓ should create one token lock for each purchase (202ms)
        ✓ should set the token locks to 7 days duration (62ms)
        ✓ should lock all of the tokens purchased (57ms)
      Purchase Tracking
        ✓ should keep a running total for transactions (320ms)
      Payments
        should be accepted
          ✓ from whitelisted contributors with the minimum purchase amount before the stage is finished (119ms)
          ✓ from whitelisted contributors with multiple purchases before the stage is finished (222ms)
          ✓ from whitelisted contributors with the maximum purchase amount before the stage is finished (122ms)
        should be rejected
          ✓ when paused (74ms)
          ✓ when contribution is below the minimum requirement
          ✓ when contribution is above the maximum requirement
          ✓ when contributor is different from beneficiary
      End of Crowdsale
        ✓ should finish the crowdsale if the USD raised hits the funding goal (261ms)
        - should finish the crowdsale if the token goal is met
        1) should finish the crowdsale if the time is past the end time

    Events emitted during test:
    ---------------------------

    Mint(to: <indexed>, amount: 5e+26)
    Transfer(from: <indexed>, to: <indexed>, value: 5e+26)
    Approval(owner: <indexed>, spender: <indexed>, value: 5e+26)
    LockedTokens(beneficiary: <indexed>, amount: 2.5e+21, releaseTime: 604800)
    TokenPurchase(purchaser: <indexed>, beneficiary: <indexed>, value: 25000000000000000, amount: 2.5e+21)

    ---------------------------

  Contract: OMITokenLock
    ✓ should have the correct token settings (92ms)
    ✓ should have the correct owner
    ✓ should only allow the owner to mint (84ms)
    ✓ should only allow 1,000,000,000 token to be minted (83ms)
    ✓ should be pausable (261ms)
    ✓ should be able to mint while paused (93ms)
    ✓ should be able to provide an allowance (166ms)

  Contract: OMITokenLock
    ✓ should store an allowance provider
    ✓ should keep track of the number of tokens locked (808ms)
    ✓ should be pausable (833ms)
    ✓ should only allow the owner to pause
    ✓ should keep track of the total amount of locked token for a given address (693ms)
    ✓ should only allow locking tokens that have been provided as an allowance to the token lock contract (416ms)
    ✓ should only allow owner to lock tokens (188ms)
    ✓ should only allow owner to revoke locked tokens (190ms)
    ✓ should allow owner to revoke locked tokens (232ms)
    ✓ should allow owner to lock tokens after the crowdsale is finished (216ms)
    ✓ should only allow the owner to finish the crowdsale
    ✓ should only allow the owner to finish the crowdsale once (86ms)
    ✓ should only allow tokens to be released after the crowdsale is finished (877ms)
    ✓ should wait until lock duration is completed before releasing tokens (1135ms)
    ✓ should reject if a beneficiary has no locks (887ms)
    ✓ should only allow the owner to call releaseAll (411ms)
    ✓ should only allow valid index ranges for releaseAll (612ms)
    2) gas consumption in a real world scenario

    Events emitted during test:
    ---------------------------

    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 1600000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 604800)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 3200000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 2419200)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 4800000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 4838400)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 6400000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 604800)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 8000000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 2419200)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 9600000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 4838400)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 11200000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 604800)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 12800000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 2419200)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 14400000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 4838400)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 16000000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 604800)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 17600000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 2419200)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 19200000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 4838400)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 20800000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 604800)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 22400000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 2419200)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 24000000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 4838400)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 25600000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 604800)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 27200000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 2419200)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 28800000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 4838400)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 30400000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 604800)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 32000000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 2419200)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 33600000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 4838400)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 35200000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 604800)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 36800000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 2419200)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 38400000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 4838400)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 40000000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 604800)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 41600000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 2419200)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 43200000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 4838400)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 44800000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 604800)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 46400000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 2419200)
    Mint(to: <indexed>, amount: 1600000)
    Transfer(from: <indexed>, to: <indexed>, value: 1600000)
    Approval(owner: <indexed>, spender: <indexed>, value: 48000000)
    LockedTokens(beneficiary: <indexed>, amount: 1600000, releaseTime: 4838400)
    FinishedCrowdsale()

    ---------------------------


  53 passing (32s)
  1 pending
  2 failing

  1) Contract: OMICrowsdale
       Main Crowdsale
         End of Crowdsale
           should finish the crowdsale if the time is past the end time:

      AssertionError: expected false to be true
      + expected - actual

      -false
      +true

      at _callee37$ (test/OMICrowdsale.test.js:381:31)
      at tryCatch (node_modules/regenerator-runtime/runtime.js:65:40)
      at Generator.invoke [as _invoke] (node_modules/regenerator-runtime/runtime.js:303:22)
      at Generator.prototype.(anonymous function) [as next] (node_modules/regenerator-runtime/runtime.js:117:21)
      at step (test/OMICrowdsale.test.js:3:191)
      at test/OMICrowdsale.test.js:3:361
      at run (node_modules/core-js/modules/es6.promise.js:75:22)
      at node_modules/core-js/modules/es6.promise.js:92:30
      at flush (node_modules/core-js/modules/_microtask.js:18:9)
      at process._tickCallback (internal/process/next_tick.js:61:11)

  2) Contract: OMITokenLock
       gas consumption in a real world scenario:
     AssertionError: expected promise to be fulfilled but it was rejected with 'Error: VM Exception while processing transaction: revert'


```