The WeiFund platform allows campaigns to register additional cosmetic non-blockchain campaign data, this is data that tightly conforms to the WeiFund [campaign data specification](http://weifund.readthedocs.io/en/latest/specifications/campaign_data_specifications/).

```
import "Owner.sol";

contract CampaignDataRegistryInterface {

/// @notice call `register` to register your campaign with a specified data store
/// @param _campaign the address of the crowdfunding campaign
/// @param _data the data store of that campaign, potentially an ipfs hash
function register(address _campaign, bytes _data) {

/// @notice call `storedDate` to retrieve data specified for a campaign address
/// @param _campaign the address of the crowdfunding campaign
/// @return the data stored in bytes
function storedData(address _campaign) constant returns (bytes dataStored);

event CampaignDataRegistered(address _campaign);
}

contract CampaignDataRegistry is CampaignDataRegistryInterface {

modifier senderIsCampaignOwner(address _campaign) {
if(Owner(_campaign).owner() != msg.sender) {
throw;
}

}

function () {
throw;
}

function register(address _campaign, bytes _data) senderIsCampaignOwner(_campaign) {
data[_campaign] = _data;
CampaignDataRegistered(_campaign);
}

function storedData(address _campaign) constant returns (bytes dataStored) {
return data[_campaign];
}

mapping(address => bytes) data;
}
```

##Contract Overview
The WeiFund campaign data registry allows any campaign owner (i.e. owner()) to specify additional cosmetic campaign data which enhances the campaign listing, viewing, contribution, refund and payout experiences on the WeiFund user interfaces.

The registry will automatically throw a EVM error if any method except “storedData” or “register” is used.
The register has a central registry method where campaign owners can register additional cosmetic campaign data to their campaign. The owners may do this multiple times. Presently, the data registered must be a n IPFS hash that has been properly formatted and converted to base58 hex code. The WeiFund UI will determine the nature of the data registered (i.e. if the data is an IPFS hash). If successful, the “CampaignDataRegistered” event will fire.

The stored data method “storedData” returns the data stored for a specific campaign by the campaign owner.
