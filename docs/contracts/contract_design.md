The WeiFund Standard Campaign only handles the intake of contributions, and the output of either campaign payout to the beneficiary account. If the campaign is a success or if the funding goal is specified above zero, refund functionality for contributors to receive a refund if the campaign is a failure.

The WeiFund StandardCampaign uses a tightly enforced state machine design specified in “modifier atStageOr” on all state changing contract methods. This state machine is stated as a modifier which ensures the campaign is in one of three phases or contract stages. There are only three stages a StandardCamapign can be in. The contract is either in the (0) “operational”, (1) “failure” or (2) “success” stage.

The contract cannot be in any other stage. The contract is in the operational stage, if the current block timestamp is less than the expiry UNIX timestamp specified at the time of contract creation.

The contract is in the “success” stage, if the current block UNIX timestamp is greater than or equal to the expiry UNIX timestamp stated at contract creation, the amount raised by contributions is greater than or equal to the funding goal and the funding goal is greater than zero.

A contributor may only contribute to the StandardCampaign if is in the (0) “operational” stage. A contributor may only receive payouts if the campaign is in the (1) “failure” stage. A campaign can only be payed out if it is in the (2) “success” stage.

The StandardCampaign allows anyone to use the contract fallback function as a contribution method. While this is not a recommended best practice in the “Ethereum Best Practices Doc”, it allows the use of QR codes to send Ether to campaigns which is a very popular feature for many Ethereum and WeiFund users.

If the contract funding goal is set to zero, this means the campaign will never hit stage “failure” (1). Any StandardCampaign with a funding goal (“fundingGoal()”) set to zero will be considered an open StandardCampaign, which means it never fails and the refund functionality can never be used on the campaign contract.

The contribution method “contributeMsgValue” simple notates the contribution made and intakes the msg.value (i.e. the Ether sent to the campaign contract). Because all contributions are notated and registered as a contribution instance, this allows third-party services to be constructed and connected with the campaign, that can use the contribution creation time, sender and amount metrics as a way of determining reward or contract logic. Essentially, it's a design model chosen on purpose to allow for other services to build fairly comprehensive third-party services such as: token or product dispersal both during and after a campaign has ended.

The payout method “payoutToBeneficiary” simply pays out the funds of the campaign out to the beneficiary account address specified. This could be anything from a vanilla Ethereum account, to a multi-signature wallet or governance structure such as a Board (see: BoardRoom.to).

The refund method “claimRefundOwed” simply pays out the refund of a specific campaign contribution. Only the contributor who made the contribution can initiate the refund claim of that Ether as a refund. Only one refund claim can be made by the rightful refund recipient per each contribution made. This means you only get one shot at refunding each contribution, so please ensure you have enough gas in your transaction and that you have properly specified the refund contribution information. The method requires to to provide a single method input stating the contribution ID as a uint256 (unsigned integer 256). The WeiFund user interface does this for you, but if you would like to do the refund through a wallet or command line system, this is the required single input. Please ensure that you are the contribution sender of the refund you are trying to claim. Only the contribution sender may refund their own contribution if the campaign  is in the failure state.

The total contributions constant method “totalContributions” is a simple method which describes the total number of contributions made to the campaign.

The total contributions by sender method “totalContributionsBySender” is a simple method which describes the total number of contributions made by a single contributor account to the campaign contract.

The contribution data structure “Contribution” is a rudimentary data structure which helps organize contribution data, such as the contribution sender, value contributed and creation date (as a UNIX standard timestamp).
