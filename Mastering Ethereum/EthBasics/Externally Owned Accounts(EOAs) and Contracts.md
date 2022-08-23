The type of account you created in the MetaMask wallet is called an _externally owned account_ (EOA). Externally owned accounts are those that have a private key; having the private key means control over access to funds or contracts. Now, you’re probably guessing there is another type of account. That other type of account is a _contract account_. A contract account has smart contract code, which a simple EOA can’t have. Furthermore, a contract account does not have a private key. Instead, it is owned (and controlled) by the logic of its smart contract code: the software program recorded on the Ethereum blockchain at the contract account’s creation and executed by the EVM.

Contracts have addresses, just like EOAs. Contracts can also send and receive ether, just like EOAs. However, when a transaction destination is a contract address, it causes that contract to _run_ in the EVM, using the transaction, and the transaction’s data, as its input. In addition to ether, transactions can contain _data_ indicating which specific function in the contract to run and what parameters to pass to that function. In this way, transactions can _call_ functions within contracts.

Note that because a contract account does not have a private key, it cannot _initiate_ a transaction. Only EOAs can initiate transactions, but contracts can _react_ to transactions by calling other contracts, building complex execution paths. One typical use of this is an EOA sending a request transaction to a multisignature smart contract wallet to send some ETH on to another address. A typical DApp programming pattern is to have Contract A calling Contract B in order to maintain a shared state across users of Contract A.

In the next few sections, we will write our first contract. You will then learn how to create, fund, and use that contract with your MetaMask wallet and test ether on the Ropsten test network.