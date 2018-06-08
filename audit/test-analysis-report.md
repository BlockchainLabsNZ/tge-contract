# Test analysis report

of Ecomi Crowdsale tests

<br>

Prepared by: 

- Alex Tikonoff, [alex.tikonoff@blockchainlabs.nz](alex.tikonoff@blockchainlabs.nz)
- Matt Lough, [matt.lough@blockchainlabs.nz](alex.tikonoff@blockchainlabs.nz)

Report: 

- June 08, 2018 – date of delivery 
- June 08, 2018 – last report update


<br>

## OMIToken.test.js

- all good

<br>

## OMIToken.test.js

- all good

<br>

## OMICrowdsale.test.js

- **shouldFulfillPurchase & shouldRejectPurchase**, lines 40-45

	```
	  const shouldFulfillPurchase = async (from, value) =>
   		 await crowdsale.buyTokens(from, { value, from }).should.be.fulfilled

	  const shouldRejectPurchase = async (from, value) => {
   		 await crowdsale.buyTokens(from, { value, from }).should.be.rejected
	  }
	```
Wrapping parentesis usage is inconsistent.

- **shouldFulfillPurchase & shouldRejectPurchase**, lines 40-45

	```
	   it('should be able to add accounts', async () => {
    *** let isWhitelisted = await crowdsale.whitelist(notWhitelisted1)   ***
        isWhitelisted.should.be.false
        await crowdsale.addToWhitelist(notWhitelisted1, { from: owner }).should
          .be.fulfilled
        isWhitelisted = await crowdsale.whitelist(notWhitelisted1)
        isWhitelisted.should.be.true
      })
		...
      it('should be able to add many accounts at once', async () => {
        await crowdsale.addManyToWhitelist([notWhitelisted1, notWhitelisted2], {
          from: owner,
        }).should.be.fulfilled
        isWhitelisted = await crowdsale.whitelist(notWhitelisted1)
        isWhitelisted.should.be.true
        isWhitelisted = await crowdsale.whitelist(notWhitelisted2)
        isWhitelisted.should.be.true
      })
      
	```
Variable declaration should move from `it(..` to the upper scope, to `describe(..`, otherwise test `should be able to add many accounts at once` will fail.

<br>



