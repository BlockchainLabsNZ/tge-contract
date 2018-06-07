# Test coverage report

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
3. Run: `docker run --rm -a STDOUT -v $(pwd)/contracts:/audit/contracts -v $(pwd)/test:/audit/test nzblabs/test-coverage`
4. Interactive testing environment to play with: `docker run --rm -a STDOUT -v $(pwd)/contracts:/audit/contracts -v $(pwd)/test:/audit/test nzblabs/test-play`. Nano and Vim are installed.

<br>

## Testing results

```
  Contract: OMICrowsdale
    Basic Functions
      Settings
        ✓ should have the correct owners and addresses (179ms)
      Token Rate
1 WEI can purchase: 6128.2 mOMI.
        ✓ should allow the rate to be updated (134ms)
        ✓ should only allow the owner to update the rate (50ms)
        ✓ should not allow rates below zero (62ms)
      Update USD Raised
        ✓ should only allow owners to update the USD raised (40ms)
        ✓ should store updated USD amounts (105ms)
      Pausable
        ✓ should only allow the owner to pause
        ✓ should only allow the owner to unpause (67ms)
        ✓ should not pause if already paused (74ms)
        ✓ should not unpause if already unpaused
      Whitelist
        ✓ should only allow owner to add accounts
        ✓ should be able to add accounts (88ms)
        ✓ should only allow owner to add many accounts at once
        ✓ should be able to add many accounts at once (91ms)
        ✓ should only allow owner to remove accounts
        ✓ should be able to remove accounts (42ms)
    Main Crowdsale
      ✓ should not allow purchases before the crowdsale start time (648ms)
      Token Lock
        ✓ should create one token lock for each purchase (387ms)
        ✓ should set the token locks to 7 days duration (108ms)
        ✓ should lock all of the tokens purchased (116ms)
      Purchase Tracking
        ✓ should keep a running total for transactions (793ms)
      Payments
        should be accepted
          ✓ from whitelisted contributors with the minimum purchase amount before the stage is finished (332ms)
          ✓ from whitelisted contributors with multiple purchases before the stage is finished (629ms)
          ✓ from whitelisted contributors with the maximum purchase amount before the stage is finished (354ms)
        should be rejected
          ✓ when paused (88ms)
          ✓ when contribution is below the minimum requirement (53ms)
          ✓ when contribution is above the maximum requirement (44ms)
          ✓ when contributor is different from beneficiary (46ms)
      End of Crowdsale
        ✓ should finish the crowdsale if the USD raised hits the funding goal (609ms)
        - should finish the crowdsale if the token goal is met
        ✓ should finish the crowdsale if the time is past the end time (683ms)

  Contract: OMITokenLock
    ✓ should have the correct token settings (131ms)
    ✓ should have the correct owner
    ✓ should only allow the owner to mint (90ms)
    ✓ should only allow 1,000,000,000 token to be minted (92ms)
    ✓ should be pausable (273ms)
    ✓ should be able to mint while paused (98ms)
    ✓ should be able to provide an allowance (199ms)

  Contract: OMITokenLock
    ✓ should store an allowance provider
    ✓ should keep track of the number of tokens locked (1268ms)
    ✓ should be pausable (1193ms)
    ✓ should only allow the owner to pause
    ✓ should keep track of the total amount of locked token for a given address (1092ms)
    ✓ should only allow locking tokens that have been provided as an allowance to the token lock contract (667ms)
    ✓ should only allow owner to lock tokens (299ms)
    ✓ should only allow owner to revoke locked tokens (293ms)
    ✓ should allow owner to revoke locked tokens (385ms)
    ✓ should allow owner to lock tokens after the crowdsale is finished (376ms)
    ✓ should only allow the owner to finish the crowdsale (38ms)
    ✓ should only allow the owner to finish the crowdsale once (159ms)
    ✓ should only allow tokens to be released after the crowdsale is finished (1297ms)
    ✓ should wait until lock duration is completed before releasing tokens (1974ms)
    ✓ should reject if a beneficiary has no locks (1499ms)
    ✓ should only allow the owner to call releaseAll (545ms)
    ✓ should only allow valid index ranges for releaseAll (1017ms)
Total gas used for 10 accounts with 3 vesting periods: 10230055
    ✓ gas consumption in a real world scenario (17570ms)


  55 passing (55s)
  1 pending

-------------------|----------|----------|----------|----------|----------------|
File               |  % Stmts | % Branch |  % Funcs |  % Lines |Uncovered Lines |
-------------------|----------|----------|----------|----------|----------------|
 contracts/        |    98.94 |    74.32 |      100 |     98.1 |                |
  OMICrowdsale.sol |    96.88 |       75 |      100 |    97.22 |            166 |
  OMIToken.sol     |      100 |      100 |      100 |      100 |                |
  OMITokenLock.sol |      100 |       74 |      100 |    98.55 |            221 |
-------------------|----------|----------|----------|----------|----------------|
All files          |    98.94 |    74.32 |      100 |     98.1 |                |
-------------------|----------|----------|----------|----------|----------------|
```

