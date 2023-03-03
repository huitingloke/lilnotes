# [QUICKNOTES] Ethereum Official Documentation

[Link](https://ethereum.org/en/developers/docs/)

# Foundational Topics

## Intro to Ethereum

- Node: computers in the network of a blockchain
    - Propagate information about EVM state and new changes — can also request execution of code from here
- ETH uses “proof of stake” — highest “weightage” of the bet wins the validity check
- Blockchain and its vibe
    - Nonce
        
        Coined for one occasion
        
    - Mining (for ETH) — keep matching Nonce with the data inside until it reaches 4 “0”s to start with
    - If you change the nonce/data of a block that occurs previously, it will affect all the blocks after that because their hashes won’t start with the 4 0’s as it’s determinant on their previous connection too
    - Distributed blockchain
        - If a blockchain has a result that is not the majority, it is bad blockchain (then it’s wrong!)
        - To check, you only need to check the hash of the most recent one, to be honest
    - Token x Coinbase
        
        ![Untitled](%5BQUICKNOTES%5D%20Ethereum%20Official%20Documentation%2003f7dc4a94634a3fa83e7d5f363b08ed/Untitled.png)
        
        - Only remembers transaction movement, so you must refer to a balance

### What is Ethereum?

- Ethereum Virtual Machine which does computational states in one way that everyone on the network agrees on
- Ether: native cryptocurrency — anyone who requests something on EVM needs a bounty to incentivize another computer to calculate it
- Smart contracts: reusable scripts on EVM that let you run programs (aka bending machine)
    - Also called Decentralized apps (dApps)
- Transaction request: request for code execution
- Transaction: fulfilled request and associated change in EVM state
- Blocks: list of transactions

## Intro to Ether

- The cryptocurrency
- EVM can only support so many transactions at a time — therefore, must pay gas fees to use it
- Wei — smallest denomination of Ether (10^-18 Ether, technical implementations)
    - Gwei — 10^-9 Ether, human readable gas fee
- Ether can be used to pay gas fees if the recipient address is a smart contract to begin the execution

## Intro to dApps

- Traits
    - Decentralized
    - Deterministic
    - Turing complete (can perform any action given the required resources)
    - Isolated — happens in Ethereum Virtual Machine — if buggy, won’t hamper normal blockchain function
- Decentralized app: combines smart contract and a frontend user interface
- Backend runs on a decentralized peer-to-peer network
- Frontend can be written on any frontend supported language and can be hosted on decentralized storage e.g. IPFS
- Smart contract: Dapp’s backend — once deployed, cannot change

## Web2 v Web3

- !!! Nothing is entirely centralized or decentralized !!! It’s really a spectrum
- Web2: companies control the data you have
- Web3: decentralized app that runs on the blockchain
- The good of Web3
    - No permission required
    - No one can deny service access
    - Payments are built in via ETH
    - Solidity is turing complete
- The bad of Web3
    - Scalability — changes need to be propogated throughout the network
    - UX is not familiar
    - Accessibility — lack of integration in modern web browsers
    - Cost
- Screenshot of centralized v decentralized
    
    ![Untitled](%5BQUICKNOTES%5D%20Ethereum%20Official%20Documentation%2003f7dc4a94634a3fa83e7d5f363b08ed/Untitled%201.png)
    

## Accounts

- Two types:
    - Externally owned accounts (EOA) — controlled by anyone with the private keys
        - 64 hex characters, can be encrypted with a password → public key generated from algorithm
        - Free, initiate transactions, transactions between these types can only be ETH/token transfers, made up by 2 types of keys (public and private)
        - Diagram
            
            ![Untitled](%5BQUICKNOTES%5D%20Ethereum%20Official%20Documentation%2003f7dc4a94634a3fa83e7d5f363b08ed/Untitled%202.png)
            
        - You hold the keys to your own account that verify your true identify
    - Contract account — smart contract, controlled by code
        - Making contract has cost, can only send transactions, external transactions can trigger codes that execute different actions (e.g. transferring tokens, even making a new contract), no private keys and are controlled by logic
        - 42 character hexadecimal address
- Hold, receive, send ETH tokens and interact with deployed smart contracts
- Four fields:
    - `nonce`: number of transactions sent from externally-owned account/number of contracts made by contract account
        - One transaction per nonce per account
    - `balance`
    - `codeHash`: code of an account on EVM — code that gets executed to play with a code fragment if the account is called
    - `storageRoot`: 256bit hash that has storage contents of the account
- Validator keys: BLS keys used to identify validators — reduce bandwidth required for network to come to consensus
- Account = keypair for user owned ETH account
    - Wallet is something that lets you interact with your account

## Transactions

- Transaction: action from externally owned account — needs gas fees
    - Needed for all smart contract interaction
- Stuff it needs
    
    ![Screenshot 2023-02-25 at 3.04.25 PM.png](%5BQUICKNOTES%5D%20Ethereum%20Official%20Documentation%2003f7dc4a94634a3fa83e7d5f363b08ed/Screenshot_2023-02-25_at_3.04.25_PM.png)
    
    ![Screenshot 2023-02-25 at 3.04.39 PM.png](%5BQUICKNOTES%5D%20Ethereum%20Official%20Documentation%2003f7dc4a94634a3fa83e7d5f363b08ed/Screenshot_2023-02-25_at_3.04.39_PM.png)
    
- Needs to be signed
    - `raw` : recursive length prefix (RLP) form
    - `tx` : JSON form
- Data
    - TLDR: read docs for more but I will try to break it down before I break myself down
    - Transactions have a hash that translate to a different form/language and a special selector so you know what type of encoding/decoding it’s using e..g some are 000000000 at the front and you’re like “ohhh so it’s this type!! so cool!!!”
- Types
    - Regular: one account to another
    - Contract deployment: transaction without a “to” address; the data is just used for the contract code
        - Executing a contract: interacts with smart contract (”to” assigned to smart contract address)
- Interpreted how?
    - TransactionType || TransactionPayload
        - Type: number between 0 to 0x7f
        - Payload: byte array defined by transaction type
    - [Read more nerd](https://eips.ethereum.org/EIPS/eip-2718)

## Blocks

- One oversized list of transaction data
- Blocks are only created and committed once every 12 seconds
- Proof of stake
    - 32 ETH must be staked to validate the blocks
    - Randomly select validator → bundle transactions, execute, determine new “state of affairs” → pass it around to other validators
    - Other validators also re-execute transactions → if block valid, add to personal DB
    - If blocks conflict, highest “stake” money wins =)
- What’s inside nerd?
    
    ![Screenshot 2023-02-25 at 3.42.46 PM.png](%5BQUICKNOTES%5D%20Ethereum%20Official%20Documentation%2003f7dc4a94634a3fa83e7d5f363b08ed/Screenshot_2023-02-25_at_3.42.46_PM.png)
    
    - Inside body
        
        ![Screenshot 2023-02-25 at 3.42.57 PM.png](%5BQUICKNOTES%5D%20Ethereum%20Official%20Documentation%2003f7dc4a94634a3fa83e7d5f363b08ed/Screenshot_2023-02-25_at_3.42.57_PM.png)
        
    - And that’s the lowest level we are going, there are like nested data in data that I ain’t typing out here, so go to [this section of the docs](https://ethereum.org/en/developers/docs/blocks/) and find it out for yourself
    - Okay wait, `execution_payload` is somewhat important
        - Updates the global state and checks if it matches `state_root` field (THIS IS FOR `execution_payload_header`)
            
            ![Screenshot 2023-02-25 at 3.46.23 PM.png](%5BQUICKNOTES%5D%20Ethereum%20Official%20Documentation%2003f7dc4a94634a3fa83e7d5f363b08ed/Screenshot_2023-02-25_at_3.46.23_PM.png)
            
        - `execution_payload` is the same, but instead of `transactions_root`, you get `transactions` , which is a healthy list of all the transactions about to be executed
- Block time: difference in time between the manifestation of different blocks
- Block size: target — 15 million gas, cap — 30 million gas

### Any questions?

- When I looked at the block time field, I saw it consistently go lower, even before the swap from proof of work to proof of stake. Is there a particular reason for this? Did the servers get faster? Did less people start using it? Or more people, leading to more computers and therefore more server power? (Is that how it even works?)

## Ethereum Virtual Machine (EVM)

- Ethereum is a “state machine” — can change based on an arbitrary set of rules and can execute machine code
    - ETH has one “canon” state — EVM computes the rules for what can be computed as a new valid state from block to block
- One big big Merkle Tree
    
    ![Untitled](%5BQUICKNOTES%5D%20Ethereum%20Official%20Documentation%2003f7dc4a94634a3fa83e7d5f363b08ed/Untitled%203.png)
    
- Deterministic
- Two transactions it has and will support
    - result in message calls
    - result in contract creation (containing smart contract bytecode — if another contract calls this, it will execute the bytecode)
- Contracts also contain a storage tree
- Opcodes will be called by the executed contracts — perform standard stack operations (stack being the LIFO thingy) and some blockchainy stuff — `ADDRESS` , `BALANCE` , `BLOCKHASH` etc
    
    ![Untitled](%5BQUICKNOTES%5D%20Ethereum%20Official%20Documentation%2003f7dc4a94634a3fa83e7d5f363b08ed/Untitled%204.png)
    
- All EVM implementations must adhere to stuff in the Ethereum Yellow paper
    - https://github.com/ethereumjs/ethereumjs-monorepo
    - https://github.com/ethereum/py-evm

### Opcodes

[https://ethereum.org/en/developers/docs/evm/opcodes/](https://ethereum.org/en/developers/docs/evm/opcodes/)

## Gas

- Unit that measures the amount of computational effort required to execute specific operations on the Eth network
- Fee required to execute Ethereum transaction
- Denoted in *****gwei***** — 10^-9 ETH
- Calculation example
    - Gas limit: 21,000 units
    - Base fee (set by protocol): 10 gwei
    - Tip (priority fee): 2 gwei
    - Max fee: 1.5 ETH
    - Formula: `units of gas used * (base fee + priority fee)`
    - `refund = max fee - (base fee + priority fee)`
- ****************Tatonnement —* leads to equilibrium block size of 15 million
    - If block size > target block size — protocol increases base fee for next block and vice versa if block size < target block size
- Base fee — increases and decreases based on the included gas (you know, the 30 million thing) — since it grows exponentially, encouraged to lower network traffic by other users until it hits equilibrium
- Priority fee — tips
- Calculating fees made easier — wallet providers would set recommended fees (improve UX babyyy) — base fee + recommended priority fee
- Gas not used is returned to the user
- EIP-1559 — what Ethereum uses today
    - VERY good video detailing what this is
    - TLDR:
        - Old version — fees were determined based on who bid the most
        - New version —  fees determined by a base price that fluctuates proportional to how much demand the previous block had, base fee is burned and miners are given a tip instead to allow some transactions to have a “priority queue”
    
    [https://youtu.be/MGemhK9t44Q](https://youtu.be/MGemhK9t44Q)
    
- Exist to prevent spam, hostile/accidental infinite loops, and code wastage
- Gas limit: how much gas you’re willing to spend
    - Standard: 21,000 units
    - If you put too little on a transaction, e.g. 1000, it will try to compute and fail but since the “work” was already done by the miner, you won’t get your 1k back
    - Layer 2 scaling — getting your transaction compiled on a different server, which is then compiled on the main server afterwards
- [Gastracker](https://etherscan.io/gastracker)

## Nodes and clients

- Node: instance of Eth software connected to other computers also running the software — forms a network
- Client: Implementation of Eth that verifies data against the protocol rules and keeps the network secure
- Two parts to Ethereum:
    - Execution client: listens to new transactions in the network, executes in EVM , holds latest state and database of all current ETH data
    - Consensus client (beacon node): implements proof of stake — enables network to achieve agreement based on validated data from executed client
- Client diversity: in order for the network to be healthy and secure, it must be sufficiently decentralized through a diversity of software clients
- Node types
    - Light — only downloads block headers, can verify data with a full node
    - Full — stores full blockchain data, full verification, all states can be derived, serves network and provides data on request
    - Archive — stores things in full nodes and builds archive of historical states, very very very big
- Why run node? → can directly, privately, trustlessly use Ethereum
    - Node verifies rules for you, can use dApps more securely and privately, yadda yadda, but can also directly stake ETH to secure the network and earn rewards…
    - Node makes Ethereum stronger and less susceptible to attacks
    - Emmett says don’t run the node because it takes up a lot of time and resources and you will regret and break down crying (embellishment)
- Synchronization nodes: syncing with latest network state
    - Execution layer sync modes:
        - Full sync: all blocks downloaded and executes every block from genesis — incrementally generates state of blockchain
        - Fast sync: downloads all blocks, downloads state, verifies against headers
        - Light sync: verifies some randomly — only syncs tip of the chain from trusted checkpoint — doesn’t yet work with POS Ethereum
        - Snap sync: uses dynamic snapshots served by peers to retrieve account and storage data without downloading intermediate Merkle tree nodes then reconstructs it locally
    - Consensus layer sync nodes:
        - Optimistic sync: EE can import beacon blocks without full verification and start syncing them
        - Checkpoint sync (aka weak subjectivity sync): node connects to remote service and downloads recent finalized states then continues verifying data (trusts third parties)
    - Note to self: There was other stuff about the nodes but they were so boring that I didn’t read it, basically its setting up a node and some further details

## Networks

- Different ETH environments you can access for development, testing, or production
- Don’t reuse your mainnet accounts on the testnet and vice versa…
- Types
    - Public — can be accessed by anyone, is the public blockchain and is determined by consensus of peers
        - Ethereum mainnet — actual value. Main main main one
        - Ethereum testnet — testing stuff in a production environment before deploying to mainnet
            - Some even have a testing proof of stake consensus mechanism!
            - Get fake ETH from faucets
            - Can try using Sepolia — kinda new so it’s got fewer data to deal with :3
        - Layer 2 testnets — separate blockchain that extends Eth and inherits its security guarantees
            - Arbitrum Goerli
            - Optimistic Goerli
    - Private — if nodes are not connected to a public network
        - Development: running privately to check if it works
        - Consortium: consensus process controlled by pre-defined set of trusted nodes e.g. private network of academic institutions (almost like a private intranet)

## Consensus mechanisms

- Consensus: general agreement has been reached — at least 66% of the nodes agree
- Consensus mechanism: entire stack of protocols, incentives, and ideas that allow a network of nodes to agree on the state of a blockchain
    - The idea is that majority always wins
- Types
    - Proof of work based
        - Block creation — miners compete to create new block and winner is rewarded with ETH
        - Security: need 51% to defraud chain
    - Proof of stake based
        - Block creation — validators create blocks — one validator randomly selected to propose → requests transactions and bundles it up → sends to other nodes in Eth network → rewarded in ETH
            - If there is a conflict, algo picks the block that forms with the greatest stake
        - Security — to control the chain, you’d need to destroy a lot of ETH
- Sybil resistance and chain selection
    - Sybil resistance mechanism: way to decide who adds the latest block
    - Sybil resistance: measures how a protocol fares against a Sybil attack (when one user pretends to be many)
    - Chain selection rule: deciding which chain is correct
        - Ethereum uses “longest chain” — and measures its weight as well (sum of vlaidator votes, weighted by validator staked-ether balances)

# Ethereum Stack

## Intro to the stack

- Level 1: EVM — handles all transaction processing on Ethereum network
    - Creates level of abstraction between code and node
    - Runs on thousands of nodes around the world
    - Uses opcode instructions to execute specific tasks — turing complete
- Level 2: smart conracts — written using programming languages that compile to opcodes
    - Opcode: low-level machine instructions
    - Are open source libraries/APIs
    - The vibe here is reuse, reduce, recycle
- Level 3: Ethereum nodes — allows you to read blockchain data/send transactions to network (e,g, transferring ETH and executing functions of smart contract)
    - Are computers running Ethereum clients that verify all transactions
    - Store the state of the blockchain and all collectively make changes
- Level 4: Ethereum client APIs — convenience libraries to communicate with blockchain
    - Can choose to just npm install a JS API or use can implement functionality server-side using Python/Java API
    - Less complex because you don’t have to interact with the node directly UWU
- Level 5: End user applications — web and mobile apps
- [Good article](https://www.preethikasireddy.com/post/the-architecture-of-a-web-3-0-application) that sums everything up as it blows your mind

## Smart contracts — and all of the vibes there

- TLDR: an automatically rule-defined enforcement agreement
    - Kind of like a digital vending machine — only gives you your stuff if all the requirements are met
- Program that runs on Ethereum blockchain — collection of code (functions) and data (state) that resides at a specific address on the blockchain
- An account you can interact with but not controlled by a user, can define rules and automatically enforce them via code, cannot be deleted, interactions are also irreversible
- Benefits
    - Will give a predictable result
    - Public
    - Pseudoanonymous so you have privacy
    - Visible terms
    - Permissionless
    - Composability — can use all the available APIs for it as well
- Limitations
    - Cannot send HTTP requests — no information about real world events (ensure consensus isn’t jeopardized)
        - Workaround with oracles
    - Max size of 24kb — workaround with The Diamond Pattern
        - Makes it possible to implement a lot of contract functionality that is compartmented into separate areas of functionality, but still using the same Ethereum address
            - Okay, basically, Diamond pattern is having like one main logic contract and multiple *****satellite contracts***** that the main one can direct data to, which technically has no max storage so you’re a winner
        - Can vibe more with [this link](https://eips.ethereum.org/EIPS/eip-2535) — warning: exceedingly long winded and you have a skill issue
- Can use `Solidity` or `Vyper` to write smart contracts but you will actually need to, unpog, compile them before they execute

## Languages

- Examples
    - Solidity (superior because I use it)
        - Object oriented, high level, curly braces, supports inheritance, libraries, and complex user-defined types
        - [Cheatsheet](https://reference.auditless.com/cheatsheet/)
    - Vyper (WAIT WAIT IT’S LIKE PYTHON I INVESTED TIME INTO THE WRONG THING)
        - Pythonic, strong typing, small and understandable compiler code, efficient bytecode generation, less features than Solidity
        - Does not support — modifiers, inheritance, inline assembly, function overloading, operator overloading, recursive calling, infinite-length loops, binary fixed points I LOVE THIS LANGUAGE
    - Yul (for experienced people)
        - Intermediate language, supports Ewasm and EVM, good target for high level optimisation for this
        - Yul+ — low-level, highly efficient extension, made for optimistic rollup (moving computation and state storage off chain), basically Yul DLC lah
    - Fe (under development)
        - Statically typed for EVM, inspired by Py and Rust, aimed to be easy to learn I’M COMING BABY

## Anatomy

- Contract data must be assigned to a location (storage or memory)

### Data

- Storage
    - Persistent data, represented by state variables, stored on blockchain — MUST DECLARE TYPE
        
        ```solidity
        contract SimpleStorage {
            uint storedData; // State variable
            // ...
        }
        ```
        
    - Types (those that I don’t know):
        - `address` : holds Ethereum address — returns hexadecimal notation with a leading 0x
        - `fixed` and `ufixed` : e.g. `fixed8x18`
            - Method of representing fractional (non-integer) numbers by storing a fixed number of digits of their fractional part
            - I haven’t felt this much pain since I had to grind Just Dance 2018 Despacito with Kayley to get 5 stars but it had to be a duet and I danced with her as the guy because she didn’t want to be the guy for like an hour straight
        - `enums` : user-defined data types that restrict the variable to have only one of the predefined values
        - Just check the [documentation](https://docs.soliditylang.org/en/latest/types.html#value-types) for the rest
- Memory
    - Values stored only for lifetime of contract function’s execution
- Environment variables
    - Special global variables e.g. `block.timestamp` which gives a `uint256` current block epoch timestamp

### Functions

- `internal` — do not create EVM calls and only accessible within current contract
- `external` — create an EVM call, can be called from other contracts and transactions
    - Cannot be called internally
- `public`— can be called internally and externally
- `private` — only visible for the contract they are derived in

```solidity
function update_name(string value) public {
    dapp_name = value;
}
//exmaple
```

- `view` — doesn’t modify state of contract’s data e.g. getter functions
    - Apparently `selfdestruct` is not considered modifying a contract’s state

```solidity
function balanceOf(address _owner) public view returns (uint256 _balance) {
    return ownerPizzaCount[_owner];
}
```

- `constructor` — executed once when contract is first deployed
- `address.send()` — can send ETH to other accounts
- Making your own
    - Requirements:
        - Parameter variable and type (if accepts parameter)
        - Declaration of internal/external
        - Declaration of pure/view/payable
        - Returns type (if value gets returned)
    
    ```solidity
    contract ExampleDapp {
        string dapp_name; // state variable
    
        // Called when the contract is deployed and initializes the value
        constructor() public {
            dapp_name = "My Example dapp";
        }
    
        // Get Function
        function read_name() public view returns(string) {
            return dapp_name;
        }
    
        // Set Function
        function update_name(string value) public {
            dapp_name = value;
        }
    }
    ```
    

### Events and logs

- Communicate with contract from front end and other apps
- When transaction is mined, contracts emit events and write logs to the blockchain that the frontend can process

## Libraries

- 2 building blocks
    - Reusable behaviours to add to your contracts (could also be inheritance in Solidity)
    - Implementation of the various standards
- Has more security but might introduce something you’re not familiar with and cause issues in the future
    - Please read documentation to avoid this issue
- Import the library → extend the library
    
    ```solidity
    import ".../Ownable.sol"; // Path to the imported library
    
    contract MyContract is Ownable {
        // The following function can only be called by the owner
        function secured() onlyOwner public {
            msg.sender.transfer(1 ether);
        }
    }
    ```
    
- Standards — defined in the form of ERCs (best to look out for standard implementations instead of importing your own) — can be imported for best practice!
- Make sure the version of the library matches the Solidity version
- Installation
    - Some can be `npm install` ed…
    - But check the Github
- Tools you can check out later:
    - OpenZeppelin Contracts
    - DappSys
    - HQ20

## Testing

- Identify bugs and vulnerabilities + reduces possibility of software errors
- Automated testing
    - Scripted testing executing repeatable tests
    - Efficient, fewer resources, provides higher levels of coverage, can be configured with test data
    - Types
        - Functional testing — checking that it works as intended (like Leetcode to see if it passes all the testcases)
            - Unit testing — individual components
                - Create assertions (simple statements specifying requirements for smart contract) e.g. “Only the admin can pause the contract”
            - Integration testing — individual components are tested together
                - Checks if the items conflict with each other
            - System testing — tests contract like it’s a fully integrated product to see if it performs as intended
        - Static/dynamic analysis
            - Static analysis
                - Examines source code/byte code before execution — debugging without actually running it
            - Dynamic analysis
                - Running in runtime and receiving back a list of potential issues and vulnerabilities
                - Fuzzing — smart contract fed dog information and sees how it responds
- Manual testing
    - Code audits, needs more skill and time, money and effort but you might be able to find defects automated testing can’t
    - Might also reveal vulnerabilities outside the scope of automated tests
    - Types
        - Code audits
            - Read through source code to uncover potential issues with an attacker’s mindset
        - Bug bounties
            - Money given to people who discover vulnerabilities
- Why test — otherwise there would be losses and after deploying, the contracts are mafan as heck to change
- Formal verification: uses formal methods — mathematically rigorous techniques for specifying and verifying software
    - Formally test assumptions
- Some e.g. of tools (more on docs) — Solidity-Coverage, Waffle, Remix Tests, OpenZeppelin Test Helpers

## Compiling

- Contract needs to be in bytecode — would turn code into something like this

```solidity
PUSH1 0x80 PUSH1 0x40 MSTORE PUSH1 0x4 CALLDATASIZE LT PUSH2 0x41 JUMPI PUSH1 0x0 CALLDATALOAD PUSH29 0x100000000000000000000000000000000000000000000000000000000 SWAP1 DIV PUSH4 0xFFFFFFFF AND DUP1 PUSH4 0xCFAE3217 EQ PUSH2 0x46 JUMPI JUMPDEST PUSH1 0x0 DUP1 REVERT JUMPDEST CALLVALUE DUP1 ISZERO PUSH2 0x52 JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST POP PUSH2 0x5B PUSH2 0xD6 JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP1 PUSH1 0x20 ADD DUP3 DUP2 SUB DUP3 MSTORE DUP4 DUP2 DUP2 MLOAD DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP DUP1 MLOAD SWAP1 PUSH1 0x20 ADD SWAP1 DUP1 DUP4 DUP4 PUSH1 0x0 JUMPDEST DUP4 DUP2 LT ISZERO PUSH2 0x9B JUMPI DUP1 DUP3 ADD MLOAD DUP2 DUP5 ADD MSTORE PUSH1 0x20 DUP2 ADD SWAP1 POP PUSH2 0x80 JUMP JUMPDEST POP POP POP POP SWAP1 POP SWAP1 DUP2 ADD SWAP1 PUSH1 0x1F AND DUP1 ISZERO PUSH2 0xC8 JUMPI DUP1 DUP3 SUB DUP1 MLOAD PUSH1 0x1 DUP4 PUSH1 0x20 SUB PUSH2 0x100 EXP SUB NOT AND DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP JUMPDEST POP SWAP3 POP POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH1 0x60 PUSH1 0x40 DUP1 MLOAD SWAP1 DUP2 ADD PUSH1 0x40 MSTORE DUP1 PUSH1 0x5 DUP2 MSTORE PUSH1 0x20 ADD PUSH32 0x48656C6C6F000000000000000000000000000000000000000000000000000000 DUP2 MSTORE POP SWAP1 POP SWAP1 JUMP STOP LOG1 PUSH6 0x627A7A723058 KECCAK256 SLT 0xec 0xe 0xf5 0xf8 SLT 0xc7 0x2d STATICCALL ADDRESS SHR 0xdb COINBASE 0xb1 BALANCE 0xe8 0xf8 DUP14 0xda 0xad DUP13 LOG1 0x4c 0xb4 0x26 0xc2 DELEGATECALL PUSH7 0x8994D3E002900
```

- Compiler produces Application Binary Interface (ABI) — JSOn file that describes the contract and its functions → JS client library reads and then calls your contract
    
    ```json
    [
      {
        "constant": true,
        "inputs": [],
        "name": "name",
        "outputs": [
          {
            "name": "",
            "type": "string"
          }
        ],
        "payable": false,
        "stateMutability": "view",
        "type": "function"
      },
      {
        "constant": false,
        "inputs": [
          {
            "name": "_spender",
            "type": "address"
          },
          {
            "name": "_value",
            "type": "uint256"
          }
        ],
        "name": "approve",
        "outputs": [
          {
            "name": "",
            "type": "bool"
          }
        ],
        "payable": false,
        "stateMutability": "nonpayable",
        "type": "function"
      },
      {
        "constant": true,
        "inputs": [],
        "name": "totalSupply",
        "outputs": [
          {
            "name": "",
            "type": "uint256"
          }
        ],
        "payable": false,
        "stateMutability": "view",
        "type": "function"
      },
      {
        "constant": false,
        "inputs": [
          {
            "name": "_from",
            "type": "address"
          },
          {
            "name": "_to",
            "type": "address"
          },
          {
            "name": "_value",
            "type": "uint256"
          }
        ],
        "name": "transferFrom",
        "outputs": [
          {
            "name": "",
            "type": "bool"
          }
        ],
        "payable": false,
        "stateMutability": "nonpayable",
        "type": "function"
      },
      {
        "constant": true,
        "inputs": [],
        "name": "decimals",
        "outputs": [
          {
            "name": "",
            "type": "uint8"
          }
        ],
        "payable": false,
        "stateMutability": "view",
        "type": "function"
      },
      {
        "constant": true,
        "inputs": [
          {
            "name": "_owner",
            "type": "address"
          }
        ],
        "name": "balanceOf",
        "outputs": [
          {
            "name": "balance",
            "type": "uint256"
          }
        ],
        "payable": false,
        "stateMutability": "view",
        "type": "function"
      },
      {
        "constant": true,
        "inputs": [],
        "name": "symbol",
        "outputs": [
          {
            "name": "",
            "type": "string"
          }
        ],
        "payable": false,
        "stateMutability": "view",
        "type": "function"
      },
      {
        "constant": false,
        "inputs": [
          {
            "name": "_to",
            "type": "address"
          },
          {
            "name": "_value",
            "type": "uint256"
          }
        ],
        "name": "transfer",
        "outputs": [
          {
            "name": "",
            "type": "bool"
          }
        ],
        "payable": false,
        "stateMutability": "nonpayable",
        "type": "function"
      },
      {
        "constant": true,
        "inputs": [
          {
            "name": "_owner",
            "type": "address"
          },
          {
            "name": "_spender",
            "type": "address"
          }
        ],
        "name": "allowance",
        "outputs": [
          {
            "name": "",
            "type": "uint256"
          }
        ],
        "payable": false,
        "stateMutability": "view",
        "type": "function"
      },
      {
        "payable": true,
        "stateMutability": "payable",
        "type": "fallback"
      },
      {
        "anonymous": false,
        "inputs": [
          {
            "indexed": true,
            "name": "owner",
            "type": "address"
          },
          {
            "indexed": true,
            "name": "spender",
            "type": "address"
          },
          {
            "indexed": false,
            "name": "value",
            "type": "uint256"
          }
        ],
        "name": "Approval",
        "type": "event"
      },
      {
        "anonymous": false,
        "inputs": [
          {
            "indexed": true,
            "name": "from",
            "type": "address"
          },
          {
            "indexed": true,
            "name": "to",
            "type": "address"
          },
          {
            "indexed": false,
            "name": "value",
            "type": "uint256"
          }
        ],
        "name": "Transfer",
        "type": "event"
      }
    ]
    ```
    

## Deploying

- Make it available to Ethereum users → send transaction containing code without specifying a receipient
- You need bytecode, ETH (for gas), development script/plugin, access to an ETH node
- Can use things like Hardhat to deploy! You will learn more when you are not lazy

## Verifying

- Source code verification: given source code compiles to the same bytecode to be executed at the contract address
    - Normally what verification refers to
- Formal verification: verifying the correctness of the smart contract (behaves as expected)
- Full (perfect) verification:
    - Malicious actors may add funny comments and variable names to mess with the verification
    - Can append extra data to the bytecode to act a cryptographical guarantee for the exactness of the source code
    - Happens in Solidity’s contract metadata — if stuff changes inside Solidity contract, metatdata changes → if metadata hash matches the bytecode then it’s a good vibe
- Why is this important?
    - Trustlessness — source code verification tools provide verification means so people can trust contracts online
    - User safety — money at stake, ensuring the contracts don’t have backdoors and other exploits
- Verification steps
    - Send transaction with data payload (compiled bytecode) to a special address → made with compiling source code + constructor arguments (you know, the one when the contract is created)
    - Input source files and compilation settings to compiler → compiler outputs bytecode → get bytecode at a given address → compare deployed bytecode with recompiled bytecode → if match, it verified → if metadata match → it full verification and not partial verification
- Tools: Etherscan (has a service), Sourcify, Tenderly (has a Hardhat plugin)

## Upgrading

- Changing business logic of a smart contract while preserving its state (upgradability and mutability are DIFFERENT)
    - Changing the code involved
    - 5 methods
- While preserving immutability by placing business logic in different contracts

### Methods

- Contract migration
    - Deploy new instance of an existing smart contract and transferring storage and balances to the new contract → migrate data to the new contract and update addresses to point to the new address → beg users to change to this one
    - Creating and managing unique states of the same software
    - Is expensive and time-intensive
- Data separation
    - Separate business logic and data storage into separate contracts
    - Logic contract calls the storage one
    - Storage contract holds the state associated with the smart contract e.g. balances and addresses (and is owned by the logic one)
        - Immutable but can change owner to a different logic contract
- Proxy patterns
    - Uses data separation but the storage contract calls the logic contract instead
    - What happens in Mickey Mouse’s Clubhouse?
        - Users interact w/ proxy contract
        - Proxy contract stores addresses of logic contract and delegates all function calls there using `delegatecall` function
        - Returned data is retrieved and returned to the user
    - `delegatecall` — opcode allowing one contract to call another with the actual execution being tied to the initial one
        - `msg.sender` and `msg.value` do not change their values
        - If function call does not match functions specified in contract — `fallback` function called to delegate it to a different contract
    - New logic contracts with upgraded business logic can be made → point the data contract to a new logic contract
- Strategy pattern
    - Behavioral software design pattern that enables selecting an algorithm at runtime. Instead of implementing a single algorithm directly, code receives run-time instructions as to which in a family of algorithms to use
    - Encourages making programmes that interface with other programs to implement specific features
    - Main contract contains core logic and has other *******************satellite contracts******************* that also hold logic that the main one can switch around with
    - Can introduce limited changes without changing core infrastructure
    - Normally used for minor upgrades
- Diamond pattern
    - Proxy pattern but this one can delegate function calls to more than one logic contract (facet)
    - Create mapping in proxy contract to different facet addresses → user makes function call → proxy contract checks mapping to find facet → `delegatecall`
    - Can upgrade small part without changing all the code, diamond pattern lets you workaround by splitting over multiple contracts, have catchall where you restrict bad entities from plaguing the entire contract
    
- Pros and cons
    
    ![Screenshot 2023-02-27 at 6.40.23 PM.png](%5BQUICKNOTES%5D%20Ethereum%20Official%20Documentation%2003f7dc4a94634a3fa83e7d5f363b08ed/Screenshot_2023-02-27_at_6.40.23_PM.png)
    
- Considerations
    - Secure access/control mechanisms to prevent unauthorized upgrades
    - Requires a lot of diligence
    - Decentralize implementing upgrades to avoid trust assumptions
    - Be aware of costs involved e.g. gas fees
    - Timelocks: protect users with delay to enforced changes on a system
        - Good: gives users a chance to leave if they don’t like it
        - Bad: cannot fast fast patch vulnerabilities

## Security

### Proper access controls

- Access control mechanisms
    - Ownable pattern
        - `onlyOwner` modifier ensures that only the contract caller/owner can continue with the contract
    - Role based control
        - Giving roles to a set of trusted participants → decentralize → e.g. 1 account mints tokens, 1 upgrades/pauses contract etc
    - Can also use multi-signature accounts
- `require()`, `assert()`, and `revert()` — guard contract operations
    - Internal safeguards!
    - `require()` — start of functions needing to fulfill a certain criteria before function occurs
    - `assert()` — detect internal errors and check for violations or invariants (logical assertion about a contract’s state that should hold true for all function executions)
    - `revert()` — used in if-else that triggers an exception if condition not satisfied
        
        ```solidity
        pragma solidity ^0.8.4;
        
        contract VendingMachine {
            address owner;
            error Unauthorized();
            function buy(uint amount) public payable {
                if (amount > msg.value / 2 ether)
                    revert("Not enough Ether provided.");
                // Perform the purchase.
            }
            function withdraw() public {
                if (msg.sender != owner)
                    revert Unauthorized();
        
                payable(msg.sender).transfer(address(this).balance);
            }
        }
        ```
        
- Test smart contracts and verify code correctness
    - Unit testing with property based testing with static and dynamic analysis
    - Formal verification (see above)
- Ask for independent review of code
    - Audits
    - Bug bounties — scaling bug bounties (setting rewards proportional to the stake of the bug)
- Follow best practices (thanks)
    - Store everything in git
    - Use pull requests that all have at least one independent reviewer
    - Use a development environment to test/compile/destroy smart contracts
    - Run code through basic code analysis tools e.g. Mythril/Slither (before each pull request is merged…)
    - Ensure code compiles without errors
    - Properly document code (NatSpec?) and describe details
        - No, self-documenting code is a myth
- Implement robust disaster recovery plans
    - Contract upgrades — could use proxy pattern
    - Emergency stops — block calls to vulnerable functions
        - 3 steps
            - Boolean indicating if contract is in stopped state (normally set to false)
            - Functions that reference the Boolean variable in the execution
            - Entity with access to emergency stop function
        - Users will need to trust you though to not go “haha funny gamer” and hit the stop whenever you want → preventable with on-chain voting, timelock, or multisig approval
    - Event monitoring
        - Event: tracking calls to smart contract functions and monitor changes to state variables
            - Log them!!! LOG ALL OF THEM!!! → easier to see what’s happening and if something is wrong, faster to respond t
        - Off-the-shelf monitoring tool also probably purchasable
- Design secure governance systems
    - Decentralized governance: turning over control over core smart contracts to community — “governance module” (democracy)
    - Potential issue — attacker gets a lot of voting power and overrides
    - Can use timelock/measuring voting power of address at historical period so no one can spontaneously attack the chain
- Reduce complexity of code to a minimum
    - Reuse libraries, write small functions, keep contracts modular by splitting business logic across multiple contracts
    - Reduces attack surface, makes it easier to reason about the correctness of the overall system, detect possible design errors early
- Defend against common smart contract vulnerabilities
    - Reentrancy
        - No concurrency → external call will pause contract’s execution until call returns, then continues normally aka “transferring control flow”
        - Reentrancy attack: malicious input is returned through the original call
            - Can prevent by using checks-effects-interactions pattern or pull payments (withdrawing funds from smart contracts instead of sending funds to accounts)
    - Integer underflows and overflows
        - Overflow: Going over a certain limit might reset to the lowest number e.g. max is `255` but number is like `257` so it registers as `1`
        - Underflow is vice versa
        - To fix, just use Solidity 0.8.0
    - Oracle manipulation
        - Oracle: sourcing offchain information and sending it on chain for smart contracts
        - Information MIGHT not be accurate though… e.g. open to manipulation
        - To avoid — use decentralised oracles that query multiple sites for information or [Time Weighted Average Price](https://docs.uniswap.org/contracts/v2/concepts/core-concepts/oracles) (TWAP) mechanism
- Visit the doc for resources to test security, ain’t no way you getting it here

### Child of curiosity

- How would you implement the global boolean variable and emergency stop a smart contract? I’m very confused and currently under the impression that once it has gone out, it cannot be modified. So if an attacker were to compromise something and you would like to shut down the contract, how does that even work if you cannot change the contract? I also remember there being talk about amending addresses and I guess my question extends to this…
    
    ****BRO YOURE ACTUALLY CRACKED YOOO THIS IS LIT****
    
    - *yeah so while you cant change the code, you can still call functions and read variables when a contract is deployed. so all emergency stop is is a function that needs to be called by usually a DAO when they decide to freeze access on other functions*
    - *by amending addresses i think you mean using a proxy to point to a different contract no?*
    - *i think you need to use assembly to make a proxy contract. Proxies are the loophole to technically make code changeable once deployed
    but proxies have also been the cause of like millions of $$ in hacked funds
    so you CAN technically change code but you'll probably lose a lot of money*

## Formal verification

- Process of evaluating the correctness of a system with respect to a formal specification
- When function satisfies specification, it is “functionally correct”, “correct by design”, or “correct by construction”
- Formal model: model which describes how an output of a mathematical function is computed given an input — allows for creation of formal specification
    - High levels: kind of black box everything, give an input and it’s correct if it produces the output you needed
        - Temporal logic: rules for reasoning about propositions qualified in terms of time
            - Used to state assertions about correct behaviour of systems
        - Capture safety and liveness properties
            - Safety property: “nothing bad ever happens” express invariance
            - Liveness property: “something eventually good happens” — express liquidity
    - Low levels: white-box view — learn about properties relevant to a contract’s execution
        - Analyse program traces and define properties of smart contract over the traces
        - Trace: sequences of function executions that alter the state of a smart contract
        - Hoare style property
            - Formal rules about correctness of program `{P}c{Q}` — P is precondition, c is the state of the program, and Q is the postcondition
            - Partially correct if P is true before function terminates and after it terminates Q is true
            - Total correctness is if P is true, Q is true, and c is guaranteed to happen
            - `require` and `assert` in Solidity can be used to check
        - Trace level property
            - Describe operations that transition a contract between different states and the relationships between the operations
            - 2 requirements — predefined states and predefined transitions
            - Used to reason about patterns of internal execution in smart contracts — assert admissible execution paths for a smart contract → techniques → verify execution never follows a path not defined
            - “users that do not deposit funds cannot vote on a proposal” → very time determined, if A doesn’t happen then B cannot happen
- Invariants: properties that a contract must remain true under every possible circumstance without any exceptions

### Formal verification techniques

- Model checking
    - Algorithm checks formal model against specification → need abstract math representation of a system → proves if math model satisfies a given logical formula
    - Normally evaluates temporal properties
    - Uses state space exploration (creates template of every possible combination… yeah you can see how that might go wrong)
- Theorem proving
    - Mathematically reasoning the correctness of the program
    - Create theorems (relationship between statements about a contract’s model and its property) to prove that a contract matches its specifications
    - Requires both humans and automation to ensure the validity of this test
- Symbolic execution
    - Analysing a smart contract by executing functions using symbolic values (e.g. x > 5) instead of concrete values (e.g. x === 5)
    - Path predicate: execution trace (like following the path of the code’s execution) as a math formula over symbolic input values
        - Use [SMT](https://en.wikipedia.org/wiki/Satisfiability_modulo_theories) solver to see if path predicate is satisfiable (exists a value that can satisfy the formula) → if path satisfied, SMT solver generates concrete value that steers execution towards that path
    - Easier to replicate issues because it’s not randomly generated (e.g. fuzzing dumps weird inputs but this one does it procedurally)

### Why use formal verification

- Reliability
- Prove functional correctness
    - Just because it cannot detect a bug though, doesn’t mean it’s not there
- Ideal verification targets — smaller sized Eth contracts
- Faster development cycle (because it relies on symbolic values e.g. “What if user tries to withdraw **n** ether?”)
- Drawbacks
    - Cost of manual labour
    - False negatives — can only check if the result matches specification, so you need to ensure the specification is correct and comprehensive
    - Performance issues — might be computationally intensive
        - Might also never be “false” if something never terminates… hard to prove some properties even if it’s well specified
- Check the docs for tools you can use to create and validate formal specifications!

## Composability

- Combining many different contracts to make new systems/outputs (like Lego blocks)
- Flash loan — having a loan without collateral/providing personal information and if you’re not able to apy it back within the same transaction, it gets reverted
- 3 principles
    - Modularity — ability of component to perform a specific task
    - Autonomy — ability to perform independently
    - Discoverability — needs to be open source
- Benefits
    - Shorter development cycle
    - Greater innovation
    - Better user experience
- Examples
    - Token swaps
    - Governance — Aragon client
    - Identity management

## Development networks

- Local blockchain instance to test your dapp — faster and more efficient than poking the testnet (e.g. no need ETH faucet, just spawn in your own money)
- Benefits
    - Determinsitclaly seeding your blockchain (free fake money), intantly produces blocks in order it’s received without delay, enhanced debugging and logging functionality
- Environments
    - Hardhat — [https://hardhat.org/](https://hardhat.org/) (for local development)
    - Goerli, Sepolia — public test blockchains

## Development frameworks

- Provide easy plugin systems so you can just jump in and start developing
- Umm,,, it’s [HardHat](https://hardhat.org/) again that I choose… UwU
    - You can use [Brownie](https://eth-brownie.readthedocs.io/en/latest/) but I’m only there because I saw the word “Python” in it’s description, so-
    - Oooh I see [Alchemy](https://www.alchemy.com/) also! And I already have an account! Please help me I am a victim of sunk cost fallacy!

## Ethereum client APIs

## Javascript APIs

- To connect to the blockchain, you need to connect to a node first
- Javascript to get JSON RPC methods to connect to the Ethereum network
    - Node needs execution node and consensus node to run (if you’re using like, AWS or something then you need to update the IP address, just check the Docs LOL)
- Use the libraries to save time
- Accessing blockchain
    
    ```jsx
    //ETHERS, ANOTHER SERVICE, EXAMPLE
    // A Web3Provider wraps a standard Web3 provider, which is
    // what MetaMask injects as window.ethereum into each page
    const provider = new ethers.providers.Web3Provider(window.ethereum)
    
    // The MetaMask plugin also allows signing transactions to
    // send ether and pay to change state within the blockchain.
    // For this, we need the account signer...
    const signer = provider.getSigner()
    ```
    
    - OMGGGG ONCE YOU SET THIS UP YOU CAN QUERY THE BLOCKCHAIN FOR STATS AND DATA LET’S GOOOOOOO
- Wallet functionality
    
    ```jsx
    //ETHERS EXAMPLE
    // Create a wallet instance from a mnemonic...
    mnemonic =
      "announce room limb pattern dry unit scale effort smooth jazz weasel alcohol"
    walletMnemonic = Wallet.fromMnemonic(mnemonic)
    
    // ...or from a private key
    walletPrivateKey = new Wallet(walletMnemonic.privateKey)
    
    walletMnemonic.address === walletPrivateKey.address
    // true
    
    // The address as a Promise per the Signer API
    walletMnemonic.getAddress()
    // { Promise: '0x71CB05EE1b1F506fF321Da3dac38f25c0c9ce6E1' }
    
    // A Wallet address is also available synchronously
    walletMnemonic.address
    // '0x71CB05EE1b1F506fF321Da3dac38f25c0c9ce6E1'
    
    // The internal cryptographic components
    walletMnemonic.privateKey
    // '0x1da6847600b0ee25e9ad9a52abbd786dd2502fa4005dd5af9310b7cc7a3b25db'
    walletMnemonic.publicKey
    // '0x04b9e72dfd423bcf95b3801ac93f4392be5ff22143f9980eb78b3a860c4843bfd04829ae61cdba4b3b1978ac5fc64f5cc2f4350e35a108a9c9a92a81200a60cd64'
    
    // The wallet mnemonic
    walletMnemonic.mnemonic
    // {
    //   locale: 'en',
    //   path: 'm/44\'/60\'/0\'/0/0',
    //   phrase: 'announce room limb pattern dry unit scale effort smooth jazz weasel alcohol'
    // }
    
    // Note: A wallet created with a private key does not
    //       have a mnemonic (the derivation prevents it)
    walletPrivateKey.mnemonic
    // null
    
    // Signing a message
    walletMnemonic.signMessage("Hello World")
    // { Promise: '0x14280e5885a19f60e536de50097e96e3738c7acae4e9e62d67272d794b8127d31c03d9cd59781d4ee31fb4e1b893bd9b020ec67dfa65cfb51e2bdadbb1de26d91c' }
    
    tx = {
      to: "0x8ba1f109551bD432803012645Ac136ddd64DBA72",
      value: utils.parseEther("1.0"),
    }
    
    // Signing a transaction
    walletMnemonic.signTransaction(tx)
    // { Promise: '0xf865808080948ba1f109551bd432803012645ac136ddd64dba72880de0b6b3a7640000801ca0918e294306d177ab7bd664f5e141436563854ebe0a3e523b9690b4922bbb52b8a01181612cec9c431c4257a79b8c9f0c980a2c49bb5a0e6ac52949163eeb565dfc' }
    
    // The connect method returns a new instance of the
    // Wallet connected to a provider
    wallet = walletMnemonic.connect(provider)
    
    // Querying the network
    wallet.getBalance()
    // { Promise: { BigNumber: "42" } }
    wallet.getTransactionCount()
    // { Promise: 0 }
    
    // Sending ether
    wallet.sendTransaction(tx)
    ```
    
    - Can create accounts and sign transactions and MORE!!! WOAHHH
- Can call smart contract functions by reading ABI (Application Binary Interface) into an object
    
    ```solidity
    //fROM THIS
    contract Test {
        uint a;
        address d = 0x12345678901234567890123456789012;
    
        function Test(uint testInt)  { a = testInt;}
    
        event Event(uint indexed b, bytes32 c);
    
        event Event2(uint indexed b, bytes32 c);
    
        function foo(uint b, bytes32 c) returns(address) {
            Event(b, c);
            return d;
        }
    }
    ```
    
    ```json
    //TO THIS
    [{
        "type":"constructor",
        "payable":false,
        "stateMutability":"nonpayable"
        "inputs":[{"name":"testInt","type":"uint256"}],
      },{
        "type":"function",
        "name":"foo",
        "constant":false,
        "payable":false,
        "stateMutability":"nonpayable",
        "inputs":[{"name":"b","type":"uint256"}, {"name":"c","type":"bytes32"}],
        "outputs":[{"name":"","type":"address"}]
      },{
        "type":"event",
        "name":"Event",
        "inputs":[{"indexed":true,"name":"b","type":"uint256"}, {"indexed":false,"name":"c","type":"bytes32"}],
        "anonymous":false
      },{
        "type":"event",
        "name":"Event2",
        "inputs":[{"indexed":true,"name":"b","type":"uint256"},{"indexed":false,"name":"c","type":"bytes32"}],
        "anonymous":false
    }]
    ```
    
    - Can send transactions and execute methods, estimate gas, deploy contracts, and moreeeee!!~
- Utility functions — make programming just that little bit easier
    - E.g. function that converts Ether (big number) to Wei (small number) without you having to calculate it
- Just use Alchemyweb3,,, or Ether.js or Web3.js

## Backend APIs

- It’s the same junk that the JS library had but now it’s for backend.
- Potential usage: Alchemy, [PythonTooling](https://snakecharmers.ethereum.org/),

## JSON RPC

- JSON-RPC — stateless, light-weight remote procedure call (RPC) protocol using JSON as a data format
- Check the JS APIs above for the easiest ways to do this
- Can communicate with a node using Engine API — look, you’re too juvenile to be doing this so please just leave it until your pea size brain can process more than 2 words
- Conventions
    - Hex value encoding — 0x beginning and no leading 0s and even number of digits and always have at least one digit
- When requests are made on Ethereum’s state, last default block is considered the height
    
    ![Screenshot 2023-02-28 at 2.59.30 PM.png](%5BQUICKNOTES%5D%20Ethereum%20Official%20Documentation%2003f7dc4a94634a3fa83e7d5f363b08ed/Screenshot_2023-02-28_at_2.59.30_PM.png)
    
- You can curl it from a node `curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"web3_clientVersion","params":[],"id":67}' 127.0.0.1:85452`
    - But I think just use JS bah
- Core methods
    - Gossip — track the head of the chain
        - `eth_BlockNumber` , `eth_sendRawTransaction`
    - State — methods that record the current state of all the data stored
        - `eth_getBalance`, `eth_getStorageAt`, `eth_getTransactionCount`, `eth_getCode`, `eth_call`, `eth_estimateGas`
    - History — historical records of every block to genesis
        - NO. I AM NOT WRITING MORE THAN 3 COMMANDS FOR THIS. YOU WANT YOU GO READ THE DOCUMENTATION. IT’S TOO MUCH THIS WHOLE PAGE IS A WIKIPEDIA ARTICLE.
        - `eth_getBlockByHash`, `eth_getTransactionReceipt`, `eth_getBlockByNumber`
- Usage example — a scuffed under the hood explanation
    - Ensure HTTP RPC interface is enabled (and like,,, assuming you’re using the GETH network)
    
    ```solidity
    geth --http --dev console 2>>geth.log
    ```
    
    - Then curl to verify index is running
    - Compile the contract oofsies
    - Decode the hex and keep curling to check how much it costs to deploy it (ouch)
    - Deploy — check transaction hash to ensure it is running
    - AND IF YOU ACTUALLY WANT TO USE THIS CONTRACT
        - Wanting to use a function like `eth_sendTransaction` requires you to fill in parameters, but anyway here’s the command to check for something that I’m not quite sure of yet — OH IT’S PAYLOAD BYTES `web3.sha3("multiply(uint256)").substring(0, 10)2`
        - Encode arguments and add it to the end of the function selector
        - Receive hash back and decode it

## Data and analytics

- Big data is big, so you want to manage it by leveraging historical + already there data
- Block explorers: can use them to see real time data on blocks and other activity
    - Like general block stats, transactions, metadata, gas fees, accounts (both users and smart contracts), tokens, network,
    - Consensus layer data: deals with the enforcement of network rules that describe what nodes within the network should do to reach consensus about the broadcasted transactions
        - Epoch (randomness inspired validators for the block), slots (opportunities for block creation), blocks, validators (those responsible for proposing block and slotting ‘em in), attestations (yes votes to block), network
- Index: a network structure meant to optimize the querying of information from across the blockchain by providing an efficient path to its storage source.
- REST — representational state transfer (describes the standards of architecture of the web) → makes it easier for the web to interact with each other
    - Read this later
- The Graph
    - Graph Network — decentralized indexing protocol for organizing blockchain data
        - Build stuff that runs on public infrastructure
    - GraphQL — devs can query open APIs just for the necessary information
        - Benefits: performance, scalability, built in accuracy
            
            ![Screenshot 2023-02-28 at 4.03.41 PM.png](%5BQUICKNOTES%5D%20Ethereum%20Official%20Documentation%2003f7dc4a94634a3fa83e7d5f363b08ed/Screenshot_2023-02-28_at_4.03.41_PM.png)
            
- Client diversity
    - More computer → more safe
- Dune analytics: preprocesses blockchain data in a SQL table
    - 4 tables: blocks, transactions, logs, traces

## Storage (decentralized)

- Peer to peer network of users who own the operational data
- Things to keep in mind as you think of big big storage
    - Persistance mechanism (making something live forever)/Incentive structure
        - Blockchain based
            - New info tacked onto the end of a node, keeping history for all time
            - Also need incentive: must pay money to the miners
        - Contract based
            - Keeping data renewed for a certain amount of time — need to “reagree” to the contract to keep the data for longer
            - Only stores hash of where data is stored
            - Additional consideration
                - IPFS — system for storing files, websites, apps, and data — no incentive but uses contract incentive
                - Can also run IPFS data on pinning service — your data gets priority (run node and host others, and your data will get renewed with priority)
                - SWARM — decentralized data storage and distribution tech w/ storage incentive system and storage rent price oracle
    - Data retention enforcement
        - Challenge mechanism
            - To ensure data is retained, node is checked for most recent block and 1 random block from the past — passes if can come up with correct data
    - Decentrality — decentralized tools without KYC (Know Your Customer)
        
        ![Untitled](%5BQUICKNOTES%5D%20Ethereum%20Official%20Documentation%2003f7dc4a94634a3fa83e7d5f363b08ed/Untitled%205.png)
        
    - Consensus — POW (proof of work) or POS (proof of stake)

## Integrated development environments (IDEs)

- Places you can code, we all know Neovim is the ultimate chad option
- Web based (that I care about) — Remix, Replit
- Desktop (that I care about) — Visual Studio Code, Remix Desktop
    - Plugins: [Solidity x Hardhat](https://marketplace.visualstudio.com/items?itemName=NomicFoundation.hardhat-solidity), [Solidity](https://marketplace.visualstudio.com/items?itemName=JuanBlanco.solidity)

## Programming languages

## Note to everyone

- I think what I’m trying to say is that I really don’t do any other languages because I am insecure if I cannot be immediately good at something or am not already familiar with it
- So all you get is Python and JS
- Haha
- Go make your own notes if you want

## [Python](https://ethereum.org/en/developers/docs/programming-languages/python/)

- Unironically not worth copy pasting links there, they’re all very good. So just read the docs for this one as it’ll guide you to everything you need
- Tools you could start exploring: Brownie, Vyper

## JS

- EZ game — [Javascript API library](https://ethereum.org/en/developers/docs/apis/javascript/) (Web3.js, Ethers.js)
- Smart contracts — Solidity!
- There’s a [JS implementation](https://github.com/ethereumjs/ethereumjs-monorepo) of EVM (that supports the latest fork rules)
- [Nodes and clients](https://github.com/ethereumjs/ethereumjs-client)
- Read more [projects](https://github.com/ethereumjs) if you’re interested :3

# Advanced

## Bridges

- Connect blockchain networks — enable connectivity and interoperability through a transportation route where tokens, messages, arbitrary data and smart contract calls can be transferred from one chain to another
    - TLDR: exchange data and move items between each other
    - Connects two blockchain ecosystems
    - Blockchains are in siloed environments — cannot naturally communicate with each other
- Benefits
    - Transfer data
    - Expand design space for what items can offer (diversification)
    - Can use different blockchains — L2
    - Developer collaboration
    - Attracting users to dapps

### Designs

- Lock and mint — lock assets on source chain; mint assets on destination chain
- Burn and mint — burn assets on source chain; mint assets on destination chain
- Atomic swaps — swap assets on source chain for assets on destination chain with another party

### Types

- Native — bootstrap liquidity on a particular blockchain (easier to move funds for this system)
- Validator/oracle based — external validator
- Generalized message passing — transfer assets + messages + arbitrary data
- Liquidity — transferring assets from one chain to another using atomic swaps (normally don’t support cross chain message passing)
- Tradeoffs
    - Security (who verifies?), convenience (to set up and to use), connectivity (and integrating to a new blockchain), ability to more complex data, cost effectiveness
    - Can be trusted and trustless
        - Trusted — external verification, fully generalized messages, connectivity, speed, cost effectiveness at the cost of security
        - Trustless — blockchain (more secure)
            - Generalized message passing — security, more complex data, cost effective, but less connected and slightly slower
            - Liquidity networks — atomic swaps to transfer assets, locally verified — good with security, gspeed, cost effective, good connectivity, but cannot pass more complex data (no cross chain message)
- Risks
    - Smart contract risk (one flaw = bye bye assets)
    - Systemic financial risks: minting canonical assets on a different chain (wrapped versions of tokens exploited)
    - Counterparty risk: trusting third party to not rug pull, censor, etc
    - Open issues: how will performance be like during network congestion? Unforeseen events (network level attacks/state rollbacks)?
- Integrations
    - Build your own — essentially very mafan
    - Showing users multiple bridge options — cumbersome onboarding when you ask users to choose their network and leave the dapp
    - Integrating a bridge — can do from in-dapp but,,, must assess and maintain bridge, using on bridge can cause a single point of failure and dependency, dapp limited by bridge’s capabilities, more functionality than just a bridge might be needed
    - Integrating multiple bridges — resource-consuming, technical communication overheads for developers
    - Integrating a bridge aggregator (access to multiple bridges) — manages the connection for you and inherit strengths of all the bridges
        - But also more smart contracts = more risks so help lah
- Have app on multiple chains — Alchemy, Hardhat, etc
- Monitoring contract activity across chains — Tenderly, TheGraph

## Standards

- Keeping things interoperable across implementations — ensure smart contracts and dapps remain composable
- [EIP](https://eips.ethereum.org/EIPS/eip-1) — Ethereum Improvement Protocols discussed by community through standard process
    - Basically a giant Reddit forum where people submit their ideas and others debate over it, and majority consensus determines whether it’s successful or not
    - And anyone can make an EIP if they follow the format
- Types
    - Standards track — any change that affects most/all Ethereum implementations
        - Core: improvements requiring consensus fork
        - Networking: DevP2P, Light Ethereum Subprotocol, proposed improvement to network protocol specifications of whisper and swarm
        - Interface: Client API/RPC specifications, language level standards (method names, contract ABIs)
        - ERC: application-level standards conventions
    - Meta track — process surrounding Ethereum/change to process
    - Informational track — Ethereum design issue/general guidelines/information to community
- Token
    - Literally almost anything — reputation points, skills, lottery tickets, financial assets, fiat currency, gold etc
    - Every token is given a value that is the same as another token (1 token will always be equivalent to 1 token)
    - All can — transfer tokens from one account to another, get current token balance of account, get total supply of tokens in the network, approve whether tokens from an account can be spent by a third party
    - Tokens
        - ERC-20: voting, staking, virtual currencies (Minecraft default skin)
            - ERC-1363: token interface for ERC-20 — supports executing recipient code after transfer/transferFrom/spender code after approve
        - ERC-721: NFT
            - Identify something/someone in a unique way — e.g. CryptoKitties, Bored Ape Yacht Club
            - ERC-2309: event emitting after making NFT
            - ERC-4000: interface extension for EIP-721 consumer role
            - ERC-4907: time-limited role with restricted permissions to ERC-721
        - ERC-777: token standard improving over ERC-20 (NOT RECOMMENDED) — extra functionality on top of tokens e.g. mixer contract for improved transaction privacy/emergency recover fund
            - Hooks: called when token is sent/received through contract (using ERC-1820 standard)
                - Don’t need double call, can reject transactions, unregistered hooks aren’t compatible — prevents accidental transfers to non ERC-777 contracts
                - Backwards compatible with ERC-20
            - Oh it gone… HAHAHAH apparently was too susceptible to different forms of attack L + ratio
        - ERC-1155: fungible and non fungible — more efficient trades and transaction bundling
            - Manages multiple token types — any combination of fungible, NFT, or maybe even semi fungible token
            - Features
                - Batch transfer: Transfer multiple assets in a single call
                - Batch balance: Get the balances of multiple assets in a single call
                - Batch approval: Approve all tokens to an address
                - Hooks: receive token hooks
                - NFT Support: If supply is only 1, treat as NFT
                - Safe transfer rules: set rules for secure transfer
        - ERC-4626: tokenized vault standard — optimize/unify technical parameters of yield-bearing vaults
            - Lowers barrier to entry

### Funny child with questions

- I think this question is more on a philosophical level as opposed to a technical one — can it just automatically be assumed that no system will run perfectly and the only perfect system is one that keeps adapting? Can it also be assumed that there will always be a bad actor who will attempt to sabotage the system for their own benefit? I think I inherently know the answer but I would like to hear your perspective on it too, if you have anything to add.
    
    *Yeah its hard for me to imagine that a system can be perfect, cause even if you compare smart contract development to hardware, hardware isn’t immutable. So at the end of the day I think there does need to be some options to change the behavour of your app, whether thats manually migrating to a new verison of a contract or doing some proxy stuff*
    
    *in terms of bad actors, yes, every system needs to take bad actors into consideration. From a more philosophical standpoint, the day that there are no murders, no wars, no domestic violence, and absolute world peace is the only day that bad actors can be ignored in mechanism/economic design*
    

## Maximal extractable value (MEV)

- Maximum value extractable from block production in excess of standard block reward and gas fees by including, excluding, and changing the order of transaction in a block
- Good
    - Many people rely on the speed of these transactions
    - Without people trying to exploit this system, it wouldn’t be as strong
- Bad
    - Sandwich trading results in worse experiences for ordinary users
    - Network congestion + high gas prices
    - Occurences of MEV between blocks may incentivize validators to reallocate position of the blockchain → consensus instability
- Examples
    - DEX arbitrage — decentralized exchange (2 DEX offering token at 2 different prices → buy from lower and sell higher)
    - Liquidation — lending protocol liquidations (LPL) → lending some money to 3rd party, if money exceeds borrowing price/percentage → searchers race to liquidate that asset instantly and get profit back
    - Sandwich trading — watch mempool for large DEX trades → buys right before the trade → sells immediately after when the price is higher
        - Riskier because not atomic
        - Prone to [salmonella attack](https://github.com/Defi-Cartel/salmonella) — TLDR: man really set bait LOLOLOLOL
    - NFT MEV — mistaken selling at lower price is snapped up by searcher
    - The long tail: check docs for more opportunities to waste energy
- Miner extractable value: used to be optimizing it for miners, but we don’t really use miners anymore so it’s now ******maximal******
- Extracted by **searchers** — running complex algorithms on blockchain data → detect profitable opportunities → have bots automatically submit profitable transactions to the network
    - Validators get a portion of the amount (because searchers need to pay high gas fees to guarantee a spot)
- Gas golfing — programming transactions so they use the least amount of gas → benefits searchers
    - E.g. using addresses that begin with as many 0s as possible to minimize storage, leaving small ERC20 token balances in contract (cost more gas to initialize storage slot)
- Generalized frontrunners: bots watching mempool to find profitable transactions → if profitability detected → pastes frontrunner’s address → frontrunner submits modified transaction at higher gas price → gets original searcher’s MEV
- Flashbots: extend execution clients with a service that lets searchers submit MEV transactions to validators without revealing to public mempool
- MEV In Proof Of Stake
    - Validator centralization — more MEV make more money for themselves → raises barrier to validation on the blockchain because of economies of scale → solo validators find it harder to validate → leads to centralization
    - Permissioned mempools — sending transactions directly to validator to validate → “dark pools” (permissioned, paywalled blockchain) → destroys Eth’s concept
    - Prevention methods (suggested)
        - Proposer builder separation
            - Block builder: specialized entities that will order transactions and build blocks as opposed to validators
            - Creates block → bid for inclusion in Beacon Chain block → PBS makes auction market where builders negotiate with validators selling blockspace
            - Commit-reveal scheme: only publish block header and bids → winning bid → signed block proposal and header
                - Must publish full block body once signed + have enough attestations to be finalized
            - How this mitigates the impact
                - Capture MEV opportunities, make validators aim to create new blocks instead of optimizing money
                - Reduce centralization risks
                - Don’t have to trust builders not to withhold blocks until it’s profitable → if the block is wrong, just discard the MEV revenue and transaction fees
        - Builder API
            - Proposed implementation of the proposer builder separation with higher trust assumptions
            - Modified engine API → used by consensus layer clients to request execution payloads from execution layer clients
                - Validators on block proposing duties request transaction bundle → include in proposed Beacon Chain block
                - Allows validators to source blocks from external entities
            - How this works (I am going to cry, on the verge of a mental breakdown, I stopped understanding English like 8 pages ago)
                - Connects validator to network of blocks running execution layer clients (builders are also kinda like validators in that they are trying to get MEV but okay whatever)
                - Validator requests execution payload (block header and bids) → execution payload header also contains validation fee
                - The validator reviews the incoming bids and picks the execution payload with the highest fee → Builder API → “blinded” Beacon block proposal (signature and execution payload header)
                - Builder API receives it back, checks it’s signed
                - Validator still expected to build block to not miss out on block proposal rewards if the Builder API fails → BUT YOU CANNOT SIGN IT OR IT WILL MISMATCH WITH THE BUILDER API
            - Example: MEV boost
                - Searchers search for profitable transactions and blocks still
                    - But they are now working with builders who build the blocks → runs optimizations to find best price
                - Transaction bundles pass through *******relayers******* which ensure the owner isn’t spammed
                - Escrows — provides data availability by storing block bodies sent by builders and block headers sent by validators → connected validator asks for profitable block → chooses highest payload (w/ the big big money)
                    - Escrows are a MEV boost concept
            - How does it mitigate MEV’s impact
                - Democratize access to MEV opportunities → eliminate trust assumptions and entry barriers for solo traders
                - More competition among block builders → lower censorship resistance
                - Provides transaction privacy to certain parties (MEV boost as a project, not necessarily Builder APIs)
                    - With multiple block builders, those act as centralized gatekeepers so we must decentralize the entire process
                    - Builder API is open sourced
            

## Oracles

- Bringing off chain information onto the chain (because technically you can’t access third party information on a blockchain for security purposes)
- Pull off chain information on chain; push on chain information (disseminate) off chain to third parties
- Bridge between off chain and on chain activities
- Could be
    - One/multiple sources
    - Centralized/decentralized
    - Immediate read/publish-subscribe/request-response
    - Input (retrieve external data for on chain contracts)/ output(disseminate data for off chain use)
    - Computational (computational tasks off chain)
- E.g. [Chainlink](https://chain.link), [Witnet](https://chain.link)

### But why

- Ethereum is deterministic by design to ensure fairness and consensus
- Oracles let you store external data for use by the chain on the chain without worrying about breaking consensus → info will be publicly available
- Contract requests data → oracle node queries data (this one can be from third party resources) → returns to contract as an oracle
    - “Hybrid smart contract” → e.g. decentralized prediction markets where the data is from other sources on the internet but the code and logic for payouts are on the smart contract

### Oracle problem

- Source of info? Is it reliable? Is data available and updated regularly? If we “trust” oracles as opposed to trustlessness,,, then aren’t we kind of not abiding by the rules of smart contracts in the first place?
- Things the oracle should be
    - Correct — authenticity and integrity to the chain so that you don’t break standards
    - Availability — should not delay executions of contracts
    - Incentive compatibility — attributability and accountability (based on quality of information and who submitted it)

### The paid actors (the interactors)

- General overview → Smart contracts → oracle contract → oracle node → data whiff whaff like some API idk → oracle node → oracle contract → smart contract
- Users — smart contracts
    - User sends data request to oracle contract
    - Requests answer
        - What sources can off chain nodes consult for info?
        - How do reporters process info from data sources and extract useful points?
        - How many oracle nodes can participate in retrieving data?
        - How should discrepenaices in report be managed?
        - What method should be implemented in filtering submissions and aggregating reports into a single value?
- Oracle contract
    - Listens for data requests, relays queries to oracle nodes, broadcasts returned data to client contracts
    - Perform computation on returned data points to produce aggregate value
    - Makes log event when receiving query
- Oracle node
    - Off-chain component → extracts info from external source, puts on chain for consumption by smart contracts
        - Listen for events from on chain oracle contract → complete task described in log
    - HTTP GET request to API → parses to blockchain format → sends onchain by including in transaction to oracle contract
    - Might need to validate the information
    - Computational oracles
        - Do computing stuff that would be too expensive to do on chain e.g. verify number in game

### Oracle design patterns

- Immediate read
    - You’re not going to believe this, but you read it immediately
- Publish subscribe
    - Data feed for other contracts to read for information → info here expected to change frequently e.g. ETH-USD prices
- Request response
    - Request arbitrary data if dataset too large to be stored/users only need small amount
    - General overview → Smart contracts → oracle contract → oracle node → data whiff whaff like some API idk → oracle node → oracle contract → smart contract
    - Users must cover all gas costs incurred UwU

### Types

- Centralised
    - Controlled by single entity
    - Good for proprietary datasets, efficient
    - Low correctness guarantee, poor availability (DoS attacks), poor incentive compatability (like, people might be more incentivized to tamper with information because there is no real reward for honesty)
- Decentralized
    - Permissionless, trustless, free from administration — need more than one partner to confirm the validity of the information
    - Could be semi decentralized — anyone can participate with owner that approves/removes nodes based on historical performance
    - Eliminate single points of failure, standalone, defined consensus mechanisms
    - Availability
        - High availability off and on chain: dependent on multiple nodes which are dependent on multiple data sources
        - Enables multiple oracles’ information to be trusted
        - Unresponsive oracles can be slashed → incentivizes speed
    - Good incentive compatability
        - Byzantine fault — components may fail and there is imperfect information on whether a component has failed
        - Achieving attributability and accountability
            - Must sign data they provide → users can filter out oracles they don’t like
            - May need nodes to place a stake → if correct, return stake and rewards, if not, slash stake
    - High correctness guarantee
        - Authenticity proof — enable independent verification of information retrieved from external sources
            - Transport layer security (TLS): oracle nodes receiving data from external sources using secure HTTP connect based on TLS protocol
            - Trusted execution environment (TEE): like a virtual environment that also ensures integrity, confidentiality, immutability
                - Prevents external processes from altering/reading code and data
        - Consensus based validation of information
            - Voting/staking on accuracy of data
                - Stake money on your answer, majority wins
                - Losers have their staked money distributed amongst the winners
                - Sybil attacks prevented — malicious attackers making multiple identities
                - Cannot prevent freeloading (copying other’s information) and lazy verification (oracle nodes following majority without self verification)
            - Schelling point mechanisms
                - Assuming multiple entities will always default to common solution to a problem in absence of any communication
                - Those who hit the schelling point are rewarded, everyone else within the bellcurve beyond a certain range is penalized
                - Minimize on-chain footprint + guarantees decentralization (because they need to be signed off before being processed)
    

### Applications

- Retrieving financial data — getting market prices and stock prices
- Generating verifiable randomness
    - Ethereum is deterministic, so it’s hard to come up with real random
    - Off-chain computation oracles can solve the issue e.g. [Chainlink VRF](https://docs.chain.link/vrf/v2/introduction)
- Getting outcomes for events — e.g. decentralized insurance applications (that require things like weather data etc)
- Automating smart contracts — might have private functions that developers need to trigger
    - Some oracles might have automation services (triggering functions according to user defined parameteres)

## Scaling

- Combating blockchain scalability issues
- Goals: increase transaction speed, transaction thoroughput (high transactions/s), without sacrificing decentralization/security

### On chain scaling (layer 1 solutions)

- Sharding
    - Splitting a database horizontally to spread the load
    - Using data techniques to confirm the data has been made available by the network as a whole
    - Creates new chains (”shards”) → lighten validator load, reduce network congestion, increase transactions per second

### Off chain scaling

- No need to change the existing Ethereum protocol
- Layer 2 scaling
    - Handling transactions off the Mainnet
    - Layer 2 nodes run by 3rd parties of any sort → transactions submitted to this node → batches into groups before putting them into Layer 1
    - Why tho: reduces network congestion, reduced gas fees, update is not at the expense of decentralization/security, can have their own efficiencies when working with other applications
- Rollups
    - Perform transaction execution outside layer 1 before data is posted to layer 1 when consensus is reached
        - Interacts with Mainnet using a smart contract of its own that takes all the transactions then verifies it using Ethereum
    - Optimistic rollups: assumes transactions are valid and just runs them → can be challenged if they are sussy (”fraud proof”) → read more [here](https://ethereum.org/en/developers/docs/scaling/optimistic-rollups/)
    - Zero knowledge rollups: runs computation off chain and submits validity proof to chain of just a little bit of the important data’s header
- State channels
    - Multisig contracts to transaction quickly and freely off chain → settle finality with Mainnet
        - Alternative: payment channels → have 2 people keep the same ledger
    - Only submit 2 on chain transactions to open and close the channel → big output and lower costs for users
- Sidechains
    - Independent EVM-compatible blockchain running in parallel to Mainnet → compatible with bridges but have their own consensus rules/block parameters
    - Do not inherit security properties of Ethereum though
    - Do not post state changes and transaction data back to Ethereum
- Plasma
    - Separate blockchain anchored to main Eth chain → uses fraud proofs to arbitrate disputes
    - Has its own method of validating things away from Ethereum using Merkle trees..? Not super sure about that the docs are very ambiguous HAHA
- Validium
    - Validity proofs (using zero knowledge rollups) but data not stored on main layer 1 chain → could have 10k transactions per second per Validium chain and multiple chains running in parallel
    - Funds can be withdrawn using Merkle proofs

### Why scale?

- Reduce overall congestion
- Different solutions can exist and work in harmony → exponential effect on future transaction speed and throughput
- Don’t necessarily always need to use Eth chain
- Something something need more than 1 to fulfill Ethereum vision

## Data availability

- Ability of nodes to download transaction data for a block while it is being proposed for addition to the chain
- Guarantee that the block proposer published all transaction data for a block and that the transaction data is available to other network participants
    - Nodes participating in consensus downloads block header and metadata to verify and confirm validity
- If we cannot reproduce data, it is taken by the blockchain to have not existed

### The problem — how do we verify that the data for the newly produced block is available?

- Even if block is valid but not fully accessible, then it could cause problems
- Issue also comes about when discussing scaling solutions — how can you ensure you fully verify all those Level 2 transactions?
- Data availability and light clients
    - Currently under research to ensure light clients don’t need to download the entire block to render data available or not
    - Stateless client concept — don’t need to store data to verify blocks?

### Data availability vs retrievability

- Data retrievability: ability of nodes to retrieve historical information from the chain
- Only need one honest node to make it retrievable

### Why so important?

- Blockchain security: otherwise there will be data withholding attacks → hackers incentivized to game the system and insert malicious, supposed to be rejected nodes
- Decentralized scalability (data availability and level 2 scaling)
    - Optimistic rollups compress their transactions into `calldata` → anyone can verify and declare innocent → if invalid → use available transaction data to come up with fraud proof and challenge it
    - Zero knowledge rollups (ZK) don’t need more validation → but you need to be able to access the state data to guarantee its functionality
        - E.g. users cannot access balances, cannot perform state updates

### Types of data availability systems

- On chain
    - Force block publishers to publish all transaction data on chain and have validating nodes download it
    - Feature of monolithic blockchains — formed from a large block of stone (metaphorically), hard to change
    - Bottlenecks on scalability
        - Slow processing speeds, needs full nodes to store increasing amounts of state, validators might need to get larger machines (disincentive)
- Off chain
    - Move data storage off the blockchain
    - Block producers provide cryptographic commitment to prove the availability of the data
    - Used by modular blockchains (blockchain architecture that separates the data and the processing elements
    - Normally separate data availability with consensus and execution
    - Negative implications for trustlessness, decentralization, and security

### Solutions

- Data availability sampling
    - Nodes sample small, random chunks of a block over multiple rounds to validate the availability
    - Good for light clients — can verify without installing everything
- Data availability proofs
    - Data availability sampling + erasure coding (double a dataset by adding redundant code → if any pieces lost, just replace with the code)
    - If anything lost → small amount of blockchain data is already enough to reconstruct the original
    - Now the attacker needs to withhold >50% of the block
    - Don’t need full nodes + light clients have statistical certainty that the entire block data was published on the network
- Data availability committees
    - Pure validiums (publish zero-knowledge proofs to verify off-chain transactions on Ethereum)
        - Kinda centralized and less secure
    - Some solve the problem by asking blocks to store data with parties that form the DAC (Data availability committee) → stores copies of off-chain data offline, but need to make it available in the event of a dispute
- Proof of data availability committees
    - Proof of stake validator system
    - Anyone can be a validator and store data off chain but must provide a bond (in a smart contract) → in case of malicious behaviour, bond is slashed
    - More secure, permissionless, trustless, well-designed incentives

### Ethereum and future of data availability

- Could use sharding
    - Network split into subchains with their own validators → full node for their shard and light node for everything else → but you can still game the system and act maliciously towards your own shard → [Danksharding](https://notes.ethereum.org/@vbuterin/proto_danksharding_faq) (verify contents of blob have been seen by the network)

## Networking layer

- Protocols (which nodes use to communicate with each other) that allow nodes to find each other and exchange information
    - “Gossiping” — one-to-many
    - Swapping requests and responses — one-to-one
- Execution and consensus clients need to talk to one another
    - Execution clients gossip transactions over execution layer peer-to-peer network
    - Needs encryption
    - RPC connection: software communication protocol that one program can use to request a service from a program located in another computer on a network without having to understand the network's details
    - Validator proposes block → transactions from local pool to go consensus clients using RPC connection → packaged into beacon blocks → consensus clients gossip beacon blocks across P2P network
        - Need 2 separate networks — one for execution clients (transaction gossip), one for consensus clients (block gossip)

### Execution layer

- Both stacks work in parallel
- Discovery stack: built atop UTP, lets node find new peers to connect to — feeds new network participants into the network
    - Discovery: finding other nodes in the network
    - Bootnodes — hardcoded to be found and connect people to the network — that’s it.
        - Nodes are connected to other nodes based on node ID, not geographical location
    - PING-PONG
        - Ping: alerts the node that new node is entering the network
            - Contains hashed information of new node, bootnode, and expiry time stamp
        - Pong: returns Ping hash
        - If both hashes match then it’s a match! Welcome to the network homie
        - Then `FIND-NEIGHBOURS` — then continue to Ping Pong with them etc etc
    - Ethereum node records (ENR)
        - Consists of signature, sequence number that tracks changes, and key:value pairs
        - Preferred network format for Ethereum nodes
    - Why is discover built on UDP?
        - UDP: User Datagram Protocol, communication protocol used across the Internet for especially time-sensitive transmissions such as video playback or DNS lookups — doesn’t formally establish a connection before data is transferred
            - Just fires continuous stream until data is received
        - It just works for finding new nodes, so there’s no need to hassle over it
- DevP2P stack: sits atop TCP, enables nodes to exchange information — enables network participants instructions
    - Protocols from Ethereum that’s implemented to establish/maintain peer to peer network
    - Interactions from new nodes are governed here
        - Sit on top of a few protocols, including RLPx
            - Cryptographic handshake (auth message verified by peer) → auto auth initiator message returned to node (key exchange process) → “hello” exchanged on the wire → protocol occurs when successfully exchange messages a few times
            - Messages contain: Protocol version, client ID, port, node ID, list of supported sub protocols
        - Wire protocol can also send disconnect messages that gives warning to peer that connection will be closed
        - Wire protocol kinda sends off a few ping-pong messages to ensure that the connection remains active
            - Provide scaffolding for useful information to be sent along subprotocols
    - Sub-protocols
        - Wire protocol
            - Define how peers communicate
            - Handles transaction exchange — exchanging pending transactions between nodes so miners can select them for inclusion in the next block
        - les
            - Light Ethereum subprotocol
            - Syncs light clients (rarely used because no incentive for full nodes to serve data to light clients)
        - Snap
            - Lets peers exchange snapshots of recent states → lets peers verify account and storage data without needing to download the Merkle tree nodes
        - Wit (witness protocol)
            - Enables exchange of state witnesses between peers, helping to sync clients to the top of the chain
        - Whisper
            - Protocol aiming to deliver secure messages between peers without writing stuff to the blockchain → is now deprecated L

### Consensus layer

- Participate in block gossip → receive blocks and broadcast (when they are block proposer)
- Still need discovery protocol so node can find peers and establish secure sessions for exchanging blocks
- Discovery
    - Uses discv5 — standalone protocol, running on UDP on a dedicated port, meant for peer discovery only
        - User Datagram Protocol: **operates on top of the Internet Protocol (IP) to transmit datagrams over a network.** UDP does not require the source and destination to establish a three-way handshake before transmission takes place. Additionally, there is no need for an end-to-end connection
- Ethereum node records
    - Node public key, IP address, UDP, TCP ports and two consensus specific fields (attestation subnet bitfield and eth2 key) → easier to find nodes in the gossip, eth2 key ensures both are connected to the same network
- libP2P
    - Supports all communication after discovery — IPv4, IPv6 → dividable into gossip/requestable domains
- Gossip
    - All information that has to spread rapidly throughout the network
    - Uses libP2P gossipsub v1 + metadata stored at each node
- Request response
    - Contains protocols from clients requesting specific information from their peers
    - E.g. specific beacon blocks
    - Returned as snappy-compressed SSZ encoded bytes

### Why consensus client prefers SSZ to RLP?

- RLP — Resource location protocol — automatic repeat request (ARQ) fragmentation protocol used over a wireless (typically cellular) air interface
- SSZ — Simple serialization — fixed offsets to decode individual parts of an encrypted message without needing to decode the entire structure
    - Can yoink specific necessary information
    - Integrates with Merkle protocols
    - Unique representation of values guaranteed

### Connecting execution and consensus clients

- Use local RPC connection — Engine API defines instructions sent between both clients
    - Share 1 Ethereum node record (ENR), `eth1` and `eth2`
    
    ![Untitled](%5BQUICKNOTES%5D%20Ethereum%20Official%20Documentation%2003f7dc4a94634a3fa83e7d5f363b08ed/Untitled%206.png)
    
    ![Untitled](%5BQUICKNOTES%5D%20Ethereum%20Official%20Documentation%2003f7dc4a94634a3fa83e7d5f363b08ed/Untitled%207.png)
    
- When consensus client is not block producer
    - Receieves a block via gossip protocol (consensus P2P)
    - Revalidates the block
    - Transactions sent to execution layer as execution payload (local RPC connection)
    - Execution layer validates and executes
    - EL passes validation data back to consensus client (validated block)
    - Consensus layer adds block to its own chain, broadcasts an attestation
- When consensus client is the block producer
    - CC receives notice it is making the next block
    - Creates block in execution client (local RPC)
    - EL gets to transaction mempool populated by transaction gossip protocol
    - EC bundles transactions, executes, generates hash
    - CC grabs transactions and block hash from EL and adds to beacon block
    - Broadcasts block over block gossip protocol
    - Other clients receive the block over the protocol and validate it
- If block is finalized, it is added to the chain

### Network addresses

- One of 3 standardized formats — multiaddr, enode, or Ethereum Node Records (ENR)
- Multiaddr
    - Multi-addresses
    - Universal format for peer to peer networks
    - Key value pairs separated by /
    - E.g. ipv4 address and value and tcp address and value
        
        `/ip4/192.168.22.27/tcp/33000`
        
    - Ethereum example
        
        `/ip4/192.168.22.27/tcp/33000/p2p/5t7Nv7dG2d6ffbvAiewVsEwWweU3LdebSqX2y1bPrW8br`
        
- Enode
    - Identifying Eth node using URL address format
    - Hexadecimal node ID encoded in username portion of the host separated with `@`
    - Port is TCP listening port — if TCP and UDP ports differ, UDP is a query parameter “discport”
    - Example
        - node with IP address `10.3.58.6`, TCP port `30303`and UDP discovery port `30301`
        
        `enode://6f8a80d14311c39f35f516fa664deaaaa13e85b2f7493f37f6144d86991ec012937307647bd3b9a82abe2974e1407241d54947bbb39763a4cac9f77166ad92a0@10.3.58.6:30303?discport=30301`
        
- Ethereum node records
    - Standard Ethereum network address format
    - Signature, sequence number, fields detailing identity scheme used to generate/validate signatures
    - Can also use key value pairs for additional information e.g. Node’s IP address
    - Consensus clients use specialized ENR structure to identify boot nodes and eth2 field info about current Ethereum fork + attestation group subnet
        - Connects nodes to peers whose attestations are aggregated together

## Data structures and encoding

- Formatting and standardizing memory-efficient ways to store data

### Patricia Merkle Trie (research more on this because brain smol)

- Basic radix tree
    - Cryptographically authenticated data structure used to store all (key, value) bindings
    - Deterministically-generated cryptographic hash digests
        
        ![Untitled](%5BQUICKNOTES%5D%20Ethereum%20Official%20Documentation%2003f7dc4a94634a3fa83e7d5f363b08ed/Untitled%208.png)
        
    - You hash the bottom two then keep hashing the results of that with each other upwards
    - Nibble: atomic unit of radix tree
    - Nodes can have a maximum of 16 children without a value element → represented as array with length → branch nodes
- Radix trees are inefficient, so here is how optimization occurs — every node is either
    - NULL
    - branch (17 item node [v0 … v15, vt])
    - leaf (2 item node [encodedPath, value])
    - extension (2 item node [encodedPath, key])
- To skip giving empty branches NULL nodes, they are simply given an extension node that skips ahead to where there is a value (key is next DB lookup)
- Traversing paths in nibbles → might have odd number → prefix odd numbered path with a flag
- Tries in Etherueum
    - Trie: type of k-ary search tree, a tree data structure used for locating specific keys
        - All Eth’s trees are Merkle Patricia Trie
            - stateRoot
            - transactionsRoot
            - receiptsRoot
    - State trie
        - One global state trie updated every time a client processes a block
        - Path is always `keccak256(ethereumAddress)` and value is always `rlp(ethereumAccount)`
    - Storage trie
        - Where all contract data lives
        - To get values: storage address, integer position of stored data, block ID → pass into `eth_getStorageAt`
        
        ```jsx
        curl -X POST --data '{"jsonrpc":"2.0", "method": "eth_getStorageAt", "params": ["0x295a70b2de5e3953354a6a8344e616ed314d7251", "0x6661e9d6d8b923d5bbaab1b96e1dd51ff6ea2a93520fdc9eb75d059238b8c5e9", "latest"], "id": 1}' localhost:8545
        
        {"jsonrpc":"2.0","id":1,"result":"0x000000000000000000000000000000000000000000000000000000000000162e"}
        ```
        
    - Transactions trie
        - Separate one for every block, stored in (key, value) pairs
        - `rlp(transactionIndex)`
    - Receipts trie
        - Every block has one indexed inside the block you mine
        - Never updated
        - Need: index of transaction in its block, receipt payload, and transaction type
        - Receipt = transaction type+ transactin payload
    

### Recursive length prefix

- Standardizes transfer of data between nodes in a space-efficient format
- Encode arbitrarily nested arrays of binary data
- Definition
    - RLP encoding function takes an item (string or list of items)
        - String here refers to a certain number of bytes of binary data
    - The explanation I did not bother to dumb down for myself
        
        ![Untitled](%5BQUICKNOTES%5D%20Ethereum%20Official%20Documentation%2003f7dc4a94634a3fa83e7d5f363b08ed/Untitled%209.png)
        
        - For a single byte whose value is in the `[0x00, 0x7f]` (decimal `[0, 127]`) range, that byte is its own RLP encoding.
        - Otherwise, if a string is 0-55 bytes long, the RLP encoding consists of a single byte with value **0x80** (dec. 128) plus the length of the string followed by the string. The range of the first byte is thus `[0x80, 0xb7]` (dec. `[128, 183]`).
        - If a string is more than 55 bytes long, the RLP encoding consists of a single byte with value **0xb7** (dec. 183) plus the length in bytes of the length of the string in binary form, followed by the length of the string, followed by the string. For example, a 1024 byte long string would be encoded as `\xb9\x04\x00` (dec. `185, 4, 0`) followed by the string. Here, `0xb9` (183 + 2 = 185) as the first byte, followed by the 2 bytes `0x0400` (dec. 1024) that denote the length of the actual string. The range of the first byte is thus `[0xb8, 0xbf]` (dec. `[184, 191]`).
        - If the total payload of a list (i.e. the combined length of all its items being RLP encoded) is 0-55 bytes long, the RLP encoding consists of a single byte with value **0xc0** plus the length of the list followed by the concatenation of the RLP encodings of the items. The range of the first byte is thus `[0xc0, 0xf7]` (dec. `[192, 247]`).
        - If the total payload of a list is more than 55 bytes long, the RLP encoding consists of a single byte with value **0xf7** plus the length in bytes of the length of the payload in binary form, followed by the length of the payload, followed by the concatenation of the RLP encodings of the items. The range of the first byte is thus `[0xf8, 0xff]` (dec. `[248, 255]`).
- Decoding
    - Decoding regarded as array of binary data
    - Process
        - According to prefix of input data and decoding the data type, length of actual data and offset
        - According to the type and offset of data, decode the data correspondingly
        - Continue to decode rest of input
    - There are other rules but they are honestly not relevant here, go read the docs if you want more

### Simple serialize

- Serialization
    - Relies on schema that must be known in advance
    - Goal: represent objects of arbitrary complexity as a string of bytes e.g. unsigned integers, Booleans
    - For variable lengths → data replaced with offset value → add actual data to heap at end of object → offset value is index for start of actual data in the heap
        
        ![Untitled](%5BQUICKNOTES%5D%20Ethereum%20Official%20Documentation%2003f7dc4a94634a3fa83e7d5f363b08ed/Untitled%2010.png)
        
- Deserialization
    - Need to know schema — precise layout of serialized data so each specific element can be deserialized from blob of bytes into meaningful object
- Merkleization
    - SSZ serialized object turns into Merkle tree representation of the same data → 32 bytes at the end
    - Keep hashing the even number leaves until you get one 32 byte hash at the top
        
        ![Untitled](%5BQUICKNOTES%5D%20Ethereum%20Official%20Documentation%2003f7dc4a94634a3fa83e7d5f363b08ed/Untitled%2011.png)
        
- Generalized indices — integer that represents node in binary Merkle tree where each node has a generalized index `2 ** depth + index in row`
    
    ![Untitled](%5BQUICKNOTES%5D%20Ethereum%20Official%20Documentation%2003f7dc4a94634a3fa83e7d5f363b08ed/Untitled%2012.png)
    
- Multiproofs
    - Providing list of generalized indices representing a specific element, allowing us to verify it against hash tree root
    - Insert chosen hash into right place in Merkle tree
    - Keep hashing the same way to see if the top hash of the confirmed correct one matches the one you inserted — then you would know it was legit

### Web3 secret storage definition

- Web3.js → make your app work on Ethereum
- Definition
    - Secret files can be named anything but good convention is `uuid.json` (uuid is the 128 bit UUID given to secret key)
    - Go to docs to learn how to get the password of the json file’s secret key…