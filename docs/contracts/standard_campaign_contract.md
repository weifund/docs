The WeiFund Standard Campaign contract template allows anyone to create, deploy and reap the benefits of a crowdfunding campaign that follows the WeiFund contract standard campaign specifications.

```javascript
import "../Campaign.sol";
import "../Owner.sol";

contract StandardCampaign is Owner, Campaign {
enum Stages {
CrowdfundOperational,
CrowdfundFailure,
CrowdfundSuccess
}

modifier atStageOr(uint256 _expectedStage) {
if (now < expiry) {
stage = uint256(Stages.CrowdfundOperational);
} else if(now >= expiry && amountRaised < fundingGoal) {
stage = uint256(Stages.CrowdfundFailure);
} else if(now >= expiry && amountRaised >= fundingGoal) {
stage = uint256(Stages.CrowdfundSuccess);
}

if (stage != _expectedStage) {
throw;
}
_
}

function () {
contributeMsgValue();
}

function contributeMsgValue() atStageOr(uint(Stages.CrowdfundOperational)) public returns (uint256 contributionID) {
contributionID = contributions.length++;
contributions[contributionID] = Contribution({
sender: msg.sender,
value: msg.value,
created: now
});
contributionsBySender[msg.sender].push(contributionID);
amountRaised += msg.value;
ContributionMade(msg.sender);
}

function payoutToBeneficiary() atStageOr(uint(Stages.CrowdfundSuccess)) public returns (uint256 amountClaimed) {
amountClaimed = this.balance;
if (!beneficiary.send(amountClaimed)) {
throw;
}
BeneficiaryPayoutClaimed(beneficiary, amountClaimed);
}

function StandardCampaign(string _name,
uint256 _expiry,
uint256 _fundingGoal,
address _beneficiary,
address _owner) {
name = _name;
expiry = _expiry;
fundingGoal = _fundingGoal;
beneficiary = _beneficiary;
owner = _owner;
}

function totalContributions() public constant returns (uint256 amount) {
return contributions.length;
}

function totalContributionsBySender(address _sender) public constant returns (uint256 amount) {
return contributionsBySender[_sender].length;
}

struct Contribution {
address sender;
uint256 value;
uint256 created;
}

uint256 public stage;
uint256 public fundingGoal;
uint256 public amountRaised;
uint256 public expiry;
address public beneficiary;
Contribution[] public contributions;
mapping(address => uint256[]) public contributionsBySender;

string public name;
string public version = "1.0.0";
string public contributeMethodABI = "contributeMsgValue():(uint256 contributionID)";
string public payoutMethodABI = "payoutToBeneficiary():(uint256 amountClaimed)";
}
```
