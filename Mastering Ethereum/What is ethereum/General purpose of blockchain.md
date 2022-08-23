## Bitcoin
<p>The original blockchain, namely Bitcoin’s blockchain, tracks the state of units of bitcoin and their ownership. You can think of Bitcoin as a distributed consensus _state machine_, where transactions cause a global _state transition_, altering the ownership of coins. The state transitions are constrained by the rules of consensus, allowing all participants to (eventually) converge on a common (consensus) state of the system, after several blocks are mined.</p>

## Ethereum
<p>Ethereum is also a distributed state machine. But instead of tracking only the state of currency ownership, Ethereum tracks the state transitions of a general-purpose data store, i.e., a store that can hold any data expressible as a _key–value tuple_. A key–value data store holds arbitrary values, each referenced by some key; for example, the value "Mastering Ethereum" referenced by the key "Book Title". In some ways, this serves the same purpose as the data storage model of _Random Access Memory_ (RAM) used by most general-purpose computers. Ethereum has memory that stores both code and data, and it uses the Ethereum blockchain to track how this memory changes over time. Like a general-purpose stored-program computer, Ethereum can load code into its state machine and _run_ that code, storing the resulting state changes in its blockchain. Two of the critical differences from most general-purpose computers are that Ethereum state changes are governed by the rules of consensus and the state is distributed globally. Ethereum answers the question: "What if we could track any arbitrary state and program the state machine to create a world-wide computer operating under consensus?"</p>


### Ethereum specification

__P2P Network__
<p>Ethereum runs on the <i>Ethereum main network</i>, which is addressable on TCP port 30303, and runs a protocol called <b>ÐΞVp2p</b>. </p>

**Consensus rules**
<p>Ethereum’s consensus rules are defined in the reference specification, the Yellow Paper </p>

**Transactions**
<p>Ethereum transactions are network messages that include (among other things) a sender, recipient, value, and data payload.</p>

**State machine**
<p>Ethereum state transitions are processed by the <b>Ethereum Virtual Machine</b> (EVM), a stack-based virtual machine that executes <i>bytecode</i> (machine-language instructions). EVM programs, called "smart contracts," are written in high-level languages (e.g., Solidity) and compiled to bytecode for execution on the EVM.</p>

__Data structures__
<p>Ethereum’s state is stored locally on each node as a <i>database</i> (usually Google’s LevelDB), which contains the transactions and system state in a serialized hashed data structure called a <i>Merkle Patricia Tree</i>.</p>

__Consensus algorithm__
<p>Ethereum uses Bitcoin’s consensus model, Nakamoto Consensus, which uses sequential single-signature blocks, weighted in importance by PoW to determine the longest chain and therefore the current state. However, there are plans to move to a PoS weighted voting system, codenamed <i>Casper</i>, in the near future.</p>

__Economic security__
<p>Ethereum currently uses a PoW algorithm called <i>Ethash</i>, but this will eventually be dropped with the move to PoS at some point in the future.</p>

__Clients__
<p>Ethereum has several interoperable implementations of the client software, the most prominent of which are <b>Go-Ethereum</b> (<b>Geth</b>) and <b>Parity</b>.</p>

__If u need more [info](https://github.com/ethereumbook/ethereumbook/blob/develop/01what-is.asciidoc#references) about each item__