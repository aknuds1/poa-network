# POA Network

## How-To

In order to set up a test POA Network blockchain, we make use of the
[POA Network Test Setup](https://github.com/aknuds1/poa-test-setup) repository.

First clone it: `git clone git@github.com:aknuds1/poa-test-setup.git`. Then install dependencies
via `npm install` and execute the included script to launch a test network:
`npm run start-test-setup`.

The *start-test-setup* script will basically do the following:

1. Start a master of ceremony node
2. Deploy secondary contracts
3. Generate initial key
4. Start the ceremony dApp
5. Conclude ceremony

## References
* [POA Network Whitepaper](https://github.com/poanetwork/wiki/wiki/POA-Network-Whitepaper)
* [Terraform setup for Azure](https://github.com/poanetwork/deployment-terraform/blob/master/azure)

Mr. Commander in POA Chatbox Telegram channel says to field him any questions about the Terraform
Ansible setup.