# POA Instructions
To launch POA Network we use Parity client with a set of validators stored in the smart contract called PoaNetworkConsensus.sol: https://github.com/poanetwork/poa-network-consensus-contracts/blob/master/contracts/PoaNetworkConsensus.sol

The address of this contract must be registered in spec.json that Parity uses: https://wiki.parity.io/Validator-Set.html (see Non-reporting contract section). Below I gave some information about spec.json a little.

Parity must be launched in the following manner:

parity --config ./config.toml

where config.toml is the configuration file that contains a path to spec.json and other necessary options.

For example, you can see how to write toml-file in our consensus repo readme: https://github.com/poanetwork/poa-network-consensus-contracts/blob/master/scripts/README.md

Generally, TOML for Parity is described in Parity's wiki: https://wiki.parity.io/Configuring-Parity-Ethereum.html

The current spec.json for our Core network can be viewed here: https://github.com/poanetwork/poa-chain-spec/blob/core/spec.json - as we can see, the address of PoaNetworkConsensus contract is 0xa105Db0e6671C7B5f4f350ff1Af6460E6C696e71 currently (see https://github.com/poanetwork/poa-chain-spec/blob/core/spec.json#L19), but its first version had the address 0x8bf38d4764929064f2d4d3a56520a76ab3df415b: https://github.com/poanetwork/poa-chain-spec/blob/core/spec.json#L106

So, when we launch a network from scratch, we should firstly compile PoaNetworkConsensus.sol and add its bytecode into spec.json: https://github.com/poanetwork/poa-chain-spec/blob/core/spec.json#L108 - the bytecode should contain the address of Master of Ceremony in the constructor, as it's described here: https://github.com/poanetwork/poa-network-consensus-contracts#start-poa-network

Then we can add other validators to PoaNetworkConsensus through so-called Ceremony process: https://github.com/poanetwork/wiki/wiki/Governance-Overview

When we want to change the code of PoaNetworkConsensus for some reason, we should make a hard fork adding its new address in spec.json. For example, we made the first hard fork on block number 772000: https://github.com/poanetwork/poa-chain-spec/blob/core/spec.json#L15-L17

We also have other smart contracts that are bound with PoaNetworkConsensus.sol and allow to change the set of validators with votings. They're all located in this repo: https://github.com/poanetwork/poa-network-consensus-contracts/tree/master/contracts

Here is a short description of each consensus smart contract:
- BallotStorage.sol is used to store voting thresholds and some keys checking logic.
- KeysManager.sol contains the keys of each validator (mining key, voting key, and payout key).
- ProxyStorage.sol keeps all addresses of all contracts and allows to change their implementation with votings that are created with VotingToChangeProxyAddress contract.
- RewardByBlock.sol is used to calculate rewards for validators: https://wiki.parity.io/Block-Reward-Contract.html
- ValidatorMetadata.sol keeps name, address, and license info for each validator.
- VotingToChangeKeys.sol allows adding/removing/changing validators and their keys.
- VotingToChangeMinThreshold.sol is used to create votings for changing the thresholds stored in BallotsStorage contract.
- VotingToChangeProxyAddress.sol allows to create votings for changing implementation of other contracts (since they are upgradable).
- VotingToManageEmissionFunds.sol is used to create votings for manage increased emission supply in our network: https://github.com/poanetwork/RFC/issues/14

You can see our sequence diagrams showing how consensus contracts are bound and interact with each other: https://github.com/poanetwork/wiki/wiki/Ballots-Overview.-Life-cycle-and-limits

We also have a useful open source tool to launch a private POA network and to deploy all the consensus contracts from scratch: https://github.com/poanetwork/poa-test-setup - it can help much to clearly understand the process of launching and deployment, i.e. how to make toml, spec.json, and in which order the consensus contracts should be deployed. That tool repeats the steps described in https://github.com/poanetwork/wiki/wiki/Master-of-Ceremony-Setup

I hope this information helped you a bit, but if you still have some questions, don't hesitate to ask.