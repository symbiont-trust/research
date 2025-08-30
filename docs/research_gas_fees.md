# Research Gas Fees

## Allow No Gas Fees for end users using a Server

We create a Server which has a private key to update state on a solidity contract.  The Server has 
a database of users.  A user logs in to the server by signing some text and sending it to the server 
to gets a JWT token.  The JWT token is used to call the server to get it to update state on the 
smart solidity contract.  Every time the server updates state it gets charged.  Therefore it can use
rate limiting on the users to prevent it spending its budget for gas fees too fast.

The server has its associated Ethereum Address so we need to charge up the address with crypto 
so the server can spend crypto on gas fees updating state on the smart contract.

The server now pays gas fees updating state instead of the end users paying gas fees.

This Server requires us to write the server code and incur costs hosting it on the cloud.

The Alternative to hosting our server is to use the ERC 4227 functionality on Ethereum style chains.


## Allow no Gas Fees for end users using ERC 4227 functionality

We want the user to trigger updating state on a contract of their liking without paying gas fees. 
For the purpose of this explanation we call that contract the State Contract.

In this design we do not need to deploy a server. However we need to talk to a Server called a 
Bundler.  We sign an instruction and some state we want updated in the State Contrac and we pass it 
to the Bundler. The Bundler triggers a smart contract update to the state contract. 

The Bundler pays gas fees but will later get a refund which is a bit more than what they spent. 
That bit extra is their motivation to participate.

The Bundler talks to a Smart Contract called an EntryPoint.  The EntryPoint talks to a 
"Smart Account" contract which allows an end user to spend or receive crypto.  The end user can use 
a wallet that supports Smart Accounts to authorise the smart account to transfer funds.  
For example metamask can be upgraded to a work with a Smart Account.

The EntryPoint also optionally talks to a PayMaster smart contract the latter of which has an 
address it can use for paying.  The idea is that either the Smart Account or the PayMaster pay gas 
to update state on the State Contract.

When we do not want the end user to pay gas fees we get the PayMaster to pay the gas fees instead. 
The PayMaster can be topped up with crypto with funds we get from else where.  For example maybe 
advert revenue can top the PayMaster up with funds so the PayMaster can pay for user gas fees to 
update state on the State Contract.

The EntryPoint can get the PayMaster to pay both for the refund to the Bundler and the cost of gas 
fees for updating state on the State Contract. 

