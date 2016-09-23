In order to be a WeiFund compliant smart contract system, campaigns’ contracts must follow the WeiFund Contract Interface. This does not ensure the campaign is in any way safe, it only ensures the campaign has enough valid blockchain interfacing to be listed on the WeiFund platform.

Custom campaign smart contract systems do not need to implement the Contract Interface directly. Instead, they can create a contract that maps their smart contract system to the Contract Interface. If that is the approach taken, custom campaign creators only need to ensure the ‘owner()’ property is implemented in their smart contract system.

Here is the WeiFund Contract Interface Version 1:
[Github - Weifund Contract Interface v1](https://github.com/weifund/weifund-contracts/blob/master/contracts/Campaign.sol)

**Examples** <br/>

- Campaign Specification being implemented directly is our first Campaign Template, the [Standard Campaign](https://github.com/weifund/weifund-contracts/blob/master/contracts/StandardCampaign.sol)

- To see an example of this second, indirect approach, you can view the SingularDTV campaign smart contract system [here]( https://github.com/ConsenSys/singulardtv-contracts/blob/master/contracts/SingularDTVWeifund.sol).

In the rest of this section, we examine the parts of the Contract Interface in more detail.

##owner():
Each campaign is required to have an “owner” property. This is the bare minimum requirement for registering your campaign contract on the WeiFund campaign and campaign data registries.

**Required Return Type** <br/>
address (a standard Ethereum address)

**Technical Description** <br/>
A constant method with a single address return output that describes the owner and operator Ethereum standard account address of the campaign. This should be either an Ethereum vanilla account or a proxy contract which can forward dynamic transactions.

**Example** <br/>
0x3bf6e47517dc9abc4559597ba4c020c07c1c892c

##amountRaised():
The total amount of Ether the campaign has raised. Note, this should be a data store that does not change even after the campaign has been paid out. Please do not use “this.balance” directly for this method, as it will set to zero on payout, and potentially affect refund or payout functionality on the WeiFund interface.

**Required Return Type** <br/>
uint256 (unsigned integer 256 bit)

**Technical Description** <br/>
A constant method with a single uint256 return output that describes the amount raised in wei denomination (i.e. the base Ether currency denomination)

**Example** <br/>
313500000000

##fundingGoal():
The total funding goal of a campaign. This is the total amount of Ether required to be raised before the campaign expiry in order for the campaign to be a success.

**Required Return Type** <br/>
uint256 (unsigned integer 256 bit)

**Technical Description** <br/>
A constant method with a single uint256 return output that describes the funding goal in wei denomination (i.e. the base Ether currency denomination)

**Example** <br/>
313500000000

##beneficiary():
This will describe the campaigns beneficiary account. If the campaign is a success (i.e. the funding goal was reached before the expiry) all funds raised in the campaign contract should be sent to this account address.

**Required Return Type** <br/>
address (Ethereum standard account address)

**Technical Description** <br/>
A constant method with a single address return output that describes the campaign beneficiary account Ethereum address where funds will be sent to if the campaign is a success.

**Example** <br/>
0x3bf6e47517dc9abc4559597ba4c020c07c1c892c

##expiry():
The campaign expiry states when campaign contribution intake is officially over and when campaign refunds (if the campaign is a failure) or campaign payout (if the campaign is a success) begins. The expiry is set as a UNIX standard timestamp.

**Required Return Type** <br/>
uint256 (unsigned integer 256 bit)

**Technical Description** <br/>
A constant method with a single uint256 return output that describes the campaign expiry in UNIX timestamp format.

**Example** <br/>
999830290 [replace with better example]

##name():
The campaign name humanizes the campaign contract so that contributors and auditors can get a sense of what the campaign registered is.

**Required Return Type** <br/>
string (a string with a length less than 100 characters)

**Technical Description** <br/>
A constant method with a single string return output that describes the campaign name.

**Example** <br/>
Nick's Crowdfunding Campaign

##version():
A WeiFund standard version marking returned as a string which states what contract interface version the campaign follows.

**Required Return Type** <br/>
string (a string with a length less than 10 characters)

**Technical Description** <br/>
A constant method with a single string return output that describes the campaign WeiFund version specification.

**Example** <br/>
0.1.0

##contributeMethodABI():
The campaign contribution method ABI description, that allows the WeiFund interface to provide specific contribution user experiences for the campaign.

**Required Return Type** <br/>
string (a single string)

**Technical Description** <br/>
A constant method with a single string return output that describes the campaigns contribution method, in Solidity standard method ABI format. This string must have no imperfections and be technically precise to the contribution method in the campaign contract. In order to ensure you have the correct information, please deploy your contracts on the WeiFund testnet platform.

**Currently Supported ABIs** <br/>
contributeMsgValue():(uint256 contributionID)
[This section needs to be updated]

##payoutMethodABI():
The campaign payout method ABI description, that allows the WeiFund interface to provide payout systems for the campaign.

**Required Return Type** <br/>
string (a single string)

**Technical Description** <br/>
A constant method with a single string return output that describes the campaigns contribution method in Solidity standard method ABI format. This string must have no imperfections and be technically precise and accurate to the payout method in the campaign contract. In order to ensure you have the correct information, please deploy your contracts on the WeiFund testnet platform. This will allow you to test the and ensure that the method details provided are correct and work with the WeiFund platform.

**Example** <br/>
payoutToBeneficiary():(uint256 amountClaimed)

##refundMethodABI():
The campaign refund method ABI description, that allows the WeiFund interface to provide a refund system for the campaign.

**Required Return Type** <br/>
string (a single string)

**Technical Description** <br/>
A constant method with a single string return output that describes the campaigns refund method in Solidity standard method ABI format. This string must have no imperfections and be technically precise and accurate to the refund method in the campaign contract. In order to ensure you have the correct information, please deploy your contracts on the WeiFund testnet platform. This will allow you to test the and ensure that the method details provided are correct and work with the WeiFund platform.
