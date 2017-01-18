## Create a Campaign

Creating a new campaign is currently a manual process that the WeiFund team performs for our clients. Choose a beneficiary to receive the funds, a goal amount to raise, an optional maximum amount to raise, and how many tokens you'd like the campaign to issue.

A beneficiary is the recipient of funds from a successful campaign on Weifund. Beneficiaries are addresses on Ethereum that represent either an externally owned account controlled by a single private key, or another smart contract that controls access to the collected funds. Funds are typically stored in the campaign smart contracts until the campaign ends.

## Payout

To transfer the funds from a campaign to its beneficiary, a payout transaction must be sent to the campaign smart contract system. Only the owner of the beneficiary account can withdraw the campaign funds.

The beneficiary account is typically a multisignature contract. Generate the
payout transaction, obtain the required signatures, and send the
transaction to the network.

## Handling the Unexpected

If something has gone wrong with your campaign, the beneficiary can choose to withdraw all funds from the campaign contract at any time by sending a payout
transaction from the beneficiary account.
