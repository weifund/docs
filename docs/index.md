# Welcome to Weifund hi

WeiFund is an open platform for crowdfunding campaigns. You can launch a campaign using one of Weifund’s secure smart contract templates (“Campaign Templates”) that we develop, or you can integrate your own smart contracts to create a custom campaign - the details of that integration are outlined below in this documentation. Weifund is built on Ethereum.

With a strong focus on security and smart contract best practices, Weifund makes it easy to launch a safe campaign that works in the Weifund user interfaces. Vetting systems provide users with assessments of campaign readiness, allowing communities to confidently fund selected campaigns. WeiFund provides both Weifund.io, our campaign portal, and clients that interact with campaigns and which are accessible from IPFS.

##The Portal
The Portal is a fully functional web-dApp where visitors can see and contribute to a curated list of campaigns. Campaign details are listed with a description of their funding goal and expiry. Users are able to contribute to the campaigns that they feel are important. As platform functionality grows, we plan to develop infrastructure for different community-based filters on the portal. You can access the portal at the [Weifund Portal](http://weifund-basic.surge.sh/).

##Clients
It will be possible to download versions of the WeiFund user interfaces (HTML, CSS, and JS) and run it as a client on your local machine. Users can interact with all features of the platform, including creating and contributing to campaigns. Such clients will be available through decentralized file-storage systems like IPFS and require the use of a running Ethereum client.

##Testnet & Livenet
As Campaign Templates are rolled-out, the WeiFund platform will support both the Ethereum (ETH) livenet and testnet. Features will emerge first on the testnet and then once validated may be released to production on the mainnet. The WeiFund portal and client can detect which network you are on and set the contract addresses accordingly. However, please ensure you are on the desired network before proceeding with creating or interacting with any WeiFund contract or listed campaign. We recommend you use and experiment with WeiFund on the Etheruem testnet before publishing your campaign to the livenet on WeiFund.
