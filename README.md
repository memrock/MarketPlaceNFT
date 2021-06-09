# NFT marketplace has to:

### 1. Accept any NFT contracts (not just ours). 


### 2. Seller should be able to create Auction or Fix price sale order, transfer NFT to the Market Place contract, and provide parameters: token price, auction duration (in Auction mode), terms of downside protection (time of protection and rate).
- 2.1. Seller should be able to cancel his order if it was not bought or there were no bids on Auction.
- 2.2. In the Auction mode, when the user makes a bid he can't cancel it. The smart contract should hold info only about the highest bidder, if another user makes a higher bid, the previous higher bidder gets refunds. 
- 2.3. In the Fix Price Sale mode, the user may send an off-chain offer with a new price and downside protection terms to the seller. If the seller accepts this offer he creates a sub-order in the smart contract and sends the link to it to the buyer. The sub-order may be limited in time. The buyer can pay it and buy NFT. In case if the seller does not accept the offer - no need to refund money (the buyer did not pay upfront).
- 2.4. All purchases  (in Auction and Fix Price sale) should be with downside protection. 

### 3. When a user buys NFT.
- 3.1. Part from paid amount transfers to our company (CompanyFee). So `amount = amount - CompanyFee;`
- 3.2. The rest splits between downside protection and seller: 

`downside amount = amount * downside protection rate;` (the rate is taken from seller order)

`seller's part = amount - downside amount;`

- 3.3. Seller's part transfers to the seller, downside part transfers to the yield-farming contract (if available).


### 4. Sellers's may claim the rest money from downside protection in one of two cases:
- 4.1. Time of protection expired
- 4.2. Current owner of NFT is not a buyer and not a SmartContract (use function isContract() to check it).


### 5. Buyer may return NFT and get back his downside protection part of money if protection time is not expired. The NFT thransfers to seller.


