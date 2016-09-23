The WeiFund Campaign Registry allows to register your campaign contact address and the address of any additional interface contract, if needed. Each campaign can only be registered once by the owner (owner():(address ownerAccount)) of the campaign. Ensure that you both have access to the owner account of the contract and that you register the campaign from that account. The campaign registry allows you to get the ID of campaigns registered (i.e. using the “idOf(address)” method) as well as the address of a campaign ID (i.e. using the “addressOf(uint256 id”).

```
import "Owner.sol";

contract CampaignRegistryInterface {
function register(address _campaign, address _interface) returns (uint256 campaignID);
function idOf(address _campaign) constant returns (uint256 campaignID);
function interfaceOf(uint256 _campaignID) constant returns (address interface);
function registeredAt(uint256 _campaignID) constant returns (uint256 registered);
function addressOf(uint256 _campaignID) constant returns (address campaign);
function numCampaigns() constant returns (uint256 count);
}

contract CampaignRegistry is CampaignRegistryInterface {
modifier validRegistration(address _campaign) {
// campaign owner is sender
if (Owner(_campaign).owner() != msg.sender) {
throw;
}

// prevent double registrations
if (campaigns.length > 0) {
if (campaigns[ids[_campaign]].addr == _campaign) {
throw;
}
}
_
}

function () {
throw;
}

function register(address _campaign, address _interface) validRegistration(_campaign) returns (uint256 campaignID) {
campaignID = campaigns.length++;
ids[_campaign] = campaignID;
campaigns[campaignID] = Campaign({
addr: _campaign,
interface: _interface,
registered: now
});
CampaignRegistered(_campaign, _interface, campaignID);
}

function idOf(address _campaign) constant returns (uint256 campaignID) {
return ids[_campaign];
}

function interfaceOf(uint256 _campaignID) constant returns (address interface) {
return campaigns[_campaignID].interface;
}

function registeredAt(uint256 _campaignID) constant returns (uint256 registered) {
return campaigns[_campaignID].registered;
}

function addressOf(uint256 _campaignID) constant returns (address campaign) {
return campaigns[_campaignID].addr;
}

function numCampaigns() constant returns (uint256 count) {
return campaigns.length;
}

struct Campaign {
address addr;
address interface;
uint256 registered;
}

mapping(address => uint) public ids;
Campaign[] public campaigns;
event CampaignRegistered(address _campaign, address _interface, uint256 _campaignID);
}
```
##Contract Overview
The WeiFund campaign registry contract is the central store for all campaign contracts listed and accessible on the platform. All campaigns must be registered through this registry before being listed on WeiFund.

The registry immediately throws an error if the fallback function is called (i.e. any time a method that is not in the contract is called).

The contract contains a central modifier to check the validity of a campaign registration (i.e. validRegistration). This checks if the campaign has not already been registered and that the campaign contract owner (i.e. owner()) account is the registration sender (I.e the “msg.sender”).

The contract has a single state changing method (i.e. “register”). This method is used to register campaign contact address and if needed, an interface contract address. Note, the interface contract address is only required if your campaign does not follow the WeiFund campaign contract specification.

The registry has a range of simple constant information retrieval getter methods, such as getting the campaign ID of a campaign address registered “idOf”, the campaign address of a campaign ID registered “addressOf”, the number of campaigns registered “numCampaigns”, the time at which a campaign was registered “registeredAt” and the interface contract address of registered campaign ID, if any “interfaceOf”.
